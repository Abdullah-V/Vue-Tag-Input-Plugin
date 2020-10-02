<template>
  <div id="root">

<div id="tagContainer">
  <tag
   v-for="(tag,index) in tags"
  :key="tag.id"
  :text="tag.text"
  :index="index"
  @deleteIndex="deleteThis($event)"
  ></tag>
  <input type="text" @keydown="addToTags">
</div>

<transition name="errorAnimation">
  <b id="error" v-if="error">"{{ errorKey }}" is already exists!</b>
</transition>

<br><br>

<label style="fontSize:23px;">
<input type="checkbox" v-model="editable" @click="focus">
Editable Mode
</label>

  </div>
</template>




<script>
import tag from './components/tag.vue'

export default {
  components: {
    tag,
  },

  data(){
    return {
      nextId:3,
      tags:[
        {
          text:"Vue.js",
          id:0,
        },
        {
          text:"Node.js",
          id:1,
        },{
          text:"MongoDB",
          id:2,
        },
      ],
      editable:false,
      error:false,
      errorKey:"",
    }
  },
  methods:{
    focus(){
      document.querySelector("input").focus()
    },
    addToTags(e){
      document.querySelector("input").value = document.querySelector("input").value.substring(0,15)
      var value = document.querySelector("input").value.trim()
      var flag = true
      this.error = false
      if(e.keyCode == 13 && value != ""){
        for(var i of this.tags){
            if(i.text.toLowerCase() == value.toLowerCase()){
              flag = false
              this.error = true
              this.errorKey = value
            }
        }
        if(flag == true){
        this.error = false
        this.tags.push({
          text:value,
          id:this.nextId,
        })
        this.nextId++
        document.querySelector("input").value = ""
        console.log(this.nextId);
        this.focus()
        }
      }
      else if(e.keyCode == 8 && document.querySelector("input").value == ""){
        if(this.editable == true){
        document.querySelector("input").value = this.tags[this.tags.length-1].text
        }
        this.tags.pop()
        this.error = false
      }
    },
    deleteThis(i){
      this.error = false
      this.tags.splice(i,1)
      this.focus()
      this.error = false
    }
  },
  created(){
    setTimeout(() => {
    this.focus()
    }, 1);
  }
}
</script>



<style>
#tagContainer{
  border: 1px solid black;
  padding: 20px 5px;
  margin: 20px 0px;
  display: flex;
  flex-wrap: wrap;
}

input[type='text']{
  outline: none;
  width: 150px;
  height: 30px;
  margin-top: 15px;
}



#error{
  position: relative;
  top: 20%;
  left: 1%;
  color: red;
}


.errorAnimation-enter{}

.errorAnimation-enter-active{
  animation: in 0.4s ease-in-out forwards;
}

.errorAnimation-leave{}

.errorAnimation-leave-active{
  animation: out 0.4s ease-in-out forwards;
}





@keyframes in{
  from{
    left: -5%;
    opacity: 0;
  }
  to{
    left: 1%;
    opacity: 1;
  }
}


@keyframes out{
  from{
    left:1%;
    opacity: 1;
  }
  to{
    left:-5%;
    opacity: 0;
  }
}


</style>
