<template>
  <div>
    <h4>Comments</h4>
    <hr>
    <span v-if="isLoading">Loading comments...</span>
    <CommentItem
      v-for="comment in comments"
      :key="comment.id"
      :comment="comment"
    />
  </div>
</template>

<script>
import CommentItem from './CommentItem'
import { fetchData } from '../utils'

export default {
  name: 'CommentList',
  components: {
    CommentItem
  },
  props: {
    postId: {
      type: Number
    }
  },

  data: () => ({
    comments: [],
    isLoading: false
  }),

  methods: {
    fetchComments () {
      this.isLoading = true
      fetchData(`https://jsonplaceholder.typicode.com/comments?postId=${this.postId}`)
        .then(res => res.json())
        .then(data => {
          this.comments = data
          this.isLoading = false
        })
        .catch(err => {
          console.log(err)
          this.isLoading = false
        })
    }
  },

  created () {
    this.fetchComments()
  }
}
</script>

<style scoped></style>
