<template>
  <div class="card-bg card has-text-success">
    <div class="card-content">
      <div>
        <span class="title has-text-success is-size-4 has-text-weight-light">
          {{ service.name }}
        </span>
        <span
          class="title has-text-success is-pulled-right is-size-4 has-text-weight-light"
        >
          {{ operational }}
        </span>
      </div>
      <div class="subtitle has-text-success has-text-weight-light">
        Status: {{ service.status_code }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Service",
  props: ["service"],
  data: () => ({}),
  computed: {
    operational() {
      return this.service.status_code === 200
        ? "Operational"
        : "Not Operational";
    },
  },
};
</script>

<style scoped>
.card-bg {
  background-color: rgb(255, 255, 255) !important;
}
</style>