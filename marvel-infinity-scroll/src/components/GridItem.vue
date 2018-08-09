<template>

    <div class="col">
        
        <div>
            {{comic.name}}
            <img :src="info.frontImage" width="200px" height="200px"/>
            <span>{{info.date}}</span>
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
      //getData();
    }
  },
  mounted(){
      this.getData();
  },
  methods: {
    getData() {
      
      fetch(this.comic.resourceURI+"?apikey=2803d13c3cd6750524164fced8a33453")
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
