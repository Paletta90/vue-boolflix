<template>

  <div id="app">

    <header>

      <HeaderComp />

    </header>

    <main>

      <MainComp />

    </main>

  </div>

</template>

<script>

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
    }

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

  header{
    height: 10vh;
    background-color: $bg-header;
  }

  main{
    height: 90vh;
    background-color: $bg-main;
  }
</style>