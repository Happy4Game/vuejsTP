<template>
  <MovieSearch></MovieSearch>
  <MovieList></MovieList>
  <MoviePagination></MoviePagination>
</template>

<script>
import MovieList from '@/components/MovieList.vue';
import MoviePagination from '@/components/MoviePagination.vue';
import MovieSearch from '@/components/movieSearch.vue';
import MovieDetail from '@/components/MovieDetail.vue';


export default {
    name: 'HomeView',
    components: { MovieList, MoviePagination, MovieSearch, MovieDetail }
}

</script>
