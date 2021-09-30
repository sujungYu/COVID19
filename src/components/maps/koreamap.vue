<template>
<div class="p1"> 
  <div class="d3 ">
    <koreaCnt></koreaCnt>
    <koreaBtn></koreaBtn>
    </div>
</div>
    
</template>

<script>
import * as d3 from 'd3';
import * as topojson from 'topojson';
import koreaCnt from '../decideCnts/koreaCnt.vue'
import koreaBtn from '../buttons/button.vue'
export default {
    name: 'Map',
    components: {
    koreaCnt,
    koreaBtn
  },
    
    
    mounted() {
      this.draw();
      
    },
    methods: {
      draw() {
        const koreaMap = require('../../assets/korea.json'); 
        console.log(koreaMap);
        const geojson = topojson.feature(koreaMap, koreaMap.objects.skorea_provinces_2018_geo); 
        // const center = d3.geoCentroid(geojson);
        const width = 600;
        const height =800;
        const svg = d3
          .select('.d3')
          .append('svg')
          .attr('width', width).attr('height', height);
        const projection = d3.geoMercator()
          .scale(1)
          .translate([0, 0]);
        const path = d3.geoPath().projection(projection);
        const bounds = path.bounds(geojson);
        const widthScale = (bounds[1][0] - bounds[0][0]) / width;
        const heightScale = (bounds[1][1] - bounds[0][1]) / height;
        const scale = 1 / Math.max(widthScale, heightScale);
        const xoffset = width / 2 - scale * (bounds[1][0] + bounds[0][0]) / 2 + 10;
        const yoffset = height / 4 - scale * (bounds[1][1] + bounds[0][1]) / 2 + 80;
        const offset = [xoffset, yoffset];
        projection.scale(scale).translate(offset); 
        svg.append('g')
          .selectAll('path').data(geojson.features)
          .enter().append('path')
          .attr('d', path)
          // .attr('transform', d3.event.transform)
      },

}
      }
    
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Black+Han+Sans&family=Nunito:wght@600;800;900&family=Ubuntu:wght@500&display=swap');
body{
   margin: 0 auto; 
}
.p1{
  width: 100%; 
  margin: 0 auto; 
  display: flex;
  justify-content: center;  

}
.d3{
  background:white; 
  width: 618px; 
  height: 750px;
  border-radius:10px;
  margin: 0 auto; 
  border: 2px solid rgba(31, 19, 19, 0.151);
  padding-left: 40px;
  position: relative;

  

}
  path {
    fill:rgb(209, 60, 60);
    stroke:white;
  }
  .koreatotal{
    font-family:"Black Han Sans";
  }
 
 
</style>