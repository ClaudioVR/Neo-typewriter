<template>
  <div class="home black">
    <vue-typer
      :text='["Wake up, Neo...", "Are you ready to write your novel?"]'
      :repeat='0'
      :shuffle='false'
      initial-action='typing'
      :pre-type-delay='70'
      :type-delay='70'
      :pre-erase-delay='5000'
      :erase-delay='100'
      erase-style='backspace'
      :erase-on-complete='false'
      caret-animation='smooth'
    ></vue-typer>
  </div>
</template>

<script>
import { VueTyper } from 'vue-typer'
export default {
  components: {
    VueTyper
  },
  data() {
    return {

    }
  },
  created() {
    setTimeout( () => {
      this.$router.push('/neo')
    }, 14500)
  }
}
</script>

<style lang="css">
.home {
  height: 100vh;
  padding: 100px 200px;
  font-family: 'Source Code Pro', monospace !important;

}
.vue-typer .custom.char.typed {
  color: #3ab508;
  font-size: 2rem;
}
</style>
