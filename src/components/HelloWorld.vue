<template>
  <div>
    <Header />
    <ListarPokemon />
  </div>

</template>
<script>
import Header from "./Header.vue";
import ListarPokemon from './ListarPokemons.vue'

export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  components: {
    Header,
    ListarPokemon
  }
};
</script>

<style scoped>
.btn-secondary,
.btn-secondary:hover,
.btn-secondary:focus {
  color: #333;
  text-shadow: none;
}

body {
  text-shadow: 0 0.05rem 0.1rem rgba(0, 0, 0, 0.5);
  box-shadow: inset 0 0 5rem rgba(0, 0, 0, 0.5);
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
</style>
