<template>
  <div id="app" class="app">
    <Form />

  </div>
</template>

<script>
import Form from './views/Form';

export default {
  name: 'App',
  components: {
    Form,
  },
}
</script>

<style lang="sass">
#app
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  color: #2d4155
</style>
