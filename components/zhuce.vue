<template>
	<div>
		<home_top></home_top>
		<div>
			<input v-model="uname"  placeholder="请输入用户名"/>
			<br />
			<input v-model="upw" placeholder="请输入密码"/>
			<br />
			<button @click="zhuce()">提交</button>
			<a href="home">首页</a>
			<a href="login">登录</a>
		</div>
	</div>
</template>

<script>
	import home_top from "./home_top.vue"
	export default{
		components:{
			home_top
		},
		data:function(){
			return{
				uname:"",
				upw:"",
			}
		},
		methods:{
			zhuce:function(){
				var o=this;
				$.ajax({
					url:"http://127.0.0.1:8081/java/ajax/zhuce",
					data:{uname:o.uname,upw:o.upw},
					success:function(r){
						if(r>0){
							alert("注册成功");
							o.$router.push("/login")
						}
					},
					xhrFields: {
					                  withCredentials: true //传递cookie,保持session的唯一性
					                },
					                crossDomain: true,
				})
			}
		}
}
</script>

<style>
</style>
