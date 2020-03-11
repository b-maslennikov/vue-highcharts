<template>
	<div ref="chart"></div>
</template>

<script>
import Highcharts from 'highcharts'

function cloneObj(obj, original, copyArray) {
	
	function callback (value, key) {
		if (Highcharts.isObject(value, !copyArray) && !Highcharts.isClass(value) && !Highcharts.isDOMElement(value)) {
			obj[key] = cloneObj(obj[key] || Highcharts.isArray(value) ? [] : {}, value, copyArray)
		} else {
			obj[key] = original[key]
		}
	}

	if (Highcharts.isArray(original)) {
		original.forEach(callback)
	} else {
		Highcharts.objectEach(original, callback)
	}
	return obj
}

export default {
	props: {
		constructorType: {
			type: String,
			default: 'chart'
		},
		options: {
			type: Object,
			required: true
		},
		callback: {
			type: Function
		},
		updateArgs: {
			type: Array,
			default: () => [true, true]
		},
		highcharts: {
			type: Object
		},
		deepCopyOnUpdate: {
			type: Boolean,
			default: true
		}
	},
	watch: {
		options: {
			handler (newValue) {
				this.chart.update(cloneObj({}, newValue, this.deepCopyOnUpdate), ...this.updateArgs)
			},
			deep: true
		}
	},
	computed: {
		instance() {
			return this.chart
		}
	},
	methods: {
		init() {
			let HC = this.highcharts || Highcharts

			if (this.options && HC[this.constructorType]) {

				let el = this.$refs.chart
				let options = cloneObj({}, this.options, true)
				let callback = this.callback ? this.callback : null

				this.chart = HC[this.constructorType](el, options, callback)

			} else {

				let msg = !this.options
					? 'The "options" parameter was not passed.'
					: `'${this.constructorType}' constructor-type is incorrect. Sometimes this error is caused by the fact, that the corresponding module wasn't imported.`
				console.warn(msg);

			}
		},
		destroy() {
			if (this.chart) {
				this.chart.destroy()
			}
		}
	},
	mounted() {
		this.init()
	},
	beforeDestroy () {
		this.destroy();
	}
}
</script>