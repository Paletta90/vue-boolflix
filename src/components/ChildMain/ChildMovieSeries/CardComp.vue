<template>

    <div>
        <!-- Copertina -->
        <img :src="`https://image.tmdb.org/t/p/${imgSize}/${datiCard.poster_path}`" alt="" width="100%">

        <div>
            <!-- Titolo del film -->
            <span>Titolo: </span>
            <span v-if="what == 'movie'">{{datiCard.title}}</span>
            <span v-else>{{datiCard.name}}</span>

            <!-- Lingua originale -->
            <h3 v-if="datiCard.original_language == 'en'"><img src="../../../assets/flag/gb.svg" alt="" width="20px"></h3>
            <h3 v-else-if="datiCard.original_language == 'it'"><img src="../../../assets/flag/it.svg" alt="" width="20px">
            </h3>
            <h4 v-else>{{datiCard.original_language}}</h4>

            <!-- Titolo originale -->
            <span>Titolo orginale: </span>
            <span v-if="what == 'movie'">{{datiCard.original_title}}</span>
            <span v-else>{{datiCard.original_name}}</span>

            <!-- Media voto -->
            <div>

                <span>Voto: </span>

                <!-- Stampo le stelle bianche in base alla media ottenuta -->
                <span v-for="(elem, index) in mediaVoto" :key="'A' + index">
                    <span>1</span>
                </span>
                <span v-for="(elem, index) in (5 - mediaVoto)" :key="'B' +index">
                    <span>2</span>
                </span>

            </div>

            <!-- Overview -->
            <div>
                <span>Overview:</span>
                <span>{{datiCard.overview}}</span>
            </div>


        </div>

    </div>

</template>

<script>
    export default {
        name: 'CardComp',

        props:{
            datiCard: [],
            what: String,
            mediaVoto: Number
        },

        data() {
            return {
                imgSize: 'w342'
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>