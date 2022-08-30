<template>
  <inputVue v-model="name"/>
</template>

<script>
import inputVue from './components/input.vue';


export default {
  name: 'App',
  components: {
    inputVue,  
  },
  data(){
    return {
      name: ''
    }
  },
  methode: {},
  
}
</script>

<style lang="scss">
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
