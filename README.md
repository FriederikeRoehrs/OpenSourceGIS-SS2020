# OpenSourceGIS-SS2020
Aufgabe: Erstellung einer Webkarte

<!doctype html>

<html lang="en">

    <head>

        <meta charset="utf-8">

        <meta http-equiv="X-UA-Compatible" content="IE=edge">

        <meta name="viewport" content="initial-scale=1,user-scalable=no,maximum-scale=1,width=device-width">

        <meta name="mobile-web-app-capable" content="yes">

        <meta name="apple-mobile-web-app-capable" content="yes">

        <link rel="stylesheet" href="css/leaflet.css">

        <link rel="stylesheet" href="css/qgis2web.css"><link rel="stylesheet" href="css/fontawesome-all.min.css">

        <link rel="stylesheet" href="css/leaflet-control-geocoder.Geocoder.css">

        <style>

        #map {

            width: 1226px;

            height: 851px;

        }

        </style>

        <title></title>

    </head>

    <body>

        <div id="map">

        </div>

        <script src="js/qgis2web_expressions.js"></script>

        <script src="js/leaflet.js"></script>

        <script src="js/leaflet.rotatedMarker.js"></script>

        <script src="js/leaflet.pattern.js"></script>

        <script src="js/leaflet-hash.js"></script>

        <script src="js/Autolinker.min.js"></script>

        <script src="js/rbush.min.js"></script>

        <script src="js/labelgun.min.js"></script>

        <script src="js/labels.js"></script>

        <script src="js/leaflet-control-geocoder.Geocoder.js"></script>

        <script src="data/appkrankenhaeuser_hh_1.js"></script>

        <script>

        var highlightLayer;

        function highlightFeature(e) {

            highlightLayer = e.target;



            if (e.target.feature.geometry.type === 'LineString') {

              highlightLayer.setStyle({

                color: '#ffff00',

              });

            } else {

              highlightLayer.setStyle({

                fillColor: '#ffff00',

                fillOpacity: 1

              });

            }

        }

        var map = L.map('map', {

            zoomControl:true, maxZoom:28, minZoom:1

        }).fitBounds([[53.45303472099218,9.729969023879676],[53.68159913770575,10.284832976120299]]);

        var hash = new L.Hash(map);

        map.attributionControl.setPrefix('<a href="https://github.com/tomchadwin/qgis2web" target="_blank">qgis2web</a> &middot; <a href="https://leafletjs.com" title="A JS library for interactive maps">Leaflet</a> &middot; <a href="https://qgis.org">QGIS</a>');

        var autolinker = new Autolinker({truncate: {length: 30, location: 'smart'}});

        var bounds_group = new L.featureGroup([]);

        function setBounds() {

        }

        map.createPane('pane_OpenStreetMap_0');

        map.getPane('pane_OpenStreetMap_0').style.zIndex = 400;

        var layer_OpenStreetMap_0 = L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {

            pane: 'pane_OpenStreetMap_0',

            opacity: 1.0,

            attribution: '',

            minZoom: 1,

            maxZoom: 28,

            minNativeZoom: 0,

            maxNativeZoom: 19

        });

        layer_OpenStreetMap_0;

        map.addLayer(layer_OpenStreetMap_0);

        function pop_appkrankenhaeuser_hh_1(feature, layer) {

            layer.on({

                mouseout: function(e) {

                    for (i in e.target._eventParents) {

                        e.target._eventParents[i].resetStyle(e.target);

                    }

                },

                mouseover: highlightFeature,

            });

            var popupContent = '<table>\

                    <tr>\

                        <th scope="row">name</th>\

                        <td>' + (feature.properties['name'] !== null ? autolinker.link(feature.properties['name'].toLocaleString()) : '') + '</td>\

                    </tr>\

                    <tr>\

                        <th scope="row">strasse</th>\

                        <td>' + (feature.properties['strasse'] !== null ? autolinker.link(feature.properties['strasse'].toLocaleString()) : '') + '</td>\

                    </tr>\

                    <tr>\

                        <th scope="row">ort</th>\

                        <td>' + (feature.properties['ort'] !== null ? autolinker.link(feature.properties['ort'].toLocaleString()) : '') + '</td>\

                    </tr>\

                </table>';

            layer.bindPopup(popupContent, {maxHeight: 400});

        }



        function style_appkrankenhaeuser_hh_1_0() {

            return {

                pane: 'pane_appkrankenhaeuser_hh_1',

                radius: 4.8,

                opacity: 1,

                color: 'rgba(0,0,0,1.0)',

                dashArray: '',

                lineCap: 'butt',

                lineJoin: 'miter',

                weight: 2.0,

                fill: true,

                fillOpacity: 1,

                fillColor: 'rgba(219,30,42,1.0)',

                interactive: true,

            }

        }

        map.createPane('pane_appkrankenhaeuser_hh_1');

        map.getPane('pane_appkrankenhaeuser_hh_1').style.zIndex = 401;

        map.getPane('pane_appkrankenhaeuser_hh_1').style['mix-blend-mode'] = 'normal';

        var layer_appkrankenhaeuser_hh_1 = new L.geoJson(json_appkrankenhaeuser_hh_1, {

            attribution: '',

            interactive: true,

            dataVar: 'json_appkrankenhaeuser_hh_1',

            layerName: 'layer_appkrankenhaeuser_hh_1',

            pane: 'pane_appkrankenhaeuser_hh_1',

            onEachFeature: pop_appkrankenhaeuser_hh_1,

            pointToLayer: function (feature, latlng) {

                var context = {

                    feature: feature,

                    variables: {}

                };

                return L.circleMarker(latlng, style_appkrankenhaeuser_hh_1_0(feature));

            },

        });

        bounds_group.addLayer(layer_appkrankenhaeuser_hh_1);

        map.addLayer(layer_appkrankenhaeuser_hh_1);

        var osmGeocoder = new L.Control.Geocoder({

            collapsed: true,

            position: 'topleft',

            text: 'Search',

            title: 'Testing'

        }).addTo(map);

        document.getElementsByClassName('leaflet-control-geocoder-icon')[0]

        .className += ' fa fa-search';

        document.getElementsByClassName('leaflet-control-geocoder-icon')[0]

        .title += 'Search for a place';

        setBounds();

        </script>

    </body>

</html>
