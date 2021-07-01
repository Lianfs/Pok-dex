<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div class="modal" role="dialog" id="modal">
        <audio id="audio">
          <source
            src="https://css-tricks.com/examples/SoundOnHover/audio/beep.ogg"
          />
        </audio>
        <div class="light-circle"></div>
        <div class="circle1" @click="$emit('closeDetail')"></div>
        <div class="circle2"></div>
        <div class="circle3"></div>
        <div class="bordaVisorPokemon">
          <div
            class="circle-red"
            style="margin-top: 10px; margin-left: 90px; border: 1px solid black"
          ></div>
          <div
            class="circle-red"
            style="
              margin-top: 10px;
              margin-left: 120px;
              border: 1px solid black;
            "
          ></div>
          <div
            class="circle-red"
            style="
              margin-top: 173px;
              margin-left: 15px;
              border: 1px solid black;
              width: 15px;
              height: 15px;
            "
          ></div>
          <div class="visorPokemon">
            <img
              :src="shineUrl"
              style="
                width: 96px;
                height: 96px;
                display: flex;
                position: absolute;
              "
            />
            <img
              :src="imageUrl"
              style="
                width: 96px;
                height: 96px;
                display: block;
                position: absolute;
              "
              id="mostrarShiny"
            />
          </div>
        </div>
        <div
          style="
            display: flex;
            position: absolute;
            top: 0;
            margin-top: 390px;
            left: 0;
            margin-left: 75px;
            width: 80px;
            height: 50px;
            background: green;
            border: 1px solid black;
            border-radius: 3px;
          "
        ></div>
        <div
          style="
            display: flex;
            position: absolute;
            top: 0;
            margin-top: 350px;
            left: 0;
            margin-left: 70px;
            width: 40px;
            height: 8px;
            background: #8b0000;
            border: 1px solid black;
            border-radius: 3px;
            box-shadow: inset 0 0 0 2px rgba(0, 0, 0, 0.24);
          "
        ></div>
        <div
          style="
            display: flex;
            position: absolute;
            top: 0;
            margin-top: 350px;
            left: 0;
            margin-left: 130px;
            width: 40px;
            height: 8px;
            background: #00008b;
            border: 1px solid black;
            border-radius: 3px;
            box-shadow: inset 0 0 0 2px rgba(0, 0, 0, 0.24);
          "
        ></div>
        <div class="junta">
          <div
            class="junta-quadrado"
            style="
              top: 0;
              border-bottom: 3px solid black;
              box-shadow: inset 2px 0 3px 0 rgba(255, 255, 255, 0.623);
            "
          ></div>
          <div
            class="junta-quadrado"
            style="
              bottom: 0;
              border-top: 3px solid black;
              box-shadow: inset 2px 0 3px 0 rgba(255, 255, 255, 0.623);
            "
          ></div>
        </div>
        <div class="container-botao">
          <div
            class="botao"
            style="
              left: 0;
              margin-left: 30px;
              border-top-right-radius: 5px;
              border-top-left-radius: 5px;
            "
          >
            <div
              class="seta-botao"
              style="
                top: 0;
                right: 0;
                margin-top: 13px;
                margin-right: 11px;
                transform: rotate(-135deg);
              "
            ></div>
          </div>
          <div
            class="botao"
            style="
              top: 0;
              margin-top: 30px;
              border-bottom-left-radius: 5px;
              border-top-left-radius: 5px;
            "
          >
            <div
              class="seta-botao"
              style="
                top: 0;
                left: 0;
                margin-top: 11px;
                margin-left: 13px;
                transform: rotate(135deg);
              "
              @click="toggle()"
            ></div>
          </div>
          <div
            class="botao"
            style="
              bottom: 0;
              margin-left: 30px;
              border-bottom-right-radius: 5px;
              border-bottom-left-radius: 5px;
            "
          >
            <div
              class="seta-botao"
              style="
                bottom: 0;
                right: 0;
                margin-bottom: 13px;
                margin-right: 11px;
                transform: rotate(45deg);
              "
            ></div>
          </div>
          <div
            class="botao"
            style="
              right: 0;
              margin-top: 30px;
              border-bottom-right-radius: 5px;
              border-top-right-radius: 5px;
            "
            @click="toggle()"
          >
            <div
              class="seta-botao"
              style="
                top: 0;
                right: 0;
                margin-top: 11px;
                margin-right: 13px;
                transform: rotate(-45deg);
              "
            ></div>
          </div>
          <div
            class="botao"
            style="left: 0; margin-top: 30px; margin-left: 30px"
          ></div>
        </div>
        <div class="modal2" role="dialog" id="modal2"></div>
        <div class="informacoes">
          <h6
            style="
              display: flex;
              top: 0;
              left: 0;
              margin-left: 20px;
              margin-top: 14px;
            "
          >
            número: {{ id }}
          </h6>
          <h6
            style="
              display: flex;
              position: absolute;
              top: 0;
              left: 0;
              margin-left: 20px;
              margin-top: 34px;
            "
          >
            nome: {{ pokemon.name }}
          </h6>
          <h6
            style="
              display: flex;
              position: absolute;
              top: 0;
              left: 0;
              margin-left: 20px;
              margin-top: 54px;
            "
          >
            altura: {{ height }}m
          </h6>
          <h6
            style="
              display: flex;
              position: absolute;
              top: 0;
              left: 0;
              margin-left: 20px;
              margin-top: 74px;
            "
          >
            peso: {{ weight }}kg
          </h6>
        </div>
        <div class="informacoes row" style="margin-top: 300px;">
          <h6
            style="
              display: flex;
              position: relative;
              left: 0;
              margin-left: 7px;
              margin-top: 15px;
            "
          >
            Habilidades:
          </h6>
          <div
            style="
              display: flex;
              position: relative;
              left: 0;
              margin-left: 7px;
              margin-top: -5px;
            "
            v-for="(value, index) in pokemon.abilities"
            :key="'value' + index"
          >
            <h6>
              {{ value.ability.name }}
            </h6>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import axios from "axios";

