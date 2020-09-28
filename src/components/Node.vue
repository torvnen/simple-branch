<template>
  <div v-bind:style="{ 'margin-left': indentTotalPx }">
    <div>Noodi {{ level }}</div>
    <div v-bind:style="{ 'margin-left': indentTotalPx }">
      <!-- Children -->
      <node
        v-for="node in nodes"
        v-bind:key="node.level"
        v-bind:level="node.level"
      />
      <!-- /Children -->
    </div>
    <div>
      <a href="null" v-on:click="addNode">[Lisää]</a><br />
      <a href="null" v-if="showRemoveButton" v-on:click="removeNode"
        >[Poista]</a
      >
    </div>
  </div>
</template>

<script>
export default {
  name: "Node",
  props: {
    level: String,
  },
  data: function() {
    return {
      indentSize: 25,
      // Children of this. Initially empty.
      nodes: [],
      /* Indent level = amount of '.' characters in the level string.
       * If no '.' characters are found, default to 0 ([].length) */
      indentLevel: (this.level.match(/[.]/) || []).length,
    };
  },
  computed: {
    indentTotalPx: function() {
      return this.indentLevel * this.indentSize + "px";
    },
    showRemoveButton: function() {
      // Nothing to remove - don't show button.
      return Array.isArray(this.nodes) && this.nodes.length > 0;
    },
  },
  methods: {
    addNode: function(event) {
      // Prevent <a> from setting window location
      event.preventDefault();

      // Sanity check: nodes prop is mutable
      if (!Array.isArray(this.nodes)) {
        // Fault tolerance: begin with an empty collection if nodes is not array.
        this.nodes = [];
      }      
      this.nodes.push({
        level: this.level + "." + (this.nodes.length + 1),
      });
    },
    removeNode: function(event) {
      // Prevent <a> from setting window location
      event.preventDefault();

      // Sanity check: nodes prop is mutable
      if (Array.isArray(this.nodes)) {
        this.nodes.pop();
      } else {
        // Fault tolerance: reset the situation
        this.nodes = [];
      }
    },
  },
};
</script>
