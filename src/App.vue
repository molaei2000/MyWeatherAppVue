<template>
  <div id="app">
    <div class="container">
      <weather/>
    </div>
  </div>
</template>

<script>

import Weather from './components/Weather'

export default {
  name: 'app',
  data () {
    return {
      
    }
  },
  components:{
    Weather
  }
}
</script>