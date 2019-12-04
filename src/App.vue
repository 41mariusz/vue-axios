<template>
<div>
  <input type="text" v-model="postTitle" placeholder="title"/>
  <input type="text" v-model="postBody" placeholder="body"/>
  <input type="button" @click="createPost()" value="submit">
  <div v-if="posts && posts.length">
    <div id="ramka" v-for="post of posts" v-bind:key="post.id">
        <p>[{{post.id}}] <strong>{{post.title}}</strong></p>
        <p>{{post.body}}</p>
        <!-- <p>author <font color="red"><i>{{users.find(e => e.id === post.userId) ? users.find(e => e.id === post.userId).name : "unknown"}}</i></font></p> -->
        <p>author <span id="author"><i>{{users.find(e => e.id === post.userId).name}}</i></span></p>
    </div>
  </div>
</div>
</template>

<style>
div#ramka {
    border-width: 1px;
    border-style: dashed;
    border-color: yellowgreen;
    padding: 3px;
    margin: 3px;
  }
  span#author {
    color: #1100ff;
    font-weight: bold;
  }
</style>

<script>
import axios from 'axios'

export default {
  name: 'app',
  data () {
    return {
      id: null,
      postBody: null,
      postTitle: null,
      users: [],
      posts: []
    }
  },
  created() {
    this.$http.get('posts').then((response) => {
      this.posts = response.data
    }),
    this.$http.get('users').then((response) => {
      this.users = response.data
    })
    .catch((e) => {
      console.error(e)
    })
  },
  methods: {
    createPost () {
      this.$http.post('posts', {
        id: this.id,
        title: this.postTitle,
        body: this.postBody
      }).then((response) => {})
      .catch((e) => {
        console.error(e)
      })
    }
  }
}
</script>
