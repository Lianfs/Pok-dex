<template>
  <div class="main">
      <div class="row">
        <div
          class="card-block border border-light"
          v-for="(pokemon, index) in pokemons"
          :key="'poke' + index"
        >
          <img
            style="width: 96px; height: 96px;"
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
  <nav aria-label="Page navigation example" style="padding-top: 2em">
    <ul class="pagination justify-content-center">
      <li class="page-item disabled">
        <button type="button" class="page-link">Anterior</button>
      </li>
      <li class="page-item">
        <button type="button" @click="next()" class="page-link">Próximo</button>
      </li>
    </ul>
  </nav>
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
      urlAtual: "",
      proximaUrl: "https://pokeapi.co/api/v2/pokemon/?limit=20&offset=",
      pokemonId: 20,
    };
  },
  created() {
    this.urlAtual = "https://pokeapi.co/api/v2/pokemon/";
    this.getPokemons();
  },
  methods: {
    getPokemons() {
      axios.get(this.urlAtual).then((resposta) => {
        this.formatPokemonDetails(resposta.data);
        this.pokemonId += 20;
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
        this.pokemonDetails.push(resposta.data.base_experience);
      });
    },
    next() {
      this.urlAtual = this.proximaUrl + this.pokemonId;
      this.getPokemons();
    },
  },
};
</script>

<style scoped>
.main {
  display: flex;
  align-items: center;
  justify-content: center;
}

.row {
  flex-direction: row;
  align-items: center;
  justify-content: center;
  width: 50em;
}

.card-block {
  height: 250px;
  width: 200px;
  background-color: #fff;
  background-position: center;
  background-size: cover;
  transition: all 0.2s ease-in-out !important;
  padding-top: 20px;
  margin: 10px;
}

.card-block:hover {
  transform: translateY(-5px);
  box-shadow: none;
}

h5:first-letter {
  text-transform: capitalize;
}
</style>
