<template>
  <div>
    <div>
      <h1 v-if="!pokemon">Espere por favor...</h1>
    </div>
    <div v-if="pokemon">
      <h1>¿Quién es este Pokémon?</h1>
      <PokemonPicture :pokemonId="pokemon.id" :shadowPokemon="shadowPokemon" />
      <PokemonOptions :pokemons="pokemonsArr" @selection="checkAnsewer" />
    </div>
    <div v-if="shadowAnswer">
      <h2 class="fade-in">{{ message }}</h2>
      <button class="fade-in" @click="newGame">Nuevo juego</button>
    </div>
  </div>
</template>

<script>
import PokemonPicture from "@/components/Mis Componentes/PokemonPicture.vue";
import PokemonOptions from "@/components/Mis Componentes/PokemonOptions.vue";
import getPokemonOptions from "@/helpers/getPokemonOptions.js";

export default {
  components: {
    PokemonPicture,
    PokemonOptions,
  },
  data() {
    return {
      pokemonsArr: [],
      pokemon: null,
      shadowPokemon: false,
      shadowAnswer: false,
      message: "",
    };
  },
  methods: {
    async mixPokemonArray() {
      try {
        this.pokemonsArr = await getPokemonOptions();
        const rndInt = Math.floor(Math.random() * this.pokemonsArr.length);
        this.pokemon = this.pokemonsArr[rndInt];
      } catch (error) {
        console.error("Error al obtener los Pokémon:", error);
      }
    },
    checkAnsewer(selectedId) {
      this.shadowPokemon = true;
      this.shadowAnswer = true;

      if (selectedId == this.pokemon.id) {
        this.message = `Correcto: ${this.pokemon.name}`;
      } else {
        this.message = `Incorrecto: ${this.pokemon.name}`;
      }
    },
    newGame() {
      this.shadowPokemon = false;
      this.shadowAnswer = false;
      this.pokemonArr = [];
      this.mixPokemonArray();
      this.pokemon = null;
    },
  },
  mounted() {
    this.mixPokemonArray();
  },
};
</script>

<style scoped>
div {
  text-align: center;
}
button {
  background-color: rgba(173, 173, 173, 0.514);
  border-radius: 5px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  cursor: pointer;
  color: rgb(0, 0, 0);
  margin-bottom: 10px;
  padding: 2px;
  width: 100px;
  transition-property: all;
  transition-duration: 0.3s;
}
button:hover {
  background-color: rgb(255, 255, 255);
}
</style>
