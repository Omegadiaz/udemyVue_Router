<template>
  <Titulo texto="Ruta con parametros" />
  <h2>Parámetro: {{$route.params.id}}</h2>
  <h2 v-if="articulo">{{this.articulo.title}}</h2>
  <p v-if="articulo">{{this.articulo.body}}</p>
  
  
</template>

<script>
import Titulo from '../components/Titulo.vue'
export default {
    components: {
        Titulo
    },
    data() {
        return {
            articulo: {}
        }
    },
    methods: {
        async cargarDatosArticulo() {
            try {
                const data = await fetch(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`)
                const datosArticulo = await data.json()
                this.articulo = datosArticulo
                
            } catch (error) {
                console.log(error)
            }
        }
    },
    created(){
         this.cargarDatosArticulo()
    }    
}
</script>

<style>

</style>