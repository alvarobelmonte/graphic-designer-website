<template>
  <component :is="getLayout" :posts="posts[0]" />
</template>

<script>
import BaelGrid from "~/components/BaelGrid";
import FullGrid from "~/components/FullGrid";
import _chunk from "lodash/chunk";
export default {
  async asyncData({ $content, params, error, store }) {
    const blogPosts = await $content("blog")
      .sortBy("createdAt", "desc")
      .only(["title", "path", "thumbnail"])
      .fetch()
      .catch((err) => {
        error({ statusCode: 404, message: "Page not found" });
      });
    const chunk = _chunk(blogPosts, 12);
    if (blogPosts.length > 12) {
      store.commit("SET_PAGINATION", {
        active: true,
        page: 1,
        itemsOnPage: chunk[0].length,
        totalItems: blogPosts.length,
        totalPages: chunk.length,
      });
    } else {
      store.commit("SET_PAGINATION", {
        active: false,
        page: 1,
        itemsOnPage: blogPosts.length,
        totalItems: blogPosts.length,
        totalPages: chunk.length,
      });
    }
    return {
      posts: chunk,
      count: blogPosts.length,
    };
  },

  transition(to, from) {
    if (!from) return "fade";
    return +to.query.page > +from.query.page ? "slide-right" : "slide-left";
  },
  name: "Index",
  components: { BaelGrid, FullGrid },
  computed: {
    getLayout() {
      return this.$store.state.info.altlayout ? "FullGrid" : "BaelGrid";
    },
  },
};
</script>

<style>
</style>
