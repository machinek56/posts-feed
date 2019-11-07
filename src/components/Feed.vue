<template>
  <div>
    <div class="feed">
      <h1 class="feed__heading">Feed</h1>

      <template v-if="isLoading">
        Loading...
      </template>

      <template v-if="!isLoading">
        <Post
          v-for="post in posts"
          :key="post.id"
          :post="post"
          :user="getUserByPost(post.userId)"
          :isFull="false"
          @select-post="selectPost"
        />
      </template>
    </div>

    <modal v-if="showModal" @close="closeModal">
      <Post
        :post="selectedPost"
        :user="getUserByPost(selectedPost.userId)"
        :isFull="true"
      />
      <CommentList :post-id="selectedPost.id"/>
    </modal>
  </div>
</template>

<script>
import Post from './Post'
import Modal from './Modal'
import CommentList from './CommentList'
import { fetchData } from '../utils'

export default {
  name: 'Feed',
  data: () => ({
    posts: [],
    users: [],
    selectedPost: {},
    showModal: false,
    isLoading: false
  }),
  components: {
    Post,
    Modal,
    CommentList
  },

  methods: {
    getUserByPost (id) {
      return this.users.find(user => user.id === id)
    },

    selectPost (post) {
      this.showModal = true
      this.selectedPost = post
    },

    fetchContent () {
      const urls = [
        'https://jsonplaceholder.typicode.com/posts',
        'https://jsonplaceholder.typicode.com/users'
      ]
      const requests = urls.map(url => fetchData(url))

      this.isLoading = true
      Promise.all(requests)
        .then(responses => Promise.all(responses.map(r => r.json())))
        .then(data => {
          this.posts = data[0]
          this.users = data[1]
        })
        .finally(() => (this.isLoading = false))
    },

    closeModal () {
      this.showModal = false
    }
  },
  created () {
    this.fetchContent()
  }
}
</script>

<style>
  .feed {
    max-width: 600px;
    margin: 0 auto;
    padding-bottom: 20px;
  }

  .feed__heading {
    margin-top: 0;
  }
</style>
