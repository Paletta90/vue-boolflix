<template>

    <div class="col-6 col-sm-4 col-md-3 col-lg-2 ">

        <CardComp  :datiCard="movie" :mediaVoto="mediaVoto" :what="what" :actors="actors"/>

    </div>

</template>

<script>
    // Import component
    import CardComp from "./ChildMovieSeries/CardComp.vue"

    export default {
        name: 'MovieComp',

        components:{
            CardComp
        },
        
        props: {
            movie: [],
            mediaVoto: Number,
            actors: []
        },

        data(){
            return{
                what: 'movie'
            }
        }
    }
</script>

<style lang="scss" scoped>
    div{
        height: 40vh;
    }
</style>