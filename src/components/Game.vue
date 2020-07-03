<template>
<div class="row">
  <div class="col-sm-12">
  <span @click="$emit('setActive', game)" 
        @mouseover="hovering = true" 
        @mouseout="hovering = false"
        :class="{ 'font-weight-bold' : game === activeGame }">{{game.title}} 
  <font-awesome-icon :icon="['far', 'check-circle']" v-if="game === activeGame"/> 
  <span v-if="hovering" class="badge badge-light">{{game.date | formatDate}}</span></span>
  </div>
  <div class="col-sm-12" v-if="hovering">
  <span class="badge badge-dark">{{game.competition.name}}</span>
  </div>
</div>
</template>

<script>
export default {
  name: 'Game',
  props: ['game', 'activeGame'],
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
  margin: 4px;
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
