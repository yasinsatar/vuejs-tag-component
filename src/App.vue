<template>
  <div class="containter">
    <app-tags v-model="tags" @changeTagsEvent="tags = $event" color="info"></app-tags>
    <div class="tags">
      {{ tags }}
    </div>
  </div>
</template>
<script>
import Tags from "./components/Tags"
export default {
  components: {
    appTags: Tags
  },
  data() {
    return {
      tags: "masa,mobilya,kitaplık",
    }
  },
  methods: {

  }
}
</script>
<style>
body {
  font-family: sans-serif;
}

.tags {
  word-break: break-word;
}
</style>