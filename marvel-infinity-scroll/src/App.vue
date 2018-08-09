<template>
  <div id="app">
    <Grid :comics="list"/>
  </div>
</template>

<script>
import Grid from './components/Grid.vue';

export default {
  name: 'app',
  data(){
    return {
      list: []
    }
  },
  components: {
    Grid,
  },
  mounted(){
    fetch('https://gateway.marvel.com:443/v1/public/characters?name=Iron%20Man&apikey=2803d13c3cd6750524164fced8a33453')
    .then(res => res.json())
    .then(json => this.list = json.data.results[0].comics.items)
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
