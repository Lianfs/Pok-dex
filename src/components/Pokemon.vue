<template>
  <div class="alinhar">
    <Header
      :apiUrl="apiUrl"
      :imageUrl="imageUrl + pokemonId + '.png'"
      @playSound="playSound"
      @setPokemonUrlSearch="setPokemonUrlSearch"
    />
    <ListarPokemon
      :imageUrl="imageUrl"
      :apiUrl="apiUrl"
      @setPokemonUrl="setPokemonUrl"
      @playSound="playSound"
      @closeDetail="closeDetail"
    />
    <PokemonDetails
      v-if="showDetail"
      :pokemonUrl="pokemonUrl"
      :imageUrl="imageUrl + pokemonId + '.png'"
      :pokemonNome="pokemonNome"
      :shineUrl="imageUrlShiny + pokemonId + '.png'"
      @closeDetail="closeDetail"
    />
    <audio id="audio" src="https://drive.google.com/uc?authuser=0&id=16kyUfDROFC21ifl05jgTAOPDGhAvqVME&export=download" autoplay="false"></audio>
  </div>
</template>
<script>
import Header from "./Header.vue";
import ListarPokemon from "./ListarPokemons.vue";
import PokemonDetails from "./PokemonDetails.vue";
import axios from "axios";

export default {
  name: "Pokemon",
  props: {
    msg: String,
  },
  data: () => {
    return {
      imageUrl:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/",
      imageUrlShiny:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/shiny/",
      apiUrl: "https://pokeapi.co/api/v2/pokemon/",
      pokemonUrl: "",
      showDetail: false,
      pokemonNome: "",
      pokemonId: 0,
    };
  },
  components: {
    Header,
    ListarPokemon,
    PokemonDetails,
  },
  methods: {
    setPokemonUrl(url) {
      this.pokemonUrl = url;
      this.pokemonNome = url.data;
      this.pokemonId = url
        .split("/")
        .filter(function (part) {
          return !!part;
        })
        .pop();
      this.showDetail = true;
    },
    setPokemonUrlSearch(url) {
      this.pokemonUrl = url;
      this.pokemonNome = url.data;
      axios.get(url).then((resposta) => {
        this.pokemonId = resposta.data.id;
        console.log(resposta.data.id);
      });
      this.showDetail = true;
    },
    closeDetail() {
      this.pokemonUrl = "";
      this.showDetail = false;
    },
    playSound() {
        var audio = document.getElementById("audio");
        audio.play();
    }
  },
};
</script>

<style scoped>
.btn-secondary,
.btn-secondary:hover,
.btn-secondary:focus {
  color: #333;
  text-shadow: none;
}

.cover-container {
  max-width: 80em;
}

.nav-space {
  padding-bottom: 40px;
}

.nav-masthead .nav-link {
  padding: 0.25rem 0;
  font-weight: 700;
  color: rgba(0, 0, 0, 0.582);
  background-color: transparent;
  border-bottom: 0.25rem solid transparent;
}

.nav-masthead .nav-link:hover,
.nav-masthead .nav-link:focus {
  border-bottom-color: rgba(255, 255, 255, 0.25);
}

.nav-masthead .nav-link + .nav-link {
  margin-left: 1rem;
}

.nav-masthead .active {
  color: black;
  border-bottom-color: black;
}

.blog-post {
  margin-bottom: 4rem;
}
.blog-post-title {
  margin-bottom: 0.25rem;
  font-size: 2.5rem;
}
.blog-post-meta {
  margin-bottom: 1.25rem;
  color: #727272;
}

.search-bar {
  position: relative;
  padding-bottom: 30px;
  max-width: 30em;
  border-width: 10px;
  border-color: black;
}

.centralizar-search {
  display: inline-block;
  padding-bottom: 3em;
}

.alinahr {
  margin: 0 auto;
  width: 50%;
}
</style>
