<template>
  <div id="app">
    <h1>Display google map</h1>

    <h2>Normal</h2>
    <Gmap
      :lat="35.003248"
      :lng="135.758471"
    />

    <h2>Set zoom</h2>
    <Gmap
      :lat="35.003248"
      :lng="135.758471"
      :zoom="19"
    />

    <h2>Custom pin</h2>
    <Gmap
      :lat="35.003248"
      :lng="135.758471"
      makerSrc="static/assets/images/maker.svg"
      :makerWidth="60"
      :makerHeight="84"
    />

    <h2>Custom map color (and custom pin)</h2>
    <Gmap
      :lat="35.003248"
      :lng="135.758471"
      type="GrayScaleMap"
      makerSrc="static/assets/images/maker.svg"
      :makerWidth="60"
      :makerHeight="84"
    />

    <h2>Custom map style (and custom pin)</h2>
    <p><a href="https://mapstyle.withgoogle.com/" target="_blank">https://mapstyle.withgoogle.com/</a> で作ったstyle jsonを使う</p>
    <Gmap
      :lat="35.622929"
      :lng="139.749772"
      makerSrc="static/assets/images/maker.svg"
      :makerWidth="60"
      :makerHeight="84"
      type="Custom"
      :styleJson='[
        {
          "elementType": "geometry",
          "stylers": [
            {
              "color": "#ebe3cd"
            }
          ]
        },
        {
          "elementType": "labels.text.fill",
          "stylers": [
            {
              "color": "#523735"
            }
          ]
        },
        {
          "elementType": "labels.text.stroke",
          "stylers": [
            {
              "color": "#f5f1e6"
            }
          ]
        },
        {
          "featureType": "administrative",
          "elementType": "geometry.stroke",
          "stylers": [
            {
              "color": "#c9b2a6"
            }
          ]
        },
        {
          "featureType": "administrative.land_parcel",
          "elementType": "geometry.stroke",
          "stylers": [
            {
              "color": "#dcd2be"
            }
          ]
        },
        {
          "featureType": "administrative.land_parcel",
          "elementType": "labels",
          "stylers": [
            {
              "visibility": "off"
            }
          ]
        },
        {
          "featureType": "administrative.land_parcel",
          "elementType": "labels.text.fill",
          "stylers": [
            {
              "color": "#ae9e90"
            }
          ]
        },
        {
          "featureType": "landscape.natural",
          "elementType": "geometry",
          "stylers": [
            {
              "color": "#dfd2ae"
            }
          ]
        },
        {
          "featureType": "poi",
          "elementType": "geometry",
          "stylers": [
            {
              "color": "#dfd2ae"
            }
          ]
        },
        {
          "featureType": "poi",
          "elementType": "labels.text.fill",
          "stylers": [
            {
              "color": "#93817c"
            }
          ]
        },
        {
          "featureType": "poi.business",
          "stylers": [
            {
              "visibility": "off"
            }
          ]
        },
        {
          "featureType": "poi.park",
          "elementType": "geometry.fill",
          "stylers": [
            {
              "color": "#a5b076"
            }
          ]
        },
        {
          "featureType": "poi.park",
          "elementType": "labels.text",
          "stylers": [
            {
              "visibility": "off"
            }
          ]
        },
        {
          "featureType": "poi.park",
          "elementType": "labels.text.fill",
          "stylers": [
            {
              "color": "#447530"
            }
          ]
        },
        {
          "featureType": "road",
          "elementType": "geometry",
          "stylers": [
            {
              "color": "#f5f1e6"
            }
          ]
        },
        {
          "featureType": "road.arterial",
          "elementType": "geometry",
          "stylers": [
            {
              "color": "#fdfcf8"
            }
          ]
        },
        {
          "featureType": "road.highway",
          "elementType": "geometry",
          "stylers": [
            {
              "color": "#f8c967"
            }
          ]
        },
        {
          "featureType": "road.highway",
          "elementType": "geometry.stroke",
          "stylers": [
            {
              "color": "#e9bc62"
            }
          ]
        },
        {
          "featureType": "road.highway.controlled_access",
          "elementType": "geometry",
          "stylers": [
            {
              "color": "#e98d58"
            }
          ]
        },
        {
          "featureType": "road.highway.controlled_access",
          "elementType": "geometry.stroke",
          "stylers": [
            {
              "color": "#db8555"
            }
          ]
        },
        {
          "featureType": "road.local",
          "elementType": "labels",
          "stylers": [
            {
              "visibility": "off"
            }
          ]
        },
        {
          "featureType": "road.local",
          "elementType": "labels.text.fill",
          "stylers": [
            {
              "color": "#806b63"
            }
          ]
        },
        {
          "featureType": "transit.line",
          "elementType": "geometry",
          "stylers": [
            {
              "color": "#dfd2ae"
            }
          ]
        },
        {
          "featureType": "transit.line",
          "elementType": "labels.text.fill",
          "stylers": [
            {
              "color": "#8f7d77"
            }
          ]
        },
        {
          "featureType": "transit.line",
          "elementType": "labels.text.stroke",
          "stylers": [
            {
              "color": "#ebe3cd"
            }
          ]
        },
        {
          "featureType": "transit.station",
          "elementType": "geometry",
          "stylers": [
            {
              "color": "#dfd2ae"
            }
          ]
        },
        {
          "featureType": "water",
          "elementType": "geometry.fill",
          "stylers": [
            {
              "color": "#b9d3c2"
            }
          ]
        },
        {
          "featureType": "water",
          "elementType": "labels.text.fill",
          "stylers": [
            {
              "color": "#92998d"
            }
          ]
        }
      ]'
    />
  </div>
</template>

<script>
import Gmap from './components/Gmap'

export default {
  name: 'App',
  components: {
    Gmap
  },
  mounted () {
    google.maps.event.addDomListener(window, 'load', () => {
      console.log('google map js 読み込み完了')
      this.$children.forEach(element => {
        if(element.$options.name === 'Gmap') {
          element.init();
        }
      });
    });
  }
}
</script>

<style lang="scss" module>
@import "../node_modules/formula-css/develop/formula.scss";
</style>
<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin: 100px 4%;
  h1 {
    margin-bottom: 20px;
    font-size: 2em;
    font-weight: bold;
    text-align: center;
  }
  h2 {
    margin-top: 80px;
    margin-bottom: 20px;
    font-size: 1.5em;
    font-weight: bold;
  }
  p {
    margin: 10px 0;
    line-height: 1.4;
  }
  a {
    color: #42b983;
  }
}
</style>
