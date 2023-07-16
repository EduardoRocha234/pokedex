<template>
  <nav
    class="navbar is-fixed-top"
    role="navigation"
    aria-label="main navigation"
    style="background-color: rgb(221, 56, 56); color: aliceblue"
  >
    <div class="navbar-brand">
      <a class="navbar-item" href="/">
        <img src="../assets/pokebola.png" />
      </a>
      <span class="is-size-3" style="margin-top: 3px;">Pokedex</span>
      <input
        v-if="!isMobile"
        class="input is-rounded is-normal navbar-item"
        style="margin-top: 6px; margin-left: 20px; width: auto"
        type="text"
        placeholder="Pesquisar Pokemom"
        v-model="search"
        aria-expanded="false"
      />
      <a
        role="button"
        class="navbar-burger"
        aria-label="menu"
        aria-expanded="false"
        data-target="navbarBasicExample"
        @click="drop = !drop"
      >
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
      </a>
    </div>

    <div
      id="navbarBasicExample"
      :class="`navbar-menu ${drop ? 'is-active' : ''}`"
    >
      <div v-if="isMobile" class="navbar-start">
        <a
          class="navbar-item"
          href="https://github.com/EduardoRocha234"
          target="blank"
        >
          Visite meu github
        </a>
        <a class="navbar-item" href="/" target="blank">
          Veja o código do projeto
        </a>
        <a class="navbar-item" href="https://pokeapi.co/" target="blank">
          API usada
        </a>
        <hr class="navbar-divider" />
        <a
          class="navbar-item"
          href="https://www.instagram.com/eduardoraleixo/"
          target="blank"
        >
          <span class="icon-text">
            <span class="icon">
              <i class="fa fa-instagram"></i>
            </span>
            <span>@eduardoraleixo</span>
          </span>
        </a>
        <a
          class="navbar-item"
          href="https://twitter.com/EduardoRochaAl7?t=uKabqUZLxCZlQ-zHLvquBA&s=09"
          target="blank"
        >
          <span class="icon-text">
            <span class="icon">
              <i class="fa fa-twitter"></i>
            </span>
            <span>@EduardoRochaAl7</span>
          </span>
        </a>
        <a
          class="navbar-item"
          href="https://www.linkedin.com/in/eduardo-rocha-aleixo-068969227/"
          target="blank"
        >
          <span class="icon-text">
            <span class="icon">
              <i class="fa fa-linkedin-square"></i>
            </span>
            <span>Meu Linkedin</span>
          </span>
        </a>
      </div>

      <div class="navbar-end" :hidden="isMobile">
        <div class="navbar-item has-dropdown is-hoverable">
          <a class="navbar-link has-text-white-ter" href="#"> Info </a>
          <div class="navbar-dropdown is-boxed is-right">
            <a
              class="navbar-item"
              href="https://github.com/EduardoRocha234"
              target="blank"
            >
              Visite meu github
            </a>
            <a class="navbar-item" href="/" target="blank">
              Veja o código do projeto
            </a>
            <a class="navbar-item" href="https://pokeapi.co/" target="blank">
              API usada
            </a>
            <hr class="navbar-divider" />
            <a
              class="navbar-item"
              href="https://www.instagram.com/eduardoraleixo/"
              target="blank"
            >
              <span class="icon-text">
                <span class="icon">
                  <i class="fa fa-instagram"></i>
                </span>
                <span>@eduardoraleixo</span>
              </span>
            </a>
            <a
              class="navbar-item"
              href="https://twitter.com/EduardoRochaAl7?t=uKabqUZLxCZlQ-zHLvquBA&s=09"
              target="blank"
            >
              <span class="icon-text">
                <span class="icon">
                  <i class="fa fa-twitter"></i>
                </span>
                <span>@EduardoRochaAl7</span>
              </span>
            </a>
            <a
              class="navbar-item"
              href="https://www.linkedin.com/in/eduardo-rocha-aleixo-068969227/"
              target="blank"
            >
              <span class="icon-text">
                <span class="icon">
                  <i class="fa fa-linkedin-square"></i>
                </span>
                <span>Meu Linkedin</span>
              </span>
            </a>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "NavBar",
  // props: {
  //   num: Number,
  //   name: String,
  //   url: String,
  // },
  data() {
    return {
      search: "",
      isMobile: false,
      windowSize: 0,
      drop: false,
    };
  },

  watch: {
    search(newValue) {
      if (newValue || newValue == "" || newValue == " ") {
        this.$emit("search", newValue);
      }
    },
  },

  mounted() {
    this.getWindowSize();
    window.addEventListener("resize", this.getWindowSize);
  },

  beforeUnmount() {
    window.removeEventListener("resize", this.getWindowSize);
  },

  methods: {
    getWindowSize() {
      this.windowSize = window.innerWidth;
      if (this.windowSize < 1036) {
        this.isMobile = true;
        this.$emit('isMobile', this.isMobile)
      } else {
        this.isMobile = false;
        this.$emit('isMobile', this.isMobile)
      }
    },
  },
};
</script>

<style></style>
