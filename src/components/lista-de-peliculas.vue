<template>
  <div style="display: flex; flex-direction: row; flex-wrap: wrap; ">
    <v-card class="mx-auto mb-10 mt-5 ml-5 mr-5 custom-card" max-width="200" v-for="{title,release_date,id,poster_path,overview} in peliculas" :key="id" >
      <v-img :src="`https://image.tmdb.org/t/p/w200/${ poster_path}`" alt="poster de la película" height="200px"></v-img>
      <v-card-title> {{ title }} </v-card-title>
      <v-card-subtitle>Estreno:{{ release_date }}</v-card-subtitle>
      <v-card-actions>
        <v-btn color="blue lighten-2" text> OverView </v-btn>
        <v-spacer></v-spacer>
        <v-btn
        :icon="show ? 'mdi-chevron-up' : 'mdi-chevron-down'"
        @click="show = !show"
      ></v-btn>
      </v-card-actions>
      <v-expand-transition>
        <div v-show="show">
          <v-divider></v-divider>
          <v-card-text>
           {{overview}}
          </v-card-text>
        </div>
      </v-expand-transition>
    </v-card>
  </div>
</template>

<script>
export default {
  props: {
    peliculas: {
      type: Array,
      default: () => [],
    },
  },
  data: () => ({
      show: false,
    }),
};
</script>
<style>
.custom-card {
  border: 1px solid black;
  border-radius: 5px;
  padding: 10px;
}
</style>
