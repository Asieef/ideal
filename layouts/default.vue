<template>
  <div>
    <Navbar />
    <Breadcrump v-if="checkRoute" />
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
