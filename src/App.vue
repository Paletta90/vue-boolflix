<template>

  <div id="app">

    <header>

      <HeaderComp @sendText="getMovies" />

    </header>

    <main class="overflow-auto">

      <!-- Se ho digitato qualcosa faccio la ricerca -->
      <div v-if="searchedText">

        <MainComp :arrayMovies="this.arraySearchedMovies" :arraySerieTv="this.arraySearchedSerieTv" />

      </div>

      <!-- Altrimenti mando in stampa messaggio di benvenuto -->
      <div v-else>

        <h1>Benvenuti su Booflix</h1>

      </div>


    </main>

  </div>

</template>

<script>
  // Axios
  import axios from 'axios'

  // Bootstrap 5
  import "bootstrap"

  // Import componenti
  import HeaderComp from "./components/HeaderComp.vue"
  import MainComp from "./components/MainComp.vue"

  export default {
    name: 'App',

    components: {
      HeaderComp,
      MainComp
    },

    data() {

      return {

        arraySearchedMovies: [],
        arraySearchedSerieTv: [],
        searchedText: false,
        apiKey: 'a55ca14d518cb8ca68ff94e5d2ff2ca4',

      }

    },

    methods: {

      // Ottengo il testo digitato, faccio chiamato Api
      getMovies(text) {

        this.searchedText = true

        axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${this.apiKey}&query=${text}`)
          .then((res) => {

            // Array con tot oggetti movie in base al testo selezionato nell'input
            this.arraySearchedMovies = res.data.results
            console.log(this.arraySearchedMovies)

          })

        axios.get(`https://api.themoviedb.org/3/search/tv?api_key=${this.apiKey}&query=${text}`)
          .then((res) => {

            // Array con tot oggetti Serie Tv in base al testo selezionato
            this.arraySearchedSerieTv = res.data.results
            console.log(this.arraySearchedSerieTv)

          })
      },

    },



  }
</script>

<style lang="scss">
  // Bootstrap 5
  @import "bootstrap/dist/css/bootstrap.min.css";

  // import file.scss
  @import "../src/assets/style/variabili.scss";
  @import "../src/assets/style/mixin.scss";


  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  header {
    height: 10vh;
    background-color: $bg-header;
  }

  main {
    height: 90vh;
    background-color: $bg-main;
  }
</style>