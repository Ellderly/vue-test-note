<template>
  <div class="app">
    <post-list
        @remove="removePost"
        :posts="posts"
        class="app_list"
    />
    <post-form
        @create="FormPost"
    />
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";



export default {
  components: {
    PostList, PostForm
  },
  data() {
    return {
      posts: [],
    }
  },
  mounted() {
    if (localStorage.getItem('posts')) {
      try {
        this.posts = JSON.parse(localStorage.getItem('posts'));
      } catch(e) {
        localStorage.removeItem('posts');
      }
    }
  },
  methods: {
    FormPost(post) {
        this.posts.push(post)
        this.savePosts()
    },
    removePost(post){
      this.posts = this.posts.filter(p => p.id !== post.id)
      this.savePosts();
    },
    savePosts(){
      const parsed = JSON.stringify(this.posts);
      localStorage.setItem('posts', parsed);
    }
  },
}
</script>

<style>
*{
  box-sizing: border-box;
  padding: 0;
  margin: 0;
  outline: none;
  font-family: sans-serif;
}
html{
  background-image: url("@/assets/bg.png");
  background-size: cover;
  }
.app{
  width: 800px;
  height: 70vh;
  margin: 100px auto 0;
  display: flex;
  flex-direction: column;
  overflow: scroll;

}
.app_list{
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  flex-wrap: nowrap;
}
.top-text{
  justify-content: flex-start;
}
</style>
