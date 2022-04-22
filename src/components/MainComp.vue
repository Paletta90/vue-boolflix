<template>

    <div>
            
            <!-- Se gli array sono stati riempiti mando in stampa -->
            <div v-if="this.arrayMovies.length > 0 || this.arraySerieTv.length > 0" class="p-5">

                <div class="container">

                    <div class="row g-5">

                        <!-- Film -->
                        <div>Film</div>
                        <MovieComp v-for="elem in arrayMovies" :key="elem.id" :movie="elem"
                            :mediaVoto="voteAverage(elem)" />

                        <!-- Serie Tv -->
                        <h1>Serie Tv</h1>

                        <SeriesTvComp v-for="elem in arraySerieTv" :key="elem.id" :serieTv="elem"
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
    // Import components
    import MovieComp from "./ChildMain/MovieComp.vue"
    import SeriesTvComp from "./ChildMain/SeriesTvComp.vue"

    export default {

        name: 'MainComp',

        components: {
            MovieComp,
            SeriesTvComp
        },

        props: {
            arrayMovies: [],
            arraySerieTv: [],
            searchedText: String
        },

        methods: {
            // Ritorna media voto da 1 a 5 arrotondate per eccesso
            voteAverage(array) {

                let average = 0;

                average = Math.round(parseInt(array.vote_average) / 2)

                return average

            }
        },

        // created(){
        //     console.log(this.arrayMovies)
        // }

        
    }
</script>

<style lang="scss" scoped>
    @import "../assets/style/mixin.scss";
    @import "../assets/style/variabili.scss";

    .cards {
        @include flex(row, space-between, center);
        flex-wrap: wrap;
    }

</style>