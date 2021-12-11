<template>
  <ul class="lists">
    <li v-for="(currentList, index) in lists" :key="index">
      <h2>List {{index + 1}}</h2>
      <ul class="hideContent accordion" :class="{'accordion-active': isHide == false}">
        <li v-for="item in currentList" :key="item.name">
          <p>{{ item.name }}</p>
          <input type="text" v-model="item.count" />
          <input type="color" v-model="item.color" />
        </li>
      </ul>
    </li>

    <!-- <li>
      <h2>List 2</h2>
      <ul class="hideContent accordion" :class="{'accordion-active': isHide == false}">
        <li v-for="item in list2" :key="item.name">
          <p>{{ item.name }}</p>
          <input type="text" v-model="item.count" />
          <input type="color" v-model="item.color" />
        </li>
      </ul>
    </li>

    <li>
      <h2>List 3</h2>
      <ul class="hideContent accordion" :class="{'accordion-active': isHide == false}">
        <li v-for="item in list3" :key="item.name">
          <p>{{ item.name }}</p>
          <input type="text" v-model="item.count" />
          <input type="color" v-model="item.color" />
        </li>
      </ul>
    </li> -->
  </ul>
</template>
<script>
export default {
  data() {
    return {
      isHide: false,

      list1: [
        { name: "Item 1", color: "", count: null },

        { name: "Item 2", color: "", count: null },

        { name: "Item 3", color: "", count: null },

        { name: "Item 4", color: "", count: null },
      ],

      list2: [
        { name: "Item 1", color: "", count: null },

        { name: "Item 2", color: "", count: null },

        { name: "Item 3", color: "", count: null },

        { name: "Item 4", color: "", count: null },

        { name: "Item 5", color: "", count: null },
      ],
      list3: [
        { name: "Item 1", color: "", count: null },

        { name: "Item 2", color: "", count: null },

        { name: "Item 3", color: "", count: null },

        { name: "Item 4", color: "", count: null },

        { name: "Item 5", color: "", count: null },

        { name: "item 6", color: "", count: null },
      ],

      lists: [this.list1, this.list2, this.list3]
    };
  },
  methods: {
    changeAccordion () {
      this.isHide = !this.isHide
    }
  },
};
</script>
<style>
ul {
  list-style: none;
}

.accordion {
  overflow: hidden;
  height: 0px;
  transition: all 1s;
}

.accordion-active {
  transition: all 1s;
  height: 100%;
}
</style>