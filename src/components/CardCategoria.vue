<script lang="ts">
import { ICategoria } from '@/types/Categoria'
import { PropType } from 'vue'
export default {
    props: {
        categoria: {
            type: Object as PropType<ICategoria>,
            required: true
        }
    }
}
</script>
<template>
{{ categoria.nome }}    
</template>