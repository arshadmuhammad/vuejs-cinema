<template>
    <div id="movie-list">
        <div v-if="filteredMovies.length">
            <movie-item v-for="movie in filteredMovies" v-bind:movie="movie.movie" v-bind:sessions="movie.sessions"></movie-item>
        </div>
        <div v-else-if="movies.length" class="no-results">
            No result.
        </div>
        <div v-else class="no-results">
            Loading...
        </div>
    </div>
</template>
<script>
    import genres from '../util/genres';
    import MovieItem from './MovieItm.vue';

    export default {
        props: ['genre', 'time', 'movies'],
        methods: {
            moviePassesGenreFilter(movie){
                if(!this.genre.length){
                    return true;
                }else {
                    let movieGeners = movie.movie.Genre.split(", ");
                    let matched = true;
                    this.genre.forEach(genre => {
                        if(movieGeners.indexOf(genre) === -1){
                            matched = false;
                        }
                    });
                    return matched;
                }
            }
        },
        computed: {
            filteredMovies(){
                return this.movies.filter(this.moviePassesGenreFilter);
            }
        },
        components: {
            MovieItem
        }
    }
</script>

<style scoped>
    #movie-list {
        display: inline-block;
    }
</style>
