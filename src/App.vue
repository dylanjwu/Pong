<template>
  <div id="app">
    <div class="heading">
      <h1>PONG</h1>
      <h4 id="score" v-if="score > 0"> score: {{ score }}</h4>
      <h4 v-else>single-player game</h4>
    </div>

    <div class="death">
      <h3 v-if="showDeath">{{ hasDied }}</h3>
    </div>
    <my-canvas
      :startingX="startingX"
      @ball-death="setDeath"
      @bar-collision="collision"
    >
    </my-canvas>
  </div>
</template>

<script>
import MyCanvas from "./components/MyCanvas.vue";

export default {
  name: "App",
  components: {
    MyCanvas,
  },

  data() {
    return {
      showDeath: false,
      startingX: 25,
      score: 0,
    };
  },

  computed: {
    hasDied: function() {
      return "Your score was " + this.score + ". Play again.";
    },
  },

  methods: {
    setStartingX: function() {
      this.startingX = Number(Math.random() * 750);
    },

    setDeath: function() {
      this.start = true;
      this.showDeath = true;
      this.setStartingX();
      console.log(this.hasDied);

      setTimeout(() => {
        this.showDeath = false;
        this.score = 0;
        console.log(this.showDeath);
      }, 2000);
    },

    collision: function() {
      console.log("collision!");
      this.score++;
      console.log(this.score);
    },
  },
};
</script>

<style>

h1 {
  text-align: center;
  font-family: Impact, Haettenschweiler, "Arial Narrow Bold", sans-serif;
  font-stretch: narrower;
  font-size: 50pt;
  color: rgb(2, 57, 2);
  margin-bottom: 0px;
}

h4 {
  text-align: center;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  color: black;
}

html {
  background-color: rgb(166, 228, 166);
}

#score {
  padding: 0px;
  text-align: center;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
}

.death {
  text-align: center;
  margin: 0 auto;
  color: red;
}
</style>
