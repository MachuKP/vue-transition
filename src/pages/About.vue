<script setup>
import { gsap } from "gsap";

const beforEnter = (el) => {
  gsap.from(el, {
    y: -60,
    opacity: 0
  })
  // el.style.transform = "translateY(-60px)"
  // el.style.opacity = 0
};
const enter = (el, done) => {
  gsap.to(el, {
    duration: 0.4,
    y: 0,
    opacity: 1,
    onComplete: done,
    ease: 'bounce.out'
  })
};
</script>

<template>
  <div class="about">
    <transition
      appear
      @before-enter="beforEnter"
      @enter="enter"
    >
      <h1>About</h1>
    </transition>
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Nisi alias
      quaerat laboriosam, quas at ex quod. Corporis rerum soluta et?
    </p>
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Nisi alias
      quaerat laboriosam, quas at ex quod. Corporis rerum soluta et?
    </p>
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Nisi alias
      quaerat laboriosam, quas at ex quod. Corporis rerum soluta et?
    </p>
  </div>
</template>

<style scoped>
.about {
  max-width: 600px;
  margin: 20px auto;
}
</style>
