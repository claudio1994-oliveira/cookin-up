<script lang="ts">
import { ref } from 'vue'
import SelecionarIngredientes from './SelecionarIngredientes.vue'
import SuaLista from './SuaLista.vue'

const ingredientes = ref<string[]>([])

export default {
  name: 'ConteudoPrincipal',
  setup() {
    return {
      ingredientes
    }
  },
  components: {
    SelecionarIngredientes,
    SuaLista
  },
  methods: {
    adicionarIngrediente(ingrediente: string) {
      ingredientes.value.push(ingrediente)
    },
    removerIngrediente(ingrediente: string) {
      ingredientes.value = ingredientes.value.filter(item => item !== ingrediente)
    }
  }
}
</script>
<template>
  <main class="conteudo-principal">
    <SuaLista :ingredientes="ingredientes" />
    <SelecionarIngredientes 
    @adicionar-ingrediente="adicionarIngrediente($event)"
    @remover-ingrediente="removerIngrediente"
    />
  </main>
</template>
<style scoped>
.conteudo-principal {
  padding: 6.5rem 7.5rem;
  border-radius: 3.75rem 3.75rem 0rem 0rem;
  background: var(--creme, #fffaf3);
  color: var(--cinza, #444);

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5rem;
}

@media only screen and (max-width: 1300px) {
  .conteudo-principal {
    padding: 5rem 3.75rem;
    gap: 3.5rem;
  }
}

@media only screen and (max-width: 767px) {
  .conteudo-principal {
    padding: 4rem 1.5rem;
    gap: 4rem;
  }
}
</style>
