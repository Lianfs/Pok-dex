<template>
  <div class="main">
    <div class="row" style="background: white;">
      <div
        class="card-block border border-light"
        v-for="(pokemon, index) in pokemons"
        :key="'poke' + index"
        @click="setPokemonUrl(pokemon.url); playSound()"
      >
        <img
          style="width: 96px; height: 96px"
          :src="urlImages + pokemon.id + '.png'"
          class="card-img-top"
          alt="..."
        />
        <div
          class="card-body"
          style="
            border-radius: 0 0 5px 5px;
            height: 55px;
            border: 1.5px solid black;
          "
        >
          <h6
            class="card-title"
            style="font-size: 17px; font-weight: bold; border-width: 5px"
          >
            {{ pokemon.name }}
          </h6>
          <p class="card-text"></p>
        </div>
      </div>
    </div>
  </div>
  <nav aria-label="Page navigation example" style="padding-top: 1em">
    <ul class="pagination justify-content-center">
      <li class="page-item">
        <button type="button" @click="previous()" class="page-link">
          Anterior
        </button>
      </li>
      <li class="page-item">
        <button type="button" @click="setFirstPage()" class="page-link">
          1
        </button>
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
  data: () => {
    return {
      pokemons: [],
      urlImages:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/",
      pokemonDetails: [],
      urlAtual: "",
      proximaUrl: "https://pokeapi.co/api/v2/pokemon/?limit=9&offset=",
      pokemonId: 0,
      showDetail: false,
      overlay: false,
      pokemonUrl: "https://pokeapi.co/api/v2/pokemon/",
      setDetailPokemonId: 0,
      urlShine:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/shiny/",
    };
  },
  components: {},
  created() {
    this.urlAtual = "https://pokeapi.co/api/v2/pokemon/?limit=9&offset=0";
    this.getPokemons();
  },
  methods: {
    getPokemons() {
      axios.get(this.urlAtual).then((resposta) => {
        this.formatPokemonDetails(resposta.data);
      });
    },
    getPokemonsPrevious() {
      axios.get(this.urlAtual).then((resposta) => {
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
        this.pokemonDetails.push(resposta.data.base_experience);
      });
    },
    next() {
      this.pokemonId += 9;
      this.urlAtual = this.proximaUrl + this.pokemonId;
      this.pokemons = [];
      this.getPokemons();
    },
    previous() {
      if (this.pokemonId >= 9) {
        this.pokemonId -= 9;
        this.urlAtual = this.proximaUrl + this.pokemonId;
        this.pokemons = [];
        this.getPokemonsPrevious();
      } else {
        console.log();
      }
    },
    setShowDetail(id) {
      this.showDetail = true;
      this.setDetailPokemonId = id;
    },
    closeShowDetail() {
      this.showDetail = false;
    },
    setFirstPage() {
      this.pokemonId = 0;
      this.urlAtual = this.proximaUrl + this.pokemonId;
      this.pokemons = [];
      this.getPokemonsPrevious();
    },
    setPokemonUrl(url) {
      this.$emit("setPokemonUrl", url);
    },
    playSound() {
      this.$emit("playSound");
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
  height: 190px;
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

h6:first-letter {
  text-transform: capitalize;
  font-weight: bold;
}
</style>
