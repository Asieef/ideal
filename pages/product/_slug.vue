<template>
  <div class="font-display py-4 border-t">
    <div class="container mx-auto">
      <div
        class="grid lg:grid-flow-col lg:grid-cols-2 grid-cols-1 gap-6 px-8 py-6"
      >
        <div class="col-span-1 border border-gray-200">
          <img
            :src="product.photo"
            :alt="product.name"
            style="width: 100%"
            class="scale-90 hover:scale-100 ease-in duration-300"
          />
        </div>

        <div class="col-span-1">
          <h2 class="font-bold text-2xl text-gray-700">{{ product.name }}</h2>
          <p class="text-gray-700 mt-6" v-html="product.short"></p>
          <div class="mt-8">
            <a
              :href="`https://comcitybd.com/product/${slug}`"
              class="bg-[#0095D9] text-white px-6 py-3 hover:bg-gray-700"
              target="_blank"
            >
              Buy Now
            </a>
          </div>
        </div>
      </div>
    </div>

    <div class="border font-semibold uppercase flex justify-center px-4 py-4">
      <div class="px-4">
        <button
          @click="selectTab(1)"
          :class="{ tabstate: currentTab == 1 }"
          class="tab"
        >
          Description
        </button>
      </div>

      <div class="px-4">
        <button
          @click="selectTab(2)"
          :class="{ tabstate: currentTab == 2 }"
          class="tab"
        >
          Specification
        </button>
      </div>
    </div>

    <div class="px-4 container mx-auto">
      <div v-if="currentTab == 1" class="tabpanel">
        <div class="px-4 py-6" v-html="product.details"></div>
      </div>

      <div v-if="currentTab == 2" class="tabpanel">
        <div class="px-4 py-6" v-html="product.short"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    value: String,
  },

  data() {
    return {
      product: [],
      slug: this.$route.params.slug,
      currentTab: 1,
    };
  },

  mounted() {
    this.getProduct();
    console.log(this.$route);
  },

  methods: {
    getProduct() {
      this.loading = true;
      this.$axios
        .get(`https://admindash.comcitybd.com/api/product/${this.slug}`)
        .then((response) => {
          this.loading = false;
          console.log(response.data);
          this.product = response.data;
        });
    },

    selectTab(selectedTab) {
      this.currentTab = selectedTab;
    },
  },
};
</script>

<style scoped>
.tabstate {
  border-bottom: 3px solid #0095d9;
}
</style>
