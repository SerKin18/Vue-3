<template>
  <form @submit.prevent>
    <h4>Создание поста</h4>
    <my-input
      v-model:value="post.title"
      placeholder="Название поста"
    />
    <my-input
      v-model:value="post.body"
      placeholder="Описание"
    />
    <my-button  @click="createPosts" 
	 style="align-self: flex-end; margin-top: 15px"
      >Создать</my-button
    >
  </form>
</template>
<script>

export default {
  data() {
    return {
      post: {
        title: "",
        body: "",
      },
    };
  },
  methods: {
    createPosts() {
      this.post.id = Date.now();
      this.$emit("create", this.post);
      this.post = {
        title: "",
        body: "",
      };
    },
  },
};
</script>
<style scoped>
form {
  display: flex;
  flex-direction: column;
}




</style>
