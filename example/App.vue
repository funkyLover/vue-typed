<template>
  <div id="app">
    <h1>{{ msg }}</h1>
    <type class="type" :str="'Well, this will type a sentence'" :type-speed="20" v-on:done="done" :cleanCursor="true"></type>
    <type class="type" :str="'Well, this will type second sentence'" :type-speed="20" v-on:done="done" v-if="sentenceIndex > 0" :cleanCursor="true"></type>
    <type class="type" :str="'Well, this will type third sentence,\nAnd it will type in a newline!'" :type-speed="20" v-on:done="done" v-if="sentenceIndex > 1" :cleanCursor="true"></type>
    <type class="type" :str="'Well, this will type fourth sentence,\n\tAnd it will type in a newline with a tab prefix!'" :type-speed="20" v-on:done="done" v-if="sentenceIndex > 2"></type>
  </div>
</template>

<script>
import Type from '../src/typed.vue'

export default {
  components: {
    Type
  },
  data () {
    return {
      msg: 'Hello Vue 2.0!',
      sentenceIndex: 0
    }
  },
  methods: {
    done () {
      this.sentenceIndex += 1
      console.log('type done')
    }
  }
}
</script>

<style>
body {
  font-family: Helvetica, sans-serif;
}
.type {
  display: block;
  width: 100%;
  white-space: pre;
}
</style>