<template>
  <div id="app">
  	
  	<leftnav></leftnav>
  	
  	<div class="main">
  		 <router-view></router-view>
  	</div>
  	
  </div>
</template>

<script>
import leftNav from '@/components/common/leftNav'

export default {
  name: 'app',
  components: {
  	leftnav: leftNav
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.main{
	width: 95%;
	height: 100%;
	float: right;
	background-color: #F8F8F8;
}
</style>
