<template>
  <div id="app" class="container">
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
.container
  margin: 0 auto
  width: 960px
@media (min-width: 1200px)
  .container
    width: 80%
@media (max-width: 991px)
  .container
    width: 720px
@media (max-width: 767px)
  .container
    width: 540px
@media (max-width: 574px)
  .container
    width: 100%
</style>