export default {
  name: "PokemonDetails",
  props: ["pokemonUrl", "imageUrl", "shineUrl", "pokemonNome"],
  data: () => {
    return {
      pokemon: "",
      height: 0,
      weight: 0,
      id: 0,
    };
  },
  methods: {
    defineInformations(url) {
      axios.get(url).then((resposta) => {
        this.pokemon = resposta.data;
        this.height = resposta.data.height / 10;
        this.weight = resposta.data.weight / 10;
        this.id = resposta.data.id;
      });
    },
    closeDetail() {
      this.$emit("closeDetail");
    },
    toggle() {
      var mydiv = document.getElementById("mostrarShiny");
      if (mydiv.style.display === "block" || mydiv.style.display === "")
        mydiv.style.display = "none";
      else mydiv.style.display = "block";
    },
  },
  created() {
    this.defineInformations(this.pokemonUrl);
  },
};
</script>

<style scoped>
.modal-backdrop {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  position: fixed;
  padding: 90px 10px 10px;
  width: calc(100% - 20px);
  height: calc(100vh - 20px);
  background: rgba(255, 255, 255, 0.719);
}

.modal {
  margin-top: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  height: 500px;
  width: 320px;
  padding: 50px 0 0;
  background-color: #ff0000;
  border-radius: 15px;
  transition: 0.5s;
  overflow: visible;
  border: 3px solid black;
  border-bottom: 0;
  box-shadow: inset 2px 2px rgba(255, 255, 255, 0.623);
}

.modal2 {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  width: 314px;
  height: 400px;
  bottom: 0;
  right: 0;
  background-color: #ff0000;
  transition: 0.5s;
  border-bottom-left-radius: 15px;
  border-bottom-right-radius: 15px;
  border: 3px solid black;
  border-left: 0;
  border-right: 0;
  box-shadow: inset 2px 2px rgba(255, 255, 255, 0.623);
}

#modal:hover > #modal2 {
  transform: rotateY(180deg) translateZ(1px) translateX(-314px);
  border-bottom-right-radius: 15px;
  border-top-left-radius: 15px;
  border-bottom-right-radius: 0;
  border: 3px solid black;
  box-shadow: inset 0 0 rgba(255, 255, 255, 0.623);
}

