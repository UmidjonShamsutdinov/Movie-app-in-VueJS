<template >
    <ul class="movie-list list-group" v-if="moviesData.length > 0">
    <MovieListItem 
      v-for="(movie, index) in moviesData" 
      :key="movie.id" 
      :movie="movie" 
      @onToggle="$emit('onToggle', $event)"  
      @onRemove="$emit('removeItem', $event)" 
    />
  </ul>
  <ul v-else class="movie-list list-group text-center">Hozircha hech qanday film mavjud emas.</ul>
</template>
<script>
import MovieListItem from "../movie-list-item/MovieListItem.vue"
export default {
    components:{
        MovieListItem,
    },
    props:{
        moviesData: {
            type: Array,
            required: true
        },
    }

}
</script>
<style scoped>
    .movie-list{
        margin-top: 2rem;
        padding: 1.5rem;
        background-color: #fcf5faf5;
        border-radius: 4px;
        box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
    }
</style>