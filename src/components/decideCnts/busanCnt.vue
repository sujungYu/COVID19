<template>
<transition name="slide-up" appear>
  <div>
<div class="cnt"><span class="koreacnt">부산 </span>백신 접종자 수 {{SecondTot[0]}} 명</div>
</div>
</transition>
</template>


<script>
import axios from 'axios'
const convert = require('xml-js');


export default {
    
  

  data () {
    return {
      SecondTot:[],
    
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
          this.SecondTot.push(d.secondTot._text)
    });

   
        
  }
}
  

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Gothic+A1:wght@400&display=swap');

div{
  margin: 0 auto;
  font-family: 'Gothic A1', sans-serif;
}
/* .slide-up {
   transition: all 1s; 
} */

.slide-up-enter, .slide-up-leave-to{
  transform: translateY(10px);
  opacity: 0;
}
.slide-up-enter-active, .slide-up-leave-active{
  transition: all 3.5s ease;
}
.cnt{
    font-size: 25px;
    padding-top: 30px;
    padding-bottom: 30px;
    text-align: left;
}
.koreacnt{
    color:royalblue
}



</style>
