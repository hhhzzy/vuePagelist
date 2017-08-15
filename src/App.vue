<template>
  <div id="app">
    <Pagelist></Pagelist>
    <PagelistTwo></PagelistTwo>
  </div>
</template>

<script>
import Pagelist from './components/Pagelist.vue'
import PagelistTwo from './components/PagelistTwo.vue'
export default {
      components:{
          Pagelist,
          PagelistTwo
      }
}
</script>

<style scoped>
  #app{text-align: center;}
</style>
