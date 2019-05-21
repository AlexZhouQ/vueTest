<template>
	<div>
		<!-- 容器盒子 -->
		<div class="dialog-wrap">
			<!-- 背景影音 -->
			<div class="dialog-cover" v-if="isShow" @click="closeMyself"></div>
				<!-- 动画效果 -->
			<transition	name="drop">
				<!-- 弹窗主体内容 -->
				<div class="dialog-content" v-if="isShow">
					<!-- 关闭按钮 -->
					<p class="dialog-close" @click="closeMyself"></p>
					<!-- 插槽显示的内容 -->
					<slot>empty</slot>	
				</div>
			</transition>
			
		</div>
	</div>
</template>
<script>
export default{
	props:{
		isShow :{
			type:Boolean,
			default:false
		}
	},
	data (){
		return {

		}
	},
	methods:{
		closeMyself (){
			// 自定义事件穿向上级
			this.$emit('on-close')
		}
	}
}
	
</script>
<style scoped>
.drop-enter-active{
	transition: all .5s linear;
}
.drop-leave-active{
	transition: all .3s linear;
}
.drop-enter{
	transform: translateY(-500px);
}
.drop-leave-active{
	transform: translateY(-500px);
}
.dialog-wrap{
	position: fixed;
	width: 100%;
	height: 100%;
	
}
.dialog-cover{
	position: fixed;background: #000;
	background:rgba(0,0,0,0.3);
	z-index: 5;
	top: 0;left: 0;
	width: 100%;height: 100%;
}
.dialog-content{
	position: fixed;
	width: 50%;left: 50%;
	margin-left: -25%;
	max-height: 50%;
	top: 20%;z-index: 10;
	overflow:auto;background: #fff;
	border: 2px solid #464068;
  	padding: 2%;line-height: 1.6;
}
.dialog-close {
  position: absolute;
  right: 5px;
  top: 5px;
  width: 20px;
  height: 20px;
  text-align: center;
  cursor: pointer;
}
.dialog-close:hover {
  color: #4fc08d;
}
</style>