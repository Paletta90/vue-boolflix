<template>

    <div class="border border-secondary">
        <!-- Copertina -->
        <img class="w-100 h-100 d-none" :src="`https://image.tmdb.org/t/p/${imgSize}/${datiCard.poster_path}`" alt="">

        <div class="d-block h-100 overflow-auto">

            <!-- Titolo del film -->
            <span class="fw-bold">Titolo: </span>
            <span v-if="what == 'movie'">{{datiCard.title}}</span>
            <span v-else>{{datiCard.name}}</span>

            <!-- Lingua originale con rispettiva bandiera se disponibile -->
            <div v-if="findFlag(datiCard.original_language)">
                <img :src="`../../../assets/flag/${String( datiCard.original_language )}.svg`" alt="" width="20px">
            </div>
            <div v-else><img src="../../../assets/flag/icons8-aiuto-50.png" alt="" width="20px"></div>

            <!-- Titolo originale -->
            <span class="fw-bold">Titolo orginale: </span>
            <span v-if="what == 'movie'">{{datiCard.original_title}}</span>
            <span v-else>{{datiCard.original_name}}</span>

            <!-- Media voto -->
            <div>

                <span class="fw-bold">Voto: </span>

                <!-- Stampo le stelle bianche in base alla media ottenuta -->
                <span v-for="(elem, index) in mediaVoto" :key="'A' + index">
                    <span><i class="fa-solid fa-star text-white"></i></span>
                </span>
                <span v-for="(elem, index) in (5 - mediaVoto)" :key="'B' +index">
                    <span><i class="fa-regular fa-star text-white"></i></span>
                </span>

            </div>

            <!-- Overview -->
            <div>
                <span class="fw-bold">Overview:</span>
                <span>{{datiCard.overview}}</span>
            </div>


        </div>

    </div>

</template>

<script>
    export default {
        name: 'CardComp',

        props: {
            datiCard: [],
            what: String,
            mediaVoto: Number,
        },

        data() {
            return {
                imgSize: 'w342',
                language: ['ar', 'es', 'fr', 'en', 'it']
            }
        },

        methods: {
            findFlag(string) {

                if (this.language.includes(string)) {
                    return true
                }

                return false
            }
        },

    }
</script>

<style lang="scss" scoped>
    img{
        object-fit: cover;
    }

        img:hover{
            display: none;
        }
    
</style>