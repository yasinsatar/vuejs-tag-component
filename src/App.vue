<template>
 <div class="containter">
    <app-tags v-model="tags"  @changeTagsEvent="(tags=$event)"></app-tags>
    <div class="tags">
    {{tags}}
  </div>
 </div>
</template>
<script>
import Tags from "./components/Tags"
export default {
  components:{
 appTags: Tags
  },
  data(){
    return{
      tags:"aaa,ddd",
    }
  },
  methods:{
 
  }
}
</script>
<style>
body {
  font-family: sans-serif;
}
</style>