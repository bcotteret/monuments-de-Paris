<template>
    <div id="map">
    </div>
</template>
<script>
import L from "leaflet";
import 'leaflet/dist/leaflet.css';

export default {
    name:"Mapbox",
    components: { },
    props: {
        sites: Array
    },
    data(){
        return{
                map: null,
                tileLayer: null,
                marker: null,
                zoom: 12,
                center: [48.853639, 2.346189],
                url: 'https://stamen-tiles-{s}.a.ssl.fastly.net/toner-lite/{z}/{x}/{y}{r}.png',
                attribution:
                    'contributors',
                currentZoom: 11,
                currentCenter: L.latLng(47.41322, -1.219482),
                showParagraph: false,
                mapOptions: {
                    zoomSnap: 0.5
                },
                showMap: true
        };
    },
    methods: {
        zoomUpdate(zoom) {
          this.currentZoom = zoom;
        },
        centerUpdate(center) {
            this.currentCenter = center;
        },
        showLongText() {
            this.showParagraph = !this.showParagraph;
        },
        innerClick() {
            alert("Click!");
        }
    },
    mounted(){
        this.map = L.map('map').setView(this.center, this.zoom);
        this.tileLayer = L.tileLayer(this.url).addTo(this.map);
        const array = this.sites;
        for (let i = 0; i < array.length; i++) {
            const s = array[i];
            var icon = L.divIcon({
                className: 'custom-div-icon',
                html: `<div class='marker-pin ${s.categorie}'></div><span class='material'>${s.id}</span>`,
                iconSize: [30, 42],
                iconAnchor: [15, 42]
                });
            this.marker = L.marker([s.latitude, s.longitude], {
                    icon: icon
                }).addTo(this.map);   
        }
    }
}
</script>
<style lang="css">
#map {
   height: 800px;
   width: 100%;
}
.marker-pin {
  width: 30px;
  height: 30px;
  border-radius: 50% 50% 50% 0;
  
  position: absolute;
  transform: rotate(-45deg);
  left: 50%;
  top: 50%;
  margin: -15px 0 0 -15px;
}

.marker-pin::after {
    content:' ';
    width: 24px;
    height: 24px;
    margin: 3px 0 0 3px;
    right: 3px;
    background: #fff;
    position: absolute;
    border-radius: 50%;
 }
.material {
    font-weight: bold;
}
.custom-div-icon span {
   position: absolute;
   width: 22px;
   font-size: 17px;
   left: 0;
   right: 0;
   margin: 7px auto;
   text-align: center;
}

.custom-div-icon i.awesome {
   margin: 12px auto;
   font-size: 17px;
}
</style>