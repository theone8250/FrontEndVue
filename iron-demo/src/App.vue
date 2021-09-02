<template>
  <div id="app">
    <DisplayNumbers />
    <AddNumbers />
  </div>
</template>

<script>
import AddNumbers from "./components/AddNumbers.vue";
import DisplayNumbers from "./components/DisplayNumbers.vue";

export default {
  name: "App",
  components: {
    AddNumbers,
    DisplayNumbers,
  },
};
</script>