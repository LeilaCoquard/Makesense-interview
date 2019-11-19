<template>
  <div id="app">
    <div class="label-description">
      <div class="label">Tags</div>
      <div class="description">
        {{ description[`${selectedTags.length}-selectedTags`][lang] }}
      </div>
    </div>
    <div class="lang-select">
      <select name="lang" v-model="lang">
        <option value="fr">Français</option>
        <option value="en">English</option>
        <option value="es">Español</option>
      </select>
    </div>
    <tagList
      label="tags"
      maxSelected="2"
      :tags="listFromApi"
      v-model="selectedTags"
      :lang="lang"
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
      description: {
        "0-selectedTags": {
          fr: "Sélectionne 2 tags dans la liste",
          en: "Select 2 tags from the list",
          es: "Seleccione 2 etiquetas de la lista"
        },
        "1-selectedTags": {
          fr: "Sélectionne encore 1 tag dans la liste",
          en: "Select one more tag from the list",
          es: "Seleccione una etiqueta más de la lista"
        },
        "2-selectedTags": {
          fr: "Vous devez enlever un tag sélectionné pour en choisir un autre",
          en: "You must remove a selected tag to choose another",
          es: "Debe eliminar una etiqueta seleccionada para elegir otra"
        }
      },
      listFromApi: [],
      selectedTags: [],
      lang: "fr"
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
        // this.setLang();
      });
  }
  // methods: {
  //   setLang() {
  //     this.listFromApi.map(r => {
  //       r.nameSelected = r.name[this.lang];
  //       r.slugSelected = r.slug[this.lang];
  //     });
  //   }
  // }
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
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  width: 60%;
}
.label-description {
  flex: 1 1;
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
.lang-select {
  border: 2px solid #e8e8e8;
  border-radius: 6px;
}
.lang-select select {
  font-family: "Raleway";
  font-weight: 600;
  font-size: 16px;
  background-color: white;
  color: #0c3944;
  border: none;
  appearance: button;
  outline: none;
  padding: 0.5em 2em 0.5em 1em;
  height: 100%;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  background: url("./image/down.svg") no-repeat calc(100% - 10px);
  cursor: pointer;
}
</style>
