<template>
<div class="row">
  <div class="col-sm-12">
  <span @click="$emit('setActive', game)" 
        @mouseover="hovering = true" 
        @mouseout="hovering = false">{{game.title}}</span>
  <span v-if="hovering" class="badge badge-warning">{{game.date | formatDate}}</span>
  </div>
  <div class="col-sm-12" v-if="hovering">
  <span class="badge badge-dark">{{game.competition.name}}</span>
  </div>
</div>
</template>

<script>
export default {
  name: 'Game',
  props: ['game'],
  data: function() {
    return {
      hovering: false
    }
  }
}
</script>

<style scoped>
.container {
  margin-left:auto;
  margin-right:auto;
  max-width: 80%;
}
span {
  padding: 4px;
  margin: 6px;
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
</style>
