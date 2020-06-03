<template>
    <div id="app">
        <Home msg="Hello world!" />
        <HistogramChartComponent></HistogramChartComponent>
        <LineChartComponent></LineChartComponent>

    </div>
</template>

<script>
	import Home from './components/Home.vue';
	import LineChartComponent from './components/LineChartComponent.vue'; 
	import HistogramChartComponent from './components/HistogramChartComponent.vue';

    export default {
        name: 'app',
        components: {
			Home,
			LineChartComponent,
            HistogramChartComponent
        }
    };
</script>

<style>
</style>

