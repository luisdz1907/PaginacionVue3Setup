<script setup>
import { ref, computed } from "vue";
import BlogPost from "./components/BlogPost.vue";
import PaginatePost from "./components/PaginatePost.vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";

const posts = ref([]);
const favorito = ref("");

const postXPagina = 20;
const inicio = ref(0);
const fin = ref(postXPagina);

const loading = ref(true);

const cambiarFvrt = (post) => {
  favorito.value = post;
};

const next = () => {
  inicio.value = inicio.value + postXPagina;
  fin.value = fin.value + postXPagina;
};
const prev = () => {
  inicio.value += -postXPagina;
  fin.value += -postXPagina;
};

fetch("https://jsonplaceholder.typicode.com/posts")
  .then((res) => res.json())
  .then((resp) => (posts.value = resp))
  .catch((e) => console.log(e))
  .finally(() => {
    setTimeout(() => {
      loading.value = false;
    }, 1000);
  });

const maxLength = computed(() => posts.value.length);
</script>
<template>
  <div class="container">
    <h2 class="my-3 text-center">Paginacion</h2>
    <PaginatePost
      class="my-2"
      @next="next"
      @prev="prev"
      :inicio="inicio"
      :fin="fin"
      :maxLength="maxLength"
    ></PaginatePost>
    <LoadingSpinner class="my-3" v-if="loading"></LoadingSpinner>
    <BlogPost
      v-else
      v-for="post in posts.slice(inicio, fin)"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      @cambiarFvrt="cambiarFvrt"
    ></BlogPost>
  </div>
</template>

<style lang="scss" scoped></style>
