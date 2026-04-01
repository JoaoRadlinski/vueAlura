<script setup lang="ts">
import type ICategorias from '../interfaces/ICategorias';
import { obterCategorias } from '../http/index';
import CardCategoria from './CardCategoria.vue';
import { onMounted, ref } from 'vue';

const categorias = ref([] as ICategorias[])

onMounted(async () => {
    categorias.value = await obterCategorias();
})
defineEmits(['adicionar-ingrediente', 'remover-ingrediente'])

</script>

<template>
    <section class="selecionar-ingredientes">
        <h1 class="cabecalho titulo-ingredientes">Ingredientes</h1>
        <p class="paragrafo-lg instrucoes">Selecione os ingredientes que você tem em casa para descobrir novas receitas.
        </p>

        <ul class="categorias">
            <li v-for="categoria in categorias" :key="categoria.nome">
                <CardCategoria :categoria="categoria" @adicionar-ingrediente="$emit('adicionar-ingrediente', $event)"
                    @remover-ingrediente="$emit('remover-ingrediente', $event)" />
            </li>
        </ul>

        <p class="paragrafo dica">Atencao: consideramos apenas os ingredientes que você selecionar.</p>


        <p class="paragrafo dica">
            *Atenção: consideramos que você tem em casa sal, pimenta e água.
        </p>

        <BotaoPrincipal texto="Buscar receitas!" />
    </section>

</template>

<style scoped>
.selecionar-ingredientes {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.titulo-ingredientes {
    color: var(--verde-medio, #3D6D4A);
    display: block;
    margin-bottom: 1.5rem;
}

.instrucoes {
    margin-bottom: 2rem;
}

.categorias {
    margin-bottom: 1rem;
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    flex-wrap: wrap;
}

.dica {
    align-self: flex-start;
    margin-bottom: 3.5rem;
}

@media only screen and (max-width: 767px) {
    .dica {
        margin-bottom: 2.5rem;
    }
}
</style>