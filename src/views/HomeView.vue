<template>
  <main v-if="!loading" class="text-black">
    <DataTitle :text="title" :dataNumber="dataNumber" />
    <FileSelector :files="stats" />
  </main>
  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-grey-500 text-3xl mt-10 mb-6">Fecthing Data</div>
    <img :src="loadingImage" class="w-24 m-auto" alt="" />
  </main>
</template>

<script>
// @ is an alias to /src
import DataTitle from "@/components/DataTitle";
import FileSelector from "@/components/FileSelector";

export default {
  name: "HomeView",
  components: {
    DataTitle,
    FileSelector,
  },
  data() {
    return {
      loading: true,
      title: "Files Number :",
      dataNumber: "",
      stats: {},
      loadingImage: require("../assets/loading.gif"),
    };
  },
  methods: {
    async fetchFbiData() {
      const res = await fetch("https://api.fbi.gov/wanted/v1/list");
      // const res = await fetch("https://catfact.ninja/fact");
      const data = await res.json();
      return data;
    },
  },
  async created() {
    const data = await this.fetchFbiData();
    console.log(data);
    console.log(data.items[1].images[0].thumb);
    this.dataNumber = data.total;
    this.stats = data.items;
    this.loading = false;
  },
};
</script>
