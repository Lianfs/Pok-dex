<template>
  <div class="home">
    <Pokemon msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Pokemon from '@/components/Pokemon.vue'

export default {
  name: 'Home',
  components: {
    Pokemon
  }
}
</script>
