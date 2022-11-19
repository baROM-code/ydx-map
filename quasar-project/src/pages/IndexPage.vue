<template>
  <q-page>
    <div class="p-4">
      <div id="map" style="width: 800px; height: 600px"></div>
    </div>
  </q-page>
</template>

<script type="text/javascript">

ymaps.ready(init);
function init(){
  coords = [51.547, 46.025];
  // Создание карты.
  var myMap = new ymaps.Map("map", {
    // Порядок по умолчанию: «широта, долгота».
    center: coords,
    zoom: 10,
    controls: ["fullscreenControl", "searchControl" , "zoomControl"]
  });
  var myPlacemark = new ymaps.Placemark(coords,{ hintContent: "Нажмите для получения прогноза погоды"}, {draggable: "true"});

  myMap.events.add('click', function (e) {
    coords = e.get('coords');
    // Перемещение точки по клику
    myPlacemark.geometry.setCoordinates(coords);

    /*
    // Вывод сведений о погоде по клику
    myMap.balloon.open(coords, {
        contentBody: 'Погода:<br><img src="http://www.7timer.info/bin/astro.php?lon=' + coords[1] + '&lat=' + coords[0] + '&ac=0&lang=en&unit=metric&output=internal&tzshift=0">'
      }
    );
     */

  });

  myPlacemark.events.add(['click', 'dragend'], function (e) {
    coords = e.get('coords');
    content = 'Погода в: <br>' +
              '<img src="http://www.7timer.info/bin/astro.php?lon=' + coords[1] + '&lat=' + coords[0] + '&ac=0&lang=en&unit=metric&output=internal&tzshift=0">';
    myPlacemark.properties.set('balloonContent', content);
  });

  myMap.geoObjects.add(myPlacemark);
}

</script>

