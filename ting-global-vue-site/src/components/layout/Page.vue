<template>
  <div class="page">
    <TheHeader />
    <PageHeading v-if="showHeading" />
    <slot />
    <TheFooter />
  </div>
</template>

<script>
import TheHeader from "./TheHeader";
import PageHeading from "./PageHeading";
import TheFooter from "./TheFooter";

export default {
  components: { TheHeader, PageHeading, TheFooter },
  props: {
    title: String,
    name: String,
    showHeading: {
      type: Boolean,
      default: true,
    },
  },
  created() {
    document.title = this.title
      ? `${this.title} – Challenge 18`
      : "Challenge 18";
    window.scrollTo(0, 0);
  },
  provide() {
    return {
      name: this.name,
      title: this.title,
    };
  },
};
</script>

<style lang="scss">
.page {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  background-color: #fff;
  position: relative;
  z-index: 10;
}
</style>
