<template>
  <div id="app">
    <NavBar
      @search="(str) => (search = str)"
      @isMobile="(bol) => (isMobile = bol)"
    />
    <div class="columns" style="margin-top: 40px">
      <div class="column"></div>
      <progress
        v-if="searchResults.length == 0"
        class="progress is-danger is-small"
        max="100"
        style="width: 500%; margin-left: -150%; margin-top: -19px"
      ></progress>
      <div class="column is-one-third">
        <div class="is-flex is-justify-content-center">
          <div class="field" v-if="isMobile" >
            <p class="control has-icons-left has-icons-right">  
              <input
                class="input is-rounded navbar-item is-hovered"
                style="margin-top: -5px; margin-left: 20px; width: auto"
                type="text"
                placeholder="Pesquisar Pokemom"
                v-model="search"
                aria-expanded="false"
              />
              <span class="icon is-small is-right">
                <i class="fa fa-search"></i>
              </span>
            </p>
          </div>
        </div>
        <hr v-if="isMobile" class="ml-2" />
        <div v-for="(pokemon, idx) in searchResults" :key="pokemon.url">
          <PokemonCard :name="pokemon.name" :url="pokemon.url" :num="idx + 1" />
        </div>
      </div>
      <div class="column"></div>
    </div>
  </div>
  <BtnTop />
</template>

<script>
import axios from "axios";
import PokemonCard from "@/components/PokeCard.vue";
import NavBar from "@/components/NavBar.vue";
import BtnTop from "@/components/BtnTop.vue";

export default {
  name: "App",
  components: {
    PokemonCard,
    NavBar,
    BtnTop,
  },
  data: () => ({
    pokemons: [],
    search: "",
    isMobile: false,
  }),

  computed: {
    searchResults() {
      if (this.search == "" || this.search == " ") {
        console.log(this.search);
        return this.pokemons;
      } else {
        console.log(this.search);
        return this.pokemons.filter(
          (pokemon) => pokemon.name == this.search.toLocaleLowerCase()
        );
      }
    },
  },

  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        console.log("Pegou a lista de pokemons");
        this.pokemons = res.data.results;
        console.log(this.pokemons);
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style></style>
