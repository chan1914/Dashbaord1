<template>
	<div>
		<div id="chartdiv" style="width: 50%; height: 400px;"></div>
	</div>
</template>

<script>
	import * as am4core from "@amcharts/amcharts4/core";
	import * as am4charts from "@amcharts/amcharts4/charts";
	import am4themes_animated from "@amcharts/amcharts4/themes/animated";

	am4core.useTheme(am4themes_animated);

	export default {
		name: 'LineChartComponent',
		//data() {
		//	return {
		//		linesClicked: false
		//	}
		//},
		//methods() {
		//	checkboxClicked(){
		//		this.linesClicked = !this.linesClicked;
		//	}
		//},
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
					"torque_log_values_id": 1,
					"torque_values": 0
				}, {
					"torque_log_values_id": 2,
					"torque_values": 0
				}, {
					"torque_log_values_id": 3,
					"torque_values": 1
				}, {
					"torque_log_values_id": 4,
					"torque_values": 1
				}, {
					"torque_log_values_id": 5,
					"torque_values": 1
				}, {
					"torque_log_values_id": 6,
					"torque_values": 2
				}, {
					"torque_log_values_id": 7,
					"torque_values": 2
				}, {
					"torque_log_values_id": 8,
					"torque_values": 2
				}, {
					"torque_log_values_id": 9,
					"torque_values": 2
				}, {
					"torque_log_values_id": 10,
					"torque_values": 3
				}, {
					"torque_log_values_id": 11,
					"torque_values": 2
				}, {
					"torque_log_values_id": 12,
					"torque_values": 1
				}];

				// Create x axis
				var xAxis = chart.xAxes.push(new am4charts.ValueAxis());
				xAxis.renderer.minGridDistance = 40;
				xAxis.renderer.labels.name = "Newtonmeter";

				// Create y axis
				var yAxis = chart.yAxes.push(new am4charts.ValueAxis());
				yAxis.baseValue = 0;

				//// Dataloader virker men vi har ikke godt data lige nu
				//chart.dataSource.url = "https://dashboardtest.imfast.io/Dashboard_data%20-%20csv.csv";
				//chart.dataSource.parser = new am4core.CSVParser();
				//chart.dataSource.parser.options.useColumnNames = true;

				// Create series
				var series = chart.series.push(new am4charts.LineSeries());
				series.dataFields.valueX = "torque_log_values_id";
				series.dataFields.valueY = "torque_values";
				series.name = "Torque curve";


				//Creating Trendlines
				function createTrendLines(data) {
					var createTrendLineLow = chart.series.push(new am4charts.LineSeries());
					createTrendLineLow.dataFields.valueX = "lowFirst";
					createTrendLineLow.dataFields.valueY = "lowLast";
					createTrendLineLow.strokeWidth = 2
					createTrendLineLow.stroke = am4core.color("#FAFA4C");
					createTrendLineLow.data = data.trendLinesLow;


					var createTrendLineMedium = chart.series.push(new am4charts.LineSeries());
					createTrendLineMedium.dataFields.valueX = "mediumFirst";
					createTrendLineMedium.dataFields.valueY = "mediumLast";
					createTrendLineMedium.strokeWidth = 2
					createTrendLineMedium.stroke = am4core.color("#26F62D");
					createTrendLineMedium.data = data.trendLinesMedium;


					var createTrendLineHigh = chart.series.push(new am4charts.LineSeries());
					createTrendLineHigh.dataFields.valueX = "highFirst";
					createTrendLineHigh.dataFields.valueY = "highLast";
					createTrendLineHigh.strokeWidth = 2
					createTrendLineHigh.stroke = am4core.color("#F62626");
					createTrendLineHigh.data = data.trendLinesHigh;

				}


				//TrendLine data - Low, Medium, High
				var trendLines = {
					trendLinesLow:
						[
							{ "lowFirst": 1, "lowLast": 8 },
							{ "lowFirst": 13, "lowLast": 8 }
						],
					trendLinesMedium:
						[
							{ "mediumFirst": 1, "mediumLast": 10 },
							{ "mediumFirst": 13, "mediumLast": 10 }
						],
					trendLinesHigh:
						[
							{ "highFirst": 1, "highLast": 13 },
							{ "highFirst": 13, "highLast": 13 }
						]
				}

				createTrendLines(trendLines);




				// Add legend
				chart.legend = new am4charts.Legend();
				chart.legend.position = "right";
				chart.legend.itemContainers.template.clickable = true
				chart.legend.itemContainers.template.focusable = true
				chart.legend.itemContainers.template.cursorOverStyle = am4core.MouseCursorStyle.default;
				chart.legend.labels.template.text = "[bold {color}]{name}[/]";
				
				

				//// Add legend
	
				//chart.legend.useDefaultMarker = true;
				//chart.legend.position = "right";

				//const marker = chart.legend.markers.template;
				//const markerColumn = marker.children.getIndex(0);


				//markerColumn.cornerRadius(0, 0, 0, 0);
				//markerColumn.defaultState.properties.fillOpacity = 0;
				//markerColumn.defaultState.properties.strokeWidth = 1;
				//markerColumn.defaultState.properties.stroke = am4core.color("#000");
				//markerColumn.defaultState.properties.strokeOpacity = 1;
				//// markerColumnActiveState.properties.fillOpacity = 0;

				//// Add custom image instead
				//const checkbox = marker.createChild(am4core.Image);
				//checkbox.width = 20;
				//checkbox.height = 20;
				//checkbox.verticalCenter = "top";
				//checkbox.horizontalCenter = "left";

				//checkbox.href = "https://cdn.onlinewebfonts.com/svg/img_207414.png";
				//checkbox.dx = 1;
				//checkbox.dy = 1;

				////const checkboxActiveState = checkbox.states.create("active");
				//checkboxActiveState.properties.opacity = 0;


			});


			// end am4core.ready()
		},
	}

</script>

<style scoped>
	#chartdiv {
		width: 50%;
		height: 300px;
	}
</style>