<template>
  <div id="app">
    <node v-bind:level="'1'"></node>
  </div>
</template>

<script>
import Node from "./components/Node.vue";

export default {
  name: "App",
  components: {
    Node,
  },
};
</script>

<style>
* {
  font-family: monospace;
  font-size: 24px;
}
a {
  font-size: 16px;
  text-decoration: none;
}
</style>
