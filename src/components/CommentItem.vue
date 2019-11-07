<template>
  <div class="comment">
    <strong class="comment__email">{{ comment.email }}</strong>
    <div class="comment__text">
      {{ comment.body }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'CommentItem',
  props: {
    comment: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
  .comment {
    margin-bottom: 20px;
  }

  .comment__email {
    margin-bottom: 5px;
  }
</style>
