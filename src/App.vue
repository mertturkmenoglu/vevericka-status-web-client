<template>
  <div class="container">
    <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <a class="navbar-item" href="https://vevericka.herokuapp.com/">
          <img
            src="https://raw.githubusercontent.com/mertturkmenoglu/vevericka-web-client/d9f9dc18be8a868c1345b375110fdf0452bf059c/src/assets/icon_primary.svg"
            width="28"
            height="28"
          />
        </a>

        <a
          role="button"
          class="navbar-burger"
          aria-label="menu"
          aria-expanded="false"
          data-target="navbarBasicExample"
        >
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>

      <div id="navbarBasicExample" class="navbar-menu">
        <div class="navbar-start">
          <a class="navbar-item" href="https://vevericka.herokuapp.com/">
            Vevericka
          </a>

          <div class="navbar-item has-dropdown is-hoverable">
            <a class="navbar-link"> More </a>

            <div class="navbar-dropdown">
              <a class="navbar-item"> About </a>
              <a class="navbar-item"> Contact </a>
              <hr class="navbar-divider" />
              <a
                class="navbar-item"
                href="https://github.com/mertturkmenoglu/vevericka-web-client/issues"
              >
                Report an issue
              </a>
            </div>
          </div>
        </div>

        <div class="navbar-end">
          <div class="navbar-item">
            <div class="buttons">
              <a
                class="button is-dark"
                href="https://github.com/mertturkmenoglu/vevericka-web-client"
              >
                <strong>GitHub</strong>
              </a>
            </div>
          </div>
        </div>
      </div>
    </nav>

    <section class="hero is-success is-small mt-3">
      <div class="hero-body has-text-centered">
        <p class="title has-text-weight-light">Vevericka Status Service</p>
      </div>
    </section>

    <div v-if="!loading" class="mt-5">
      <div v-for="s in statuses" :key="s.name">
        <div class="container">
          <Service :service="s" class="mb-3" />
        </div>
      </div>
    </div>
    <div v-else>
      <b-loading v-model="loading" :can-cancel="false"></b-loading>
    </div>
  </div>
</template>

<script>
import Service from "@/components/Service";

export default {
  name: "App",
  components: { Service },
  data: () => ({
    URL: "https://bubbly-mantis-303320.ey.r.appspot.com/api/v1/statuses",
    statuses: [],
    loading: true,
  }),
  methods: {
    async fetchStatuses() {
      const response = await fetch(this.URL);
      const { data } = await response.json();
      this.statuses = data.statuses;
    },
  },
  mounted() {
    this.fetchStatuses().then(() => (this.loading = false));
  },
};
</script>

<style>
</style>
