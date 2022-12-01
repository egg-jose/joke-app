<template>
  <div class="container" :style="{'background-color': backgroundColor}">
    <Joke :joke="joke"/>
    <Button @btn-click="clickSearch" text="Get Random Joke" />
  </div>
</template>

<script>
import Button from './components/Button';
import Joke from './components/Joke';

export default {
  name: 'App',
  components: {
    Button,
    Joke,
  },
  data() {
    return {
      joke: {},
      colorCategory: {
        "Programming": "#17BEBB",
        "Pun": "#695958",
        "Spooky": "#28464B",
        "Christmas": "#931621",
      },
    }
  },
  methods: {
    async getJoke() {
      const res = await fetch('https://v2.jokeapi.dev/joke/Programming,Pun,Spooky,Christmas?type=twopart');
      const data = await res.json();
      return data;
    },
    async clickSearch() {
      this.joke = await this.getJoke();
    }
  },
  async created() {
    this.joke =  await this.getJoke();
  },
  computed: {
    backgroundColor() {
      return this.colorCategory[this.joke.category]
    }
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Lexend+Deca&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Lexend Deca", sans-serif;
  color: #0a2847;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.btn {
  display: inline-block;
  background: #0a2847;
  color: #e9e9e9;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 60px;
  font-family: inherit;
}
.btn:active {
  transform: scale(0.98);
}
</style>
