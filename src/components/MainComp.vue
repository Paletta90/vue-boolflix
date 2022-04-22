<template>

    <div>

        <div v-for="(elem, index) in arrayMovies" :key="index" class="text-white">
            <h2>{{elem.title}}</h2>
            <h3>{{elem.orginal_title}}</h3>
            <h4>{{elem.original_language}}</h4>
            <h5>{{elem.vote_average}}</h5>
        </div>

    </div>

</template>

<script>
export default {
    name: 'MainComp',

    props:{
        arrayMovies: []
    }
}
</script>

<style lang="scss" scoped>

</style>