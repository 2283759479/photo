<template>
	<div>
		<home_top></home_top>
		<div>
			<input v-model="uname"  placeholder="请输入用户名"/>
			<br />
			<input v-model="upw" placeholder="请输入密码"/>
			<br />
			<button @click="login()">提交</button>
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
		mounted() {
			
		},
		methods:{
			login:function(){
				var o=this;
				$.ajax({
					url:"http://127.0.0.1:8081/java/ajax/login",
					data:{uname:o.uname,upw:o.upw},
					success:function(r){
						
						if(r){
							$.ajax({
								url:"http://127.0.0.1:8081/java/ajax/useronline",
								success:function(r){
									alert("小垃圾，恭喜你呦，登录成功");
									 o.$router.push("/home");
								},
								xhrFields: {
								                  withCredentials: true //传递cookie,保持session的唯一性
								                },
								                crossDomain: true,
								})
						}
						
					},
					xhrFields: {
					                  withCredentials: true //传递cookie,保持session的唯一性
					                },
					                crossDomain: true,
				})
				
			},
		}
	}
</script>

<style>
</style>
