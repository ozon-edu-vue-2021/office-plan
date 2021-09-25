<template>
  <div class="menu">
    <div class="toolbar">
      <div class="toolbar__header">Меню</div>
      <div class="toolbar__actions"></div>
    </div>
    <div class="content">
      <div class="legend">
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
      <div class="profile"></div>
    </div>
  </div>
</template>

<script>
import LegendItem from "./LegendItem.vue";
import Draggable from "vuedraggable";
import legend from "@/assets/legend.json";

export default {
  components: {
    LegendItem,
    Draggable,
  },
  data: function () {
    return {
      legend: [],
    };
  },
  created() {
    this.loadLegend();
  },
  methods: {
    loadLegend() {
      this.legend = legend;
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
