<template>
<div>
        <div>
            <button class= "Jeju button">일일{{displayFirst.today[0]}}누적{{displayFirst.total[0]}}</button>
            <!-- <button class= "Jeju button">{{displaySecond}}</button> -->
        </div>
</div>
</template>

<script>
import axios from 'axios'
const convert = require('xml-js');

export default {

    data () {
    return {
        js:[],
      displayFirst:[],
      displaySecond:[],
      firstCnt:[],
      firstTot:[],
      SecondCnt:[],
      SecondTot:[]
    
    };
  },
  
   
  

  async created(){
    
      const { data } = await axios.get('/irgd/cov19stats.do?list=sido');
      console.log(data);
      var json = convert.xml2json(data,{ compact: true } )
      const js=JSON.parse(json)
      console.log(js);
      const newdata = js.response.body.items.item.filter(function(e){
          return e.sidoNm._text=="부산광역시"
        })
        console.log(newdata);


      newdata.forEach(d => {
          this.firstCnt.push(d.firstCnt._text)
          this.firstTot.push(d.firstTot._text)
          this.SecondCnt.push(d.secondCnt._text)
          this.SecondTot.push(d.secondTot._text)
    });

    this.displayFirst = {
        today: this.firstCnt,
        total: this.firstTot,
        
    };
    this.displaySecond={
        today: this.SecondCnt,
        total: this.SecondTot,
    }
    // this.displayFirst= [First
    // this.displaySecond= Second
    // console.log(First);
   
   }
    
}
  

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Gothic+A1:wght@200&display=swap');

div{
  text-align: left;
  
}
.button{
    font-family: 'Gothic A1', sans-serif;
    font-size: 15px;
    /* display: block; */
    background: white;
    justify-content: center;
    border:1px solid rgba(216, 215, 215, 0.596);
    border-radius: 5px;
    box-shadow:1px 1px rgba(170, 170, 170, 0.541);
    position: absolute;
    width: 45px;
    transition: background 0.25s ease-in;
}
.button:hover {
  background: rgba(59, 56, 56, 0.89);
  color:white;
  /* applied to the hover state, so this transition will be applied when a hover is triggered */
  transition: background 0.35s ease-out;
  border:none;
  box-shadow: none;
}
/* span{
    display: block;
    white-space: normal;
} */

.red{
    font-weight: bolder;
    color: red;
}
.Jeju{
    top: 580px;
    left:230px;
}


</style>
