<template>
<div class="container">
    <h1 class="header text-center mt-2 mb-5">People Directory</h1>
    <div class="pagination">
      <button class="btn btn-prev" @click="loadPeople(pagination.previous)"
              :disabled="!pagination.previous">
          Previous Page
      </button>
      <!-- <span class="mt-3">Page {{page}} of {{totalPage}}</span> -->
      <button class="btn btn-next" @click="loadPeople(pagination.next)"
        :disabled="!pagination.next">Next Page
    </button>
  </div>
  
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

    .pagination{
      .btn{
        border: none;
        color: #866ec7;
        cursor: pointer;
        margin: 10px;

        &:hover{
        background-color: #866ec7;
        color: white;
      }
      }
      
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
      PulseLoader,

    },
    data() {
      return {
        peoplelists: [],
        pagination: {},
        loading: true,
        errors: [],
        pagination: {},
        page: '',
        pageno: 0,
        totalPage: 8
      }
    },
    methods: {
      loadPeople(url){
        let vm = this;
        axios.get(url)
          .then(response => {
            // JSON responses are automatically parsed.
            this.peoplelists = response.data.results
            vm.makePagination(response.data)
            this.loading = false;
          })
          .catch(e => {
            this.errors.push(e)
          })
      },

       makePagination(data){
          let pagination = {
            next : data.next,
            previous: data.previous,
          }
          this.pagination = pagination
      },
    },
    
    mounted () {
      this.loadPeople(url)
  }
  }
</script>