<template>
  <div>
    <h2>{{ storeState }}</h2>
  </div>
</template>


<script>
import { EventBus } from "../EventBus.js";
import { store } from "../store.js";

export default {
  data() {
    return {
      storeState: store.state.numbers,
    };
  },
  methods: {
    handleAddNumber() {
      EventBus.$on("addNumber", (payload) => {
        this.numbers.push(payload);
      });
    },
  },
  created() {
    this.handleAddNumber();
    console.log(store);
  },
};
</script>