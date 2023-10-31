<script setup>
defineProps({
    minInicio:Boolean,
    maxFin:Boolean,
    paginaActual:Number
})
const emit = defineEmits(["clickBtnInicio","clickBtnFin"])
</script>
<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button type="button" @click="emit('clickBtnInicio')" :disabled="minInicio" class="btn btn-info">Atras</button>
        <button class="btn btn-primary">Pagina {{ paginaActual }}</button>
        <button type="button" @click="emit('clickBtnFin')" :disabled="maxFin" class="btn btn-info">Siguiente</button>
    </div>
</template>