#modal:hover {
  transform: translateX(-130px);
  border-left: 3px solid black;
  border-top: 3px solid black;
  border-right: 3px solid black;
  border-bottom-right-radius: 0;
}

.modal:hover > .light-circle {
  background: #74c6fa;
}

.modal:hover > .detalhe {
  border: 0;
}

.modal:hover > .informacoes {
  transition: all 0.2s ease 0.4s;
  opacity: 1;
}

.circle1:hover {
  background: #ff584d;
}

.visorPokemon {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  width: 160px;
  height: 140px;
  background: lightblue;
  border: 1px solid black;
  border-radius: 7px;
  margin-bottom: 5px;
}

.bordaVisorPokemon {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  width: 220px;
  height: 205px;
  background: white;
  top: 0;
  margin-top: 130px;
  border-radius: 7px;
  border-bottom-left-radius: 30px;
  border: 2px solid black;
}

.junta {
  display: flex;
  width: 20px;
  height: 400px;
  position: absolute;
  bottom: 0;
  right: 0;
  border-left: 3px solid black;
  border-top: 3px solid black;
  border-bottom: 3px solid black;
  border-radius: 3px;
}

.junta-quadrado {
  display: flex;
  width: 20px;
  height: 30px;
  position: absolute;
}

.light-circle {
  position: absolute;
  display: flex;
  top: 0;
  left: 0;
  width: 70px;
  height: 70px;
  border-radius: 50%;
  background: rgb(0, 110, 255);
  border: 7px solid white;
  margin-top: 10px;
  margin-left: 10px;
  transition: 0.8s;
  box-shadow: inset 0 0 7px 3px rgba(68, 68, 68, 0.24);
}

.circle1 {
  position: absolute;
  display: flex;
  top: 0;
  left: 0;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #ff0000;
  border: 2px solid black;
  margin-top: 15px;
  margin-left: 90px;
  transition: 0.4s;
  box-shadow: inset 0 0 0 2px rgba(0, 0, 0, 0.24);
}

.circle2 {
  position: absolute;
  display: flex;
  top: 0;
  left: 0;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: yellow;
  border: 2px solid black;
  margin-top: 15px;
  margin-left: 115px;
  box-shadow: inset 0 0 0 2px rgba(0, 0, 0, 0.24);
}

.circle3 {
  display: flex;
  position: absolute;
  top: 0;
  left: 0;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: green;
  border: 2px solid black;
  margin-top: 15px;
  margin-left: 140px;
  box-shadow: inset 0 0 0 2px rgba(0, 0, 0, 0.24);
}

.circle-red {
  display: flex;
  position: absolute;
  top: 0;
  left: 0;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: red;
}

.container-botao {
  display: flex;
  position: absolute;
  bottom: 0;
  right: 0;
  width: 90px;
  height: 90px;
  margin-right: 50px;
  margin-bottom: 40px;
}

.botao {
  display: flex;
  position: absolute;
  width: 30px;
  height: 30px;
  background: black;
}

.seta-botao {
  display: flex;
  position: absolute;
  justify-content: center;
  align-items: center;
  border-left: 8px solid transparent;
  border-right: 0px solid transparent;
  border-bottom: 8px solid white;
}

.detalhe {
  display: flex;
  position: absolute;
  bottom: 0;
  border: 2px solid black;
  width: 110px;
  height: 13px;
  margin-bottom: 20px;
  border-radius: 10px;
  transition: 0.7s;
}

.botao:active > .seta-botao {
  border-left: 6px solid transparent;
  border-right: 0px solid transparent;
  border-bottom: 6px solid white;
}

.informacoes {
  display: flex;
  position: absolute;
  top: 0;
  left: 0;
  margin-top: 150px;
  margin-left: 370px;
  width: 200px;
  height: 100px;
  opacity: 0;
  background: black;
  border-radius: 4px;
}

h6 {
  color: white;
  font-family: "Press Start 2P", sans-serif;
  font-size: 10px;
}

@import url("https://fonts.googleapis.com/css?family=Press+Start+2P");
</style>