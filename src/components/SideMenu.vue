<template>
  <div class="menu">
    <div class="toolbar">
      <div class="toolbar__header">Меню</div>
      <div class="toolbar__actions"></div>
    </div>
    <div class="content">
      <div class="legend">
        <div v-if="legend.length > 0" class="legend__items">
          <legend-item
            v-for="(item, index) in legend"
            :key="index"
            :color="item.color"
            :text="item.text"
            :counter="item.counter"
            class="legend__item"
          />
        </div>
        <span v-else class="legend--empty">Список пуст</span>
      </div>
      <div class="profile"></div>
    </div>
  </div>
</template>

<script>
import LegendItem from "./LegendItem.vue";
export default {
  components: {
    LegendItem,
  },
  data: function () {
    return {
      legend: [],
    };
  },
  methods: {
    loadLegend() {
      throw new Error("Not implemented");
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
  margin-top: 24px;
  flex: 1;
}

.content .legend {
  display: flex;
  height: 100%;
}

.content .legend .legend__items {
  flex: 1;
  width: 100%;
}

.content .legend .legend__items .legend__item {
  margin-top: 12px;
}

.content .legend .legend--empty {
  align-self: center;
  width: 100%;
  text-align: center;
}
</style>
