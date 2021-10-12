<template>
    <div class="can" v-if="arrdecideCnt.length>0">
        <div class="canvas" >
      <h3 class="ti">
          <p class="pd">최근 7일 <span class=blue>확진자</span> 추이</p>
        <bar-chart  :width=650 :height=240 :chartData="arrdecideCnt" :options="chartOptions" >
          <!-- <Btn/> -->
        </bar-chart>
        </h3>
        </div>
    </div>
</template>

<script>
import {Bar} from 'vue-chartjs'
import axios from 'axios'
import moment from 'moment'
import Chart from 'chart.js'

import BarChart from './BarChart.vue'
// import Btn from '../buttons/graphbutton.vue'


export default {
    
  extends: Bar,
  components:{
    BarChart,
    // Btn
  },

  data () {
    return {
      arrdecideCnt:[],
      chartOptions:{
        responsive: false,
        maintainAspectRatio: false,

        legend:{
          display: false,
        },

        tooltips:{ 
          enabled: false,
          // displayColors:false,
          // backgroundColor: '#0a6dff',
          // titleFontColor:'white',
          // titleFontSize: 10,
          // bodyFontColor:'white',
          // bodyFontSize: 15,

        },

        hover:{
          animationDuration: 0
        },
        animation:{
          duration:1,
          onComplete: function () {
                 var chartInstance = this.chart,
                 ctx = chartInstance.ctx;
                 ctx.font = Chart.helpers.fontString(Chart.defaults.global.defaultFontSize, Chart.defaults.global.defaultFontStyle, Chart.defaults.global.defaultFontFamily);
                 ctx.fillStyle = 'rgba(43, 22, 22, 0.8)';
                 ctx.textAlign = 'center';
                 ctx.textBaseline = 'center';

                 this.data.datasets.forEach(function (dataset, i) {
                    var meta = chartInstance.controller.getDatasetMeta(i);
                    meta.data.forEach(function (bar, index) {
                       var data = dataset.data[index];
                       ctx.fillText(data, bar._model.x, bar._model.y - 3);
                    });
                 });
              }
          
        },


          scales:{
           yAxes:[{
            // display: false,
            gridLines:{
              display:true,
              brawBorder:false,
              color:"rgba(238, 238, 238, 0.979)"
            },
            ticks:{
              stepSize: 50,
              max:100,
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
    },
  
  async created(){
    
      const startCreateDt = moment().subtract(7,'d').format('YYYYMMDD')
      const endCreateDt = moment().format('YYYYMMDD')
      const { data } = await axios.get('/openapi/service/rest/Covid19/getCovid19SidoInfStateJson?serviceKey=SGsOrRFvsbOZ6Oa2wrwdLE9yTZeH%2FFNwx9nlqc2jYcC6d1cN7%2FLg4gpfcipuXnxVCVDSdrxgjw8kNv7pvEfNaw%3D%3D&pageNo=1&numOfRows=10&startCreateDt='+ startCreateDt +'&endCreateDt='+endCreateDt);
        console.log(data);
        const newdata = data.response.body.items.item.filter(function(e){
            return e.gubun=="부산"
        })
        console.log(newdata);

      newdata.forEach(d => {
          const stateDt = moment(d.createDt, "YYYY-MM-DD").format("MM.DD");
            // this.totaldecideCnt.push(d.defCnt)
            const {
            defCnt,
        } = d;

            this.arrdecideCnt.push({stateDt, total: defCnt});
            
          });
  }
}
   
  

</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Gothic+A1:wght@400&display=swap');
div{
   /* text-align: center; */
   margin: auto 0;
   
}
.can{
  
  /* align-items: center; */
  text-align: left;
  /* position: absolute; */
  
  
  
  
}
.canvas{
  margin:0 auto;
  display: flex;
  /* justify-content: space-between; */
  margin-top: 2%;
  background-color: white;
  text-align: left;
  position: relative;
  border-radius:10px;
  width: 710px;
  height:240%;
  border:  2px solid rgba(43, 22, 22, 0.089);
  padding-top: 1%;
  /* padding-left: 2%; */
  margin-bottom: 2%;
}
.ti{
    position: relative;
    /* padding: 1%; */
    
}

.pd{
    padding-left: 3.5%;
    font-family: 'Gothic A1', sans-serif;
    padding-top:3%;
    font-size: 25px;
}
.blue{
    color:royalblue
}
</style>