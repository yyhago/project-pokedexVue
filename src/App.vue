<template>
  <div>
    <h2>Começando Aplicação | VUE</h2>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      pokemons: [],
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((resp) => {
        console.log("Lista Pokemon Feita com Sucesso!");
        this.pokemons = resp.data.results;
      });
  },
};
</script>

<style scoped></style>
