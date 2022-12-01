<template>
  <div class="joke-card">
    <p class="category">Category: {{joke.category}}</p>
    <div v-if="joke.type === 'single'">
      <h1>{{joke.joke}}</h1>
    </div>
    <div v-if="joke.type === 'twopart'" >
      <h1>{{joke.setup}}</h1>
      <h1 :class="hidePunchLine ? 'blurry-text' : ''" @click="showText()">{{joke.delivery}}</h1>
    </div>
  </div>
</template>

<script>

export default {
  name: "Joke",
  data() {
    return {
      hidePunchLine: true
    }
  },
  props: {
    joke: Object,
  },
  methods: {
    showText() {
      this.hidePunchLine = false;
    }
  },
  watch: {
    joke() {
      this.hidePunchLine=true;
    }
  }
};
</script>

<style scoped>
.joke-card {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  text-align: left;
  border: 8px solid #0a2847;
  border-radius: 20px;
  padding: 40px;
  background-color: #f0ffff;
  max-width: 800px;
}
.category {
  margin-bottom: 20px;
}
h1{
  margin-bottom: 20px;
}

.blurry-text {
  color: transparent;
  text-shadow: 0 0 10px rgba(0,0,0,0.5);
  cursor: pointer;
}

</style>
