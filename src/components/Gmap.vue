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
        lat: 35.681236,
        lng: 139.767125
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
      self.data.lat = (!self.lat) ? self.data.lat : self.lat
      self.data.lng = (!self.lng) ? self.data.lng : self.lng
      self.data.zoom = (!self.zoom) ? self.data.zoom : self.zoom
      let makerSrc = self.makerSrc
      let makerWidth = self.makerWidth
      let makerHeight = self.makerHeight
      let style = self.type
      let json = self.styleJson

      // 地図を表示
      self.data.map = new google.maps.Map(self.$el, {
        center: {lat: self.data.lat, lng: self.data.lng},
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
      if(style === 'Custom' && json !== '') {
        let mapStyle = json;
        let mapType = new google.maps.StyledMapType(mapStyle);
        self.data.map.mapTypes.set( 'CustomMap', mapType);
        self.data.map.setMapTypeId( 'CustomMap' );
      }

      // ピンを立てる
      let pos = {lat: self.data.lat, lng: self.data.lng};
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
