<template>
  <div class="container-fluid" style="width: 60em; padding-top: 5em">
    <div class="scrolling-wrapper row flex-row flex-nowrap mt-4 pb-4 pt-2">
      <div
        class="card-block border border-secondary"
        v-for="(pokemon, index) in pokemons"
        :key="'poke' + index"
      >
        <img
          style="width: 96px; height: 96px"
          :src="urlImages + pokemon.id + '.png'"
          class="card-img-top"
          alt="..."
        />
        <div class="card-body">
          <h5 class="card-title">{{ pokemon.name }}</h5>
          <p class="card-text"></p>
          <a href="#" class="btn btn-dark">Detalhes</a>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  data() {
    return {
      pokemons: [],
      urlImages:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/",
      pokemonDetails: [],
    };
  },
  mounted() {
    this.getPokemons();
  },
  methods: {
    async getPokemons() {
        axios.get("https://pokeapi.co/api/v2/pokemon/").then((resposta) => {
          this.formatPokemonDetails(resposta.data);
        }); 
    },
    formatPokemonDetails(data) {
      data.results.forEach((pokemon) => {
        pokemon.id = pokemon.url
          .split("/")
          .filter(function (part) {
            return !!part;
          })
          .pop();
        this.pokemons.push(pokemon);
        this.definePokemonDetails(pokemon.url);
      });
    },
    definePokemonDetails(url) {
      axios.get(url).then((resposta) => {
        console.log(resposta.data);
        this.pokemonDetails.push(resposta.data.base_experience);
      });
    },
  },
};
</script>

<style scoped>
.scrolling-wrapper {
  overflow-x: auto;
}

.card-block {
  height: 250px;
  width: 200px;
  background-color: #fff;
  background-position: center;
  background-size: cover;
  transition: all 0.2s ease-in-out !important;
  border-radius: 24px;
  margin: 10px;
  padding-top: 20px;
}

.card-block:hover {
  transform: translateY(-5px);
  box-shadow: none;
}

h5:first-letter {
  text-transform: capitalize;
}

.scroll-trigger {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100px;
  font-size: 2em;
  color: black;
}
</style>
