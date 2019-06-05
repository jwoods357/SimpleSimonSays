<template>
  <div id="app">
    <h1>Simple Simon Says</h1>
    <Game></Game>
  </div>
</template>

<script>

import Game
  from "./components/Game";

export default {
  name: 'app',
  components: {Game},
  data () {
    return {
    }
  }
}
</script>

<style lang="scss">
#app {
  margin: auto;
  width: 50%;
  padding: 10px;
}

h1, h2 {
  font-weight: normal;
  text-align: center;
}
</style>
