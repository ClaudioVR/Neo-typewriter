<template>
  <div class="screen black">
    <v-container class="">
      <div id="title" class="text-center">#3ab508 NeoTyper</div>
      <div id="subtitle" class="text-center">your mindfulness online typer</div>

      <TextEditor class="mt-5" />

    </v-container>
  </div>
</template>

<script>
import TextEditor from '../components/TextEditor.vue';
  export default {
    name: 'HelloWorld',
    components: {
      TextEditor
    },
    data: () => ({

    }),
  }
</script>

<style>
.screen {
  height: 10000px;
  font-family: 'Source Code Pro', monospace !important;
  color: #3ab508;
}

#title {
  font-size: 2rem;
  color: #3ab508;
  text-shadow: 2px 2px 5px #3ab508;
}

#subtitle {
  font-size: .8rem;
  color: #3ab508;
}

#input-15 {
  color: #3ab508;
}

*:focus {
  outline: none;
}

.ProseMirror {
  border: 1px solid #3ab508;
  border-radius: 5px;
  min-height: 700px;
  padding: 1rem;
}

</style>
