<template>
 <div id="app">
  <list-panel @update-lists="setLists"></list-panel>
  <result-panel :inputLists="lists" @delete-square="incrementCount"></result-panel>
 </div>
</template>

<script>
import ListPanel from "./components/ListPanel.vue"
import ResultPanel from "./components/ResultPanel.vue"

export default {
  components: {
    ListPanel,
    ResultPanel
  },
  data() {
    return {
      lists: [
        {title: "List 1"},
        {title: "List 2"},
        {title: "List 3"},
      ],
    }
  },
  
  methods: {
    setLists(data) {
      this.lists = data;
    },

    incrementCount(item) {
      item.count--;
    }
  }
}
</script>

<style>
  #app {
    display: flex;
    width: 100%;
  }
</style>
