<template>
<div class="container">
    <h1 class="header text-center mt-2 mb-5">People Directory</h1>
  
  <PeopleList :peoplelists="peoplelists"/>

  <div v-if="loading" class=" text-center">
    <PulseLoader class="loader" color="#866ec7" />
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
  import PeopleList from '@/components/peoplelist/PeopleList'
  import axios from 'axios';
  import PulseLoader from 'vue-spinner/src/PulseLoader.vue'
  const url = 'https://swapi.co/api/people/';
  export default {
    components: {
      PeopleList,
      PulseLoader
    },
    data() {
      return {
        peoplelists: [],
        errors: [],
        loading: true
      }
    },
    methods: {
      loadPeople(){
        axios.get(url)
          .then(response => {
            // JSON responses are automatically parsed.
            this.peoplelists = response.data.results
            this.loading = false;
          })
          .catch(e => {
            this.errors.push(e)
          })
      },
    },
    
    mounted () {
      this.loadPeople()
  }
  }
</script>