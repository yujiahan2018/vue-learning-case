<template>
  <div>
    <SearchVue/>
    <br/>
    <ListVue/>
  </div>
</template>

<script>
  import ListVue from './components/ListVue.vue'
  import SearchVue from './components/SearchVue.vue'

  export default {
    name: 'App',
    
    components: {
      ListVue,
      SearchVue,
    
    },
    
  } 
</script>

<style>
  
</style>
