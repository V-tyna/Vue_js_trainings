
<script setup>
import { ref, watch } from 'vue';
import Post from './components/Post.vue';

const message = ref('Hello World!');
const textInput = ref('');
const postFilterInput = ref('');
const filteredPosts = ref([]);
const state = {
  count: ref(0),
  posts: ref([
    { id: 1, title: 'Angular', description: 
    `Angular is an application-design framework and development platform for 
    creating efficient and sophisticated single-page apps.` },
    { id: 2, title: 'React', description: 
    `React has been designed from the start for gradual adoption, and you can use as little or 
    as much React as you need. Whether you want to get a taste of React, add some interactivity 
    to a simple HTML page, or start a complex React-powered app, the links in this section will help you get started.` },
    { id: 3, title: 'Vue', description: 
    `Vue (pronounced /vjuː/, like view) is a JavaScript framework for building user interfaces. 
    It builds on top of standard HTML, CSS and JavaScript, and provides a declarative and
     component-based programming model that helps you efficiently develop user interfaces, 
    be it simple or complex.` },
  ])
};
const increase = () => {
  state.count.value++;
}
const decrease = () => {
  state.count.value--;
}
const filterPostHandler = (e) => {
  if (!e.target.value.trim()) {
    filteredPosts.value = [];
  } else {
    filteredPosts.value = [...state.posts.value].filter(post => {
    return post.title.toLowerCase().includes(e.target.value.toLowerCase().trim());
  });
  }
}


</script>
  
<template>
  <h1>{{ message }}</h1>
  <input v-model='textInput' placeholder='Type something here...' />
  <p>
    Typed text: {{ textInput}}
  </p>
  <button @click='increase'>
    Increase
  </button>
  <button @click='decrease'>
    Decrease
  </button>
  <p>
    Increased value: {{ state.count }}
  </p>

  <hr />
  <form>
    <label for='postsFilter'>Filter posts by title: </label>
    <input type='text' id='postFilter' v-model='postFilterInput' @input='(e) => filterPostHandler(e)' />
    <p>Search query: {{ postFilterInput }}</p>
  </form>
  <Post v-for='post in filteredPosts' :key='post.id' :title='post.title' :description='post.description' />
  <br />
  <hr />

  <h2>Posts: </h2>
  <Post v-for='post in state.posts.value' :key='post.id' :title='post.title' :description='post.description' />
  <h3>Something</h3>
</template>