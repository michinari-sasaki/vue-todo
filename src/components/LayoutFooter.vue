<template>
  <footer>@ {{ copyDate }} MyToDo</footer>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "LayoutFooter",
  data: function() {
    return {
      copyDate: 0,
    };
  },
  methods: {
    getYear: function() {
      this.copyDate = new Date().getFullYear();
    },
  },
  mounted: function() {
    this.getYear();
  },
});
</script>

<style scoped lang="scss"></style>
