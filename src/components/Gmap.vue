<template>
  <div class="gmap"></div>
</template>

<script>
export default {
  name: 'Gmap',
  data () {
    return {
      data: {
        map: '',
        zoom: 17,
        lat: '35.681236',
        lng: '139.767125'
      }
    }
  },
  props: {
    lat: Number,
    lng: Number,
    makerSrc: String,
    makerWidth: Number,
    makerHeight: Number,
    type: String
  },
  methods: {
    init () {
      let self = this
      let lat = this.lat
      let lng = this.lng
      let makerSrc = this.makerSrc
      let makerWidth = this.makerWidth
      let makerHeight = this.makerHeight
      let style = this.type

      // 地図を表示
      self.data.map = new google.maps.Map(self.$el, {
        center: {lat: lat, lng: lng},
        zoom: self.data.zoom
      });

      // 地図をグレースケールに
      if(style === 'GrayScaleMap') {
        let mapStyle = [{
          "stylers": [{
            "saturation": -100
          }]
        }];
        let mapType = new google.maps.StyledMapType(mapStyle);
        self.data.map.mapTypes.set( 'GrayScaleMap', mapType);
        self.data.map.setMapTypeId( 'GrayScaleMap' );
      }

      // ピンを立てる
      let pos = {lat: lat, lng: lng};
      self.addMaker(pos, makerSrc, makerWidth, makerHeight);
    },
    addMaker (position, src, width, height) {
      let self = this;

      if(src && width && height) {
        new google.maps.Marker({
          position: position,
          icon: src,
          map: self.data.map
        });
      } else {
        new google.maps.Marker({
          position: position,
          map: self.data.map
        });
      }
    }
  }
}
</script>

<style lang="scss">
.gmap {
  width: 100%;
  height: 400px;
  background: #eeeeee;
}
</style>
