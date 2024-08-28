<script>
  // Código Javascript aqui
  import Header from './components/Header.vue';
  import Conteudo from './components/Conteudo.vue';
  import Footer from './components/Footer.vue';
  export default {
    components: {
      Header,
      Conteudo,
      Footer
    },
    data() {
        return {
        }
    }
  }
</script>

<template>
  <!-- Blocos/Componentes aqui -->
  <Header />
  <main class="container d-flex flex-column">
    <Conteudo />
  </main>
  <Footer />
</template>

<style scoped>
/* Código CSS aqui */
</style>
