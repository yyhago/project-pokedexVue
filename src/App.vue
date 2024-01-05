<template>
  <div id="app">
    <h2 class="namePrincipal">Lista de Pokemon | Vue</h2>
    <input
      type="text"
      placeholder="Procure seu melhor pokemon..."
      v-model="busca"
    />
    <div class="column is-half is-offset-one-quarter">
      <div v-for="(poke, index) in resultBusca" :key="index">
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon.vue";

export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      busca: "",
    };
  },
  created() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((resp) => {
        console.log("Lista Pokemon Feita com Sucesso!");
        this.pokemons = resp.data.results;
      });
  },
  components: {
    Pokemon,
  },
  computed: {
    resultBusca() {
      const buscaLower = this.busca.toLowerCase();
      if (buscaLower === "" || buscaLower === " ") {
        return this.pokemons;
      } else {
        return this.pokemons.filter((pokemon) =>
          pokemon.name.toLowerCase().includes(buscaLower)
        );
      }
    },
  },
  methods: {
    realizarBusca() {
    },
  },
};
</script>


<style scoped>
#app {
  padding: 5rem;
  justify-content: center;
  align-items: center;

}

.namePrincipal {
  color: #000000;
  text-align: center;
  padding-bottom: 2rem;
  font-size: 30px;
  font-weight: bold;
}

input {
  display: flex;
  margin: 0 auto;
  width: 420px;
  height: 2rem;
  padding: 20px;
  background-color: #04b2d9;
  color: black;
  border: none;
  border-radius: 7px;
  padding-left: 20px;
  cursor: pointer;
}

#buscaBtn {
  display: flex;
  margin: 0 auto;
  background-color: #04b2d9;
  color: rgb(0, 0, 0);
  border: none;
  border-radius: 7px;
  width: 420px;
  margin-top: 10px;
}
</style>
