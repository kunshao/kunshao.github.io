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
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
<script async defer
src="https://maps.googleapis.com/maps/api/js?key=AIzaSyD5zz1ag4UQvBIYHfy0b1uLLt4QWnkygJE&callback=initMap">
</script>
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
        $.getJSON("/cities.json", function(data) {
            $.each(data, async function(key, city) {
                if (city.latlng == null) {
                    // look up city coordinates if not already known. Manually store in cities.json for now to avoid OVER_QUERY_LIMIT response from Geocoder API
                    geocoder.geocode({'address': city.name}, function(results, status){
                        if (status == 'OK') {
                            console.log(city.name + results[0].geometry.location)
                        } else {
                            console.log('Geocode was not successful for the following reason: ' + status);
                        }
                    }); 
                } else {
                    var latlng = { lat: parseFloat(city.latlng[0]), lng: parseFloat(city.latlng[1])};
                    var marker = new google.maps.Marker({
                        map: map,
                        position: latlng,
                        animation: google.maps.Animation.DROP,
                        title: city.name,
                        lable: city.name
                    });
                }   
            });
        });
        
    }
</script>