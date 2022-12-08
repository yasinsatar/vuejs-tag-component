<template>
    <div class="tag-container" @click="focused">
     <Tag 
     v-for="(tag,index) in tags"
     :tag="tag"
     :index="index"
     @selectedRemoveTagEvent="selectedRemoveTag($event)"
      />
    <input 
    type="text" 
    @keydown.enter="addTag"
    @keydown.backspace="removeTag"
    >
    <div class="error" v-show="error">Bu etiket daha önceden eklenmiştir!</div>

  </div>
</template>

<script>
import Tag from "./Tag.vue"
export default {
  components:{
    Tag 
  },
  props: {
    value: {
      required: false,
    }
  },
  data() {
    return {
      tags: [],
      error: false,
    }
  },
  created(){
   if(this.value){
    if(this.value.length>0){
      this.tags= this.value.split(",");
    }
   }
  },
  methods: {
    addTag(event) {
      let input = event.target;
      let text = input.value.trim();
      let matchedTag = false;
      if (text.length > 0) {
        this.tags.forEach(tag => {
          if (tag.toLowerCase() === text.toLowerCase()) {
            matchedTag = true;
            return false;
          }
        });

        if (!matchedTag) {
          this.tags.push(text);
        } else {
          this.error = true;
          setTimeout(() => {
            this.error = false;
          }, 2000)
        }
      }
      input.value = "";
    },
    removeTag(e){
      if(e.target.value.trim().length<=0){
        this.tags.splice(this.tags.length -1,1);
      }   
    },
    selectedRemoveTag(index){
      this.tags.splice(index,1);
    },
    focused(){
      document.querySelector('input[type="text"]').focus();
    }
  },
  watch:{
    tags:function(value){
      this.$emit("changeTagsEvent", value.join(","));
    
    }
  }
}
</script>
<style scoped>
.tag-container {
  border: 1px solid #ccc;
  padding: 20px;
}


input {
  outline: none;
  height: 30px;
  border:none;
}

.error {
  font-size: 12px;
  color: red;
  margin-top: 5px;
}
</style>