# Poverty_and_Voting
One Stop Early Voting Sities in NC counties with high rates of poverty
## Intro
This map explores the accessability of 2020 One Stop Voting Sites in North Carolina to a vulnerable population of people living below the poverty line.
<br>
[*2020 Poverty Guidelines by HHS*](https://aspe.hhs.gov/poverty-guidelines)
<br>
[*More Info*](https://www.ncsbe.gov/voting/vote-early-person) on One Stop Early Voting in NC
### Major Functions
##### Adding Place Markers
    pointToLayer: function(feature, latlng) {
      var id = 0;
      if (feature.properties.property_t == "World") {id = 0; }
      return L.marker(latlng, {icon: L.divIcon({
                                className: 'fas fa-info markers-color-' + (id + 0).toString() })});
    },
      attribution: 'One Stop Voting Sites &copy; NC OneMap | Population Living Below The Poverty Line &copy; US Census Bureau | Base Map &copy; CartoDB | Map Author: Karyn Reid '
    }).addTo(mymap);
#### Adding Popups
     onEachFeature: function (feature, layer) {
      layer.bindPopup(feature.properties.Place_addr);
    },
##### Choosing the Symbolism of Choropleth Map
     function setColor(density) {
    var id = 0;
     if (density > 0.28) { id = 5; } // highest density
      else if (density > 0.23 && density <= 0.28) {id = 4; }
      else if (density > 0.18 && density <= 0.23) {id = 3; }
      else if (density > 0.13 && density <= 0.18) { id = 2; }
      else if (density > 0.08 && density <= 0.13) {id = 1; }
      else { id = 0; } // lowest density
    return colors[id];
    }

     function style(feature) {
    return {
      fillColor: setColor(feature.properties.Density),
      fillOpacity: 0.3,
      weight: 2,
      opacity: 1,
      color: '#b4b4b4',
      dashArray: '4'
    };
     }
     L.geoJson.ajax("assets/4326Poly_BelPov.geojson", {
    style: style
    }).addTo(mymap);
#### Adding a Legend
    legend.onAdd = function() {
    var div = L.DomUtil.create('div', 'legend');

    div.innerHTML += '<b>Population living below the poverty line</b><br />';
    div.innerHTML += '<i style="background: ' + colors[4] + '; opacity: 0.5"></i><p>>28%</p>';
    div.innerHTML += '<i style="background: ' + colors[3] + '; opacity: 0.5"></i><p>23%-28%</p>';
           div.innerHTML += '<i style="background: ' + colors[2] + '; opacity: 0.5"></i><p>18%-22%</p>';
           div.innerHTML += '<i style="background: ' + colors[1] + '; opacity: 0.5"></i><p>13%-17%</p>';
           div.innerHTML += '<i style="background: ' + colors[0] + '; opacity: 0.5"></i><p><12%</p>';

    div.innerHTML += '<hr><b>Voting Sites<b><br />';
    div.innerHTML += '<i class="fas fa-info"></i><p>One Stop</p>';
    return div;
    };
    legend.addTo(mymap);
### Libraries
#### Style Library from Font Awesome
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.14.0/css/all.css">

#### Leaflet.ajax Library
    <script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet-ajax/2.1.0/leaflet.ajax.min.js"></script>

#### Chroma.js Library
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/chroma-js/1.3.4/chroma.min.js"></script>

#### Google Fonts Library
    <link href="https://fonts.googleapis.com/css?family=Faustina" rel="stylesheet">

### Data Sources
POINTS: NC OneMap - [One Stop Voting Sites (2020)](https://www.nconemap.gov/datasets/north-carolina-one-stop-voting-sites)
<br>
CHOROPLETH: US Census Bureau - 2014-2018 American Community Survey 5-Year Estimates (csv)<br>
[Population Below the Poverty Line (2018)](https://data.census.gov/cedsci/table?t=Official%20Poverty%20Measure%3APopulations%20and%20People&g=0400000US37.050000&y=2018&tid=ACSDT5Y2018.B17001&moe=false&hidePreview=true)
<br>
NC_counties (shp)- NC OneMap
