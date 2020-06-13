<template>
	<div id="chartdiv"></div>
</template>

<script>
	import * as am4core from "@amcharts/amcharts4/core";
	import * as am4charts from "@amcharts/amcharts4/charts";
	import am4themes_animated from "@amcharts/amcharts4/themes/animated";

	am4core.useTheme(am4themes_animated);

	export default {
		name: 'HistogramChartComponent',
		mounted() {
			am4core.ready(function () {

				var chart = am4core.create("chartdiv", am4charts.GaugeChart);
				chart.innerRadius = -15;

				var axis = chart.xAxes.push(new am4charts.ValueAxis());
				axis.min = 0;
				axis.max = 100;
				axis.strictMinMax = true;

				var gradient = new am4core.LinearGradient();
				gradient.stops.push({ color: am4core.color("red") })
				gradient.stops.push({ color: am4core.color("yellow") })
				gradient.stops.push({ color: am4core.color("green") })

				axis.renderer.line.stroke = gradient;
				axis.renderer.line.strokeWidth = 15;
				axis.renderer.line.strokeOpacity = 1;

				axis.renderer.grid.template.disabled = true;

				var hand = chart.hands.push(new am4charts.ClockHand());
				hand.radius = am4core.percent(97);

				setInterval(function () {
					hand.showValue(Math.random() * 100, 1000, am4core.ease.cubicOut);
				}, 2000);


			}); // end am4core.ready()
		}
	}
</script>

<style scoped>
	#chartdiv {
		width: 50%;
		height: 200px;
	}
	
</style>