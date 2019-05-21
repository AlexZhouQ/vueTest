<template>
	<div class="index-wrap">
		<div class="index-left">
			<!-- 产品信息 -->
			<div class="index-left-block">
				
				<h2>全部产品</h2>
				<template v-for="product in productList">
					<h3>{{product.title}}</h3>
					<ul>
						<li v-for="item in product.list">
							<a :href="item.url">{{item.name}}</a>
							<span v-if="item.hot" class="hot-tag">HOT</span>
						</li>
					</ul>
					<div class="hr" v-if="!product.last"></div>
				</template>
			</div>
			<!-- 最新消息 -->
			<div class="index-left-block lastest-news">
				<h2>最新消息</h2>
				<ul>
					<li v-for="item in newsList"> 
						<a :href="item.url" class="new-item">{{item.title}}</a>
					</li>
				</ul>
			</div>
		</div>
		<!-- 右侧信息 -->
		<div class="index-right">
			<!-- banner图部分 -->
			<slideshow :slides="slides" :inv="invTime"></slideshow>
			<!-- 右侧下半部分 -->
			<div class="index-board-list">
				<div v-for="(item,index) in boardList" class="index-board-item"
				:class="[{'line-last':index %2 !==0},'index-board-'+item.id]">
					<div class="index-board-item-inner">
						<h2>{{item.title}}</h2>
						<p>{{item.derection}}</p>
						<div class="index-board-button">
							<router-link class="button" :to="{path:'detail/'+item.tokey}">立即购买</router-link>	
						</div>
					</div>
				</div>
			</div>

		</div>
	</div>
</template>

<script>
import slideshow from '../components/slideShow'
export default{
	components:{
		slideshow
	},
	/*
	生命周期勾子函数
	created:function(){
		this.$http.get('api/getNewsList').then(
			(res) => {
				this.newsList = res.data
			},
			(err) =>{
				console.log("error")
			}
		)
	},*/

	data (){
		return {
			invTime: 2000,
	      	slides: [
		        {
		          src: require('../assets/slideShow/pic1.jpg'),
		          title: 'xxx1',
		          href: 'detail/analysis'  
		        },
		        {
		          src: require('../assets/slideShow/pic2.jpg'),
		          title: 'xxx2',
		          href: 'detail/count'
		        },
		        {
		          src: require('../assets/slideShow/pic3.jpg'),
		          title: 'xxx3',
		          href: 'http://xxx.xxx.com' 
		        },
		        {
		          src: require('../assets/slideShow/pic4.jpg'),
		          title: 'xxx4',
		          href: 'detail/forecast'
		        }
	      	],
			boardList:[
				{
					title:'开放产品',derection:'开放产品是一款开放产品',id:'car',tokey:'analysis'
				},
				{
					title:'品牌营销',derection:'品牌营销帮助你的产品更好地找到定位',id:'earth',tokey:'count'
				},
				{
					title:'使命必达',derection:'使命必达快速迭代永远保持最前端的速度',id:'loud',tokey:'forecast'
				},
				{
					title:'勇攀高峰',derection:'帮你勇闯高峰，到达事业的顶峰',id:'hill',tokey:'publish'
				}
			],
			newsList:[
				{title:'百度头条',url:'http://www.baidu.com'},
				{title:'腾讯新闻',url:'http://www.baidu.com'},
				{title:'大鱼号',url:'http://www.baidu.com'},
				{title:'百家讲堂',url:'http://www.baidu.com'},
				{title:'德云相声',url:'http://www.baidu.com'},
				{title:'最新电影',url:'http://www.baidu.com'},
				{title:'最新电视剧',url:'http://www.baidu.com'},
				{title:'古装武侠',url:'http://www.baidu.com'},
			],
			productList:{
				pc: {
		            title: 'PC产品',
		            list: [
			            {name: '数据统计',url: 'http://starcraft.com'},
			            {name: '数据预测',url: 'http://warcraft.com'},
			            {name: '流量分析',url: 'http://overwatch.com',hot: true},
			            {name: '广告发布',url: 'http://hearstone.com'}
		            ]
	        	},
				app:{
					title:'app端产品',
					last:true,
					list:[
						{
			              name: '91助手',
			              url: 'http://weixin.com'
			            },
			            {
			              name: '产品助手',
			              url: 'http://twitter.com',
			              hot: true
			            },
			            {
			              name: '智能地图',
			              url: 'http://maps.com'
			            },
			            {
			              name: '团队语音',
			              url: 'http://phone.com'
			            }
		            ]
				}
			
			}
		}
	}
}
</script>

<style scoped>
/*最外层包裹盒子*/ 
.index-wrap {
	width:1200px;
	margin:0 auto;
	overflow:hidden;
}
.index-left{
	float:left;
	width:300px;
	text-align:left;
}
.index-right{
	float:left;
	width:900px;
}

.index-left-block{
	margin:15px;
	background:#fff;
	box-shadow:0 0 1px #ddd;
}
.index-left-block .hr {
  margin-bottom: 20px;
}
.index-left-block h2 {
  background: #4fc08d;
  color: #fff;
  padding: 10px 15px;
  margin-bottom: 20px;
}
.index-left-block h3 {
  padding: 0 15px 5px 15px;
  font-weight: bold;
  color: #222;
}
.index-left-block ul {
  padding: 10px 15px;
}
.index-left-block li {
  padding: 5px;
}
/**/ 
.index-board-list {
  overflow: hidden;
}
.index-board-item {
  float: left;
  width: 400px;
  background: #fff;
  box-shadow: 0 0 1px #ddd;
  padding: 20px;
  margin-right: 20px;
  margin-bottom: 20px;
}
.index-board-item-inner {
  min-height: 125px;
  padding-left: 120px;
}
.index-board-car .index-board-item-inner{
  background: url(../assets/images/1.png) no-repeat;
}
.index-board-loud .index-board-item-inner{
  background: url(../assets/images/2.png) no-repeat;
}
.index-board-earth .index-board-item-inner{
  background: url(../assets/images/3.png) no-repeat;
}
.index-board-hill .index-board-item-inner{
  background: url(../assets/images/4.png) no-repeat;
}
.index-board-item h2 {
  font-size: 18px;
  font-weight: bold;
  color: #000;
  margin-bottom: 15px;
}
.line-last {
  margin-right: 0;
}
.index-board-button {
    margin-top: 20px;
    width: 100px;
	height: 50px;
	line-height: 50px;
	background: antiquewhite;
	text-align: center;
}

.lastest-news {
  min-height: 512px;
}
.hot-tag {
  background: red;
  color: #fff;
}
.new-item {
  display: inline-block;
  width: 230px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
</style>