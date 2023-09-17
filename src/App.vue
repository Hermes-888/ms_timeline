<template>
  <div id="app" class="noselect">
    <div class="instructions">Select an item to view details</div>
    <div class="selected-date"
      v-show="selectedItem.itemUniqueKey"
    >
      <div v-text="selectedItem.itemUniqueKey"></div>
      <div v-text="selectedItem.date"></div>
    </div>
    
    <vue-horizontal-timeline 
      :items="items"
      :titleClass="'noselect'"
      :contentClass="'noselect'"
      @click="selected"
    />
    <content-panel
      :itemContent="itemContent"
    />
  </div>
</template>

<script>
/**
 * MS Timeline
 * load data from external file?
 * click to view itemSelected: data, images, links, pdf
 * in a panel below the timeline
 * https://github.com/guastallaigor/vue-horizontal-timeline
 * 
 * moved to /components to use content v-html
 * ToDo: fetch items from external data.json file
 *      add a scrollable panel below timeline for content
 */
// import VueHorizontalTimeline from "vue-horizontal-timeline";
import VueHorizontalTimeline from "./components/VueHorizontalTimeline.vue";
import ContentPanel from "./components/ContentPanel.vue";

export default {
  name: 'App',
  components: {
    VueHorizontalTimeline,
    ContentPanel
  },
  data() {
    return {
      debug: true,
      uniqueKey: '',
      selectedItem: {},
      itemContent: '',// url, String or stringified json?
      items: [
        {
          itemUniqueKey: '1',
          title: "Title example 1",
          content:
          "Lorem ipsum dolor sit amet, <b>consectetur</b> adipiscing elit.",
          isLink: false,
          date: '8/18/17',
          boxCssClass: '',
          stepCssClass: ''
        },
        {
          itemUniqueKey: '2-anything',
          title: "MRI results",
          content:
          "msData/lumbar-9-20-21.pdf",
          isLink: true,
          date: '09/20/21',
          boxCssClass: '',
          stepCssClass: ''
        },
        {
          itemUniqueKey: '3',
          title: "Title example 3",
          content:
          "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
          isLink: false,
          date: '02/10/23',
          boxCssClass: '',
          stepCssClass: ''
        },
      ]
    }
  },
  // mounted() { fetch(data.json) }
  methods: {
    selected: function(item) {
      this.uniqueKey = item.itemUniqueKey;// useful?
      let itemKey = item.itemUniqueKey;// useful?
      // reset & mark selected
      this.items.forEach(function(anItem) {
        if (anItem.itemUniqueKey === itemKey) {
          anItem.stepCssClass = 'step-green';
          anItem.boxCssClass = 'selected';
        } else {
          anItem.boxCssClass = '';
          anItem.stepCssClass = '';
        }
      });

      this.selectedItem = item;
      // if isLink, fetch html, txt, pdf content
      // else
      this.itemContent = item.content;//JSON.stringify(item.content);

      if (this.debug) {
        // console.log();
        console.log('selected', item.title, item.content, item);
      }
    }
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding: 10px;
  background-color: #f0f0f0;
}
.instructions {
  font-weight: bold;
}
.timeline {
  padding: 4em 0 !important;
}
.noselect {
  user-select: none;
}
.selected-date {
  position: absolute;
  top: 2px;
  left: 30px;
  z-index: 1;
  padding: 5px;
  text-align: left;
  font-weight: bold;
  color: #333333;
  border: 1px solid #333333;
  background-color: #ffffff;
}

.selected {
  background-color: rgb(228, 248, 250) !important;
  border-right: 2px solid #666666 !important;
  border-bottom: 2px solid #666666 !important;
  box-shadow: 5px 5px 12px rgb(10, 10, 10 / 30%) !important;
}
.step-green::after {
  background: green !important;
}

.NOTE--border-blue {
  -webkit-filter:drop-shadow(-1px 0px 0 #03a9f4) drop-shadow(1px 1px 0 #03a9f4) drop-shadow(0px -1px 0 #03a9f4);
  filter:drop-shadow(-1px 0px 0 #03a9f4) drop-shadow(1px 1px 0 #03a9f4) drop-shadow(0px -1px 0 #03a9f4);
}
</style>