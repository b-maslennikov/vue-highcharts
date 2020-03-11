<h1 align="center">Vue-Highcharts</h1>

It's extended version of this: https://github.com/highcharts/highcharts-vue

# Installation
Using npm
```shell
$ npm i @tattdogg/vue-highcharts
```

# Usage
```javascript
import VueHighcharts from '@tattdogg/vue-highcharts'

components: {
	VueHighcharts
}
```

```html
<vue-highcharts :options="options" ref="chart">
```

```javascript
this.$refs.chart.instance.showLoading('Loading...'); // or any other highcharts method or property
```