<template>
    <div class="max-w-5xl mx-auto mt-12">
      <h1 class="text-2xl font-bold text-center mb-8">Posts</h1>
      <div v-for="post in posts" :key="post.id" class="bg-white rounded-lg p-6 mb-4 shadow">
        <h2 class="text-xl font-semibold">{{ post.title }}</h2>
        <p>{{ post.body }}</p>
      </div>
      <div class="pagination flex justify-center items-center mt-4">
        <button
          @click="changePage(-1)"
          :disabled="currentPage <= 1"
          class="bg-slate-500 text-white py-2 px-4 rounded hover:bg-slate-700 disabled:opacity-50 mr-2"
        >
          Previous
        </button>
        <span>Page {{ currentPage }}</span>
        <button
          @click="changePage(1)"
          :disabled="!morePostsAvailable"
          class="bg-slate-500 text-white py-2 px-4 rounded hover:bg-slate-700 ml-2 disabled:opacity-50 mr-2"
        >
          Next
        </button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'PostsView',
    data() {
      return {
        posts: [],
        currentPage: 1,
        limit: 10,
        morePostsAvailable: true
      };
    },
    methods: {
      fetchPosts() {
        const apiUrl = `https://jsonplaceholder.typicode.com/posts?_page=${this.currentPage}&_limit=${this.limit}`;
        fetch(apiUrl)
          .then(response => response.json())
          .then(data => {
            this.posts = data;
            this.morePostsAvailable = data.length === this.limit;
          })
          .catch(error => console.error('Error:', error));
      },
      changePage(change) {
        if (change === 1 && !this.morePostsAvailable) return;
            this.currentPage += change;
            this.fetchPosts();
      }
    },
    mounted() {
      this.fetchPosts();
    }
  };
  </script>
  
  <style>
  /* Tailwind CSS is included via PostCSS, see project setup */
  </style>
  