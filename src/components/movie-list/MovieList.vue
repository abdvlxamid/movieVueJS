<template>
  <ul class="movie-list list-group">
    <MovieListItem
      v-for="movie in movies"
      v-bind:movie="movie"
      :key="movie.id"
      @onDelete="$emit('onDelete', movie.id)"
      @onToggle="$emit('onToggle', $event)"
      
    />
  </ul>
</template>
<script>
import MovieListItem from "@/components/movie-list-item/MovieListItem.vue";
export default {
  components: { MovieListItem },
  props: {
    movies: {
      type: Object,
      required: true,
    },
  },
};
</script>
<style scoped>
.movie-list {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
