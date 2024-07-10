<script setup>

//const props = defineProps(['title','id','body','colorText']);
const props = defineProps({
    title: String,
    id: Number,
    body: {
        type:String,
        default: 'Sin descripcion'
    },
    colorText: String
})

const emits = defineEmits('emitirFavorito');

</script>

<template>
    <div class="card">
    <div class="card-body">
        <h5 class="card-title"
        :class="`text-${colorText}`">{{ id }} - {{title}}</h5>
        <p>{{ body }}</p>
        <button 
        @click="emits('emitirFavorito', title)"
        class="btn btn-success">Yo soy el favorito!</button>
    </div>
    </div>

</template>