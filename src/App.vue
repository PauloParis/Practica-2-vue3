<template>
  <LoadingSpinner v-if="loading"/>
  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mi post favorito: {{favorito}}</h2>
    <PaginationPost 
      class="mb-2" 
      @pageNext="next" 
      @pagePrevius="previus"
      :inicio="inicio"
      :fin="fin"
      :maxlenght="posts.length"
    ></PaginationPost>
    <BlogPost
      class="mb-2"
      v-for="post in posts.slice(inicio,fin)" 
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      :colorText="post.colorText"
      @cambiarFavoritoNombre="cambiarFavorito"
    ></BlogPost>
  </div>
</template>

<script setup>
import BlogPost from './components/BlogPost.vue'
import PaginationPost from './components/PaginatePost.vue'
import LoadingSpinner from './components/LoadingSpinner.vue'
import { onMounted, ref } from 'vue';


const posts = ref([]);
const postxpage = 10; //cuantos elementos queremos por pagina
const inicio = ref(0);
const fin = ref(postxpage);

const loading = ref(true);


const favorito = ref('');
const cambiarFavorito = (post) => {
  favorito.value = post;
}

const next = () => {
  inicio.value = inicio.value + postxpage;
  fin.value = fin.value + postxpage;
}

const previus = () => {
  inicio.value = inicio.value - postxpage;
  fin.value = fin.value - postxpage;
}
/*
fetch('https://jsonplaceholder.typicode.com/posts')
  .then(res => res.json())
  .then((data) => posts.value = data)
  .catch((error) => console.log(error))
  .finally(() => {
    setTimeout(() => {
      loading.value = false
    }, 2000)
  })
*/

//una vez que se monté el sitio web, hacemos el onMounted
//se carga el template y luego se activa el onMounted
//no es el mas optimo
/*
onMounted (async () => {
  //loading.value = true;
  try {
    const res = await fetch ('https://jsonplaceholder.typicode.com/posts');
    const data = await res.json();
    posts.value = data;
  } catch (error) {
      console.log(error);
  } finally {
      setTimeout (() => {
        loading.value = false;
      }, 3000) 
  }
})*/


const obtenerJSON = async() => {
  try {
    const res = await fetch ('https://jsonplaceholder.typicode.com/posts');
    const data = await res.json();
    posts.value = data;
  } catch (error) {
      console.log(error);
  } finally {
      setTimeout (() => {
        loading.value = false;
      }, 3000) 
  }
} 
obtenerJSON(); //esta función async podría llamarse desde el onMounted y queda mejor

/*onMounted(()=>{
  obtenerJSON();
})*/

</script>