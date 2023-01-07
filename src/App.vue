<template>
  <!-- <div class="td-form"> -->
  <FormComponent @save="keep" :tdList="tdList"></FormComponent>
  <div>
    <p>You have {{ showleft }} things to do</p>
  </div>
  <!-- </div> -->

  <ul>
    <li
      v-for="(list, index) in reverseList"
      :key="list.id"
      @click="doneIt(list)"
      :class="{ line: list.checked }"
    >
      <!-- :class="{line : list.checked}" จะทำ class นั้นๆ เมื่อ list.checked เป็น true -->
      <span class="index">{{ index + 1 }} .</span> {{ list.text }}
      <div v-if="list.checked" class="btn">
        <button @click="remove(list)">Delete</button>
      </div>
    </li>
  </ul>
</template>

<script>
import FormComponent from "./components/FormComponent.vue";
export default {
  name: "app",
  data() {
    return {
      tdList: [],
    };
  },
  components: {
    FormComponent,
  },
  methods: {
    keep(list) {
      this.tdList.push(list);
    },
    doneIt(list) {
      list.checked = !list.checked;
    },
    remove(list) {
      this.tdList = this.tdList.filter((item) => {
        return item.id !== list.id;
      });
    },
  },
  computed: {
    reverseList() {
      return [...this.tdList].reverse();
    },
    showleft() {
      return this.tdList.length;
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Slabo+27px&display=swap');
* {
  box-sizing: border-box;
}
body {
  margin: 0;
  text-align: center;
  font-family: 'Slabo 27px', serif;
  background-color: aquamarine;
}
.line {
  text-decoration: line-through;
}
ul li {
  font-size: 1.5rem;
  cursor: pointer;
  margin-bottom: 0.5rem;
  width: fit-content;
  margin-left: 37%;
}
ul {
  list-style-type: none;
  padding: 0;
  margin-top: 2rem;
}
.index {
  margin-right: 0.5rem;
}
.btn{
  text-align: end ;
}
</style>
