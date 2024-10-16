<script>
import Pokemon from "./pages/Pokemon.vue";
export default {
  components: {
    Pokemon,
  },
  data() {
    return {};
  },
  mounted() {
    this.$nextTick(() => {
      this.setScrollbarHeight();
      window.addEventListener("resize", this.setScrollbarHeight);
    });
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.setScrollbarHeight);
  },
  methods: {
    setScrollbarHeight() {
      const customScrollbar = this.$refs.customScrollbar;
      customScrollbar.style.maxHeight = "100vh"; // Set max-height to 100% of viewport height
    },
  },
};
</script>

<template>
  <section ref="customScrollbar" class="custom-scrollbar">
    <Pokemon />
  </section>
</template>
