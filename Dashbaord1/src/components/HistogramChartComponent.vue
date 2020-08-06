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

				// Themes begin
				am4core.useTheme(am4themes_animated);
				// Themes end

				// Create chart instance
				var chart = am4core.create("chartdiv", am4charts.XYChart);
				chart.scrollbarX = new am4core.Scrollbar();

				// Creating Axes
				var xAxis = chart.xAxes.push(new am4charts.ValueAxis())
				xAxis.dataFields.useColumnNames = "torque_log_values_id";

				var yAxis = chart.yAxes.push(new am4charts.ValueAxis())
				yAxis.dataFields.useColumnNames = "torque_values";

				// Dataloader virker lige nu men vi har ikke godt data
				chart.dataSource.url = "https://dashboardtest.imfast.io/TouqueData.CSV";
				chart.dataSource.parser = new am4core.CSVParser();
				chart.dataSource.parser.options.useColumnNames = true;
				
				// Create series
				var series = chart.series.push(new am4charts.ColumnSeries());
				series.dataFields.valueX = "torque_log_values_id";
				series.dataFields.valueY = "torque_values";
				series.columns.template.strokeWidth = 0;

				//series.tensionX = 1;
				series.bullets.push(new am4charts.CircleBullet());

				//Add Legend
				chart.legend = new am4charts.Legend();
				



			}); // end am4core.ready()

		},
	}
</script>

<style scoped>
	#chartdiv {
		width: 50%;
		height: 500px;
	}
</style>