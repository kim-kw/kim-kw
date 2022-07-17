<template>
    <div class="container text-center  mt-5 mb-5">
    <h1 class="mt-5 fw-bolder text-success "> ABLOG </h1>
     <div class="table-responsive my-5">
      
      <!-- The table component -->
       <Table :fields='fields' :studentData ="studentData"></Table>
     </div>
 
</div>
</template>

<script>
export default {
  setup(){

    //An array of values for the data
       const studentData = [
      {Report:"SOSP", Lat: 15.4, Lon:135.2, Distance:94.4, Consumption:32.1},
     {Report:"NOON", Lat: 17.3, Lon:162.8, Distance:96.2, Consumption:34.5},
      {Report:"NOON", Lat: 20.6, Lon:171.4, Distance:90.3, Consumption:33.4},
     {Report:"NOON", Lat: 31.6, Lon:172.3, Distance:89.2, Consumption:36.1},
      {Report:"EOSP", Lat: 21.9, Lon:176.2, Distance:91.5, Consumption:35.3},  
    ]

    const fields = [
      'Report','Lat','Lon','Distance','Consumption'
    ]

    return{studentData,fields}
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
