<template>
  <div>
    <Total/>
    <Map/>
    <Graph/>
  </div>
</template>

<script>
import Total from '../components/totaltitles/koreatotal.vue'
import Map from '../components/maps/koreamap.vue'
import Graph from '../components/graphs/koreagraph.vue'
export default {
  // name: 'map',
  components: {
    Total,
    Map,
    Graph,
  },
  
}
</script>

<style scoped>
div{
  margin: 0 auto;
  text-align: center;
  position: relative;
}

    
</style>
