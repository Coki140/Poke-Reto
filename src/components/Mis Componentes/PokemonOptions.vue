<template>
  <div class="options-container">
    <h2>Su nombre es:</h2>
    <ul>
      <li
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        @click="$emit('selection', pokemon.id)"
      >
        {{ pokemon.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    pokemons: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style>
ul {
  list-style-type: none;
}
li {
  background-color: rgba(173, 173, 173, 0.514);
  border-radius: 5px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  cursor: pointer;
  color: rgb(0, 0, 0);
  margin-bottom: 10px;
  padding: 2px;
  width: 100px;
}

li:hover {
  background-color: rgba(184, 184, 184);
}

.options-container {
  display: flex;
  justify-content: center;
}
</style>
