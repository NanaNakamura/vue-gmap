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
    zoom: Number,
    makerSrc: String,
    makerWidth: Number,
    makerHeight: Number,
    type: String,
    styleJson: Array
  },
  methods: {
    init () {
      let self = this
      let lat = self.lat
      let lng = self.lng
      let zoom = self.zoom
      let makerSrc = self.makerSrc
      let makerWidth = self.makerWidth
      let makerHeight = self.makerHeight
      let style = self.type
      let json = self.styleJson

      // ズームの値
      if(zoom) {
        self.data.zoom = zoom
      }

      // 地図を表示
      self.data.map = new google.maps.Map(self.$el, {
        center: {lat: lat, lng: lng},
        zoom: self.data.zoom,
        // コントローラーの設定
        zoomControl: true,
        mapTypeControl: false,
        scaleControl: true,
        streetViewControl: false,
        rotateControl: false,
        fullscreenControl: false
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
      // 地図をCustomに
      if(style === 'Custom') {
        let mapStyle = json;
        let mapType = new google.maps.StyledMapType(mapStyle);
        self.data.map.mapTypes.set( 'CustomMap', mapType);
        self.data.map.setMapTypeId( 'CustomMap' );
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
