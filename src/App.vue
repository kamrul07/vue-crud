<script setup>
import list from './components/list.vue';
import create from './components/create.vue';
import {useToast} from 'vue-toast-notification';
import { ref } from 'vue';
const selectedProduct = ref(null);
</script>

<template>
  {{ selectedProduct }}
<list v-model:selectedProduct ="selectedProduct"  />
<create v-model:activeProduct="selectedProduct" />
</template>

<style scoped>

</style>
