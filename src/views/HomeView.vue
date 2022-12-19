<template>
  <main v-if="!loading">showData</main>
  <main
    class="flex flex-col align-center justify-center text-center"
    v-else="loading"
  >
    <div class="text-gray-500 text-3xl mt-10 mb-6">Fetching Data</div>
    <img :src="loadingImg" class="w-24 m-auto" alt="" />
  </main>
</template>

<script>
export default {
  name: "HomeView",
  components: {},
  data() {
    return {
      loading: true,
      title: "Global",
      dataData: "",
      stats: {},
      countries: [],
      loadingImg: require("../assets/hourglass.gif"),
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();
      return data;
    },
  },
  async created() {
    const data = await this.fetchCovidData();

    this.dataData = data.Date;
    this.stats = data.Global;
    this.countries = data.countries;
    this.loading = false;
  },
};
</script>
