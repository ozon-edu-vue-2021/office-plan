<template>
  <pie-chart ref="chart" />
</template>

<script>
import { Doughnut as PieChart } from "vue-chartjs";

export default {
  components: {
    PieChart,
  },
  props: {
    data: {
      type: Object,
      default: null,
    },
  },
  data: function () {
    return {
      currentHoverItemIndex: -1,
    };
  },
  watch: {
    data: {
      // immediate: true,
      handler: function (data) {
        this.drawChart(data);
      },
    },
  },
  mounted() {
    this.drawChart(this.data);
  },
  methods: {
    drawChart(data) {
      this.$refs["chart"].renderChart(data, {
        borderWidth: "10px",
        legend: {
          display: false,
        },
        hover: {
          mode: "nearest",
          intersect: false,
          onHover: (e, item) => {
            if (typeof item[0]?._index !== "number") {
              this.currentHoverItemIndex = -1;

              this.$emit("slice:hover", {
                index: this.currentHoverItemIndex,
              });
            } else if (item[0]?._index !== this.currentHoverItemIndex) {
              this.currentHoverItemIndex = item[0]._index;

              this.$emit("slice:hover", {
                index: this.currentHoverItemIndex,
              });
            }
          },
        },
      });
    },
  },
};
</script>
