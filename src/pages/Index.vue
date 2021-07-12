<template>
  <div>
    <q-input class="q-pa-xl" rounded outlined v-model="query" type="text" label="Search" />
    <SearchResult :query="query" />
  </div>
</template>

<script>
import SearchResult from "components/SearchResult.vue";

export default {
  components: {
    SearchResult,
  },
  data() {
    return {
      query: "",
    };
  },
};
</script>

<style lang="scss" scoped>
</style>