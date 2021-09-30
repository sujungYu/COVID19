<template>
  <div>
   <h1>코로나바이러스-19</h1>
   <h2>{{$moment().format(' YYYY. MM. DD.')}}</h2>
  <div >
    <Home/>
  </div>
  
  </div>
</template>

<script>
import Home from './views/Home.vue'
export default {
  name: 'App',
  components: {
    Home
  },
   
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Black+Han+Sans&family=Nunito:wght@600;800;900&family=Ubuntu:wght@500&display=swap');

div{
  background-color:rgba(243, 242, 242, 0.986);
}

h1{
  font-family:"Black Han Sans";
  font-size: 80px;
  text-align: center;
  border-radius: 10px;
  margin-bottom: 0.1%;
  background-color: white;
  width: 618px;
  margin: 0 auto;
  border: 2px solid rgba(31, 19, 19, 0.151);
  border-bottom: white;
  height: 150px;
  padding-top: 35px;
}
h2{
  margin-top: 0.1%;
  font-family:"Black Han Sans";
  font-size: 30px;
  border-radius: 10px;
  text-align: center;
  background-color: white;
  width: 618px;
   margin: 0 auto;
   border: 2px solid rgba(31, 19, 19, 0.151)
}

</style>
