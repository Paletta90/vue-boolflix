<template>

    <div class="border border-secondary flip-card">

        <div class="flip-card-inner">

            <!-- Copertina -->
            <div class="w-100 h-100 flip-card-front">
                <img class="w-100 h-100" :src="`https://image.tmdb.org/t/p/${imgSize}/${datiCard.poster_path}`" alt="">
            </div>

            <div class="h-100 overflow-auto flip-card-back">

                <!-- Titolo del film -->
                <span class="fw-bold">Titolo: </span>
                <span v-if="what == 'movie'">{{datiCard.title}}</span>
                <span v-else>{{datiCard.name}}</span>

                <!-- Lingua originale con rispettiva bandiera se disponibile -->
                <div v-if="findFlag(datiCard.original_language)">
                    <img :src="`../../../assets/flag/${String( datiCard.original_language )}.svg`" alt="" width="20px">
                </div>
                <div v-else><img src="../../../assets/flag/notfound.png" alt="" width="20px"></div>

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
    .flip-card {
        background-color: transparent;
        width: 100%;
        height: 100%;
        perspective: 1000px;
    }

    .flip-card-inner {
        position: relative;
        width: 100%;
        height: 100%;
        transition: transform 1s;
        transform-style: preserve-3d;
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    }

    .flip-card:hover .flip-card-inner {
        transform: rotateY(180deg);
    }

    .flip-card-front,
    .flip-card-back {
        position: absolute;
        width: 100%;
        height: 100%;
        backface-visibility: hidden;
    }

    .flip-card-front {
        background-color: #bbb;
        color: black;
    }

    .flip-card-back {
        color: white;
        transform: rotateY(180deg);
    }
</style>