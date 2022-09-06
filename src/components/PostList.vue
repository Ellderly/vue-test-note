<template>
<div  v-if="posts.length > 0">
  <div
      class="post"
      v-for="(post) in posts"
      :key="post"
  >
    <div>
      <div class="title">{{post.title}}</div>
      <div class="body">{{post.body}}</div>
    </div>
    <v-button
        class="removePost"
        @click="$emit('remove', post)"
    ></v-button>
  </div>
</div>
  <h2 class="postNan top-text" v-else>
    Пока нет никаких постов
  </h2>

</template>


<script>
import VButton from "@/components/UI/VButton";
export default {
  components: {VButton},
  emits: ['remove'],
  props: {
   posts: {
     type: Array,
     required: true
   }
  },
  data() {
    return{

    }
  },

}
</script>

<style scoped>
.post{
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: rgba(255, 255, 255, 0.7);
  padding: 10px 15px;
  border-radius: 10px;
  color: #424242;
  word-wrap: break-word;
  margin: 0 0 30px 0;
}
.removePost{
  min-width: 30px;
  height: 30px;
  border-radius: 100%;
  border: none;
  background: #fff;
  cursor: pointer;
  transition: .3s;
  position: relative;
  overflow: hidden;
}
.removePost::before,
.removePost::after{
  content: '';
  position: absolute;
  width: 20px;
  height: 2px;
  background: #000;
  top: 15px;
  transition: .2s ease-in-out;
  opacity: 0;
}
.removePost::before{
  left: 0;
}
.removePost:hover::before{
  left: 5px;
  opacity: 1;
  transform: rotate(45deg);
}
.removePost::after{
  right: 0;
}
.removePost:hover::after{
  right: 5px;
  opacity: 1;
  transform: rotate(-45deg);
}
.removePost:hover{
  background: #d98080;
}
.title{
  font-size: 25px;
  color: darkred;
  margin-bottom: 5px;
}
.postNan{
  text-align: center;
  font-size: 40px;
  margin-top: 50px;
  color: rgba(255, 255, 255, 0.5);
  user-select: none;
}

</style>


