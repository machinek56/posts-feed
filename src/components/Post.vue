<template>
  <div class="post" :class="{'post--full': isFull}">
    <h2>
      <template v-if="!isFull">
        <a href=""
           class="post__link"
           @click.prevent="showFullPost">
          {{ post.title }}
        </a>
      </template>
      <template v-else>
        {{ post.title }}
      </template>
    </h2>
    <p>{{ isFull ? post.body : truncateText(post.body) }}</p>
    <em>{{ user.name }}</em>
  </div>
</template>

<script>
export default {
  name: 'Post',

  props: {
    post: {
      type: Object
    },
    user: {
      type: Object
    },
    isFull: {
      type: Boolean
    }
  },

  methods: {
    truncateText (text) {
      return text.substring(0, 80) + '...'
    },
    showFullPost () {
      this.$emit('select-post', this.post)
    }
  }
}
</script>

<style scoped>
  .post {
    background-color: #fff;
    padding: 10px 20px;
    margin-bottom: 20px;
    box-shadow: 0 0 10px 1px #e8e8e8;
  }

  .post:last-child {
    margin-bottom: 0;
  }

  .post--full {
    box-shadow: none;
    padding: 10px 0;
  }

  .post__link {
    color: #2c3e50;
    text-decoration: none;
  }

  .post__link:hover {
    text-decoration: underline;
    color: #4b6d93;
  }
</style>
