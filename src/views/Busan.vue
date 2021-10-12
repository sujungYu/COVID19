<template>
  <div>
    <BusanTotal/>
      <BusanMap/>
      <BusanGraph/>
      
    </div>
</template>

<script>
import BusanMap from '../components/maps/busanmap.vue'
import BusanTotal from '../components/totaltitles/busantotal.vue'
import BusanGraph from '../components/graphs/busangraph.vue'

export default {
  // name: 'map',
  components: {
    BusanMap,
    BusanTotal,
    BusanGraph
  },
  
}
</script>

<style scoped>
body{
  margin: 0 auto;
  text-align: center;
  
}
div{
  position: relative;
}
    
</style>
