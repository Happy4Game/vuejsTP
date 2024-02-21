<template>
    <div class="text-center">
        <!-- detail vue (v-dialog or something like this) -->
        
        <v-btn
        color="primary"
        >
        Plus d'informations

            <v-dialog
                v-model="dialog"
                activator="parent"
                width="auto"
            >
                <v-card>
                    <v-card-text style="text-align: center;">
                        <p>{{ response.title }}</p>
                        <img width="125px" :src="'https://image.tmdb.org/t/p/w500/'+response.poster_path">
                        <br>
                        <v-chip v-for="genre in response.genres">{{ genre.name }}</v-chip>
                        <h3>Production</h3>
                        <v-avatar size="75" v-for="company in response.production_companies" :image="'https://image.tmdb.org/t/p/w500/' + company.logo_path">{{ company.name }}</v-avatar>
                        <br>
                        <h3>Résumé :</h3>
                        {{ response.overview }}
                        <br>
                    </v-card-text>
                    <v-card-actions>
                        <v-btn color="primary" block @click="dialog = false">Fermer le détail</v-btn>
                    </v-card-actions>
                </v-card>
            </v-dialog>
        </v-btn>
    </div>
</template>
<script>

const axios = require('axios');
const apikey = require('../config.json')
export default {
    name: 'MovieDetail',
    props:{
        movieId: {
            type: Number,
            required: true
        }
    },
    data(){
        return {
            dialog: false,
            response : []
        }
    },
    methods: {
        getDetails() {
            axios.get('https://api.themoviedb.org/3/movie/' + this.movieId + '?language=fr-fr', {
                headers : 'Authorization: Bearer ' + apikey.api_key
            })
            .then((response) => {
                // handle success
                this.response = response.data
            })
        }
    },
    mounted() {
        this.getDetails();
    },
}
</script>