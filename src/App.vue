<template>
  <div id="app">
    <as-input v-model="myInput"></as-input>
  </div>
</template>

<script>
import AsInput from "./components/AsInput.vue";

export default {
  name: "App",
  data() {
    return {
      myInput: ''
    }
  },
  components: {
    AsInput,
  },
};
</script>

<style></style>
