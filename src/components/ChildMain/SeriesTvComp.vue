<template>

    <div class="col-6 col-sm-4 col-md-3 col-lg-2">

        <CardComp  :datiCard="serieTv" :mediaVoto="mediaVoto" :what="what"/>

    </div>

</template>

<script>

    // Import components
    import CardComp from "./ChildMovieSeries/CardComp.vue"

    export default {
        name: 'SeriesTvComp',

        components:{
            CardComp
        },

        props: {
            serieTv: [],
            imgSize: String,
            mediaVoto: Number,
        },

        data(){
            return{
                what: 'Serie'
            }
        }
    }
</script>

<style lang="scss" scoped>
   div{
       height: 40vh;
   }
</style>