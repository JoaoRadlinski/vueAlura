<script setup lang="ts">
import { ref } from 'vue'
import Tag from './Tag.vue'



const props = defineProps<{
  ingrediente: string
}>()

const emit = defineEmits(['adicionar-ingrediente', 'remover-ingrediente'])
const selecionado = ref(false)

function aoClicar() {
  selecionado.value = !selecionado.value

  if (selecionado.value) {
    emit('adicionar-ingrediente', props.ingrediente)
  } else {
    emit('remover-ingrediente', props.ingrediente)
  }
}

</script>

<template>
  <button 
    class="ingrediente" 
    @click="aoClicar"
    type="button"
    :aria-pressed="selecionado"
  >
    <Tag :texto="ingrediente" :ativa="selecionado" />
  </button>
</template>

<style scoped>
.ingrediente {
  cursor: pointer;
  background: none;
  border: none;
  padding: 0;
}
</style>