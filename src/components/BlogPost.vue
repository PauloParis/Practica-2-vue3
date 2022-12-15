<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title" :class="`text-${colorText}`"> {{id}} - {{title}}  </h5>
            <p>{{body}}</p>
            <button @click="emit('cambiarFavoritoNombre', title)" class="btn btn-outline-primary">Favorito</button>
        </div>
    </div>
</template>

<script setup>
//------pasar por el props como array--------------
//defineProps(['title', "id", "body", 'colorText'])
//const props = defineProps(['title', "id", "body", 'colorText'])
//console.log(props.title)

//------pasar el props como objeto---------------

defineProps({
    title: String,
    id: Number,
    colorText: String,
    body: {
        type: String,
        default: "Sin descripción"
    }
})

const emit = defineEmits(['cambiarFavoritoNombre']);
//emit ('cambiarFavoritoNombre', title) //para ser accedido desde el script
</script>