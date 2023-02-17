<script setup>
defineProps(["inicio", "fin", 'maxLength']);
const emit = defineEmits(["next", "prev"]);
</script>
<template>
  <div class="btn-group">
    <button
      type="button"
      :disabled="inicio == 0"
      @click="$emit('prev')"
      class="btn btn-outline-primary"
    >
      Anterior
    </button>
    <button
      type="button"
      :disabled=" fin >= maxLength"
      @click="$emit('next')"
      class="btn btn-outline-primary"
    >
      Siguiente
    </button>
  </div>
</template>

<style scoped></style>
