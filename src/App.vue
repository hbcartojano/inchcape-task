<template>
  <PostsView/>
</template>

<script>
import PostsView from './components/PostsView.vue'

export default {
  name: 'App',
  components: {
    PostsView
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
