<template>

    <div>

        <!-- Se gli array sono stati riempiti mando in stampa -->
        <div v-if="this.arrayMovies.length > 0 || this.arraySerieTv.length > 0">

            <div>

                <!-- Film -->
                <div>Film</div>
                <MovieComp v-for="(elem, index) in arrayMovies" :key="index" 
                :movie="elem" 
                :imgSize="imgSize" 
                :mediaVoto ="voteAverage(elem)"
                />

            </div>

            <div>

                <!-- Serie Tv -->
                <h1>Serie Tv</h1>
                <SeriesTvComp v-for="(elem, index) in arraySerieTv" :key="index" 
                :serieTv="elem" 
                :imgSize="imgSize" 
                :mediaVoto="voteAverage(elem)"
                />

            </div>

        </div>

        <!-- Altrimenti mando messaggio di mancata ricerca -->
        <div v-else>
            <h1>Non sono prenseti film o serie tv da lei richieste</h1>
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
            arraySerieTv: []
        },

        data() {
            return {
                imgSize: 'w342'
            }
        },

        methods: {
            // Ritorna media voto da 1 a 5 arrotondate per eccesso
            voteAverage(array) {

                let average = 0;

                average = Math.round(parseInt(array.vote_average) / 2)

                return average

            }
        }
    }
</script>

<style lang="scss" scoped>

</style>