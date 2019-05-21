<template>
	<!-- 容器盒子 -->
	<div class="slide-show" @mouseover="this.clearInv" @mouseout="this.runInv">
		<!-- 图片 -->
		<div class="slide-img">
			<a :href="slides[nowIndex].href">
				<transition name="slide-trans">
					<img v-if="isShow" :src="slides[nowIndex].src" alt="">
				</transition>
				<transition name="slide-trans-old">
					<img v-if="!isShow" :src="slides[nowIndex].src" alt="">
				</transition>
			</a>
		</div>
		<!-- 图片信息 -->
		<h2>{{slides[nowIndex].title}}</h2>
		<!-- 按钮以及页码 -->
		<ul class="slide-pages">
			<li @click="goto(prevIndex)">&lt;</li>
			<li v-for="(item,index) in slides" @click="goto(index)">
				<a >{{index + 1}}</a>
			</li>
			<li @click="goto(nextIndex)">&gt;</li>
		</ul>
	</div>
</template>

<script>
export default{
	props:{
		slides:{
			type:Array,
			default:[]
		},
		inv:{
			type:Number,
			default:1000
		}
	},
	data (){
		return{
			nowIndex:0,
			isShow:true
		}
	},
	computed:{
		// 这里通过使用计算属性实现页面跳转，优雅简单，不用写复杂的
		// 原生JS
		// 上一页
		prevIndex (){
			if(this.nowIndex === 0){
				return this.slides.length - 1
			}else{
				return this.nowIndex - 1
			}
		},
		// 下一页
		nextIndex (){
			if(this.nowIndex === this.slides.length -1){
				return 0
			}else{
				return this.nowIndex + 1
			}
		}
	},
	methods:{
		goto (index){
			this.isShow = false
	      	setTimeout(() => {
	        	this.isShow = true
	        	this.nowIndex = index
	      	}, 10)
			// this.nowIndex = index
		},
		runInv (){
			this.invId = setInterval( () => {
				this.goto(this.nextIndex)
			},this.inv)
		},
		clearInv (){
			clearInterval(this.invId)
		}
		// 鼠标移入移除事件控制图片的开始/暂停下一页
	},
	mounted (){
		this.runInv();
	}
}
</script>
/*
小结：、
1.标签上通过v-bind绑定属性，就可以与data中定义的属性绑定在一起，达到赋值data中的属性
传递给标签上的属性。
2.父子组件之间的通讯是：父组件通过属性传递数据给子组件。子组件则通过自定义事件反馈自身的数据给
父组件。【在父组件中使用子组件，首先导入子组件，在子组件上通过属性传值，子组件内必须定义props属
性，在其中设置传入的数据的类型等属性。】
3.使用transition标签制作动画时，注意四个位置代表的意义。
 */ 

<style scoped>
/*动画进入*/ 
.slide-trans-enter-active {
  transition: all .5s;
}
/*动画进入*/ 
.slide-trans-enter {
  transform: translateX(900px);
}
/*离开过程动画*/ 
.slide-trans-old-leave-active {
  transition: all .5s;
  transform: translateX(-900px);
}
.slide-show {
  position: relative;
  margin: 15px 15px 15px 0;
  width: 900px;
  height: 500px;
  overflow: hidden;
}
.slide-show h2 {
  position: absolute;
  width: 100%;
  height: 100%;
  color: #fff;
  background: #000;
  opacity: .5;
  bottom: 0;
  height: 30px;
  text-align: left;
  padding-left: 15px;
  line-height: 30px;
}
.slide-img {
  width: 100%;
}
.slide-img img {
  width: 100%;
  position: absolute;
  top: 0;
}
.slide-pages {
  position: absolute;
  bottom: 10px;
  right: 15px;
}
.slide-pages li {
  display: inline-block;
  padding: 0 10px;
  cursor: pointer;
  color: #fff;
}
.slide-pages li .on {
  text-decoration: underline;
}
</style>