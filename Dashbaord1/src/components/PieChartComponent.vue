<template>
	<div id="chartdiv"></div>
</template>

<script>
	import * as am4core from "@amcharts/amcharts4/core";
	import * as am4charts from "@amcharts/amcharts4/charts";
	import am4themes_animated from "@amcharts/amcharts4/themes/animated";

	am4core.useTheme(am4themes_animated);

	export default {
		name: 'PieChartComponent',
		mounted() {
			am4core.ready(function () {
				var chart = am4core.create("chartdiv", am4charts.PieChart);

				// Set data
				var selected;
				var types = [{
					type: "Antal skruer",
					percent: 75,
					color: chart.colors.getIndex(15)
				}, {
					type: "Antal fejl",
					percent: 25,
					color: chart.colors.getIndex(9)
				}];

				// Add data
				chart.data = generateChartData();

				// Add and configure Series
				var pieSeries = chart.series.push(new am4charts.PieSeries());
				pieSeries.dataFields.value = "percent";
				pieSeries.dataFields.category = "type";
				pieSeries.slices.template.propertyFields.fill = "color";
				pieSeries.slices.template.propertyFields.isActive = "pulled";
				pieSeries.slices.template.strokeWidth = 0;

				function generateChartData() {
					var chartData = [];
					for (var i = 0; i < types.length; i++) {
						if (i == selected) {
							for (var x = 0; x < types[i].subs.length; x++) {
								chartData.push({
									type: types[i].subs[x].type,
									percent: types[i].subs[x].percent,
									color: types[i].color,
									pulled: true
								});
							}
						} else {
							chartData.push({
								type: types[i].type,
								percent: types[i].percent,
								color: types[i].color,
								id: i
							});
						}
					}
					return chartData;
				}

				//pieSeries.slices.template.events.on("hit", function (event) {
				//	if (event.target.dataItem.dataContext.id != undefined) {
				//		selected = event.target.dataItem.dataContext.id;
				//	} else {
				//		selected = undefined;
				//	}
				//	chart.data = generateChartData();
				//});

			}); // end am4core.ready()
		}
	}
</script>

<style scoped>
	#chartdiv {
		width: 50%;
		height: 350px;
	}
</style>