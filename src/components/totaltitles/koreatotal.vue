<template>
   <div class="overview-wrapper">
     <div v-for="item in display" v-bind:key="item">
        <div :class="{ [item.color]: true, 'ov-item': true }">
        <div class="ov-title">{{ item.title }}</div>
        <div class="number-title">{{item.total}}</div>
        <div class="number">▲{{item.today}}</div>
        </div>
        </div>
     </div>
</template>

<script>
import axios from 'axios'
import moment from 'moment'


export default {
  

  data () {
    return {
      display:[],
      totaldecideCnt:[],
      totaldeathCnt:[],
      totalclearCnt:[],
      totalexamCnt:[]
    };
  },
  
  async created(){
    
      const startCreateDt = moment().subtract(1,'d').format('YYYYMMDD')
      const endCreateDt = moment().format('YYYYMMDD')
      const { data } = await axios.get('/openapi/service/rest/Covid19/getCovid19InfStateJson?serviceKey=SGsOrRFvsbOZ6Oa2wrwdLE9yTZeH%2FFNwx9nlqc2jYcC6d1cN7%2FLg4gpfcipuXnxVCVDSdrxgjw8kNv7pvEfNaw%3D%3D&pageNo=1&numOfRows=10&startCreateDt='+ startCreateDt +'&endCreateDt='+endCreateDt);

      data.response.body.items.item.forEach(d => {
        this.totaldecideCnt.push(d.decideCnt)
        this.totaldeathCnt.push(d.deathCnt)
        this.totalclearCnt.push(d.clearCnt)
        this.totalexamCnt.push(d.examCnt)
    });

    const cases= {
      color: "red",
      background:"red",
      title:"확진자",
      total:this.totaldecideCnt[0],
      today:this.totaldecideCnt[0]-this.totaldecideCnt[1],
    }
    const deaths={
      color: "purple",
      background:"red",
      title:"사망자",
      total: this.totaldeathCnt[0],
      today: this.totaldeathCnt[0]-this.totaldeathCnt[1],
    }
    const clear={
      color: "green",
      background:"red",
      title:"격리해제",
      total: this.totalclearCnt[0],
      today: this.totalclearCnt[0]-this.totalclearCnt[1],
    }
    const exam={
      color: "orange",
      background:"red",
      title:"검사 중",
      total: this.totalexamCnt[0],
      today: this.totalexamCnt[0]-this.totalexamCnt[1],
    }
    this.display= [cases, deaths, clear, exam]
   
  }
    
}
  

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Gruppo&display=swap');

div{
  margin: 0 auto;
}

.overview-wrapper {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-between;
  background: white;
  width: 700px;
  height: 140px;
  border-radius: 10px;
  text-align: center;
  margin-top: 2%;
  margin-bottom: 2%;
  padding-top: 24px;
  border: 2px solid rgba(31, 19, 19, 0.089);

}


.ov-title {
  font-size: 1em;
  opacity: .6;
  font-size: 17px;
  font-family:'Gruppo';
}

.ov-item {
  position: relative;
  z-index: 100;
}

.number-title {
  line-height: 1.2em;
  font-size: 28px;
}

.number {
  opacity: 0.6;
  font-size: 17px;
  padding-bottom: 0px;
}


.red {
  color: red;
}
.orange {
  color: orange;
}
.purple {
  color: purple;
}
.green {
  color: green;
}

</style>
