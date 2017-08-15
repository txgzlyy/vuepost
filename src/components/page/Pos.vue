<template>
  <div class="hello">
  	<el-row>
  		<el-col :span="7" class="order" id="order-list">
  			<el-tabs>
  				<el-tab-pane label="点餐">
  					<el-table :data="tabData" style="width: 100%">
  						<el-table-column prop="goodsName" label="商品名"></el-table-column>
  						<el-table-column prop="count" label="数量" width="70"></el-table-column>
  						<el-table-column prop="price" label="价格" width="70"></el-table-column>
  						<el-table-column label="操作" width="120" fixed="right">
  							<template scope="scope">
  								<el-button type="text" size="middle" @click="addOrder(scope.row)">增加</el-button>
  							  <el-button type="text" size="middle" @click="deleScope(scope.row)">减少</el-button>
  							</template>
  						</el-table-column>
  					</el-table>
  					<div class="lastOrder">
  						<small>数量：</small>{{totalcount}}   <small>价格：</small>{{totalsumm}}
  					</div>
  					<div class="div-btn">
  						<el-button type="warning">挂单</el-button>
  						<el-button type="danger" @click="dele">删除</el-button>
  						<el-button type="success" @click="sum">结账</el-button>
  					</div>
  				</el-tab-pane>
  				<el-tab-pane label="挂单"></el-tab-pane>
  				<el-tab-pane label="外卖"></el-tab-pane>
  			</el-tabs>
  		</el-col>
  		
  		<el-col :span="17">
  			<div style="margin: 0;padding: 0;">
  				<div class="name-bt">
  					热卖商品
	  			</div>
	  			<div class="ofen-goods">
	  				<ul class="goods-list">
	  					<li v-for="goods in oftenGoods" @click="addOrder(goods)">
	  						<span class="title">{{goods.goodsName}}</span>
	  						<span class="o-price">￥ {{goods.price}} 元</span>
	  					</li>
	  				</ul>
	  			</div>
	  			
	  			<div class="goods-class">
	  				<el-tabs>
	  					<el-tab-pane label="主食">
	  						<div>
									<ul class='cookList'>
									    <li v-for="goods in type0Goods" @click="addOrder(goods)">
									        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
									        <span class="foodName">{{goods.goodsName}}</span>
									        <span class="foodPrice">￥{{goods.price}}元</span>
									    </li>
									</ul>
	  						</div>
	  					</el-tab-pane>
	  					<el-tab-pane label="饮料">
	  						<div>
									<ul class='cookList'>
									    <li v-for="goods in type1Goods" @click="addOrder(goods)">
									        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
									        <span class="foodName">{{goods.goodsName}}</span>
									        <span class="foodPrice">￥{{goods.price}}元</span>
									    </li>
									</ul>
	  						</div>
	  					</el-tab-pane>
	  					<el-tab-pane label="小吃">
	  						<div>
									<ul class='cookList'>
									    <li v-for="goods in type2Goods" @click="addOrder(goods)">
									        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
									        <span class="foodName">{{goods.goodsName}}</span>
									        <span class="foodPrice">￥{{goods.price}}元</span>
									    </li>
									</ul>
	  						</div>
	  					</el-tab-pane>
	  					<el-tab-pane label="套餐">
	  					    <div>
									<ul class='cookList'>
									    <li v-for="goods in type3Goods" @click="addOrder(goods)">
									        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
									        <span class="foodName">{{goods.goodsName}}</span>
									        <span class="foodPrice">￥{{goods.price}}元</span>
									    </li>
									</ul>
	  						</div>
	  					</el-tab-pane>
	  				</el-tabs>
	  			</div>
  			</div>
  			
  		</el-col>
  	</el-row>
  </div>
</template>

<script>
    import axios from 'axios';	
