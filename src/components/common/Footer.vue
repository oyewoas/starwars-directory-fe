<template>
  	<footer class="container" id="footer">
	    <div class="row">
			<div id="footer-text" class="col-md-12 text-center py-3">
				<span>&copy; 2019, All rights reserved</span>
			</div>
		</div>
    </footer>
</template>

<style lang='scss' scoped>
    
</style>
<script>
 // Utilities
  import {
    mapGetters,
  } from 'vuex'
  export default {
    data() {
      return {
        
      }
		},
    computed: {
      ...mapGetters(['links'])
    },
    methods: { 
    }
	
  }
</script>