<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <div class="add__btns">
      <my-button @click="showDialog">Создать пользователя</my-button>
      <my-select 
		v-model="selectedSort"
		:options="sortOptions" />
    </div>
    <my-dialog v-model:show="dialogVisible">
      <post-form @create="createPost" />
    </my-dialog>
    <post-list :posts="posts" @remove="removePost" v-if="!isPostsLoading" />
    <div v-else>Идет загрузка...</div>
  </div>
</template>
<script>
import PostForm from "./components/PostForm";
import PostList from "@/components/PostList";
import axios from "axios";
export default {
  components: {
    PostForm,
    PostList,
  },

  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostsLoading: false,
      selectedSort: '',
      sortOptions: [
        { value: "title", name: "По названию" },
        { value: "body", name: "По описанию" },
      ]
    };
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter((p) => p.id !== post.id);
    },
    showDialog() {
      this.dialogVisible = true;
    },
    async fetchPosts() {
      try {
        this.isPostsLoading = true;
        setTimeout(async () => {
          const response = await axios.get(
            "https://jsonplaceholder.typicode.com/posts?_limit=10"
          );
          this.isPostsLoading = false;
          console.log(response);
          this.posts = response.data;
        }, 1000);
      } catch (err) {
        alert("Ошибка");
      } finally {
        //   this.isPostsLoading = false;
      }
    },
  },
  mounted() {
    this.fetchPosts();
  },
  watch:{
	selectedSort(newValue){
	},
	dialogVisible(newValue){
console.log(newValue);

	}
  }
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.app {
  padding: 20px;
}
.add__btns {
  display: flex;
  margin: 15px 0px;
  justify-content: space-between;
}
</style>
