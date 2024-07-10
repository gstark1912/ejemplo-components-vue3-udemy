<script setup>
import { ref, computed, onMounted } from 'vue';
import BlogPost from './components/BlogPost.vue'
import PaginatePost from './components/PaginatePost.vue'
import LoadingSpinner from './components/LoadingSpinner.vue';
let favorito = ref('');
const cambiarFavorito = (post) => {
  favorito.value = post;
}

onMounted(async () => {
  fetchData();
})

const fetchData = async () => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts');
    posts.value = await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    setTimeout(() => {
      loading.value = false;
    }, 1000);
  }
}

const loading = ref(true);
const posts = ref([]);

const postsLength = computed(() => posts.value.length);

const currentPage = ref(0);
const postsPerPage = 10;
const previousPage = () => {
  if (currentPage.value != 0) {
    loading.value = true;
    setTimeout(() => {
      loading.value = false;
    }, 100);
    currentPage.value -= postsPerPage;
  }
};
const nextPage = () => {
  if (currentPage.value <= postsLength.value) {
    loading.value = true;
    setTimeout(() => {
      loading.value = false;
    }, 100);
    currentPage.value += postsPerPage;
  }
};


</script>

<template>
  <LoadingSpinner v-if="loading" />
  <div class="container" v-else>
    <h1>App</h1>
    <h1>Mis Post favorito: {{ favorito }}</h1>


    <PaginatePost class="mb-2" @previousPage="previousPage" @nextPage="nextPage" :init="currentPage"
      :end="currentPage + postsPerPage" :maxLength="postsLength" />

    <BlogPost class="mb-2" v-for="p in posts.slice(currentPage, currentPage + postsPerPage - 1)" :key="p.id"
      :title="p.title" :id="p.id" :body="p.body" :colorText="p.colorText" @emitirFavorito="cambiarFavorito" />

  </div>
</template>