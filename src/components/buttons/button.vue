<template>
<div>
        <div>
            <button @click="jeju" class= "Jeju button">{{display[0].name}}<span class="red">{{display[0].today}}</span></button>
            <button @click="gyeongnam" class= "Gyeongnam button">{{display[1].name}}<span class="red">{{display[1].today}}</span></button>
            <button @click="gyeongbuk" class= "Gyeongbuk button">{{display[2].name}}<span class="red">{{display[2].today}}</span></button>
            <button @click="jeoanam" class= "Jeoanam button">{{display[3].name}}<span class="red">{{display[3].today}}</span></button>
            <button @click="jeoanbuk" class= "Jeoanbuk button">{{display[4].name}}<span class="red">{{display[4].today}}</span></button>
            <button @click="chungnam" class= "Chungnam button">{{display[5].name}}<span class="red">{{display[5].today}}</span></button>
            <button @click="chungbuk" class= "Chungbuk button">{{display[6].name}}<span class="red">{{display[6].today}}</span></button>
            <button @click="gangwon" class= "Gangwon button">{{display[7].name}}<span class="red">{{display[7].today}}</span></button>
            <button @click="gyeonggi" class= "Gyeonggi button">{{display[8].name}}<span class="red">{{display[8].today}}</span></button>
            <button @click="sejong" class= "Sejong button">{{display[9].name}}<span class="red">{{display[9].today}}</span></button>
            <button @click="ulsan" class= "Ulsan button">{{display[10].name}}<span class="red">{{display[10].today}}</span></button>
            <button @click="daejeon" class= "Daejeon button">{{display[11].name}}<span class="red">{{display[11].today}}</span></button>
            <button @click="gwangju" class= "Gwangju button">{{display[12].name}}<span class="red">{{display[12].today}}</span></button>
            <button @click="incheon" class= "Incheon button">{{display[13].name}}<span class="red">{{display[13].today}}</span></button>
            <button @click="daegu" class= "Daegu button">{{display[14].name}}<span class="red">{{display[14].today}}</span></button>
            <button @click="busan" class= "Busan button">{{display[15].name}}<span class="red">{{display[15].today}}</span></button>
            <button @click="seoul" class= "Seoul button">{{display[16].name}}<span class="red">{{display[16].today}}</span></button>
            
        

        </div>
</div>
</template>

<script>
import axios from 'axios'
import moment from 'moment'


