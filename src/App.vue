<template>
    <div id="app">
        <div class="office">
            <Map
                :selectedLegendItemIndex="selectedLegendItemIndex"
                :isUserOpenned="isUserOpenned"
                @table-selected="onTableSelect"
            />
            <SideMenu
                :isUserOpenned.sync="isUserOpenned"
                :person="selectedPerson"
                @legend:item-hover="selectedLegendItemIndex = $event.legendIndex"
            />
        </div>
    </div>
</template>

<script>
import Map from "./components/Map.vue";
import SideMenu from "./components/SideMenu.vue";
import people from "@/assets/data/people.json";

export default {
  components: {
    Map,
    SideMenu,
  },
  data() {
    return {
      isUserOpenned: false,
      selectedPerson: null,
      selectedLegendItemIndex: -1,
    }
  },
  methods: {
    onTableSelect(tableId) {
      if(tableId === null) {
        this.isUserOpenned = false;
        this.selectedPerson = null;
        return;
      }

      const foundedPerson = people.find(person => person.tableId === Number(tableId));
      if(foundedPerson) {
        this.isUserOpenned = true;
        this.selectedPerson = foundedPerson;
      }
    }
  },
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    color: #2c3e50;
    background-color: #fafafa;
    padding: 24px;
    box-sizing: border-box;
}

html,
body,
#app {
    height: 100%;
}

* {
    box-sizing: border-box;
}

h3 {
    margin-top: 0px;
}

.office {
    display: grid;
    grid-template-columns: 1fr 320px;
    border-radius: 6px;
    border: 1px solid #ccd8e4;
    height: 100%;
    background: white;
    max-width: 1500px;
    margin: 0 auto;
}
</style>
