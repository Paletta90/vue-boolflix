<template>

  <div id="app">

    <header>

      <HeaderComp @sendText="getMovies" />

    </header>

    <main class="overflow-auto">

      <!-- Se ho digitato qualcosa faccio la ricerca -->
      <!-- Assegno delle classi per centrare il loader al centro della pagina -->
      <div v-if="searchedText != ''" class="h-100"
        :class="!(this.isLoadedMovie && this.isLoadedSerie) ? 'd-flex justify-content-center align-items-center' : '' ">

        <!-- Quando ho caricato i dati vado in stampa -->
        <div v-if="this.isLoadedMovie && this.isLoadedSerie">

          <MainComp :arrayMovies="this.arraySearchedMovies" :arraySerieTv="this.arraySearchedSerieTv"
            :searchedText="this.searchedText" :apiKey="apiKey" />

        </div>

        <!-- Altrimenti mostro un loader -->
        <div v-else class="loader"></div>


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

        // Array dove inserisco film
        arraySearchedMovies: [],
        // Array dove inserisco Serie Tv
        arraySearchedSerieTv: [],
        // testo inserito
        searchedText: '',
        // Booleani per che ci informano quando sono terminate le chiamate axos
        isLoadedMovie: false,
        isLoadedSerie: false,
        // Api key personale
        apiKey: 'a55ca14d518cb8ca68ff94e5d2ff2ca4',
        // Lingua di ricerca
        language: 'it'

      }

    },

    methods: {

      // Metodo che ottiene il testo digitato e filtro film e serie tv
      getMovies(text) {
        
        // Se non digito nulla o solo spazi non faccio accadere nulla
        if (text != '' && text.replace(/\s/g, '').length != 0) {

          // Riempio il dato con il testo digitato
          this.searchedText = text

          // Chiamata Axios per i film
          axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${this.apiKey}&query=${this.searchedText}&language=${this.language}`)
            .then((res) => {

              // Array con tot oggetti movie in base al testo selezionato nell'input
              this.arraySearchedMovies = res.data.results

              // La chiamta è stata effettuata
              this.isLoadedMovie = true

            })

          // Chaiamato axios per le serie tv
          axios.get(`https://api.themoviedb.org/3/search/tv?api_key=${this.apiKey}&query=${this.searchedText}`)
            .then((res) => {

              // Array con tot oggetti Serie Tv in base al testo selezionato
              this.arraySearchedSerieTv = res.data.results

              // La chiamata è stata effettuata
              this.isLoadedSerie = true

            })
        }


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

  // Classi per creare il loader
  .loader {
    border: 16px solid #f3f3f3;
    border-radius: 50%;
    border-top: 16px solid $color-title;
    width: 120px;
    height: 120px;
    -webkit-animation: spin 2s linear infinite;
    animation: spin 2s linear infinite;
  }

  @keyframes spin {
    0% {
      transform: rotate(0deg);
    }

    100% {
      transform: rotate(360deg);
    }
  }
</style>