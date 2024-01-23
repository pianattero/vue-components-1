<script setup>

//IMPORTS
import {computed, onMounted, ref} from 'vue';

import BlogPost from './components/BlogPost.vue';
import PageButton from './components/PageButton.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

//HOOKS
const loading = ref(true)
onMounted(() => {
  fetchData()
});

//COMPUTED
const maxLength = computed(() => posts.value.length);

//METHODS
const changeFavorite = (title) => {
  favorite.value = title
};

const next = () => {
  start.value += postOnPage
  end.value += postOnPage
};

const prev = () => {
  start.value -= postOnPage
  end.value -= postOnPage
};

const fetchData = async () => {
  try{
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json()
  } catch (error) {
    console.log(error)
  } finally {
    loading.value = false
  }
}

const posts = ref([]);
const favorite = ref('');

const postOnPage = 10
const start = ref(0);
const end = ref(postOnPage)

</script>

<template>
  <LoadingSpinner v-if="loading === true"/>
  <div class="container" v-else>
    <h1>APP</h1>
  
    <h2>Mi Post Favorito: {{ favorite }}</h2>
  
    <PageButton
    @emit-next="next"
    @emit-prev="prev"
    :start="start"
    :end="end"
    :maxLength="maxLength"
    />
  
    <BlogPost
    v-for="post in posts.slice(start, end)"
    :key="post.id"
    :title="post.title"
    :id="post.id"
    :body="post.body"
    @emits-values="changeFavorite"
    />
  </div>

</template>

<style>

</style>
