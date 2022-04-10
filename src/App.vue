<template>
  <div id="app">
    <Splitting debug sentence="Hello my name is Adam" wordClassName="WORDZ" characterClassName="CHARZ"/>
  </div>
</template>

<script>
import Splitting from './components/Splitting.vue'

export default {
  name: 'App',
  components: {Splitting}
}
</script>