export default {
	data(){
		return{
			totalsumm:0,
			totalcount:0,
			tabData:[],
		  oftenGoods:[],
		  type0Goods:[],
		  type1Goods:[],
		  type2Goods:[],
		  type3Goods:[]
		}
	},
	created(){
		axios.get('http://jspang.com/DemoApi/oftenGoods.php')
		.then((respons)=>{
			//console.log(respons);
			this.oftenGoods = respons.data
		})
		.catch((err)=>{
			console.log(err);
			alert('获取数据失败！')
		});
		axios.get('http://jspang.com/DemoApi/typeGoods.php')
		.then((respons)=>{
			//console.log(respons);
			this.type0Goods = respons.data[0];
			this.type1Goods = respons.data[1];
			this.type2Goods = respons.data[2];
			this.type3Goods = respons.data[3];
		})
		.catch((err)=>{
			console.log(err);
			alert('获取数据失败！')
		});
	},
	mounted(){
		var docuHei = document.body.clientHeight;
		document.getElementById('order-list').style.height = docuHei+'px'
	},
	methods:{
		addOrder(goods){
			// 判断列表中有没有这个商品
			let isHave = false; 
			this.tabData.forEach(item=>{
				if(item.goodsId == goods.goodsId){
					isHave = true;
				}
			});
			
			//根据条件书写业务逻辑
			if(isHave){   //  该商品已存在   只有数量增加
				let arr = this.tabData.filter(o=>o.goodsId == goods.goodsId);
				arr[0].count++;
			}else{
				let newgoods = {
					goodsId: goods.goodsId,
					goodsName: goods.goodsName,
					price: goods.price,
					count:1
				}
				this.tabData.push(newgoods)
			};
			this.getMonny()
		},
		sum(){  //  结账
	    if(this.totalcount!=0){
	    	this.tabData = [];
				this.totalsumm=0;
				this.totalcount=0;
				this.$message({
					message: '结账成功，感谢您的光临！',
					type: 'success'
				})
	    }else{
	    	this.$message.error('不能空结，老板了解你急切的心情！')
	    }
		},
		deleScope(scope){          //  删除单个商品
        //  id不同的筛选出来      把id相同的那组帅选掉
        this.tabData = this.tabData.filter(o=>o.goodsId != scope.goodsId);   
        this.getMonny()
		},
		dele(){       // 删除订单
			this.tabData = [];
			this.totalsumm=0;
			this.totalcount=0;
		},
		getMonny(){
			this.totalsumm=0;
			this.totalcount=0;
			if(this.tabData){
				this.tabData.forEach(item=>{
					this.totalcount += item.count;
					this.totalsumm += item.count * item.price
				});
			}
		}
		
	}
  
  
}
</script>


<style scoped>
.order{
	background-color: #fff;
	border-right:1px solid #ccc;
}
.div-btn{
	margin-top: 20px;
}
.name-bt{
	padding: 0 10px;
	height: 40px;
	border-bottom:1px solid #ccc;
	background-color: #fff;
	font: 22px/40px helvetica;
	text-align: left;
}
.goods-list li{
	list-style: none;
	float: left;
	font: 18px/20px helvetica;
	padding:10px;
	border:1px solid #D2E0F8;
	background-color: #fff;
	margin: 10px;
}
.o-price{
	color: #006EED;
}
.goods-class{
	margin-top: 20px;
	clear: both;
}
  .cookList li{  
       list-style: none;
       width:23%;
       border:1px solid #E5E9F2;
       height: auot;
       overflow: hidden;
       background-color:#fff;
       padding: 2px;
       float:left;
       margin: 2px;
 
   }
   .cookList li span{
       
        display: block;
        float:left;
   }
   .foodImg{
       width: 40%;
   }
   .foodName{
       font-size: 18px;
       padding-left: 10px;
       color:brown;
 
   }
   .foodPrice{
       font-size: 16px;
       padding-left: 10px;
       padding-top:10px;
   }
   .lastOrder{
   	   font: 18px/40px helvetica;
   	   border-bottom: 1px solid #E5E9F2;
   }
</style>
