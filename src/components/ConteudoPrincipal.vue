<script lang="ts">
import { ref } from 'vue'
import SelecionarIngredientes from './SelecionarIngredientes.vue'
import SuaLista from './SuaLista.vue'
import MostraReceitas from './MostraReceitas.vue'

type Pagina = 'SelecionarIngredientes' | 'MostrarReceitas'

const ingredientes = ref<string[]>([])
const conteudo = ref<string>('SelecionarIngredientes' as Pagina)

export default {
  name: 'ConteudoPrincipal',
  setup() {
    return {
      ingredientes,
      conteudo
    }
  },
  components: {
    SelecionarIngredientes,
    SuaLista,
    MostraReceitas
  },
  methods: {
    adicionarIngrediente(ingrediente: string) {
      ingredientes.value.push(ingrediente)
    },
    removerIngrediente(ingrediente: string) {
      ingredientes.value = ingredientes.value.filter((item) => item !== ingrediente)
    },
    navegar(pagina: Pagina) {
      conteudo.value = pagina
    }
  }
}
</script>
<template>
  <main class="conteudo-principal">
    <SuaLista :ingredientes="ingredientes" />
    <KeepAlive include="SelecionarIngredientes">
      <SelecionarIngredientes
          v-if="conteudo === 'SelecionarIngredientes'"
          @adicionar-ingrediente="adicionarIngrediente($event)"
          @remover-ingrediente="removerIngrediente"
          @buscar-receitas="navegar('MostrarReceitas')"
        />
        <MostraReceitas
          v-else-if="conteudo === 'MostrarReceitas'"
          @editar-receitas="navegar('SelecionarIngredientes')"
        />
    </KeepAlive>
    
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
