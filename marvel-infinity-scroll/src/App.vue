<template>
  <div id="app" class="container">


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
@media screen and (min-width: 600px) {
  .grid {
    display: flex;
    flex-wrap: wrap;
    flex-direction: row;
  }
  .cell {
    width: calc(50% - 2rem);
  }

  .overlay{
    display: block;
    width: 100%;
  }
}

@media screen and (min-width: 1000px) {
  .cell {
    width: calc(33.3333% - 2rem);
  }

   .overlay{
    width: 33.33333%;
  }
}

.container {
  margin: 0 auto;
  max-width: 1200px;
  padding: 0 1rem;
}

.responsive-image {
  max-width: 100%;
}

.cell {
  margin: 1rem;
}

.cell img {
  display: block;
}


.overlay{
  padding: 1em 0;
  float: left;
  width: 100%;
}


.overlay .title{
  color: #1a1a1a;
  text-align: center;
  margin-bottom: 10px;
}

.content {
  position: relative;
  width: 90%;
  max-width: 400px;
  margin: auto;
  overflow: hidden;
}

.content .content-overlay {
  background: rgba(0,0,0,0.7);
  position: absolute;
  height: 99%;
  width: 100%;
  left: 0;
  top: 0;
  bottom: 0;
  right: 0;
  opacity: 0;
  -webkit-transition: all 0.4s ease-in-out 0s;
  -moz-transition: all 0.4s ease-in-out 0s;
  transition: all 0.4s ease-in-out 0s;
}

.content:hover .content-overlay{
  opacity: 1;
}

.content-image{
  width: 100%;
}

.content-details {
  position: absolute;
  text-align: center;
  padding-left: 1em;
  padding-right: 1em;
  width: 100%;
  top: 50%;
  left: 50%;
  opacity: 0;
  -webkit-transform: translate(-50%, -50%);
  -moz-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  -webkit-transition: all 0.3s ease-in-out 0s;
  -moz-transition: all 0.3s ease-in-out 0s;
  transition: all 0.3s ease-in-out 0s;
}

.content:hover .content-details{
  top: 50%;
  left: 50%;
  opacity: 1;
}

.content-details h3{
  color: #fff;
  font-weight: 500;
  letter-spacing: 0.15em;
  margin-bottom: 0.5em;
  text-transform: uppercase;
}

.content-details p{
  color: #fff;
  font-size: 0.8em;
}

.fadeIn-bottom{
  top: 80%;
}

.fadeIn-top{
  top: 20%;
}

.fadeIn-left{
  left: 20%;
}

.fadeIn-right{
  left: 80%;
}
/* O container geral define a perspectiva */  
.flip-container { perspective: 1000; }  	

/* vira os containers frente e verso quando o mouse passa em cima */
.flip-container.flip .flipper {  	
  transform: rotateY(180deg);  
}
 
.flip-container, .front, .back {  	
  width: 320px;  	
  height: 480px;  
}

/* define a velocidade da transição */
.flipper {  	
  transition: 0.6s;  	
  transform-style: preserve-3d;    	
  position: relative;  
}
    
/* esconde o verso durante a animação */
.front, .back {  	
  backface-visibility: hidden;    	
  position: absolute;  	
  top: 0;  	
 left: 0;  
}
    
/* frente posicionada sobre o verso */
.front { z-index: 2;  }    

/* verso inicialmente escondido */
.back { transform: rotateY(180deg); }
</style>
