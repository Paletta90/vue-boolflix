<template>

    <div>
        <!-- Film -->
        <div>Film</div>
        <div v-for="(elem, index) in arrayMovies" :key="index" class="text-white">

            <!-- Titolo del film -->
            <h2>{{elem.title}}</h2>

            <!-- Lingua originale -->
            <h3 v-if="elem.original_language == 'en'"><img src="../assets/flag/gb.svg" alt="" width="20px"></h3>
            <h3 v-else-if="elem.original_language == 'it'"><img src="../assets/flag/it.svg" alt="" width="20px"></h3>
            <h4 v-else>{{elem.original_language}}</h4>

            <!-- Titolo originale -->
            <h3>{{elem.original_title}}</h3>
            
            <!-- Media voto -->
            <h5>{{elem.vote_average}}</h5>

        </div>

        <!-- Serie Tv -->
        <h1>Serie Tv</h1>
        <div v-for="(elem, index) in arraySerieTv" :key="index" class="text-danger">

            <!-- Titolo della serie tv -->
            <h2>{{elem.name}}</h2>

            <!-- Lingua originale -->
            <h3 v-if="elem.original_language == 'en'"><img src="../assets/flag/gb.svg" alt="" width="20px"></h3>
            <h3 v-else-if="elem.original_language == 'it'"><img src="../assets/flag/it.svg" alt="" width="20px"></h3>
            <h4 v-else>{{elem.original_language}}</h4>

            <!-- Titolo originale -->
            <h3>{{elem.orginal_name}}</h3>

            <!-- Media voto -->
            <h5>{{elem.vote_average}}</h5>
            
        </div>

    </div>

</template>

<script>
export default {
    name: 'MainComp',

    props:{
        arrayMovies: [],
        arraySerieTv: []
    }
}
</script>

<style lang="scss" scoped>

</style>