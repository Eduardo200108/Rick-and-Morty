<script>
import axios from "axios";

let API_URL = `https://rickandmortyapi.com/api/character`;

export default {
  data() {
    return {
      info: [],
      personajes: [],
      cont: 2,
    };
  },

  mounted() {
    axios.get(API_URL).then((response) => {
      this.info = response.data.info;
      this.personajes = response.data.results;
    });
  },

  methods: {
    pag(num) {
      API_URL = "https://rickandmortyapi.com/api/character/?page=" + num;
      console.log(API_URL);
      axios.get(API_URL).then((response) => {
        console.log(response.config);
        this.info = response.data.info;
        this.personajes = response.data.results;
      });
      this.cont++;
    },
  },
};
</script>

<template>
  <h2 class="flex text-center justify-center gap-10 p-5">
    Hay {{ info.count }} personajes en el programa de Rick & Morty
  </h2>
  <button @click="pag(cont)">{{ cont }}</button>
  <button
    class="bg-cyan-400 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full"
    @click="pag(cont)"
  >
    página {{ cont }}   
  </button>
  <ul>
    <li v-for="p in personajes" class="flex text-center justify-center gap-10 p-5">
      <!--centrar imagenes-->
      <a>{{ p.name }} id:{{ p.id }} estado:{{ p.status }}</a>
      <img v-bind:src="p.image" alt="no image" /><!--lector de imagenes-->
    </li>
  </ul>
</template>
<style>
@import url("https://fonts.googleapis.com/css2?family=Patrick+Hand+SC&display=swap");
* {
  font-family: "Patrick Hand SC", cursive;
}
</style>
