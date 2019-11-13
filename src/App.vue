<template>
  <div id="app">
    <div class="label">Tags</div>
    <div class="description" v-if="selectedTags.length === 0">
      Sélectionne 2 tags dans la liste
    </div>
    <div class="description" v-if="selectedTags.length === 1">
      Sélectionne encore 1 tag dans la liste
    </div>
    <div class="description" v-else>
      Vous devez enlever un tag sélectionné pour en choisir un autre
    </div>
    <tagList
      label="tags"
      maxSelected="2"
      :tags="listFromApi"
      v-model="selectedTags"
    />
  </div>
</template>

<script>
import tagList from "./components/tagList.vue";
import axios from "axios";

export default {
  name: "app",
  data() {
    return {
      listFromApi: [],
      selectedTags: ["5d41514a8f4abb59988c3245"]
    };
  },
  components: {
    tagList
  },
  mounted() {
    axios
      .get(
        "https://api.projects.makesense.org/v1/taxonomies?limit=200&sort=-createdAt&type=legalForm"
      )
      .then(response => {
        this.listFromApi = response.data.data;
      });
  }
};
</script>

<style>
@font-face {
  font-family: "Raleway";
  font-style: normal;
  font-display: swap;
  src: local("Raleway Black"), local("Raleway-Black"),
    url(https://fonts.gstatic.com/s/raleway/v14/1Ptrg8zYS_SKggPNwK4vWqhPANqczVsq4A.woff2)
      format("woff2");
  unicode-range: U+0100-024F, U+0259, U+1E00-1EFF, U+2020, U+20A0-20AB,
    U+20AD-20CF, U+2113, U+2C60-2C7F, U+A720-A7FF;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 16px;
}
.label {
  font-family: "Raleway";
  font-size: 1.25em;
  color: #0c3944;
  text-align: left;
  font-weight: 900;
}
.description {
  font-family: "Raleway";
  font-size: 16px;
  color: #0c3944;
  text-align: left;
  font-weight: 300;
}
</style>
