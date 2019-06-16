<template>
<div>
    <select @change="onSelectedValue">
      <option v-for="(item,index) in itemSource" 
              :key="item" 
              :value="index" 
              :selected="index==value">
              <span>{{item}}</span>
      </option>
    </select>
  <!-- <span>Hello world</span> -->
</div>
</template>


<script>

let onSelectedValue= function(eventArgs){
  this.$emit("input", this.category, eventArgs.target.value);
}

export default {
  name: "ComboBox",
  props : ["category", "itemSource"],
  methods : {
    onSelectedValue
  }
}

</script>

<style scoped>

</style>

