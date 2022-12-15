<template>
    <div>
        <div class="btn-group" role="group" aria-label="Basic example">
        <button 
            @click="emit('pagePrevius')" 
            type="button" 
            class="btn btn-outline-primary"
            :disabled="inicio<=0"
        >Previus {{inicio}}</button>
        
        <button 
            @click="emit('pageNext')" 
            type="button" 
            class="btn btn-outline-primary"
            :disabled="fin>=maxlenght"
        >Next {{fin}}</button>
</div>
    </div>
</template>

<script setup>

const props = defineProps(['inicio', 'fin', 'maxlenght'])
const emit = defineEmits(['pageNext', 'pagePrevius'])

</script>
