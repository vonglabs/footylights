<template>
  <div id="app" class="container">
      <div class="row">
        <div class="col-sm-12">
          <h1><strong>Footylights</strong></h1>
        </div>
      </div>
      <hr>
      <div class="row">
        <div id="activeGame" class="col-12 col-sm-8 text-center">
          <div v-if="activeGame">
            <h3><strong>{{activeGame.title}}</strong></h3>
            <h4><span class="badge badge-dark">{{activeGame.competition.name}}</span>
                <span class="badge badge-warning">{{activeGame.date | formatDate}}</span>
            </h4>
            <hr>
            <div v-html="activeGame.embed">
            </div>
          </div>
        </div>
        <div id="games" class="col-12 col-sm-4 text-left">
            <div class="input-group mb-3 box">
              <div class="input-group-prepend">
                <span class="input-group-text"><font-awesome-icon :icon="['far', 'futbol']" size="lg"/></span>
              </div>
              <input type="text" v-model="searchedTeam" class="form-control" placeholder="Search for a team">
            </div>
            <div class="box">
            <Game v-for="game in filteredGames" v-on:setActive="setActive" :key="game.title" :game="game" :activeGame="activeGame"/>
            </div>
        </div>    
      </div>
      <hr>
      <div id="footer" class="row">
        <div class="col-12 col-sm-12 text-right">
        © 2020 - vong labs 
        <a target="_blank" rel="noopener noreferrer" href="https://github.com/vonglabs"><font-awesome-icon :icon="['fab', 'github-alt']" size="lg"/></a>
        </div>
      </div>
  </div>
  
</template>

<script>
import Game from './components/Game.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Game
  },
  data () {
    return {
      searchedTeam: '',
      games: [],
      activeGame: null
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
  },
  methods: {
    setActive: function (game) {
      this.activeGame = game;
      window.scrollTo(0,0);
    },
    getLeagues: function () {
			return [...new Set(this.games.map(g => g.competition))];
    }
  },
  computed: {
    filteredGames() {
      if (!this.searchedTeam) return this.games
      return this.games.filter(g => g.title.toLowerCase().includes(this.searchedTeam.toLowerCase()));
    }
  } 
}
</script>

<style>
@media (max-width: 768px) {
  .container {
    width: 100%;
    max-width: none;
  }
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.box {
  padding: 15px;
  background-color: #e6fff2;
  -moz-border-radius-topleft: 20px;
  -moz-border-radius-topright: 20px;
  -moz-border-radius-bottomright: 20px;
  -moz-border-radius-bottomleft: 20px;
  -webkit-border-radius: 20px 20px 20px 20px;
  border-radius: 20px 20px 20px 20px;
}

.container {
  margin-top: 20px;
  margin-bottom: 20px;
}

.badge {
  margin: 4px;
}

a:link {
  color: green;
  background-color: transparent;
  text-decoration: none;
}

a:visited {
  color: red;
  background-color: transparent;
  text-decoration: none;
}

a:hover {
  color: pink;
  background-color: transparent;
  text-decoration: underline;
}

#footer {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: right;
  color: #2c3e50;
}
</style>
