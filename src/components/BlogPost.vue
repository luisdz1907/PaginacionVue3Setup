<script setup >
defineProps({
  title: String,
  id: Number,
  body: {
    type: String,
    defuault: "Sin descripcion",
  },
});
const emit = defineEmits(['cambiarFvrt', 'next'])
</script>
<template>
  <div class="card my-3">
    <div class="card-body">
      <h5 class="card-title text-center">{{ id }} - {{ title }}</h5>
      <p class="text-center">{{ body }}</p>
      <button type="button" @click="emit('cambiarFvrt', title)" class="btn btn-primary my-2 d-block w-100">Favorito</button>
    </div>
  </div>
</template>

<style scoped></style>
