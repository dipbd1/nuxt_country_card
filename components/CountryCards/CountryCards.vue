<template>
  <div class="parent-flex">
    <div
      class="row no-gutters border rounded overflow-hidden flex-md-row mb-4 shadow-sm h-md-250 position-relative w-100 mx-4 flex-item"
      v-for="country in countries"
      :key="country.area"
    >
      <div class="col p-4 d-flex flex-column position-static">
        <strong class="d-inline-block mb-2 text-success">{{
          country.name.official
        }}</strong>
        <h3 class="mb-0">{{ country.name.common }}</h3>
        <div class="mb-1 text-muted" v-if="country.capital">
          {{ country.capital[0] }}
        </div>
        <p class="mb-auto"></p>
        <nuxt-link
          :to="`countries/${country.name.common}`"
          class="stretched-link"
          >Country Detail Page</nuxt-link
        >
      </div>
      <div class="col-auto d-none d-lg-block mh-80 border border-secondary">
        <!-- here we will place the flag from countries -->
        <img :src="country.flags.png" alt="flag" class="img-fluid" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CountryCards",
  data() {
    return {
      countries: [],
    };
  },
  async fetch() {
    this.countries = await this.$axios.$get(
      "https://restcountries.com/v3.1/all"
    );
  },
  components: {},
  computed: {},
  methods: {},
};
</script>

<style scoped>
*,
*::before,
*::after {
  box-sizing: border-box;
}

.parent-flex {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  /* padding: 40px calc((100% - (270px * 3)) / 2); */
}

.flex-item {
  flex: 0 0 320px;
}
</style>
