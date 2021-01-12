<template>
	<div>
		
		
		
		<div>
			<nav class="navbar navbar-default" role="navigation">
				<div class="container-fluid"> 
				<div class="navbar-header">
					<button type="button" class="navbar-toggle" data-toggle="collapse"
							data-target="#example-navbar-collapse">
						<span class="sr-only">切换导航</span>
						<span class="icon-bar"></span>
						<span class="icon-bar"></span>
						<span class="icon-bar"></span>
					</button>
					
					<a class="navbar-brand" href="#">OA系统</a>
					
				</div>
				<div class="collapse navbar-collapse" id="example-navbar-collapse">
					<ul class="nav navbar-nav">
						<li class="active">
							
							<router-link to="home">首页</router-link>
							
							</li>
						<li class="active">
							
							
							</li>
							
						<li>
							
							<router-link to="/zhuce">注册</router-link>
							
						</li>
						<li class="dropdown">
							<a href="#" class="dropdown-toggle" data-toggle="dropdown">
								
								<router-link v-if="online==''" to="/login">登录</router-link>
								<span class="uname" style="color: #00BFFF;" v-else>{{online.uname}}</span> 
								
								 <b class="caret"></b>
							</a>
							<ul class="dropdown-menu">
								<li><a href="#">头像</a></li>
								<li><a href="#">个人信息</a></li>
								<li><a href="http://127.0.0.1:8081/java/logout">退出</a></li>
							</ul>
						</li>
					</ul>
				</div>
				</div>
			</nav>
		</div>
	</div>
</template>

<script>
	export default{
		components:{
			
		},
		data:function(){
			return{
				online:[],
				
			}
		},
		mounted() {
			this.useronline()
		},
		methods:{
			//检测用户是否在线
			    useronline:function(){
			             var o = this;
			             $.ajax({
			               url: "http://127.0.0.1:8081/java/ajax/useronline",
			               success: function(r) {
								
			                  o.online = r;
							 
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

<style scoped="">
	.uname{
		/* line-height: 50px; */
		padding: 0 0 0 10px;
	}
</style>
