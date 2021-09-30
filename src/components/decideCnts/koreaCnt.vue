<template>
 <div class="cnt"><span class="koreacnt">전국</span> 누적 확진자 수 {{totaldecideCnt[0]}} 명</div>
</template>

<script>
import axios from 'axios'
import moment from 'moment'


export default {
  

  data () {
    return {
      totaldecideCnt:[],
    
    };
  },
  
  async created(){
    
      const startCreateDt = moment().subtract(1,'d').format('YYYYMMDD')
      const endCreateDt = moment().format('YYYYMMDD')
      const { data } = await axios.get('/openapi/service/rest/Covid19/getCovid19InfStateJson?serviceKey=SGsOrRFvsbOZ6Oa2wrwdLE9yTZeH%2FFNwx9nlqc2jYcC6d1cN7%2FLg4gpfcipuXnxVCVDSdrxgjw8kNv7pvEfNaw%3D%3D&pageNo=1&numOfRows=10&startCreateDt='+ startCreateDt +'&endCreateDt='+endCreateDt);
      console.log(data);

      data.response.body.items.item.forEach(d => {
        this.totaldecideCnt.push(d.decideCnt)
    });

   
  }
    
}
  

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Black+Han+Sans&family=Nunito:wght@600;800;900&family=Ubuntu:wght@500&display=swap');

div{
  margin: 0 auto;
  font-family:"Black Han Sans";
}

.cnt{
    font-size: 25px;
    padding-top: 30px;
    padding-bottom: 30px;
}
.koreacnt{
    color:royalblue
}



</style>
