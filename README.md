<h1 align="center">Vue-Highcharts</h1>

It's an extended version of the official highcharts wrapper: https://github.com/highcharts/highcharts-vue

It allows you to use highchart props and methods from your code.


# Installation
Using npm
```shell
$ npm i @tattdogg/vue-highcharts
```

# Usage
```javascript
import { Chart } from '@tattdogg/vue-highcharts'

components: {
	highcharts: Chart
}
```

```html
<highcharts :options="options" ref="chart" />
```

```javascript
this.$refs.chart.instance.showLoading('Loading...'); // or any other highcharts method or property
```

TypeScript is supported.