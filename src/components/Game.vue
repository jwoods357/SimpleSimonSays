<template>
    <div class="game">
        <div class="red"></div>
        <div class="blue"></div>
        <div class="yellow"></div>
        <div class="green"></div>
        <tools></tools>
    </div>
</template>

<script>
    import Tools
        from "./Tools";

    export default {
        name: "game",
        components: {Tools},
    }
</script>

<style scoped>
    .game {
        background: #385a94;
        border-radius: 50%;
        height: 500px;
        width: 500px;
        position: relative;
        border-style: solid;
        border-width: 10px;
        margin: auto;
        margin-top: 60px;
        box-shadow: 8px 8px 15px 5px #888888;
    }

    .red {
        position: absolute;
        height: 250px;
        width: 250px;
        border-radius: 250px 0 0 0;
        -moz-border-radius: 250px 0 0 0;
        -webkit-border-radius: 250px 0 0 0;
        background: darkgreen;
        top: 50%;
        left: 50%;
        margin: -250px 0px 0px -250px;
        border-style: solid;
        border-width: 5px;
        box-sizing: border-box;
        -moz-box-sizing: border-box;
        -webkit-box-sizing: border-box;
    }

    .blue {
        position: absolute;
        height: 250px;
        width: 250px;
        border-radius: 0 250px 0 0;
        -moz-border-radius: 0 250px 0 0;
        -webkit-border-radius: 0 250px 0 0;
        background: darkred;
        top: 50%;
        left: 50%;
        margin: -250px 0px 0px 0px;
        border-style: solid;
        border-width: 5px;
        box-sizing: border-box;
        -moz-box-sizing: border-box;
        -webkit-box-sizing: border-box;
    }

    .yellow {
        position: absolute;
        height: 250px;
        width: 250px;
        border-radius: 0 0 0 250px;
        -moz-border-radius: 0 0 0 250px;
        -webkit-border-radius: 0 0 0 250px;
        background: goldenrod;
        top: 50%;
        left: 50%;
        margin: 0px -250px 0px -250px;
        border-style: solid;
        border-width: 5px;
        box-sizing: border-box;
        -moz-box-sizing: border-box;
        -webkit-box-sizing: border-box;
    }

    .green {
        position: absolute;
        height: 250px;
        width: 250px;
        border-radius: 0 0 250px 0;
        -moz-border-radius: 0 0 250px 0;
        -webkit-border-radius: 0 0 250px 0;
        background: darkblue;
        top: 50%;
        left: 50%;
        margin: 0px 0px -250px 0px;
        border-style: solid;
        border-width: 5px;
        box-sizing: border-box;
        -moz-box-sizing: border-box;
        -webkit-box-sizing: border-box;
    }
</style>
