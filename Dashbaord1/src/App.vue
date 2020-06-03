<template>
    <div id="app">
        <Home msg="Hello world!" />
        <!--<HistogramChartComponent></HistogramChartComponent>-->
        <!--<LineChartComponent></LineChartComponent>-->
        <!--<PieChartComponent></PieChartComponent>-->
        <GaugeChartComponent></GaugeChartComponent>
    </div>
</template>

<script>
	import Home from './components/Home.vue';
	import LineChartComponent from './components/LineChartComponent.vue'; 
	import HistogramChartComponent from './components/HistogramChartComponent.vue';
	import PieChartComponent from './components/PieChartComponent.vue';
	import GaugeChartComponent from './components/GaugeChartComponent.vue';


    export default {
        name: 'app',
        components: {
			Home,
			LineChartComponent,
			HistogramChartComponent,
			PieChartComponent,
            GaugeChartComponent
        }
    };
</script>

<style>
</style>

