# vue-scroll-loader 

![](https://img.shields.io/github/license/molvqingtai/vue-scroll-loader.svg) ![](https://img.shields.io/github/size/molvqingtai/vue-scroll-loader/dist/vue-scroll-loader.umd.min.js.svg) ![](https://img.shields.io/npm/dt/vue-scroll-loader.svg) ![](https://img.shields.io/npm/v/vue-scroll-loader.svg) 



A vue-scroll-loader plugin for vue.js.



## Install

**NPM**

```shell
npm install vue-scroll-loader
```

**CDN**

```html
<script src="https://unpkg.com/vue-scroll-loader"></script>
```



## Usage

Use **scroll-loader** to enable the scroll load, and use **loader-*** props to define its options.

The method appointed as the props of **loader-method** will be executed when the bottom of the element reaches the bottom of the viewport.

```html
<scroll-loader :loader-method="getImagesInfo" :loader-enable="loadMore">
	<!-- You can replace the default loading animation with slot here. -->
</scroll-loader>
```

```javascript
import Vue from 'vue'
import ScrollLoader from 'vue-scroll-loader'

Vue.use(ScrollLoader)

new Vue({
    el: '#app',
    data() {
      return {
        loadMore: true,
        page: 1,
        pageSize: 9,
        images: [],
      }
    },
    methods: {
      getImagesInfo() {
        axios.get('https://api.example.com/', {
            params: {
              page: this.page++,
              per_page: this.pageSize,
            }
          })
          .then(res => {
            this.images.concat(res.data)
            
            // Stop scroll-loader
            res.data.length < this.pageSize && (this.loadMore = false)
          })
          .catch(error => {
            console.log(error);
          })
      },
      handleLoad(e) {
        console.log(e)
      }
    },
    mounted() {
      this.getImagesInfo()
    }
  })
```



## Options

| Props            | Description                                                  | **Required** | Type     | Default |
| ---------------- | ------------------------------------------------------------ | ------------ | -------- | ------- |
| :loader-method   | Scrolling to the bottom to execute the method                | true         | Function | --      |
| :loader-enable   | Scroll-loader will be disabled if the value of this props is false. | true         | Boolean  | --      |
| :loder-throttle  | Check the frequency of scrolling to the bottom (ms)          | false        | Number   | 100     |
| :loader-distance | The minimum distance between the bottom of the scroll-loader and the bottom of the viewport before the ":loader-method" method is executed. | false        | Number   | 0       |
| loader-color     | Load the color of the animation                              | false        | String   | #96C8FF |




## License

[MIT](https://github.com/molvqingtai/vue-scroll-loader/blob/dev/LICENSE)