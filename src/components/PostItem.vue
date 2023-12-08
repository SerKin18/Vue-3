<template>
  <div class="post">
    <div>
      <div><strong>Название:</strong>{{ post.title }}</div>
      <div><strong>Описание:</strong>{{ post.body }}</div>
    </div>
	 <div class="post__btn">
		<my-button>Удалить</my-button>
	 </div>
  </div>
</template>
<script>
import MyButton from'@/components/UI/MyButton'
export default {
	components:{MyButton},
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
};
</script>
<style scoped>
.post {
  margin-top: 15px;
  padding: 15px;
  border: 1px solid teal;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
