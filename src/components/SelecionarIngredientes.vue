<script lang="ts">
import { obterCategorias } from './http/index'
import CadCategoria from './CardCategoria.vue'
import BotaoPrincipal from './BotaoPrincipal.vue'

export default {
  data() {
    return {
      categorias: []
    }
  },
  components: {
    CadCategoria,
    BotaoPrincipal
  },
  async created() {
    this.categorias = await obterCategorias()
  },
  emits: ['adicionarIngrediente', 'removerIngrediente', 'buscarReceitas']
}
</script>

<template>
  <section class="seleconar-ingredientes">
    <h1 class="cabecalho titulo-ingredientes">Ingredientes</h1>
    <p class="paragrafo-lg instrucoes">
      Selecione os ingredientes que você quer usar nesta receita.
    </p>
    <ul class="categorias">
      <li v-for="categoria in categorias" :key="categoria.nome">
        <CadCategoria
          :categoria="categoria"
          @adicionar-ingrediente="$emit('adicionarIngrediente', $event)"
          @remover-ingrediente="$emit('removerIngrediente', $event)"
        />
      </li>
    </ul>
    <p class="paragrafo dica">*Atenção: consideramos que você tem em casa sal, pimenta e alho.</p>
    <div class="btn-principal">
      <BotaoPrincipal texto="Buscar receitas!" @click="$emit('buscarReceitas')" />
    </div>
  </section>
</template>

<style scoped>
.btn-principal {
  display: flex;
  justify-content: center;
}
.selecionar-ingredientes {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.titulo-ingredientes {
  color: var(--verde-medio, #3d6d4a);
  display: block;
  margin-bottom: 1.5rem;
  text-align: center;
}

.instrucoes {
  margin-bottom: 2rem;
  text-align: center;
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
