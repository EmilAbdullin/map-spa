<template>
    <div id="map"></div>
</template>

<script>
export default {
     mounted:function(){
        ymaps.ready(initMap);
        function initMap() {
            let myMap = new ymaps.Map('map', {
                center: [55.753994, 37.622093],
                zoom: 9
            });
        }
    }
}
</script>

<style>
    #map{
        width: 600px;
        height: 400px;
        margin: 0;
        padding: 0;
        display: none;
    }
</style>