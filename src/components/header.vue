<template>
	<div class="">
		<!-- 图标链接 -->
		<img v-bind:src="{{imgsrc}}" alt="">
		<div v-for="item in lists">
			{{item.name}}
			<span>|</span>
		</div>
	</div>
</template>

<script>
export default{
	name:'Header',
	data:{
		lists:[
			{values:'登录'},
			{values:'注册'},
			{values:'关于'},
		]
		
	},
	computed:{
		imgsrc:'../assets/timg.jpg'
	}
}

</script>

<style>
	
</style>