<script lang="ts">
import Tag from './Tag.vue';

export default {
    props: {
       ingrediente: {
           type: String,
           required: true
       }
    },
    components: {
        Tag
    },
    data() {
        return {
            selecionado: false
        }
    },
    
  methods: {
    adicionarIngrediente() {
        this.selecionado = !this.selecionado
        if (this.selecionado) {
            this.$emit('adicionar-ingrediente', this.ingrediente);
        } else {
            this.$emit('remover-ingrediente', this.ingrediente);
        }
    }
  },
  emits: ['adicionar-ingrediente', 'remover-ingrediente']
}
</script>
<template>
    <button class="ingrediente" @click="adicionarIngrediente" :aria-pressed="selecionado">
        <Tag :texto="ingrediente" :ativa="selecionado" />
    </button>
</template>
<style scoped>
.ingrediente {
    cursor: pointer;
    transition: background 0.3s;
}
</style>