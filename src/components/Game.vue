<template>
    <div class="game">
        <div class="red" v-on:click= "handleClick($event)"></div>
        <div class="blue" v-on:click= "handleClick($event)"></div>
        <div class="yellow" v-on:click= "handleClick($event)"></div>
        <div class="green" v-on:click= "handleClick($event)"></div>
        <tools></tools>
    </div>
</template>

<script>
    import Tools
        from "./Tools";

    export default {
        name: "game",
        components: {Tools},
        data() {
            return {
                order: [],
                playerOrder: [],
                good: null,
                flash: null,
                turn: 0,
                win: null,
                compTurn: null,
                intervalId: null
            }
        },
        methods: {
            handleClick(target) {
                const self = this
                this.playerOrder.push(self.currentIndex)
                this.check()
                // Bind styling attributes
                //target.style.opacity = "0.5"
                //target.style.filter = "alpha(opacity=50)"

                if(!this.win) {
                    setTimeout(() => {
                        // Bind styling attributes
                        // target.style.opacity = "0"
                        // target.style.filter = "alpha(opacity=0)"
                    }, 300)
                }
            },
            check() {
                if (this.playerOrder[this.playerOrder.length - 1] !== this.order[this.playerOrder.length - 1])
                    this.good = false

                if (this.playerOrder.length == 3 && this.good) {
                    this.winGame()
                }

                if (this.good == false) {
                    // Bind styling attributes
                    // flashColor()
                    // turnCounter.innerHTML = "NO!"
                    setTimeout(() => {
                        // Bind styling attributes
                        //turnCounter.innerHTML = turn;
                        //clearColor()
                        this.play()
                    }, 800)
                }

                if (this.turn == this.playerOrder.length && this.good && !this.win) {
                    this.turn++
                    this.playerOrder = []
                    this.compTurn = true
                    this.flash = 0
                    // Bind styling attributes
                    //turnCounter.innerHTML = this.turn;
                    this.intervalId = setInterval(this.gameTurn, 800)
                }
            },
            gameTurn() {

                if (this.flash == this.turn) {
                    clearInterval(this.intervalId)
                    this.compTurn = false
                    // Bind styling attributes
                    //clearColor()
                }

                if (this.compTurn) {
                    // Bind styling attributes
                    //clearColor();
                    setTimeout(() => {
                        if (this.order[this.flash] == 1)  //one() // Bind styling attributes
                        if (this.order[this.flash] == 2)  //two() // Bind styling attributes
                        if (this.order[this.flash] == 3)  //three() // Bind styling attributes
                        if (this.order[this.flash] == 4)  //four() // Bind styling attributes
                        this.flash++
                    }, 200)
                }
            },
            play() {
                this.win = false
                this.order = []
                this.playerOrder = []
                this.flash = 0
                this.intervalId = 0
                this.turn = 1
                // Bind styling attributes
                //turnCounter.innerHTML = 1
                this.good = true
                for (var i = 0; i < 20; i++) {
                    this.order.push(Math.floor(Math.random() * 4) + 1)
                }
                this.compTurn = true
                this.intervalId = setInterval(this.gameTurn, 800)
            },
            winGame() {
                // Bind styling attributes
                //flashColor();
                //turnCounter.innerHTML = "WIN!";
                win = true;
            }
        },
        created() {
            Event.$on('start', (name) => {
                this.play();
            })
        }
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
