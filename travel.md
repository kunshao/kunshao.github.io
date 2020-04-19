---
layout: page
title: Travel
permalink: /travel/
---

<link rel="stylesheet" href="/assets/css/style.css">
<h5>"Travel makes one modest, you see what a tiny place you occupy in the world." - Gustave Flaubert</h5>
<!--The div element for the map -->
<div id="map"></div>
<!-- Replace the value of the key parameter with your own API key. -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
<script src="https://developers.google.com/maps/documentation/javascript/examples/markerclusterer/markerclustererplus@4.0.1.min.js"></script>
<script async defer src="https://maps.googleapis.com/maps/api/js?key=AIzaSyD5zz1ag4UQvBIYHfy0b1uLLt4QWnkygJE&callback=initMap"></script>
<script>
    // Initialize and add the map
    function initMap() {
        // The location of Seattle
        var seattle = {lat: 47.606, lng: -122.332};
        // The map, centered at Seattle
        var mapOptions = {
            zoom: 1, 
            center: seattle
        }
        var map = new google.maps.Map(
        document.getElementById('map'), mapOptions);
        var geocoder = new google.maps.Geocoder();
        $.getJSON("/cities.json", function(cities) {
            var markers = cities.map(function(city, i) {
                        var latlng = { lat: parseFloat(city.latlng[0]), lng: parseFloat(city.latlng[1])};                   
                        var imageString = `<img class='city-image' src='/assets/img/${city.name}.jpg'/>`;
                        var imagewindow = new google.maps.InfoWindow({
                            content: imageString
                        });
                        var marker = new google.maps.Marker({
                            map: map,
                            position: latlng,
                            animation: google.maps.Animation.DROP,
                            title: city.name,
                        });
                        imagewindow.open(map, marker);
                        return marker;
                    });            
            var markerCluster = new MarkerClusterer(map, markers,
                    {imagePath: 'https://developers.google.com/maps/documentation/javascript/examples/markerclusterer/m'});
        });          
    }
</script>