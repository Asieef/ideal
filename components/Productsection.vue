<template>
  <div class="font-display py-8">
    <div class="text-center lg:text-3xl text-lg font-light">
      <h2>Products</h2>
    </div>
    <div class="container mx-auto">
      <div
        class="grid lg:grid-cols-5 grid-cols-1 gap-6 px-6 py-12 justify-items-center"
        v-if="products != null"
      >
        <div class="" v-for="product in products" :key="product.slug">
          <router-link :to="`/product/${product.slug}`">
            <img
              :src="product.thumbnail"
              alt="Casing"
              style="width: 250px"
              class="border"
            />
            <p class="text-gray-900 text-sm font-semibold py-4">
              {{ product.name }}
            </p>
          </router-link>

          <button
            class="inline-flex items-center hover:text-white hover:bg-[#0095D9] border py-1 px-3 focus:outline-none text-base mt-4 md:mt-0"
          >
            Learn More
            <svg
              fill="none"
              stroke="currentColor"
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              class="w-4 h-4 ml-1"
              viewBox="0 0 24 24"
            >
              <path d="M5 12h14M12 5l7 7-7 7"></path>
            </svg>
          </button>
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
