<template>
  <div>
    <Navbar />
    <div class="hidden lg:block">
      <Breadcrump v-if="checkRoute" />
    </div>
    <Nuxt />
    <Footer />
  </div>
</template>

<script>
export default {
  computed: {
    checkRoute() {
      return this.$route.name !== "index";
    },
  },
};
</script>
