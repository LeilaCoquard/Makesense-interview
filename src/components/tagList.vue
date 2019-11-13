<template>
  <div>
    <div class="tag-selected-container">
      <div class="selected-tag tag" v-for="id in value" :key="id">
        {{ displaySelectedTag(id) }}
        <img class="croix" src="../image/croix.svg" />
      </div>
    </div>

    <div class="tag-container">
      <div
        class="tag"
        v-for="tag in tags"
        :key="tag.id"
        @click="addTag(tag._id)"
      >
        <p>{{ tag.name.fr }}</p>
        <img class="plus" src="../image/plus.svg" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "tagList",
  props: ["label", "maxSelected", "tags", "value"],
  methods: {
    displaySelectedTag(id) {
      return this.tags.find(tag => tag._id === id).name.fr;
    },
    addTag(id) {
      this.value.push(id);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.tag-selected-container {
  display: flex;
  flex-wrap: wrap;
}
.tag {
  border: 2px solid #979797;
  border-radius: 1.6em;
  padding: 0.8em 1.5em;
  padding-right: 2em;
  display: flex;
}
.selected-tag {
  background: #fabe3c;
  border-color: #fabe3c;
}
.tag-container {
  border: 2px dashed #e8e8e8;
  border-radius: 6px;
  padding: 1.25em;
  display: flex;
  flex-wrap: wrap;
  margin-top: 1em;
}
p {
  margin: 0;
}
.plus,
.croix {
  margin: 0.2em;
}
</style>
