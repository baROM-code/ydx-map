<template>
  <q-page>
    <div class="p-4">
      <p>Map</p>
      <div id="map" style="width: 800px; height: 600px"></div>
    </div>
  </q-page>
</template>

<script type="text/javascript">

ymaps.ready(init);
function init(){
  // Создание карты.
  var myMap = new ymaps.Map("map", {
    // Порядок по умолчанию: «широта, долгота».
    center: [55.76, 37.64],
    zoom: 7
  });
}
</script>

