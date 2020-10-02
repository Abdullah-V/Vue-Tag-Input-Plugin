<template>


<span class="tag">
  <span class="content">{{ text }}</span>
  <span class="close" @click="sendIndex(index)"><b> x</b></span>
</span>



</template>

<script>
export default {
  props:{
    text:{
      required:true,
    },
    index:{
      required:true
    }
  },
  methods:{
    sendIndex(i){
      this.$emit('deleteIndex',i)
    }
  }
}
</script>



<style>

.tag{
  background-color: orange;
  padding: 15px;
  font-size: 17px;
  margin: 5px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  cursor:default;
}

.tag .close{
  font-size: 19px;
  cursor: pointer;
}



</style>
