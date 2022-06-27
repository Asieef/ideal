<template>
  <div>
    <div class="font-display">
      <div class="mt-14 mx-10">
        <div
          class="grid lg:grid-cols-4 grid-cols-1 gap-6 px-6 container mx-auto"
          v-if="products != null"
        >
          <div class="" v-for="product in products" :key="product.slug">
            <ProductPod :product="product" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [],
      category: "ups",
      cat_id: [22],
    };
  },
  mounted() {
    this.getData();
  },
  methods: {
    getData() {
      this.$axios
        .get("https://admindash.comcitybd.com/api/brand/Ideal%20UPS/6", {
          params: {
            id: this.cat_id,
          },
        })
        .then((response) => {
          console.log(response.data);
          this.products = response.data.data;
        });
    },
  },
};
</script>
