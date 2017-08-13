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
  								<el-button type="text" size="middle">增加</el-button>
  							  <el-button type="text" size="middle">删除</el-button>
  							</template>
  						</el-table-column>
  					</el-table>
  					<div class="div-btn">
  						<el-button type="warning">挂单</el-button>
  						<el-button type="danger">删除</el-button>
  						<el-button type="success">结账</el-button>
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
	  					<li v-for="goods in oftenGoods">
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
									    <li v-for="goods in type0Goods">
									        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
									        <span class="foodName">{{goods.goodsName}}</span>
									        <span class="foodPrice">￥{{goods.price}}元</span>
									    </li>
									</ul>
	  						</div>
	  					</el-tab-pane>
	  					<el-tab-pane label="饮料"></el-tab-pane>
	  					<el-tab-pane label="小吃"></el-tab-pane>
	  					<el-tab-pane label="套餐"></el-tab-pane>
	  				</el-tabs>
	  			</div>
	  			
	  			
  			</div>
  			
  		</el-col>
  	</el-row>
  </div>
</template>

<script>
export default {
	data(){
		return{
			tabData:[
			  {
          goodsName: '可口可乐',
          price: 8,
          count:1
        }, {
          
          goodsName: '香辣鸡腿堡',
          price: 15,
          count:1
        }, {
         
          goodsName: '爱心薯条',
          price: 8,
          count:1
        }, {
         
          goodsName: '甜筒',
          price: 8,
          count:1
        }
      ],
      oftenGoods:[
          {
              goodsId:1,
              goodsName:'香辣鸡腿堡',
              price:18
          }, {
              goodsId:2,
              goodsName:'田园鸡腿堡',
              price:15
          }, {
              goodsId:3,
              goodsName:'和风汉堡',
              price:15
          }, {
              goodsId:4,
              goodsName:'快乐全家桶',
              price:80
          }, {
              goodsId:5,
              goodsName:'脆皮炸鸡腿',
              price:10
          }, {
              goodsId:6,
              goodsName:'魔法鸡块',
              price:20
          }, {
              goodsId:7,
              goodsName:'可乐大杯',
              price:10
          }, {
              goodsId:8,
              goodsName:'雪顶咖啡',
              price:18
          }, {
              goodsId:9,
              goodsName:'大块鸡米花',
              price:15
          }, {
              goodsId:20,
              goodsName:'香脆鸡柳',
              price:17
          }
      ],
      type0Goods:[
          {
              goodsId:1,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
              goodsName:'香辣鸡腿堡',
              price:18
          }, {
              goodsId:2,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'田园鸡腿堡',
              price:15
          }, {
              goodsId:3,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
              goodsName:'和风汉堡',
              price:15
          }, {
              goodsId:4,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'快乐全家桶',
              price:80
          }, {
              goodsId:5,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'脆皮炸鸡腿',
              price:10
          }, {
              goodsId:6,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
              goodsName:'魔法鸡块',
              price:20
          }, {
              goodsId:7,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
              goodsName:'可乐大杯',
              price:10
          }, {
              goodsId:8,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'雪顶咖啡',
              price:18
          }, {
              goodsId:9,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'大块鸡米花',
              price:15
          }, {
              goodsId:20,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'香脆鸡柳',
              price:17
          }
          
      ],
        
		}
	},
	mounted(){
		var docuHei = document.body.clientHeight;
		document.getElementById('order-list').style.height = docuHei+'px'
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
</style>
