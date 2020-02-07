<template>
  <div id="app">
    <Map/>
  </div>
</template>

<script>
import Map from '@/components/Map'
export default {
  name:'app',
  components: {
    Map
  },
   methods:{
      getDistance(){
          ymaps.geocode('Питер', {
              results: 1
          }).then(res => {
                  let firstCoords = res.geoObjects.get(0).geometry.getCoordinates();
                  ymaps.geocode('питер',{
                    results:1
                  }).then(res =>{
                     let secondCoords = res.geoObjects.get(0).geometry.getCoordinates();
                      console.log(Math.round(ymaps.coordSystem.geo.getDistance(firstCoords,secondCoords)/1000));
                  }).catch(err =>{
                    console.log(err);
                  })
          }).catch(err =>{
              console.log(err);
          })
      }
   }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width:100%;
  height: 100vh;
}
</style>



