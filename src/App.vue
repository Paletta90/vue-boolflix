<template>

  <div id="app">

    <header>

      <HeaderComp @sendText="getMovies" />

    </header>

    <main>

      <MainComp :arrayMovies="this.arraySearchedMovies"/>

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
        apiKey: 'a55ca14d518cb8ca68ff94e5d2ff2ca4',

      }

    },

    methods: {

      // Ottengo il testo digitato, faccio chiamato Api
      getMovies(text) {

        axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${this.apiKey}&query=${text}`)
          .then((res) => {

            // Array con tot oggetti movie in base al testo selezionato nell'input
            this.arraySearchedMovies = res.data.results
            console.log(this.arraySearchedMovies)

          })
      }

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