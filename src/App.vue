<template>
  <LayoutHeader />
  <LayoutContent />
  <LayoutFooter />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import LayoutHeader from "./components/LayoutHeader.vue";
import LayoutContent from "./components/LayoutContent.vue";
import LayoutFooter from "./components/LayoutFooter.vue";

export default defineComponent({
  name: "App",
  components: {
    LayoutHeader,
    LayoutContent,
    LayoutFooter,
  },
});
</script>

<style lang="scss">
@import "~@/assets/scss/reset.scss";
@import "~@/assets/scss/common.scss";
</style>
