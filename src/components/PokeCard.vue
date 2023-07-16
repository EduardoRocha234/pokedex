<template>
  <div id="pokemon">
    <div
      class="card"
      style="background-color: rgb(221, 56, 56); border: solid 4px black"
    >
      <div class="card-image is-flex is-justify-content-center" id="image">
        <div id="border-img">
          <div id="desc">
            <p class="title is-4">{{ upper }}</p>
            <p class="subtitle is-6">{{ pokemon.type }}</p>
          </div>
          <figure class="image is-128x128 mt-4">
            <img :src="currentImg" :alt="upper" />
          </figure>
        </div>
      </div>
      <div class="card-content is-flex is-justify-content-space-between">
        <div>
          <table class="table mt-4" id="tableStats">
            <tbody v-for="(stat, idx) in pokemon.stats" :key="idx">
              <tr>
                <th>{{ stat.stat.name.toUpperCase() }}</th>
                <th>
                  <progress
                    :class="`progress ${colorProgress(idx)} is-small`"
                    :value="stat.base_stat"
                    max="100"
                    style="width: 5rem"
                  ></progress>
                </th>
                <th>{{ stat.base_stat }}</th>
              </tr>
            </tbody>
          </table>
        </div>
        <a
          style="cursor: pointer; padding-top: 3.8rem; padding-left: 1.7rem"
          @click="mudarSprite"
        >
          <figure class="image is-64x64 mr-4" :id="name">
            <img src="./../assets/control.png" />
          </figure>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "PokeCard",
  props: {
    num: Number,
    name: String,
    url: String,
  },

  data() {
    return {
      isFront: true,
      currentImg: "",
      pokemon: {
        type: "",
        front: "",
        back: "",
        stats: [],
      },
    };
  },

  computed: {
    upper() {
      return this.name[0].toUpperCase() + this.name.slice(1);
    },
  },

  methods: {
    mudarSprite() {
      if (this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.back;
      } else {
        this.isFront = true;
        this.currentImg = this.pokemon.front;
      }

      var joystick = document.getElementById(this.name);
      joystick.classList.toggle("reduzido");
      setTimeout(() => {
        joystick.classList.remove("reduzido");
      }, 1);
    },
    colorProgress(idx) {
      if (idx == 0) {
        return "is-primary";
      } else if (idx == 1) {
        return "is-link";
      } else if (idx == 2) {
        return "is-info";
      } else if (idx == 3) {
        return "is-success";
      } else if (idx == 4) {
        return "is-warning";
      }
      return "progress";
    },
  },

  created() {
    axios
      .get(this.url)
      .then((res) => {
        this.pokemon.type = res.data.types[0].type.name;
        this.pokemon.front = res.data.sprites.front_default;
        this.pokemon.back = res.data.sprites.back_default;
        this.pokemon.stats = res.data.stats;
        this.currentImg = this.pokemon.front;
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style src="../../public/css/pokecard.css" />
