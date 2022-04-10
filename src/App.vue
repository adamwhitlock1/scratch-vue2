<template>
  <div id="app">
    <input type="text" v-model="customSentence" style="width: 90vw">
    <Splitting debug :sentence="customSentence" :hover="addHoverClass" />
  </div>
</template>

<script>
import { gsap } from 'gsap'
import Splitting from './components/Splitting.vue'

export default {
  name: 'App',
  components: {Splitting},
  data() {
    return {
      customSentence: "Type a sentence here and behold the magic!"
    }
  },
  methods: {
    addHoverClass({ref}) {
      ref.classList.add('hover-bro')
      gsap.fromTo(ref,{autoAlpha:1},{autoAlpha:0, duration: 0.5});
    }
  }
}
</script>

