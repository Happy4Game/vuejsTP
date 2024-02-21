<template>
    <!-- list of movies -->
    <v-container>
        <v-row>
            <v-col v-for="trend in trends">
                <v-card align="center" width="300px" height="310px" >
                    <img width="125px" :src="'https://image.tmdb.org/t/p/w500/'+trend.poster_path">
                    <v-card-title>
                        {{ trend.title }}
                    </v-card-title>
                    <v-card-subtitle >
                        {{trend.overview}}
                    </v-card-subtitle>
                    <v-card-actions>
                        <movie-detail v-if="trend.id != 0" :movie-id="trend.id"></movie-detail>
                    </v-card-actions>
                </v-card>
            </v-col>
        </v-row>
    </v-container>
    
</template>
<script>
import MovieDetail from './MovieDetail.vue';

const axios = require('axios');
const apikey = require('../config.json')

export default {
    name: 'MoviesList',
    data() {
        return {
            trends: []
        };
    },
    methods: {
        getTrends() {
            axios.get('https://api.themoviedb.org/3/discover/movie?include_adult=false&include_video=false&language=fr-FR&page=1&sort_by=popularity.desc', {
                headers: 'Authorization: Bearer ' + apikey.api_key
            })
                .then((response) => {
                // handle success
                this.trends = response.data.results;
            });
        }
    },
    mounted() {
        this.getTrends();
    },
    components: { MovieDetail }
}

</script>