<template>
  <Titulo texto="Título de mi blog"/>
  <div v-for="(item,index) in arrayBlog" :key="index">
      <router-link :to="`/blog/${item.id}`">
        {{item.title}}
    </router-link>
  </div>
</template>

<script>
import Titulo from "../components/Titulo.vue";
export default {
    data() {
        return {
            arrayBlog: [],
            dataListo: false,
        }
    },
    components:{
        Titulo
    },
    methods: {
        async consumirApi() {
            try {
                const data = await fetch('https://jsonplaceholder.typicode.com/posts')
                const array = await data.json()
                if(array){
                    this.dataListo = true
                }
                this.arrayBlog = array
                
            } catch (error) {
                console.log(error)
            } 
        }
    },
    created() {
        this.consumirApi()
    }
}
</script>

<style>

</style>