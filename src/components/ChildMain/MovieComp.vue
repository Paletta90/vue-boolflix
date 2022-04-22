<template>

    <div>

        <!-- Copertina -->
        <img :src="`https://image.tmdb.org/t/p/${imgSize}/${movie.poster_path}`" alt="">

        <!-- Titolo del film -->
        <h2>{{movie.title}}</h2>

        <!-- Lingua originale -->
        <h3 v-if="movie.original_language == 'en'"><img src="../../assets/flag/gb.svg" alt="" width="20px"></h3>
        <h3 v-else-if="movie.original_language == 'it'"><img src="../../assets/flag/it.svg" alt="" width="20px"></h3>
        <h4 v-else>{{movie.original_language}}</h4>

        <!-- Titolo originale -->
        <h3>{{movie.original_title}}</h3>

        <!-- Media voto -->
         <div>

            <h5>{{movie.vote_average}}</h5>

            <!-- Stampo le stelle bianche in base alla media ottenuta -->
             <div v-for="(elem, index) in mediaVoto" :key="index">
                <h5>1</h5>
            </div>
             <div v-for="(elem, index) in (5 -mediaVoto)" :key="index">
                <h5>2</h5>
            </div>
            
        </div>

    </div>

</template>

<script>
    export default {
        name: 'MovieComp',

        props:{
            movie: [],
            imgSize: String,
            mediaVoto: Number
        }
    }
</script>

<style lang="sss" scoped>

</style>