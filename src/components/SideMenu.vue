<template>
  <div class="menu">
    <div class="toolbar">
      <div class="toolbar__header">Меню</div>
      <div class="toolbar__actions"></div>
    </div>
    <div class="content">
      <div class="legend">
        <div class="legend__data">
          <div v-if="legend.length > 0" class="legend__items">
            <draggable v-model="legend">
              <legend-item
                v-for="(item, index) in legend"
                :key="index"
                :color="item.color"
                :text="item.text"
                :counter="item.counter"
                class="legend__item"
              />
            </draggable>
          </div>
          <span v-else class="legend--empty">Список пуст</span>
        </div>
        <div class="legend__chart">
          <pie-chart ref="chart" />
        </div>
      </div>
      <div class="profile"></div>
    </div>
  </div>
</template>

<script>
import legend from "@/assets/legend.json";
import LegendItem from "./LegendItem.vue";
import Draggable from "vuedraggable";
import { Doughnut as PieChart } from "vue-chartjs";

export default {
  components: {
    LegendItem,
    Draggable,
    PieChart,
  },
  data: function () {
    return {
      legend: [],
      legendChartData: null,
    };
  },
  created() {
    this.loadLegend();
  },
  mounted() {
    this.makeChart();
  },
  methods: {
    loadLegend() {
      this.legend = legend;
    },
    makeChart() {
      this.legendChartData = {
        plugins: {
          legend: {
            display: false,
          },
        },
        labels: legend.map((it) => it.text),
        datasets: [
          {
            label: "Легенда",
            backgroundColor: legend.map((legendItem) => legendItem.color),
            data: legend.map((legendItem) => legendItem.counter),
          },
        ],
      };

      this.$refs["chart"].renderChart(this.legendChartData, {
        borderWidth: "10px",
        hoverBackgroundColor: "red",
        hoverBorderWidth: "10px",
        legend: {
          display: false,
        },
      });
    },
  },
};
</script>

<style scoped>
.menu {
  border-left: 1px solid #ccd8e4;
  padding: 24px;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

.toolbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  display: none;
}

.toolbar .toolbar__actions button {
  font-size: 0.76rem;
  text-transform: uppercase;
  letter-spacing: 0.08rem;
  padding: 2px 6px;
}

.content {
  flex: 1;
}

.content .legend {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
}

.content .legend .legend__data {
  display: flex;
  height: 100%;
}

.content .legend .legend__items {
  flex: 1;
  width: 100%;
}

.content .legend .legend__items .legend__item:not(:first-child) {
  margin-top: 16px;
}

.content .legend .legend__items .legend__item {
  cursor: pointer;
}

.content .legend .legend__items .legend__item.sortable-chosen {
  opacity: 25%;
}

.content .legend .legend--empty {
  align-self: center;
  width: 100%;
  text-align: center;
}
</style>
