<template>
<div id="highlights">
  <div v-for="game in games" :key="game.title">
    <h2><span @click="desactiveAll(); game.active = !game.active">{{ game.title }}</span></h2>
    <div class="container" v-if="game.active" v-html="game.embed">
    </div>
  </div>

</div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Highlights',
  data () {
    return {
      games: []
    }
  },
  methods: {
    desactiveAll: function () {
      this.games = this.games.map(game => 
        {
          game.active = false;
          return game;
        })
    }
  },
  mounted () {
    axios
      .get('https://www.scorebat.com/video-api/v1/')
      .then(response => (this.games = response.data.map(game => 
        {
          game.active = false;
          return game;
        }
          )));
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  margin-left:auto;
  margin-right:auto;
  max-width: 60%;
}
span {
  padding: 10px;
}
span:hover {
  cursor: pointer;
  -moz-border-radius-topleft: 10px;
  -moz-border-radius-topright: 10px;
  -moz-border-radius-bottomright: 10px;
  -moz-border-radius-bottomleft: 10px;
  -webkit-border-radius: 10px 10px 10px 10px;
  border-radius: 10px 10px 10px 10px;
  color:white;
  background-color: #42b983;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
