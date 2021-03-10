<template>
  <div class="container column">
    <VueAdminForm
            @changeTitle="changeTitleHandler"
            @changeSubtitle="changeSubtitleHandler"
            @changeText="changeTextHandler"
            @changeAvatar="changeAvatarHandler"
    ></VueAdminForm>

    <VueFormContent
            :header="header"
            :blogComponents="blogComponents"
    >
    </VueFormContent>
    <div v-if="isLoadingBlog" class="absolute">
      <VueLoader ></VueLoader>
    </div>


  </div>

  <div class="container">
    <p>
      <button class="btn primary" @click="loadComments">Загрузить комментарии</button>
    </p>
    <VueComments v-if="showComments" :comments="comments"></VueComments>
    <VueLoader v-if="isLoading"></VueLoader>
  </div>
</template>

<script>
  import VueAdminForm from "./components/VueAdminForm"
  import VueFormContent from "./components/VueFormContent";
  import VueComments from "./components/VueComments";
  import VueLoader from "./components/VueLoader";

export default {
    components: {VueComments, VueFormContent, VueAdminForm, VueLoader},
    beforeMount() {
      this.loadPost()
    },
  data() {
      return {
        header: '',
        blogComponents: [],
        showComments: false,
        isLoading: false,
        comments: [],
        isLoadingBlog: false
      }
    },
    methods: {
      changeTitleHandler(val) {
        this.header = val
      },
      changeSubtitleHandler(val) {
        this.createComponent(val, 'subtitle')
      },
      changeTextHandler(val) {
        this.createComponent(val, 'text')
      },
      changeAvatarHandler(val) {
        this.createComponent(val, 'avatar')
      },
      async createComponent(text, componentName) {
        const obj = {
          componentName,
          text,
          id: Math.random()
        }

        const response = await fetch('https://vue-generate-blog-default-rtdb.firebaseio.com/posts.json', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(obj)
        })
        const res = await response.json()
        this.blogComponents[res.name] = obj
      },
      async loadPost() {
        this.isLoadingBlog = true
        const res = await fetch('https://vue-generate-blog-default-rtdb.firebaseio.com/posts.json', {
          method: 'GET',
          headers: {
            'Content-Type': 'application/json'
          }
        })

        const data = await res.json()
        //console.log(data) // will do it
        this.blogComponents = data
        this.isLoadingBlog = false
      },
      async loadComments() {
        this.isLoading = true
        const response = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=42', {
          method: "GET",
          headers: {
            'Content-Type': 'application/json'
          }
        })
        const comments = await response.json()
        this.comments = await comments.slice()
        this.showComments = true
        this.isLoading = false
      }
    }
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }

  .absolute {
    z-index: 99;
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    margin: auto;
    background: transparent;
  }

  .absolute .loader:after {
    background: #fff;
  }
  .absolute .loader:before {
    background: #2c3e50;
  }
</style>
