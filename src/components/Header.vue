<template>
  <header class="p-3 mb-3 border-bottom">
    <div class="container">
      <div
        class="
          d-flex
          flex-wrap
          align-items-center
          justify-content-center justify-content-lg-start
        "
      >
        <a
          href="/"
          class="
            d-flex
            align-items-center
            mb-2 mb-lg-0
            text-dark text-decoration-none
          "
        >
        <img style="width: 80px" src="../assets/logo.png" alt="">
        </a>
        <ul
          class="
            nav
            col-12 col-lg-auto
            me-lg-auto
            mb-2
            justify-content-center
            mb-md-0
          "
        ></ul>
        <form class="col-12 col-lg-auto mb-3 mb-lg-0 me-lg-3">
          <input type="text" v-model="pokemonName">
          <div
            style="
              display: flex;
              position: absolute;
              right: 0;
              top: 0;
              margin-top: 22px;
              margin-right: 30px;
              width: 40px;
              height: 30px;
              background: #ff0000;
              border: none;
              border-radius: 4px;
            "
            @click="setPokemonUrl(); playSound()"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="14"
              height="14"
              fill="currentColor"
              class="bi bi-search"
              viewBox="0 0 16 16"
              style="color: white; margin-top: 8px; margin-left: 13px"
            >
              <path
                d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"
              />
            </svg>
          </div>
        </form>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
  props: ["apiUrl"],
  data: () => {
    return {
      pokemonName: "",
    };
  },
  methods: {
    setPokemonUrl() {
      if (this.pokemonName !== "")
        this.$emit("setPokemonUrlSearch", this.apiUrl + this.pokemonName.toLowerCase());
    },
    playSound() {
      this.$emit("playSound");
    },
  },
};
</script>

<style scoped>
.form-control-dark {
  color: #fff;
  background-color: var(--bs-dark);
  border-color: var(--bs-gray);
}
.form-control-dark:focus {
  color: #fff;
  background-color: var(--bs-dark);
  border-color: #fff;
  box-shadow: 0 0 0 0.25rem rgba(255, 255, 255, 0.25);
}

.bi {
  vertical-align: -0.125em;
  fill: currentColor;
}

.text-small {
  font-size: 85%;
}

.dropdown-toggle {
  outline: 0;
}
</style>