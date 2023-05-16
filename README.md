# Chame-a-Brigada
Aplicativo para informações sobre incêndios 
<!DOCTYPE html>
<html>
<head>
    <title>Aplicativo de Incêndios</title>
    <meta charset="utf-8" />
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/leaflet.css" />
    <style>
        #map {
            height: 400px;
            width: 100%;
        }
    </style>
</head>
<body>
    <div id="map"></div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/leaflet.js"></script>
    <script>
        // Configurar o mapa
        var map = L.map('map').setView([0, 0], 13);

        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors',
            maxZoom: 18
        }).addTo(map);

        // Adicionar marcador
        map.on('click', function (event) {
            var marker = L.marker(event.latlng).addTo(map);
            var latitude = event.latlng.lat;
            var longitude = event.latlng.lng;

            console.log("Latitude: " + latitude + ", Longitude: " + longitude);
        });

        // Obter a localização do usuário
        if (navigator.geolocation) {
            navigator.geolocation.getCurrentPosition(function (position) {
                var userLocation = [position.coords.latitude, position.coords.longitude];
                map.setView(userLocation, 13);

                var userMarker = L.marker(userLocation).addTo(map);
                userMarker.bindPopup("Sua localização atual").openPopup();
            }, function (error) {
                console.log("Erro ao obter a localização do usuário: " + error.message);
            });
        } else {
            console.log("Navegador não suporta Geolocalização");
        }
    </script>
</body>
</html>
