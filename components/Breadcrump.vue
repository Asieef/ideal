<template>
  <div class="font-display container mx-auto">
    <div class="ml-10 py-2">
      <nav aria-label="Breadcrumb">
        <ol
          role="list"
          class="flex items-center space-x-1 text-sm text-gray-500"
        >
          <li>
            <nuxt-link
              to="/"
              class="block transition-colors hover:text-gray-700"
            >
              Home
            </nuxt-link>
          </li>
          <template v-for="crumb in crumbs">
            <li>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="w-4 h-4"
                viewBox="0 0 20 20"
                fill="currentColor"
              >
                <path
                  fill-rule="evenodd"
                  d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
                  clip-rule="evenodd"
                />
              </svg>
            </li>

            <li>
              <nuxt-link
                :to="crumb.title"
                class="block transition-colors hover:text-gray-700 capitalize"
              >
                {{ crumb.path && title !== null ? title : crumb.title }}
              </nuxt-link>
            </li>
          </template>
        </ol>
      </nav>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: null,
    },
  },

  computed: {
    crumbs() {
      const fullPath = this.$route.fullPath;
      const params = fullPath.startsWith("/")
        ? fullPath.substring(1).split("/")
        : fullPath.split("/");
      const crumbs = [];

      let path = "";

      params.forEach((param, index) => {
        path = `${path}/${param}`;
        const match = this.$router.match(path);

        if (match.name !== null) {
          crumbs.push({
            title: param.replace(/-/g, " "),
            ...match,
          });
        }
      });

      return crumbs;
    },
  },
};
</script>
