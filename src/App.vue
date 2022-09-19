<template>
  <div class="main">
    <the-header></the-header>
    <div class="center">
      <div class="img-container">
        <img src="./img/undraw_ideation_re_8i2h.png" alt="Farming girl" />
      </div>
      <router-view v-slot="slotProps" class="static-element">
        <transition name="route" mode="out-in">
          <component :is="slotProps.Component"></component>
        </transition>
      </router-view>
    </div>
  </div>
</template>

<script>
import TheHeader from './components/layout/TheHeader.vue';

export default {
  components: {
    TheHeader,
  },
  created() {
    this.$store.dispatch('tryLogin');
  },
  computed: {
    didAutoLogout() {
      return this.$store.getters.didAutoLogout;
    },
  },
  watch: {
    didAutoLogout(curValue, oldValue) {
      if (curValue && curValue !== oldValue) {
        this.$router.replace('/coaches');
      }
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

* {
  box-sizing: border-box;
}

html {
  font-family: 'Roboto', sans-serif;
}

body {
  margin: 0;
}

.center {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
}

.static-element {
  width: 50vw;
}

.route-enter-from {
  opacity: 0;
  transform: translateY(-30px);
}

.route-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
.route-enter-to,
.route-leave-from {
  opacity: 1;
  transform: translateY(0);
}

.route-enter-active {
  transition: all 0.3s ease-out;
}
.route-leave-active {
  transition: all 0.3s ease-out;
}
.img-container {
  width: 40vw;
  overflow: hidden;
  text-align: center;
}
img {
  width: 100%;
  transform: scaleX(-1);
  pointer-events: none;
}

@media screen and (max-width: 768px) {
  .center {
    flex-direction: column;
  }
  .img-container {
    width: 100vw;
    pointer-events: none;
  }
  .static-element {
    width: 90vw;
  }
}
</style>
