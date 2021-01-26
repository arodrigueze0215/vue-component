<template>
  <Select :items="items"
      placeholder="Choose Something" 
      :multiselect="false"/>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core'
import { faAmbulance, faBox, faBrain } from '@fortawesome/free-solid-svg-icons'
library.add(faAmbulance, faBox, faBrain)
import Select from './components/Select/Select'


export default {
  name: 'App',
  components: {
    Select
  },
  data () {
    return {
      items: [ 
        {name:'Andres',checked:false, icon:'brain'},
        {name:'Daniela',checked:false, icon:'ambulance'},
        {name:'Rafael',checked:false, icon:'box'},

      ]
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
