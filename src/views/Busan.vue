<template>
  <div>
    <BusanTotal/>
      <BusanMap/>
      
    </div>
</template>

<script>
import BusanMap from '../components/maps/busanmap.vue'
import BusanTotal from '../components/totaltitles/busantotal.vue'

export default {
  // name: 'map',
  components: {
    BusanMap,
    BusanTotal
  },
  
}
</script>

<style scoped>
body{
  margin: 0 auto;
  text-align: center;
}
    
</style>
