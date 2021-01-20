<template>
  <nav ref="navBar" :data-nav="`${pagetitle}`" id="navbar">
    <div class="r xs-border-bottom">
      <div class="c-4 xs-text-left xs-p2 sm-border-right">
        <div class="item">
          <nuxt-link class="sitename" to="/" exact>
            {{$store.state.info.sitename}}
            <span class="subtitle">gráfico</span>
          </nuxt-link>
        </div>
      </div>

      <div
        class="menu-nav c-4 xs-border-top xs-border-bottom sm-border-bottom-none sm-border-top-none sm-border-left-none sm-border-right xs-p2"
      >
        <ul class="menu-container">
          <li>
            <nuxt-link to="/bio" exact>bio</nuxt-link>
          </li>
          <li>premios</li>
          <li>cartel</li>
          <li>logos</li>
          <li>ilustración</li>
          <li>editorial</li>
          <li>calendarios</li>
          <li>contacto</li>
        </ul>
      </div>
    </div>
  </nav>
</template>
<script>
import _capitalize from "lodash/capitalize";
export default {
  data() {
    return {};
  },
  computed: {
    pagetitle() {
      return this.$store.state.current.title;
    },

    path() {
      const split = _get(this.$store, "state.current.dir").split("/");

      return split.length && split[1] !== "page" ? _capitalize(split[1]) : null;
    },
  },
};
</script>
<style lang="scss">
#navbar {
  z-index: 999;
}
.titlebar .item {
  overflow-x: none;
}
.results {
  padding-left: 0;
  transform: translateY(17px);
  width: 30vw;
}
.results li {
  list-style-type: none;
  margin-left: 0;
}
nav {
  position: fixed;
  background: rgb(29, 29, 29);
  top: 0;
  left: 0;
  right: 0;
}
.sitename {
  color: #fff;
  font-family: "Inter", sans-serif;
  text-transform: lowercase;
  font-weight: 800;
  font-size: 1.3rem;
}

.menu-nav {
  margin-top: 2%;
}
.menu-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: left;
  list-style-type: none;
  color: #fff;
  padding: 0;
}
.menu-container li {
  margin: 0.2rem;
  padding: 0rem 0.1rem;
  font-size: 0.7rem;
}
@media only screen and (max-width: 40rem) {
  .results {
    width: 94vw;
  }
}

.subtitle {
  font-family: "Sofia", cursive;
  text-transform: lowercase;
  font-weight: 100;
}
</style>