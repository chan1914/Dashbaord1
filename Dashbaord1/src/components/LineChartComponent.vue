<template>
	<div id="chartdiv"></div>
</template>

<script>
	import * as am4core from "@amcharts/amcharts4/core";
	import * as am4charts from "@amcharts/amcharts4/charts";
	import am4themes_animated from "@amcharts/amcharts4/themes/animated";

	am4core.useTheme(am4themes_animated);

	export default {
		name: 'LineChartComponent',
		mounted() {
			am4core.ready(function () {

				// Themes begin
				am4core.useTheme(am4themes_animated);
				// Themes end

				// Create chart instance
				var chart = am4core.create("chartdiv", am4charts.XYChart);
				chart.paddingRight = 20;


				//Datasets for momentkurve
				chart.data = [{
					"torque_log_values_id": 0,
					"torque_values": 0
				}, {
					"torque_log_values_id": 2,
					"torque_values": 1
				}, {
					"torque_log_values_id": 3,
					"torque_values": 3
				}, {
					"torque_log_values_id": 8,
					"torque_values": 3
				}, {
					"torque_log_values_id": 15,
					"torque_values": 4
				}, {
					"torque_log_values_id": 25,
					"torque_values": 5
				}, {
					"torque_log_values_id": 50,
					"torque_values": 4
				}, {
					"torque_log_values_id": 70,
					"torque_values": 1
				}, {
					"torque_log_values_id": 100,
					"torque_values": 0

				}];

				// Create axes
				var categoryAxis = chart.xAxes.push(new am4charts.CategoryAxis());
				categoryAxis.dataFields.category = "torque_log_values_id";
				categoryAxis.renderer.minGridDistance = 50;
				categoryAxis.renderer.grid.template.location = 0.5;
				categoryAxis.renderer.ticks.template.length = 10;


				// Create value axis
				var valueAxis = chart.yAxes.push(new am4charts.ValueAxis());
				valueAxis.baseValue = 0;

				// Create series
				var series = chart.series.push(new am4charts.LineSeries());
				series.dataFields.valueY = "torque_values";
				series.dataFields.categoryX = "torque_log_values_id";
				series.strokeWidth = 2;
				series.tensionX = 0.77;

				// bullet is added because we add tooltip to a bullet for it to change color
				var bullet = series.bullets.push(new am4charts.Bullet());
				bullet.tooltipText = "{valueY}";

				bullet.adapter.add("fill", function (fill, target) {
					if (target.dataItem.valueY < 0) {
						return am4core.color("#FF0000");
					}
					return fill;
				})
				var range = valueAxis.createSeriesRange(series);
				range.value = 0;
				range.endValue = -1000;
				range.contents.stroke = am4core.color("#FF0000");
				range.contents.fill = range.contents.stroke;

			}); // end am4core.ready()
		},
	}
</script>

<style scoped>
	#chartdiv {
		width: 40%;
		height: 300px;
	}
</style>