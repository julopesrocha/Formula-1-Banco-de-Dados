<template>
  <div id="app">
    <h1>Consultas do Banco de Dados</h1>
    <div v-for="(consulta, index) in consultas" :key="index">
      <Consulta :data="consulta.data" :title="consulta.title" />
    </div>
  </div>
</template>

<script>
import Consulta from "./components/Consulta.vue";

export default {
  name: "App",
  components: {
    Consulta,
  },
  data() {
    return {
      consultas: [
        { title: "Consulta 1: Pilotos e Equipes", data: [] },
        { title: "Consulta 2: Corridas e Circuitos", data: [] },
        { title: "Consulta 3: Equipes e Total de Pilotos", data: [] },
        { title: "Consulta 4: Resultados de Pilotos", data: [] },
        { title: "Consulta 5: Circuitos e Média de Rodadas", data: [] },
      ],
    };
  },
  async mounted() {
    // Busca os dados para cada consulta
    for (let i = 1; i <= 5; i++) {
      const response = await fetch(`http://127.0.0.1:5000/consulta${i}`);
      const data = await response.json();
      this.consultas[i - 1].data = data;
    }
  },
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  text-align: center;
  margin: 20px;
}
</style>
