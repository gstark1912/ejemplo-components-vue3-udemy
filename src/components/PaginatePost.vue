<script setup>

defineProps(['init','end','postsLength'])
const emits = defineEmits(['previousPage', 'nextPage']);

</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button type="button" class="btn btn-secondary" @click="emits('previousPage')"
        :disabled="init == 0"
        >Previous {{ init == "0" ? "" : init }}</button>
        <button type="button" class="btn btn-secondary" @click="emits('nextPage')"
        :disabled="end == 100">Next {{ end }}</button>        
    </div>
</template>