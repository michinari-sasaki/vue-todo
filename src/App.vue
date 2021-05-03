<template>
  <LayoutContent />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import LayoutContent from "./components/LayoutContent.vue";

export default defineComponent({
  name: "App",
  components: {
    LayoutContent,
  },
});
</script>

<style lang="scss">
@import "~@/assets/scss/reset.scss";
@import "~@/assets/scss/common.scss";
</style>
