<template>
  <div>
    <div class="tag-selected-container">
      <div
        class="selected-tag tag"
        v-for="selectedTag in selectedTags"
        :key="selectedTag.id"
      >
        {{ selectedTag.name }}
        <img class="croix" src="../image/croix.svg" @click="deleteTag(selectedTag.id)"/>
      </div>
    </div>
    <div class="tag-container">
      <div
        class="tag"
        v-for="tag in unselectedTags"
        :key="tag._id"
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
  computed: {
    unselectedTags() {
      return this.tags.filter(t => this.value.indexOf(t._id) === -1);
    },
    selectedTags() {
      let array = [];
      this.value.map(v =>
        this.tags.map(t => (t._id === v ? array.push({id: t._id, name:t.name.fr}) : ""))
      );
      return array;
    }
  },
  methods: {
    addTag(id) {
      if (this.value.length < 2) {
        this.value.push(id);
      }
    },
    deleteTag(id) {
      this.value.splice(this.value.indexOf(id), 1);
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
  margin: 0.5em;
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
