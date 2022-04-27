<template>

    <div class="flip-card">

        <div class="flip-card-inner">

            <!-- Copertina -->
            <div class="w-100 h-100 flip-card-front border">
                <img class="w-100 h-100" :src="`https://image.tmdb.org/t/p/${imgSize}/${datiCard.poster_path}`" alt="">
            </div>

            <div class="h-100 overflow-auto flip-card-back p-2">

                <!-- Titolo del film -->
                <div class="mb-1">
                    <span class="fw-bold">Titolo: </span>
                    <span v-if="what == 'movie'">{{datiCard.title}}</span>
                    <span v-else>{{datiCard.name}}</span>
                </div>


                <!-- Lingua originale con rispettiva bandiera se disponibile -->
                <div class="mb-1">
                    <div v-if="findFlag(datiCard.original_language)">
                        <img :src="require(`../../../assets/flag/${String( datiCard.original_language )}.svg`)" alt=""
                            width="20px">
                    </div>
                    <div v-else><img :src="require('../../../assets/flag/notfound.png')" alt="" width="20px"></div>
                </div>


                <!-- Titolo originale -->
                <div class="mb-1">
                    <span class="fw-bold">Titolo orginale: </span>
                    <span v-if="what == 'movie'">{{datiCard.original_title}}</span>
                    <span v-else>{{datiCard.original_name}}</span>
                </div>


                <!-- Attori-->
                <div class="mb-1">

                    <span class="fw-bold">Cast: </span>

                    <!-- Stampo le stelle bianche in base alla media ottenuta -->
                    <span v-for="(elem, index) in actors" :key="'B' + index">
                        <span>{{elem}} </span>
                    </span>

                </div>

                <!-- Media voto -->
                <div class="mb-1">

                    <span class="fw-bold">Voto: </span>

                    <!-- Stampo le stelle bianche in base alla media ottenuta -->
                    <span v-for="(elem, index) in 5" :key="'A' + index">
                        <span><i class="fa-star" :class="(index <= mediaVoto) ? 'fa-solid' : 'fa-regular' "></i></span>
                    </span>

                </div>

                <!-- Overview -->
                <div>
                    <span class="fw-bold">Overview: </span>
                    <span class="f-small">{{datiCard.overview}}</span>
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
            actors: []
        },

        data() {
            return {
                imgSize: 'w342',
                language: ['ar', 'es', 'fr', 'en', 'it'],
            }
        },

        methods: {
            // Metodo per ricercare la bandiera della lingua orginale
            findFlag(string) {

                if (this.language.includes(string)) {
                    return true
                }

                return false
            },

        }

    }
</script>

<style lang="scss" scoped>
    .fa-solid {
        color: yellow
    }

    .f-small {
        font-size: 0.7rem;
    }

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
        background-color: rgb(26, 36, 46);
    }

    ::-webkit-scrollbar {
        width: 2px;
    }

    ::-webkit-scrollbar-track {
        background: #f1f1f1;
    }

    ::-webkit-scrollbar-thumb {
        background: #888;
    }
</style>