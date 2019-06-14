<template>
<div class="container">
    <h1 class="header text-center mt-2 mb-5">Planets Directory</h1>

    <PlanetList :planetlists="planetlists"/>

    <div v-if="loading" class="text-center">
      <PulseLoader class="loader" color="#866ec7"/>
    </div>
</div>
</template>

<style lang="scss" scoped>
  .container{
    margin-top: 100px;

      .loader{
      margin-top: 200px;
      margin-bottom: 200px;
    }
    .header{
      color: #866ec7;
      font-weight: bolder;
      text-transform: uppercase
    }
  }
</style>


<script>
  import PlanetList from '@/components/planetlist/PlanetList'
  import axios from 'axios';
  import PulseLoader from 'vue-spinner/src/PulseLoader.vue'

  export default {
    components: {
      PlanetList,
      PulseLoader
    },
    data() {
      return {
        planetlists: [],
        errors: [],
        loading: true
      }
    },

    mounted () {
      axios.get(`https://swapi.co/api/planets/`)
      .then(response => {
        // JSON responses are automatically parsed.
        this.planetlists = response.data.results
         this.loading = false

      })
      .catch(e => {
        this.errors.push(e)
      })
  }
  }
</script>