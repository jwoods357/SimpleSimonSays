<template>
    <div class="game">
        <div class="green" v-bind:class="{flashButton: active.green === true}" v-on:click= "handleClick($event)"></div>
        <div class="red" v-bind:class="{flashButton: active.red === true}" v-on:click= "handleClick($event)"></div>
        <div class="yellow" v-bind:class="{flashButton: active.yellow === true}" v-on:click= "handleClick($event)"></div>
        <div class="blue" v-bind:class="{flashButton: active.blue === true}" v-on:click= "handleClick($event)"></div>
        <div class="tools">
          <high-score></high-score>
          <round></round>
          <div class="roundText">
            Round
          </div>
          <div class="highScoreText">
            High Score
          </div>
          <button type="button" class="startButton" v-on:click= "play()">Start</button>
        </div>
    </div>
</template>

<script>
    import Round
      from "./Round";

    import HighScore
      from "./HighScore";

    export default {
        name: "game",
        components: {
            HighScore,
            Round},
        data() {
            return {
                order: [],
                playerOrder: [],
                good: null,
                flash: null,
                turn: 0,
                win: null,
                compTurn: null,
                intervalId: null,
                clickCount: 0,
                active:{
                    green: false,
                    red: false,
                    yellow: false,
                    blue: false,
                },
                highScore: 0,
            }
        },
        methods: {
            handleClick(target) {
                // Get player selection
                const self = this
                let index;

                console.log(target.currentTarget.className)

                switch(target.currentTarget.className) {
                    case "green":
                        index = 1;
                        break;
                    case "red":
                        index = 2;
                        break;
                    case "yellow":
                        index = 3;
                        break;
                    case "blue":
                        index = 4;
                        break;
                }

                self.playerOrder.push(index)
                self.check()
            },
            check() {
                const self = this

                if (self.playerOrder[self.playerOrder.length - 1] !== self.order[self.playerOrder.length - 1]) {
                    self.good = false
                }

                if (self.good == false) {
                    self.flashColor()

                    setTimeout(() => {
                        self.clearColor()
                        self.play()
                    }, 800)
                }

                if (self.turn == self.playerOrder.length && self.good ) {
                    console.log('current Highscore: ' + localStorage.highScore)
                    if( self.turn > ( localStorage.highScore || 0 )) {
                      console.log('New High Score: ' + self.turn)

                     self.highScore = self.turn;
                    }

                    self.turn++
                    self.playerOrder = []
                    self.compTurn = true
                    self.flash = 0
                    self.intervalId = setInterval(self.gameTurn, 800)
                }
            },
            gameTurn() {
                const self = this

                // Will stop sequence based on turn
                if (self.flash == self.turn) {
                    clearInterval(self.intervalId)
                    self.compTurn = false
                    self.clearColor()
                }

                if (this.compTurn) {
                    // Will flash sequence using binded classes after interval
                    self.clearColor();
                    setTimeout(() => {
                        switch (self.order[self.flash]) {
                            case 1:
                                self.active.green = true
                                break;
                            case 2:
                                self.active.red = true
                                break;
                            case 3:
                                self.active.yellow = true
                                break;
                            case 4:
                                self.active.blue = true
                                break;
                        }

                        self.flash++
                    }, 200)
                }
            },
            play() {
                const self = this

                self.win = false
                self.order = []
                self.playerOrder = []
                self.flash = 0
                self.intervalId = 0
                self.turn = 1
                self.good = true

                //Set order of colors to for current round
                for (var i = 0; i < 20; i++) {
                    self.order.push(Math.floor(Math.random() * 4) + 1)
                }

                self.compTurn = true
                self.intervalId = setInterval(self.gameTurn, 800)
            },
            clearColor() {
                const self = this

                self.active.red = false;
                self.active.blue = false;
                self.active.green = false;
                self.active.yellow = false;
            },
            flashColor() {
                const self = this

                self.active.red = true;
                self.active.blue = true;
                self.active.green = true;
                self.active.yellow = true;
            },
        },
        mounted() {
            const self = this

            if (localStorage.highScore) {
                self.highScore = localStorage.highScore;
            }
        },
        watch: {
            highScore(newHighScore) {
                localStorage.highScore = newHighScore;
            }
      }
    }
</script>

<style scoped>

    .highScoreText {
        position: absolute;
        margin-left: 80px;
        margin-top: 25px;
    }

    .roundText {
      position: absolute;
      margin-left: 94px;
      margin-top: 147px;
    }

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

    .green {

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

    .red {
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

    .blue {
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

    .green, .red, .yellow, .blue {
        opacity: 0.5;
        filter: alpha(opacity=50);
    }

    .flashButton {
        opacity: 1;
        filter: alpha(opacity=100);
    }

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
