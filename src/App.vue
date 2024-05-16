<template>
  <div id="app">
    <h1 class="py-3">Registro de tarjeta de crédito</h1>

    <CardTarjeta />
  </div>
</template>

<script>
import CardTarjeta from "./components/CardTarjeta.vue";
export default {
  name: "App",
  components: {
    CardTarjeta,
  },
};
// document
//   .getElementById("generarCard")
//   .addEventListener("click", function (event) {
//     event.preventDefault();
//   });
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center;
  color: #ffffff;
  margin-top: 30px;
  margin-bottom: 30px; */
}
body {
  background: url("./assets/background.jpg");
  background-size: cover;
  background-attachment: fixed;
}
h1 {
  text-align: center;
  color: white;
  text-transform: uppercase;
  font-weight: bolder;
}
</style>