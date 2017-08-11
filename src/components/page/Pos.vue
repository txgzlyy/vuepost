<template>
  <div class="hello">
  	<el-row>
  		<el-col :span="7" class="order" id="order-list">
  			我是订单栏目
  		</el-col>
  		<el-col :span="17">
  			我是商品栏目
  		</el-col>
  	</el-row>
  </div>
</template>

<script>
export default {
	mounted(){
		var docuHei = document.body.clientHeight;
		document.getElementById('order-list').style.height = docuHei+'px'
	}
  
  
}
</script>


<style scoped>
.order{
	background-color: #fff;
}
</style>
