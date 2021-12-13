<template>
  <div>
    <h4>{{ country }}</h4>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  async asyncData({ params, $axios }) {
    let countries = await $axios.$get("https://restcountries.com/v3.1/all");
    let country = {
      ...countries.find((country) => country.name.common === params.slug),
    };
    return { country };
  },
};
</script>
