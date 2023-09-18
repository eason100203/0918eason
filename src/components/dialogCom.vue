<script setup>
import { ref, reactive, computed, defineProps,defineEmits} from 'vue'

const props=defineProps({
  title: {
    type: String,
    required: true
  },
  content:{
    type: String,
    required: true
  },
  showDia:{
    type:Boolean,
    required:true
  }
})

const emit = defineEmits(['change'])

// const {emit}=defineEmits(['change'])
  

const closeBtn=ref(false)
const enterdia=()=>{
  closeBtn.value=true
//確定後要把父元件控制boolean的value改回預設值,才可繼續使用
emit('change')
}
  
</script>

<template>
 <div class='diva' v-show="props.showDia" :style="{display:closeBtn?'none':''}">
   <h1>{{props.title}}</h1>
   <p>{{props.content}}</p>
   <button @click="enterdia">確定</button>
 </div>
</template>

<style scoped>

  .diva{
    position: fixed;
    bottom:50%;
    width:60%;
    height:200px;
    box-shadow: 0 0 5px gray;
    background-color:white;
    z-index:999;
  }
</style>