<template>
  <ul class="result-panel">
    <li v-for="(list, listIndex) in inputLists" :key="listIndex" class="single-list">
      <h2>{{list.title}}</h2>
      <div v-for="item in inputLists[listIndex].innerList" :key="item.name">
          <div v-if="item.isChecked" class="squares-container">
            <template v-for="(square,squareIndex) in +item.count" :key="squareIndex">
              <div  @click="deleteSquare(item)" :style="{backgroundColor: item.color}" class="color-square" ></div>
            </template>
          </div>  
      </div>
    </li>
  </ul>
</template>
<script>
export default {
  props: {
    inputLists: {
      type: Object,
      default: {}
    },
  },
  methods: {
      deleteSquare (item) {
        this.$emit('deleteSquare', item)
      }
    },
};
</script>
<style scoped>
 .result-panel {
  width: 45%;
  padding: 20px;
  border: 2px solid rgb(17, 17, 17);
 }

 .single-list {
   margin-bottom: 15px;
   padding: 10px;
   border: 2px solid rgb(17, 17, 17);
 }

 .squares-container {
   display: flex;
   flex-wrap: wrap;
   margin-bottom: 10px;
 }

  .color-square {
    margin-right: 5px;
    margin-bottom: 5px;
  }
</style>