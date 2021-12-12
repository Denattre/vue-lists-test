<template>
  <ul class="lists">
    <li v-for="(currentList, listIndex) in lists" :key="listIndex">
      <div class="title-container">
        <svg
          :class="{open: !currentList.isHide}"
          fill="none"
          stroke="currentColor"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 16 10"
          aria-hidden="true"
        >
          <path
            d="M15 1.2l-7 7-7-7"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
        <input :id="currentList.title" 
          :class="{dotCheckbox: lists[listIndex].innerList.some(item => item.isChecked) && !lists[listIndex].innerList.every(item => item.isChecked)}" 
          type="checkbox" 
          @change="selectAll(currentList, $event)" 
          :checked="lists[listIndex].innerList.some(item => item.isChecked)">

        <label :for="currentList.title" 
          :class="{checkboxLabel: lists[listIndex].innerList.some(item => item.isChecked)&& !lists[listIndex].innerList.every(item => item.isChecked)}"
          ></label>
        <h2 @click="changeAccordion(currentList)">{{ currentList.title }}</h2>
      </div>
      <ul
        class="accordion"
        :class="{ 'accordion-active': !currentList.isHide }"
      >
        <li v-for="item in lists[listIndex].innerList" :key="item.name" class="list-content">
          <div>
            <p>{{ item.name }}</p>
            <input type="checkbox" v-model="item.isChecked" @change="updateLists"/>
            <input type="number" min="0" v-model="item.count" @input="updateLists; numberValid($event)"  />
            <input type="color" v-model="item.color" @change="updateLists"/>
          </div>
          <div class="display-content">
            <div class="display-content__count">{{ item.count }}</div>
            <div class="color-square" :style="{ backgroundColor: item.color }"></div>
          </div>
        </li>
      </ul>
    </li>
  </ul>
</template>
<script>
export default {
  data() {
    return {
      isHide: true,
      lists: [
        {
          title: "List 1",
          isHide: true,
          innerList: [
            { name: "Item 1", color: "#000000", count: 0, isChecked: false },

            { name: "Item 2", color: "#000000", count: 0, isChecked: false },

            { name: "Item 3", color: "#000000", count: 0, isChecked: false },

            { name: "Item 4", color: "#000000", count: 0, isChecked: false },
          ],
        },
        {
          title: "List 2",
          isHide: true,
          innerList: [
            { name: "Item 1", color: "#000000", count: 0, isChecked: false },

            { name: "Item 2", color: "#000000", count: 0, isChecked: false },

            { name: "Item 3", color: "#000000", count: 0, isChecked: false },

            { name: "Item 4", color: "#000000", count: 0, isChecked: false },

            { name: "Item 5", color: "#000000", count: 0, isChecked: false },
          ],
        },
        {
          title: "List 3",
          isHide: true,
          innerList: [
            { name: "Item 1", color: "#000000", count: 0, isChecked: false },

            { name: "Item 2", color: "#000000", count: 0, isChecked: false },

            { name: "Item 3", color: "#000000", count: 0, isChecked: false },

            { name: "Item 4", color: "#000000", count: 0, isChecked: false },

            { name: "Item 5", color: "#000000", count: 0, isChecked: false },

            { name: "item 6", color: "#000000", count: 0, isChecked: false },
          ],
        },
      ],
    };
  },
  methods: {
    changeAccordion(list) {
      list.isHide = !list.isHide
    },

    updateLists () {
      this.$emit('updateLists', this.lists)
    },

    numberValid (event) {
      var numberPattern = /^[^\s()-]*$/;
      event.target.value = event.target.value.match(numberPattern)
    },

    selectAll(list, event) {
        let titleIsChecked = list.innerList.some(item => item.isChecked)
        list.innerList.map(item => {
          if (titleIsChecked) item.isChecked = false
          else item.isChecked = true
        })
    },
  },
  
};
</script>
<style>
ul {
  list-style: none;
}

h2 {
  cursor: pointer;
}

input {
  margin-right: 5px;
}

svg {
  width: 10px;
  transform: rotate(-90deg);
  transition: transform ease .3s;
}

.open {
  transform: rotate(0);
}

.title-container {
  display: flex;
  align-items: center;
}

.dotCheckbox {
  position: absolute;
  z-index: -1;
  opacity: 0;
}

.dotCheckbox + .checkboxLabel::before {
  content: '';
  display: inline-block;
  width: 11px;
  height: 11px;
  border: 1px solid black;
  margin-right: 8px;
  background-repeat: no-repeat;
  background-position: center center;
  border-radius: 3px;
  transform: translate(4px, 2px);
}
.dotCheckbox:checked + .checkboxLabel::before {
  background-image: url('../assets/dot.svg');
  background-size: 7px 7px;
}

.lists {
  width: 45%;
  padding-right: 20px;
  padding-bottom: 20px;
  margin-right: 15px;
  border: 2px solid rgb(17, 17, 17);
  
}

.list-content {
  display: flex;
  justify-content: space-between;
}

.display-content {
  display: flex;
  align-self: end;
}

.display-content__count {
  margin-right: 5px;
}

.color-square {
  width: 20px;
  height: 20px;
}


.accordion {
  overflow: hidden;
  max-height: 0;
  transition: max-height ease .3s;
}

.accordion-active {
   overflow: hidden;
   max-height: 1000px;
  transform: translateY(0);
}
</style>