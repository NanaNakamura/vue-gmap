# vue-gmap

グーグルマップを表示するコンポーネント

🗾<a href="https://dev.1-10.net/nakamura/c/vue-gmap/index.html" target="_blank">Demo</a>


## Usage

### HTML
```
<template>
  <Gmap
    :lat="35.003248"
    :lng="135.758471"
  />
</template>
```

| Props | Type | Default | Description |
|-------|------|---------|-------------|
| lat | Number | 35.681236 | (必須) 緯度 |
| lng | Number | 139.767125 | (必須) 経度 |
| zoom | Number | 17 | (任意) 地図のズームレベル(0～18) |
| makerSrc | String |  | (任意) オリジナルマーカーを設定する場合の画像パス |
| makerWidth | Number |  | (任意) オリジナルマーカーの画像の横幅 |
| makerHeight | Number |  | (任意) オリジナルマーカーの画像の縦幅 |
| type | String |  | (任意) `GrayScaleMap` or `CustomMap` |
| styleJson | Array |  | (任意) CustomMapのみ記入  https://mapstyle.withgoogle.com/ で作ったstyle jsonを使う  |


### scripts

.vueファイルコンポーネントフォルダーにコピペして、  
componentsに追加？

```
import Gmap from './components/Gmap'

export default {
  components: {
    Gmap
  },
  mounted () {
    // グーグルマップAPIの読み込み
    google.maps.event.addDomListener(window, 'load', () => {
      this.$children.forEach(element => {
        if(element.$options.name === 'Gmap') {
          element.init();
        }
      });
    });
  }
}
```

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# SCSSを有効化
npm install sass-loader node-sass --save-dev

<style lang="scss">
/* write SASS! */
</style>

# reset CSSをインストール
npm install --save formula-css

# jquery をインストール
npm install --save jquery
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
