<template>
    <div class="cell">
    <div class="flip-container" @click="toogleClass">  	
      <div class="flipper">  		
        <div class="front">  			
          <div class="responsive-image  overlay">
            <div class="content">
              <div>
                <div class="content-overlay"></div>
                <img :src="info.frontImage"  class="content-image"/>
                <div class="content-details fadeIn-bottom">
                  <h3 class="content-title">{{ info.name }}</h3>
                </div>
              </div>
            </div>
          </div>  		
        </div>  		
        <div class="back">  			
          	<p class="content-text">{{ info.date | formatDatePTBR }}</p>
        </div>  	
      </div>  
    </div>
  </div>
</template>

<script>
export default {
  props: ["comic"],
  data() {
    return {
      info: null
    };
  },
  watch: {
    comic: function(newValue, oldValue) {
      console.log(newValue);
    }
  },
  filters: {
    formatDatePTBR(value) {
      return new Date(value).toLocaleDateString("pt-BR");
    }
  },
  mounted() {
    this.getData();
  },
  methods: {
    getFlipContainer(el) {
      if(el == null) return null;

      if (
        el.classList.value &&
        el.classList.value.indexOf("flip-container") > -1
      ) {
        return el;
      }
      return this.getFlipContainer(el.parentElement);
    },
    toogleClass(event) {
      debugger;
      const el = this.getFlipContainer(event.target);

      if (el) el.classList.toggle("flip");
    },
    getData() {
      fetch(this.comic.resourceURI + "?apikey=2803d13c3cd6750524164fced8a33453")
        .then(res => res.json())
        .then(json => {
          const results = json.data.results[0];
          this.info = {
            name: this.comic.name,
            date: results.dates[0].date,
            thumbnail: `${results.thumbnail.path}.${
              results.thumbnail.extension
            }`,
            frontImage: `${results.images[0].path}.${
              results.images[0].extension
            }`
          };
        });
    }
  }
};
</script>

<style>
</style>
