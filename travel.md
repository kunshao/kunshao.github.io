---
layout: page
title: Travel
permalink: /travel/
---

<link rel="stylesheet" href="/assets/css/style.css">
<h4>"I haven’t been everywhere, but it’s on my list." - Susan Sontag</h4>
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
        var frankfurt = {lat: 50.1109, lng: 8.6821};
        // The map, centered at Seattle
        var mapOptions = {
            zoom: 3, 
            center: frankfurt
        }
        var map = new google.maps.Map(
        document.getElementById('map'), mapOptions);
        var geocoder = new google.maps.Geocoder();
        $.getJSON("/cities.json", function(cities) {
            var markers = cities.map(function(city, i) {
                        var latlng = { lat: parseFloat(city.latlng[0]), lng: parseFloat(city.latlng[1])};                   
                        var imageString = `<span>${city.name.replace(/\_/g, ' ')}</span><br><img class='city-image' src='/assets/img/${city.name}.JPG'/>`;
                        var imagewindow = new google.maps.InfoWindow({
                            content: imageString
                        });
                        var marker = new google.maps.Marker({
                            map: map,
                            position: latlng,
                            title: city.name,
                        });
                        imagewindow.open(map, marker);
                        marker.addListener('click', function() {
                            imagewindow.open(map, marker);
                        });
                        return marker;
                    });            
            var markerCluster = new MarkerClusterer(map, markers,
                    {imagePath: 'https://developers.google.com/maps/documentation/javascript/examples/markerclusterer/m'});
        });          
    }
</script>