<template>
  <div class="tools">
    <round></round>
    <button type="button" class="startButton" v-on:click= "start()">Start</button>
  </div>
</template>

<script>
    import Round
      from "./Round";

    export default {
        name: "Tools",
        components: {Round},
        methods: {
            start () {
                Event.$emit('start', this.name)
            }
        }
    }
</script>

<style scoped>

  .tools {
    position: absolute;
    background: grey;
    border-radius: 50%;
    height: 250px;
    width: 250px;
    border-style: solid;
    border-width: 10px;
    top: 50%;
    left: 50%;
    margin: -125px 0px 0px -125px;
    box-sizing: border-box;
    -moz-box-sizing: border-box;
    -webkit-box-sizing: border-box;
  }

  button{height:20px; position:relative; margin: -20px -50px; width:100px; top:50%; left:50%;}
</style>
