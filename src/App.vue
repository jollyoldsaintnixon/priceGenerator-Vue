<template>
  <OuterFrame msg="Welcome to Your Vue.js App" />
</template>

<script>
import OuterFrame from "./components/OuterFrame.vue";

export default {
  name: "App",
  components: {
    OuterFrame,
  },
};
</script>

<style>
#app {
  font-family: "Open Sans";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
