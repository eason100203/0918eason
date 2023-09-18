
<script setup>
import { ref, reactive, computed, defineProps} from 'vue'
import dialogCom from './dialogCom.vue'
const props=defineProps({
  msg: {
    type: String,
    required: true
  }
})


  const searchData=async ()=>{  
  const response = await fetch(`https://www.omdbapi.com/?i=tt3896198&apikey=8341bfbe&t=${props.msg}`);
  const movies = await response.json();
  movieData.value=movies   
  console.log(movieData.value.Response)
  }
  const movieData=ref('222')
  const inputEdit=ref([])
  const alreadyCol=ref(false)
  const insertMov=(v)=>{
    let checkMovie=inputEdit.value.find((movie)=>{ return movie.Title == v.Title})
    if(checkMovie){
      alreadyCol.value=true
      //我子元件按確定時我應該要把父元件alreadyCol.value的值再次變成false要怎麼做?
      //子元件控制父元件的value值這樣好嗎?有沒有更好的方法?
    }else{
      inputEdit.value.push(v)
    }
    // console.log(inputEdit.value)
  }
  const deleteaa=(v)=>{
   inputEdit.value=inputEdit.value.filter((i)=>{
     return i.Title != v
   })
  }
  const reSearch=async (v)=>{
     const response = await fetch(`https://www.omdbapi.com/?i=tt3896198&apikey=8341bfbe&t=${v.Title}`);
  const movies = await response.json();
  movieData.value=movies   
  console.log(movieData.value.Response)
  }

  const testchange=()=>{
    alreadyCol.value=false
  }

  

  
</script>

<template>
  <div class="dis">
  <div style="width:50%">
  <button style="margin:2px"  @click="searchData">查詢電影</button>
    <button :class="movieData.Response==='True'?'':'disN'" @click='insertMov(movieData)'>加入清單</button>
    <p class="">電影名稱: {{movieData.Title}}</p>
    <p class="">上映日期: {{movieData.Year}}</p>
    <p class="">演員列表: {{movieData.Actors}}</p>
    <img :src="movieData.Poster" :class="movieData.Poster==='N/A'?'disN':''">
     </div>
  <div style="width:80%;margin-left:30px">
      <p>收藏清單:</p>
       <ul>
         <li v-for='item in inputEdit'>
          <span @click="reSearch(item)" class="cursor" >{{item.Title}}</span>
  <span @click="deleteaa(item.Title)"><button>X</button></span>
         </li>     
       </ul>
    </div>
  </div>

  <dialogCom  title="已收藏" content="清單已收藏過" :showDia="alreadyCol" @change="testchange"/>
</template>
<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

p{
  margin:5px;
}

.dis {
    display:flex;
  }

.cursor{
  cursor:pointer;
}


button{
  border-radius:5px;
  border:1px gray solid;
  background-color:whitesmoke;
  cursor:pointer;
}
  
button:hover{
  border-radius:5px;
  border:1px gray solid;
  background-color:gray;
  color:white;
  cursor:pointer;
  scale:1.05
}
  
  
.greetings h1,
.greetings h3 {
  text-align: center;
}

.disN {
    display:none;
  }


</style>
