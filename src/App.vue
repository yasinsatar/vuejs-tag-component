<template>
 <div class="containter">
  <div class="tag-container">
    <span class="tag" v-for="(tag,index) in tags">
      <span class="content">{{ tag }}</span>
      <span class="close" @click="selectedRemoveTag(index)">X</span>
    </span>
    <input 
    type="text" 
    @keydown.enter="addTag"
    @keydown.backspace="removeTag"
    >
    <div class="error" v-show="error">Bu etiket daha önceden eklenmiştir!</div>
  
  </div>
  <div class="tags">
    {{tags.join(",")}}
  </div>
 </div>
</template>
<script>
export default {
  data() {
    return {
      tags: [],
      error: false,
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
    }
  }
}
</script>
<style>
body {
  font-family: sans-serif;
}

.tag-container {
  border: 1px solid #ccc;
  padding: 20px;
}

.tag {
  background-color: #fbbd08;
  padding: 10px;
  cursor: default;
  font-size: 14px;
  margin-right: 10px;
  margin-bottom: 10px;
}

.tag .close {
  font-size: 12px;
  cursor: pointer;
}

input {
  outline: none;
  height: 30px;

}

.error {
  font-size: 12px;
  color: red;
  margin-top: 5px;
}
</style>