<template>
  <div id="app">
    <h1>Display google map</h1>

    <h2>Normal</h2>
    <Gmap :lat="35.003248" :lng="135.758471"></Gmap>

    <h2>Custom pin</h2>
    <Gmap :lat="35.003248" :lng="135.758471" maker-src="static/assets/images/maker.svg" :makerWidth="60" :makerHeight="84"></Gmap>

    <h2>Custom map color</h2>
    <Gmap :lat="35.003248" :lng="135.758471" type="GrayScaleMap" maker-src="static/assets/images/maker.svg" :makerWidth="60" :makerHeight="84"></Gmap>
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
}
</style>
