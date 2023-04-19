<template>
  <div class="divBackground">
    <pantalla-de-carga v-if="isLoading"></pantalla-de-carga>
    <lista-de-peliculas :peliculas="peliculas"></lista-de-peliculas>
    <div>
      <div class="d-flex justify-center">
        <v-col cols="12" sm="6" md="2" v-if="currentPage > 1" @click="obtenerPeliculas(currentPage - 1)">
          <v-btn block rounded="lg" size="x-large">Anterior</v-btn>
        </v-col>
        <v-col cols="12" sm="6" md="2" v-if="currentPage < totalPages" @click="obtenerPeliculas(currentPage + 1)">
          <v-btn block rounded="lg" size="x-large">Siguiente</v-btn>
        </v-col>   
      </div>  
    </div>
  </div>
</template>

<script>
import listaDePeliculas from './lista-de-peliculas.vue';
import pantallaDeCarga from './pantalla-de-carga.vue';
import axios from 'axios';

const apiKey = "03621d8f72e756648930273c73fe26b1"

// https://api.themoviedb.org/3/movie/popular?api_key=03621d8f72e756648930273c73fe26b1# 
const tmdbApi = axios.create({
  baseURL: 'https://api.themoviedb.org/3/movie',
  params: { api_key: apiKey }
})


export default {
  components: {
    pantallaDeCarga,
    listaDePeliculas,
  },
  data() {
    return {
      isLoading: true,
      peliculas: [],
      currentPage: 1,
      totalPages: null,
    };
  },
  mounted() {
    this.obtenerPeliculas(this.currentPage)
  },

  methods:{
     obtenerPeliculas(page) {
      this.isLoading = true
      tmdbApi.get('/popular',{params:{page}})
      .then(res => {
         console.log(res.data)
         const { results,page,total_pages } = res.data
         console.log('resultados', results,'page:',page,'total_page:',total_pages)
           this.peliculas = results
           this.totalPages = total_pages
           this.currentPage = page
           this.isLoading = false
    })
    .catch(error => {
      console.error(error)
      this.isLoading=false
    })
},
},
};
</script>
<style>
.divBackground{
background: #010101;
background: linear-gradient(135deg, #010101, #ED01FF);
}
</style>
