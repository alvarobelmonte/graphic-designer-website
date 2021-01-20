<template>
  <div :class="['xs-text-6 md-text-5 bael-grid']">
    <div v-if="posts.length" class="r full-height browse">
      <div
        v-intersect
        v-for="(p,i) in posts"
        :key="i"
        class="xs-border xs-border-top-none xs-border-left-none xs-p2 bcg-item"
        :style="`transition-delay:0.${i * .5}s`"
      >
        <div class="item xs-block xs-full-height xs-flex">
          <nuxt-link
            class=""
            :to="p.path"
          >
          <img class="flex-align-center flex-justify-center " :src="p.thumbnail" alt="">
          </nuxt-link>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  props: {
    posts: {
      type: Array,
    },
  },
  data() {
    return {};
  },
  computed: {
    hasPagination() {
      return this.$store.state.pagination.active || false;
    },
  },
};
</script>

<style>
.bael-grid .bcg-item {
  opacity: 0;
  transition: 0.2s opacity ease-out;
}
.bael-grid .intersected.bcg-item {
  opacity: 1;
  transition: 0.2s opacity ease-out;
}
</style>
