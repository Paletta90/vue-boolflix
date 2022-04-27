<template>

    <div>

        <!-- Se gli array sono stati riempiti mando in stampa -->
        <div v-if="this.arrayMovies.length > 0 || this.arraySerieTv.length > 0" class="p-5">

            <div class="container">

                <div class="row g-2">

                    <!-- Film -->
                    <h1 class="fw-bold text-white">Film</h1>
                    <MovieComp v-for="elem in arrayMovies" :key="elem.id" :movie="elem" :id="elem.id"
                        :mediaVoto="voteAverage(elem)" :actors="getActors(elem.id)" />

                    <!-- Serie Tv -->
                    <h1 class="fw-bold text-white mt-5">Serie Tv</h1>
                    <SeriesTvComp v-for="elem in arraySerieTv" :key="elem.id" :serieTv="elem" :id="elem.id"
                        :mediaVoto="voteAverage(elem)" />

                </div>

            </div>

        </div>

        <!-- Altrimenti mando messaggio di mancata ricerca -->
        <div v-else-if="this.arrayMovies.length == 0 && this.arraySerieTv.length == 0">
            <h1>Nessun risultato trovato per "{{searchedText}}"</h1>
        </div>

    </div>

</template>

<script>
    import axios from 'axios'

    // Import components
    import MovieComp from "./ChildMain/MovieComp.vue"
    import SeriesTvComp from "./ChildMain/SeriesTvComp.vue"

    export default {

        name: 'MainComp',

        components: {
            MovieComp,
            SeriesTvComp
        },

        data() {
            return {
                actors: [],
            }
        },

        props: {
            arrayMovies: [],
            arraySerieTv: [],
            searchedText: String,
            apiKey: String
        },

        methods: {
            // Ritorna media voto da 1 a 5 arrotondate per eccesso
            voteAverage(array) {

                let average = 0;

                average = Math.round(parseInt(array.vote_average) / 2)

                return average

            },

            // Metodo per ottenere i primi 5 attori del film con una chiamata axios
            getActors(id) {

                let actors = [];

                axios.get(`https://api.themoviedb.org/3/movie/${id}/credits?api_key=${this.apiKey}&language=it`)
                    .then((res) => {
                        
                        console.log(res.data.cast)
                        for (let i = 0; i < 5; i++) {
                            // console.log("Attore " + i + res.data.cast[i].name)
                            actors.push(res.data.cast[i].name)
                        }
                        console.log(actors)
                        return actors

                    })

            
            }
        },

    }
</script>

<style lang="scss" scoped>
    @import "../assets/style/mixin.scss";
    @import "../assets/style/variabili.scss";
</style>