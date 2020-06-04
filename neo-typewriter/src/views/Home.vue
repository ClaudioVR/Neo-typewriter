<template>
  <div class="home black">
    <vue-typer
      :text='["Wake up, Neo...", "It is time to write..."]'
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
    console.log(window.innerWidth)
    setTimeout( () => {
      this.$router.push('/neo')
    }, 12500)
  }
}
</script>

<style lang="css">
.home {
  height: 100vh;
  /* font-family: 'Source Code Pro', monospace !important; */
  font-family: 'Press Start 2P', cursive !important;
  padding: 50px 30px;
}
.vue-typer .custom.char.typed {
  color: #3ab508;
  font-size: .7rem;
}

@media only screen and (min-width: 700px) {
  .home {
    padding: 60px;
  }
  .vue-typer .custom.char.typed {
    font-size: 1.5rem !important;
  }
}
</style>
