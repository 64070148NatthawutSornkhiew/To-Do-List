<template>
  <form @submit.prevent="saveData">
    <div>
      <h1>To Do List App</h1>
      <input type="text" v-model="text" />
      <button :disabled="text.length < 1">Add to list</button>
    </div>
  </form>
</template>
<script>
let cnt = 0;
export default {
  name: "FormInput",
  data() {
    return {
      text: "",
    };
  },
  props: ["tdList"],
  methods: {
    saveData() {
      const newData = {
        id: cnt++,
        text: this.text,
        checked: false,
      };
      this.$emit("save", newData);
      this.resetData();
    },
    resetData() {
      this.text = "";
    },
  },
};
</script>

<style scoped>
input{
    width: 20%;
  }
  button{
    margin: 0 0 0 0.5rem;
    
  }
</style>
