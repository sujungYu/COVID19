<template>
  <div>
    <Total/>
    <div>
      <Map/>
    </div>
    <div>
      <Graph/>
    </div>
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
body{
  margin: 0 auto;
  text-align: center;
}
    
</style>
