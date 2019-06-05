<template>
    <div class="highScore">{{this.$parent.highScore}}</div>
</template>

<script>
    export default {
        name: "HighScore"
    }
</script>

<style scoped>
    .highScore{
        position: absolute;
        background: #330000;
        color: red;
        font-family: courier;
        font-size: 20px;
        height: 30px;
        width: 50px;
        margin-left: 90px;
        margin-top: 50px;
        text-align: center;
        vertical-align: middle;
        line-height: 30px;
    }
</style>
