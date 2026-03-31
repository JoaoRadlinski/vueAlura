<script lang="ts">
import type ICategorias from '../interfaces/ICategorias';
import { obterCategorias } from '../http/index';
import CardCategoria from './CardCategoria.vue';

export default {
    components: { CardCategoria },
    data() {
        return {
            categorias: [] as ICategorias[]
        }
    },
     async created() {
         this.categorias = await obterCategorias();
     },
    }   


</script>

<template>
    <section class="selecionar-ingredientes">
        <h1 class="cabecalho titulo ingredientes">Ingredientes</h1>
        <p class="paragrafo-lg instrucoes">Selecione os ingredientes que você tem em casa para descobrir novas receitas.
        </p>

        <ul class="categorias">
            <li v-for="categoria in categorias" :key="categoria.nome">
                <CardCategoria :categoria="categoria"  />
            </li>
        </ul>

        <p class="paragrafo dica">Atencao: consideramos apenas os ingredientes que você selecionar.</p>
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