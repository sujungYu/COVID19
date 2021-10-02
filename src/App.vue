<template>
  <div>
   <h1><span class="red">corona</span> DATA</h1>
   <h2>{{$moment().format(' YYYY. MM. DD.')}}</h2>
    <router-view></router-view>
  </div>
  
</template>

<script>


export default {
  name: 'App',
  components: {
  },
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@200&display=swap');
@import url('https://fonts.googleapis.com/css2?family=M+PLUS+Rounded+1c:wght@300&display=swap');


h1{
  font-family:'Poppins';
  font-size: 75px;
  border-radius: 10px;
  background-color: white;
  width: 700px;
  margin: 0 auto;
  border: 2px solid rgba(31, 19, 19, 0.089);
  border-bottom: white;
  height: 150px;
  margin-top: 35px;
  padding-top: 33px;
}
h2{
  margin-top: 0.1%;
  font-family: 'M PLUS Rounded 1c', sans-serif;
  font-size: 25px;
  border-radius: 10px;
  /* text-align: center; */
  background-color: rgba(197, 196, 196, 0.089);
  width: 700px;
   margin: 0 auto;
   border: 2px solid rgba(31, 19, 19, 0.089);
}
.red{
  color:rgba(255, 0, 0, 0.788);
}

</style>
