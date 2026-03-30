<script lang="ts">
import type ICategorias from '@/interfaces/ICategorias';
import { PropType } from 'vue';
export default {
    props: {
        categoria: {
            type: Object as PropType<ICategorias>,
            required: true
        }
    }
}
</script>

<template>
<div>
    {{ categoria.nome }}
    {{ categoria.imagem }}
</div>
</template>