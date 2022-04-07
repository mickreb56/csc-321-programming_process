<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/openlayers/openlayers.github.io@master/en/v6.14.1/css/ol.css" type="text/css">
    <style>
      .map {
        height: 400px;
        width: 100%;
      }
    </style>
    <script src="https://cdn.jsdelivr.net/gh/openlayers/openlayers.github.io@master/en/v6.14.1/build/ol.js"></script>
    <title>OpenLayers example</title>
  </head>
  <body>
    <h2>My Map</h2>
    <div id="map" class="map"></div>
    <div id="popup" class="ol-popup">
        <a href="#" id="popup-closer" class="ol-popup-closer"></a>
        <div id="popup-content"></div>
    </div>   
    <script type="text/javascript">
        var map = new ol.Map({
        target: 'map',
        layers: [
          new ol.layer.Tile({
            source: new ol.source.OSM()

          })
        ],
        view: new ol.View({
          center: ol.proj.fromLonLat([128.251586, 35.818329]),
          zoom: 2
        })

      });
        var layer1 = new ol.layer.Vector({
            source: new ol.source.Vector({
                features: [
                    new ol.Feature({
                        geometry: new ol.geom.Point(ol.proj.fromLonLat([128.251586, 35.818329]))
                    })
                ]
            })
        });

        var layer2 = new ol.layer.Vector({
            source: new ol.source.Vector({
                features: [
                    new ol.Feature({
                        geometry: new ol.geom.Point(ol.proj.fromLonLat([-119.331665, 36.317557]))
                    })
                ]
            })
        });

        var layer3 = new ol.layer.Vector({
            source: new ol.source.Vector({
                features: [
                    new ol.Feature({
                        geometry: new ol.geom.Point(ol.proj.fromLonLat([-120.719322, 35.560568]))
                    })
                ]
            })
        });

        var layer4 = new ol.layer.Vector({
            source: new ol.source.Vector({
                features: [
                    new ol.Feature({
                        geometry: new ol.geom.Point(ol.proj.fromLonLat([-77.094646, 38.984826]))
                    })
                ]
            })
        });

        var layer5 = new ol.layer.Vector({
            source: new ol.source.Vector({
                features: [
                    new ol.Feature({
                        geometry: new ol.geom.Point(ol.proj.fromLonLat([-118.156124, 33.788145]))
                    })
                ]
            })
        });
    map.addLayer(layer1);
    map.addLayer(layer2);
    map.addLayer(layer3);
    map.addLayer(layer4);
    map.addLayer(layer5);

    var container = document.getElementById('popup');
    var content = document.getElementById('popup-content');
    var closer = document.getElementById('popup-closer');

    var overlay = new ol.Overlay({
        element: container,
        autoPan: true,
        autoPanAnimation: {
            duration: 250
        }
    });
    map.addOverlay(overlay);

    closer.onclick = function() {
        overlay.setPosition(undefined);
        closer.blur();
        return false;
    };
    map.on('singleclick', function (event) {
     if (map.hasFeatureAtPixel(event.pixel) === true) {
         var coordinate = event.coordinate;
        // change the innerHTMl content based on the feature and popup there name based on the location
            // content.innerHTML = '<p>' + '<b>' + 'Michael' + '</b>' + '</p>' + '<p>' + '<b>' + 'Jiwon' + '</b>' + '</p>' + '<p>' + '<b>' + 'Sarah' + '</b>' + '</p>' + '<p>' + '<b>' + 'Emily' + '</b>' + '</p>' + '<p>' + '<b>' + 'Logan' + '</b>' + '</p>';
            // content.innerHTML = '<p>' + names[0] + '</p>';

        

         content.innerHTML = '<b>A person lives here!</b><br />But I wont say who ¯\\_(ツ)_/¯';
         overlay.setPosition(coordinate);
     } else {
         overlay.setPosition(undefined);
         closer.blur();
     }
 });
    </script>
  </body>
</html>