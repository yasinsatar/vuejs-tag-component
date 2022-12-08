<template>
  <span class="tag" >
      <span class="content">{{ tag }}</span>
      <span class="close" @click="$emit('selectedRemoveTagEvent', index)">X</span>
    </span>
</template>
<script>
export default{
 props: ["tag","index"],
methods:{
  
}
}
</script>
<style scoped>
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

</style>