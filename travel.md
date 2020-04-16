---
layout: page
title: Travel
permalink: /travel/
---

<link rel="stylesheet" href="/assets/css/style.css">
<h3></h3>
<!--The div element for the map -->
<div id="map"></div>
<!-- Replace the value of the key parameter with your own API key. -->
<script async defer
src="https://maps.googleapis.com/maps/api/js?key=AIzaSyD5zz1ag4UQvBIYHfy0b1uLLt4QWnkygJE&callback=initMap">
</script>
<script>
    // Initialize and add the map
    function initMap() {
    // The location of Seattle
    var seattle = {lat: 47.606, lng: -122.332};
    // The map, centered at Seattle
    var map = new google.maps.Map(
        document.getElementById('map'), {zoom: 4, center: seattle});
    // The marker, positioned at Seattle
    var marker = new google.maps.Marker({position: seattle, map: map});
    }
</script>