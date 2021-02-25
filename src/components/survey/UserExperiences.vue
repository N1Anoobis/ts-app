<template>
  <section>
    <base-card>
      <h2>Submitted Experiences</h2>
      <div>
        <base-button @click.native="loadExpieriences"
          >Load Submitted Experiences</base-button
        >
      </div>
      <p v-if="isLoading">Loading...</p>
      <p v-else-if="!isLoading && !results">Add some reviews</p>
      <ul v-else-if="!isLoading && results">
        <survey-result
          v-for="result in results"
          :key="result.id"
          :name="result.name"
          :rating="result.rating"
        ></survey-result>
      </ul>
    </base-card>
  </section>
</template>

<script>
import SurveyResult from "./SurveyResult.vue";
import axios from "axios";
export default {
  // props: ['results'],
  components: {
    SurveyResult,
  },
  data() {
    return {
      results: [],
      isLoading: false,
    };
  },
  methods: {
    loadExpieriences() {
      this.isLoading = true;
      axios
        .get(
          "https://vue-app-b4ba8-default-rtdb.europe-west1.firebasedatabase.app/.json"
        )
        .then((res) => {
          this.isLoading = false;
          const data = res.data;
          console.log(res.data);
          const result = [];
          // for (const id in data) {
          //   result.push({
          //     id: id,
          //     name: data[id].name,
          //     rating: data[id].rating,
          //   });
          // }
          // console.log(data);
          this.results = res.data;
        });
    },
  },
  mounted() {
    this.loadExpieriences();
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
