<template>
  <form @submit.prevent>
   <div>
     <input
         type="text"
         placeholder="Введите название"
         v-model.trim="v$.post.title.$model"
         maxlength="15"
         class="input"
     >

     <div class="input-errors" v-for="(error, index) of v$.post.title.$errors" :key="index">
       <div class="error-msg">Введите текст</div>
     </div>
   </div>

    <div>
      <input
          type="text"
          placeholder="Введите описание"
          v-model.trim="v$.post.body.$model"
          maxlength="40"
          class="input"
      >

      <div class="input-errors" v-for="(error, index) of v$.post.body.$errors" :key="index">
        <div class="error-msg">Введите текст</div>
      </div>
    </div>
    <v-button class="btn" @click="FormPost">

      Отправить
    </v-button>
  </form>

</template>

<script>
import VButton from "@/components/UI/VButton";
import useVuelidate from '@vuelidate/core'
import { required, minLength } from '@vuelidate/validators'


export default {
  components: {VButton},

  setup () {
    return {
      v$: useVuelidate(),
    }
  },
  data() {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  },
  validations () {
    return {
      post: {
        title: {
          required, name_validator: {
            $message: 'Введите текст'
          }
        },
        body: {
          required, name_validator: {
            $message: 'Введите текст'
          }
        }
      }
    }
  },
  methods: {
    FormPost() {
      if (this.post.title !== '' && this.post.body !== '') {
        this.post.id = Date.now()
        this.$emit('create', this.post)
        this.post = {
          title: '',
          body: ''
        }
      }
    },
  },
}
</script>

<style scoped>

form{
  margin-top: auto;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.input{
  border: none;
  padding: 10px 15px;
  border-radius: 10px;
  background: rgba(255, 255, 255, 0.85);
  font-size: 17px;
  width: 100%;
}
input + input{
  margin-top: 10px;
}

.btn{
  align-self: flex-end;
  margin-top: 10px;
  padding: 10px 15px;
  border-radius: 10px;
  border: none;
  transition: .2s ease-in-out;
  cursor: pointer;
}
.btn:hover{
  background: #c4c4c4;
}
.input-errors{
  color: rgba(255, 0, 0, 0.78)
}
</style>

