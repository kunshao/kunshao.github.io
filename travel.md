---
layout: page
title: Travel
permalink: /travel/
---

<script src="https://www.webglearth.com/v2/api.js"></script>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>

<script>
    function initialize() {
        var earth = new WE.map('earth_div');
        WE.tileLayer('http://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',{
            attribution: '© OpenStreetMap contributors'
        }).addTo(earth);

        $.getJSON("/cities.json", function(data) {
            $.each(data, function(key, city) {
                var marker = WE.marker(city.coordinates).addTo(earth);
                marker.bindPopup(`<b>${city.name}</b>`, {maxWidth: 150, closeButton: true}).openPopup();

                if (key === 0) {
                    earth.setView(city.coordinates, 2.5);
                }     
            });
        });
    }
</script>
<body onload="initialize()">
    <div id="earth_div"></div>
</body>