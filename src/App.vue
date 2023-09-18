<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import searchMovie from './components/searchMovie.vue'
import { ref, reactive, computed} from 'vue'

const hehe=ref('')
</script>

<template>
  <main>
    <input type='text' style="width:50%; line-height:20px" v-model='hehe' placeholder="請輸入想查詢電影">
    <hr style="margin:10px 0;">
    <searchMovie :msg='hehe'/>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
