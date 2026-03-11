<script>
mapboxgl.accessToken = 'pk.eyJ1IjoibWl6cmFoeW0yMiIsImEiOiJjbW1rdGNhMW4xbHRhMnFwbjE1MmRsYWYyIn0.iclB5PQyXs_QLHQ2b7J8hA';

const map = new mapboxgl.Map({
container: 'map',
style: 'mapbox://styles/mapbox/streets-v12',
center: [-93.0, 15.3],
zoom: 9
});

map.on('load', () => {

map.addSource('subzonas', {
type: 'geojson',
data: 'zubzoni-aecixz.geojson'
});

map.addLayer({
id: 'subzonas-fill',
type: 'fill',
source: 'subzonas',
paint: {
'fill-color': '#088',
'fill-opacity': 0.5
}
});

map.addLayer({
id: 'subzonas-outline',
type: 'line',
source: 'subzonas',
paint: {
'line-color': '#000',
'line-width': 1
}
});

map.on('click', 'subzonas-fill', (e) => {
const props = e.features[0].properties;

new mapboxgl.Popup()
.setLngLat(e.lngLat)
.setHTML(`
<h3>${props.Subzonif}</h3>
<p><strong>Zonificación:</strong> ${props.Zonif}</p>
<p><strong>Usos permitidos:</strong> ${props.Usos_permitidos}</p>
<p><strong>Usos compatibles:</strong> ${props.Usos_compatibles}</p>
<p><strong>Usos condicionados:</strong> ${props.Usos_condicionados}</p>
`)
.addTo(map);
});

map.on('mouseenter', 'subzonas-fill', () => {
map.getCanvas().style.cursor = 'pointer';
});

map.on('mouseleave', 'subzonas-fill', () => {
map.getCanvas().style.cursor = '';
});

});
</script>
