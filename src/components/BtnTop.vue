<template>
    <a class="button is-rounded fixed-button" @click="scrollToTop">
      <span class="icon">
        <i class="fa fa-arrow-up" style="color: aliceblue;"></i>
      </span>
      <!-- <span>Topo</span> -->
    </a>
</template>

<script>
export default {
  name: "BtnTop",
  methods: {
    scrollToTop() {
      window.scrollTo({top: 0, behavior: "smooth"});
    },
  },
};
</script>

<style scoped>
.fixed-button {
  position: fixed;
  bottom: 20px;
  right: 20px;
  z-index: 999;
  background-color: rgb(216, 63, 63);
  color: aliceblue;
  border: 0px;
  transition: all 0.3s ease-in-out;
}

.ampliado {
  transform: scale(1.2);
}

.reduzido {
  transform: scale(0.8);
}
</style>
