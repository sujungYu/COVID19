<template>
    <div class="graphstyle" v-if="arrdecideCnt.length>0">
        <line-chart :height="40" :chartData="arrdecideCnt" :options="chartOptions" ></line-chart>
    </div>
</template>

<script>
import {Line} from 'vue-chartjs'
import axios from 'axios'
import moment from 'moment'

import LineChart from './LineChart.vue'

export default {
  extends: Line,
  components:{
    LineChart
  },

  data () {
    return {
      arrdecideCnt:[],
      chartOptions:{
        
        legend:{
          display: false,
        },

        tooltips:{ 
          enabled: true,
        },
        hover:{
          animationDuration: 0
        },
        animation:{
          duration:1,
        },

        options:{
          responsive: false,

          scales:{
           yAxes:[{
            // display: false,
            gridLines:{
              display:true,
              brawBorder:false,
              color:"rgba(238, 238, 238, 0.979)"
            },
            ticks:{
              stepSize: 500,
              color: "rgba(238, 238, 238, 0.979)"
            }
          }],
          xAxes:[{
            gridLines:{
            display:false,
            drawBorder:false,
            },
            ticks:{
              fontSize:12,
              color: "rgba(238, 238, 238, 0.979)"
            },
          }],
          
        }

        }
        
      }
    };
  },
  
  async created(){
    
      const startCreateDt = moment().subtract(8,'d').format('YYYYMMDD')
      const endCreateDt = moment().format('YYYYMMDD')
      const { data } = await axios.get('/openapi/service/rest/Covid19/getCovid19InfStateJson?serviceKey=SGsOrRFvsbOZ6Oa2wrwdLE9yTZeH%2FFNwx9nlqc2jYcC6d1cN7%2FLg4gpfcipuXnxVCVDSdrxgjw8kNv7pvEfNaw%3D%3D&pageNo=1&numOfRows=10&startCreateDt='+ startCreateDt +'&endCreateDt='+endCreateDt);

      data.response.body.items.item.forEach(d => {
        const stateDt = moment(d.stateDt, "YYYYMMDD").format("MM.DD");

        const {
            decideCnt,
        } = d;
        
        this.arrdecideCnt.push({stateDt, total: decideCnt});
   
      
    });
   
  }
    
}
  

</script>

<style>


.graphstyle{
    border-radius:10px;
    background-color: white;
    
    margin-top: 5%;
    margin-right: 10%;
    margin-left: 0%;
    
}

</style>
