<script setup>
import { computed, onMounted, ref } from 'vue';
import BlogPost from "./components/BlogPost.vue"
import PaginatePost from "./components/PaginatePost.vue"
import LoadingSpinner from './components/LoadingSpinner.Vue';

  const linkApi="https://jsonplaceholder.typicode.com/posts"

  const posts=ref([])
  const postXpage=10
  const inicio=ref(0)
  const fin=ref(postXpage)
  const pagina =ref(1)
  const loading = ref(true)

  /*
  onMounted(async()=>{
    try{
      const response = await fetch(linkApi)
      posts.value=await response.json()
    }catch(error){
      console.error(error)
    }finally{
      loading.value=false
    }
  })
  */
 

  /*
  fetch(linkApi)
    .then((res)=>res.json())
    .then((data)=>{posts.value=data})
    .catch((e)=>console.log(e))
    .finally(()=>{
      setTimeout(()=>{
        loading.value=false
      },500)
    })
    */
   const fetchData=async()=>{
      try{
        const response = await fetch(linkApi)
        posts.value=await response.json()
      }catch(error){
        console.error(error)
      }finally{
        loading.value=false
      }
   }
   fetchData()

  const botonInicio=()=>{
      inicio.value-=postXpage
      fin.value-=postXpage
      pagina.value-=1
  }
  const botonFin=()=>{
      inicio.value+=postXpage
      fin.value+=postXpage
      pagina.value+=1
  }

  const minInicio = computed(()=>{
    return inicio.value <= 0 ? true:false
  })
  const maxFin=computed(()=>{
    return fin.value >= posts.value.length ? true:false
  })

</script>

<template>
  <LoadingSpinner v-if="loading"/>
  <div class="container" v-else>
    <h1>App</h1>
    <PaginatePost
     class="mb-2"
     :minInicio="minInicio"
     :maxFin="maxFin"
     :paginaActual="pagina"
     @clickBtnInicio="botonInicio"
     @clickBtnFin="botonFin"
     />
    <BlogPost
    class="mb-2"
    v-for="post in posts.slice(inicio, fin)"
    :key="post.id"
    :id="post.id"
    :title="post.title"
    :body="post.body"
    />
  </div>
</template>