export default {
    methods:{
        jeju(){
            this.$router.push('Jeju')
        },
        gyeongnam(){
            this.$router.push('Gyeongnam')
        },
        gyeongbuk(){
            this.$router.push('Gyeongbuk')
        },
        jeoanam(){
            this.$router.push('Jeoanam')
        },
        jeoanbuk(){
            this.$router.push('Jeoanbuk')
        },
        chungnam(){
            this.$router.push('Chungnam')
        },
        chungbuk(){
            this.$router.push('Chungbuk')
        },
        gangwon(){
            this.$router.push('Gangwon')
        },
        gyeonggi(){
            this.$router.push('Gyeonggi')
        },
        sejong(){
            this.$router.push('Sejong')
        },
        ulsan(){
            this.$router.push('Ulsan')
        },
        daejeon(){
            this.$router.push('Daejeon')
        },
        gwangju(){
            this.$router.push('Gwangju')
        },
        incheon(){
            this.$router.push('Incheon')
        },
        daegu(){
            this.$router.push('Daegu')
        },
        busan(){
            this.$router.push('Busan')
        },
        seoul(){
            this.$router.push('Seoul')
        }
    },

     data () {
    return {
      display:[],
      totaldecideCnt:[],
      totalname:[],
    
    };
  },
  
  
  async created(){
    
      const startCreateDt = moment().format('YYYYMMDD')
      const endCreateDt = moment().format('YYYYMMDD')
      const { data } = await axios.get('/openapi/service/rest/Covid19/getCovid19SidoInfStateJson?serviceKey=SGsOrRFvsbOZ6Oa2wrwdLE9yTZeH%2FFNwx9nlqc2jYcC6d1cN7%2FLg4gpfcipuXnxVCVDSdrxgjw8kNv7pvEfNaw%3D%3D&pageNo=1&numOfRows=10&startCreateDt='+ startCreateDt +'&endCreateDt='+endCreateDt);
      console.log(data);

      data.response.body.items.item.forEach(d => {
          this.totaldecideCnt.push(d.incDec)
          this.totalname.push(d.gubun)
    });

    const Jeju = {
        name: this.totalname[1],
        today: this.totaldecideCnt[1]
    }
    const Gyeongsangnamdo = {
        name: this.totalname[2],
        today: this.totaldecideCnt[2]
    }
    const Gyeongsangbukdo = {
        name: this.totalname[3],
        today: this.totaldecideCnt[3]
    }
    const Jeollanamdo = {
        name: this.totalname[4],
        today: this.totaldecideCnt[4]
    }
    const Jeollabukdo = {
        name: this.totalname[5],
        today: this.totaldecideCnt[5]
    }
    const Chungcheongnamdo = {
        name: this.totalname[6],
        today: this.totaldecideCnt[6]
    }
    const Chungcheongbukdo = {
        name: this.totalname[7],
        today: this.totaldecideCnt[7]
    }
    const Gangwondo = {
        name: this.totalname[8],
        today: this.totaldecideCnt[8]
    }
    const Gyeonggido = {
        name: this.totalname[9],
        today: this.totaldecideCnt[9]
    }
    const Sejong = {
        name: this.totalname[10],
        today: this.totaldecideCnt[10]
    }
    const Ulsan = {
        name: this.totalname[11],
        today: this.totaldecideCnt[11]
    }
    const Daejeon = {
        name: this.totalname[12],
        today: this.totaldecideCnt[12]
    }
    const Gwangju = {
        name: this.totalname[13],
        today: this.totaldecideCnt[13]
    }
    const Incheon = {
        name: this.totalname[14],
        today: this.totaldecideCnt[14]
    }
    const Daegu = {
        name: this.totalname[15],
        today: this.totaldecideCnt[15]
    }
    const Busan = {
        name: this.totalname[16],
        today: this.totaldecideCnt[16]
    }
    const Seoul = {
        name: this.totalname[17],
        today: this.totaldecideCnt[17]
    }


    this.display= [Jeju, Gyeongsangnamdo, Gyeongsangbukdo, Jeollanamdo, Jeollabukdo, Chungcheongnamdo, Chungcheongbukdo,  Gangwondo, Gyeonggido, Sejong, Ulsan, Daejeon, Gwangju, Incheon, Daegu, Busan, Seoul]
   
   }
    
}
  

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Black+Han+Sans&family=Nunito:wght@600;800;900&family=Ubuntu:wght@500&display=swap');

div{
  margin: 0 auto;
  
}
.button{
    font-family:"Black Han Sans";
    display: flex;
    background: white;
    justify-content: center;
    border:1px solid rgb(216, 215, 215);
    border-radius: 6px;
    box-shadow:2px 2px rgb(170, 170, 170);
    position: absolute;
    
}
.red{
    color: red;
}
.Jeju{
    top: 600px;
    left:200px;
}
.Gyeongnam{
    top: 430px;
    left:320px;
}
.Gyeongbuk{
    top: 270px;
    left:390px;
}
.Jeoanam{
    top:480px;
    left:160px;
}
.Jeoanbuk{
    top:380px;
    left:180px;
}
.Chungnam{
    top:280px;
    left:170px;
}
.Chungbuk {
    top:260px;
    left:300px;
}
.Gangwon{
    top:170px;
    left:330px;
}
.Gyeonggi{
    top:130px;
    left:200px;
}
.Sejong{
    top:290px;
    left:240px;
}
.Ulsan{
    top:350px;
    left:400px;
}
.Daejeon{
    top:340px;
    left:250px;
}
.Gwangju{
    top:440px;
    left:230px;
}
.Incheon{
    top:180px;
    left:140px;
}
.Daegu{
    top:340px;
    left:325px;
}
.Busan{
    top:445px;
    left:400px;
}
.Seoul{
    top:200px;
    left:250px;
}






</style>
