<template>
  <div>
    <h1>{{ title }}</h1>
    <GChart type="ScatterChart" @ready="onChartReady"/>
    <div id="chart"></div>
  </div>
</template>

<script>
import { GChart } from "vue-google-charts";
import { log } from "util";

export default {
  name: "Chart",
  props: {
    title: String
  },
  data() {
    return {
      chartOptions: {
        height: 640,
        width: 1024,
        series: {
          0: { axis: 'y-l' },
          1: { axis: 'y-r' }
        },
        chart: {
          title: "Exploring the Publication Set",
          subtitle: "data & geo cluster"
        },
        axes: {
          x: {"x": {label: "Politics"}},
          y: {
            "y-l": { label: "Research method" },
            "y-r": { label: "Matter" }
          }
        },
        // group by x value
        aggregationTarget: 'category',
      }
    };
  },
  methods: {
    onChartReady(chart, google) {
      // request our data
      fetch("data.json")
        .then(data => data.json())
        .then(data => {
          console.table(data);
          let that = this;
          this.$data.fetchedData = data;
          google.charts.load("current", { packages: ["scatter"] });
          google.charts.setOnLoadCallback(function() {
            that.initializeDataTable(data);
          });
        });
    },
    initializeDataTable(data) {
      let dataTable = new google.visualization.DataTable();
      let columns = [
        "Politics",
        "Method",
        "Subject",
        "Matter",
        "Cluster 1",
        "Cluster 2",
        "Cluster 3",
        "Connectivity",
        "Disconnectiviry",
        "Country 1",
        "Country 2",
        "Country 3",
        "Country 4",
        "Country 5",
        "Country 6",
        "Country 7",
        "Country 8",
        "Country 9",
        "Country 10",
        "Country 11",
        "Country 12"
      ];

      // TODO: Map country codes from ISO 3166-1 numeric to string

      columns.forEach(column => {
        dataTable.addColumn("number", column);
      });

      dataTable.addRows(data);

      let chart = new google.charts.Scatter(document.getElementById("chart"));

      chart.draw(
        dataTable,
        google.charts.Scatter.convertOptions(this.$data.chartOptions)
      );
    }
  },
  components: {
    GChart
  }
};
</script>

<style>
#chart > div:first-child {
  margin: 0 auto;
}
/* hide no-columns-error from empty initializer chart */
[id^="google-visualization-errors"] {
  display: none;
}
</style>
