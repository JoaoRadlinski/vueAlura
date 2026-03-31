<script setup lang="ts">
import { ref } from 'vue'
import Tag from './Tag.vue'

defineProps<{
  ingrediente: string
}>()

const selecionado = ref(false)

</script>

<template>
  <button class="ingrediente" @click="selecionado = !selecionado">
    <Tag :texto="ingrediente" :ativa="selecionado" />
  </button>
</template>