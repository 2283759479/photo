<template>
	<div>
		<home_top></home_top>
		<cebian></cebian>
	
		
		<table class="table table-danger table-hover">
			<tr>
				<td>车牌号</td>
				<td>进度</td>
				<td>维修人员</td>
				<td>维修项目</td>
				<td>金额</td>
				<td>操作</td>
				
			</tr>
			
			<tr v-for="v in jobs" >
				<td>{{myche.chepai}}</td>
				<td v-if="v.start==0">未开工</td>
				<td v-if="v.start==1">已开工</td>
				<td v-if="v.start==2">已完工</td>
				<td>
					<input v-model="v.people" />
				</td>
				<td><!-- {{v.xiangmu}} -->
					<input v-model="v.xiangmu" />
				</td>
				<td><!-- {{v.money}} -->
					<input v-model="v.money" />
				</td>
				<td>
					<button @click="updateJob()" class="btn btn-info">开工</button>
					<button @click="" class="btn btn-success">提交</button>
					<!-- <button @click="updateJobs()" class="btn btn-success">完工</button> -->
					
				</td>
			</tr>
			
		</table>
	</div>
</template>

<script>
	import home_top from "./home_top.vue"
	/* import bootstrap from "./bootstrap.vue" */
	import cebian from "./cebian.vue"
	export default{
		components:{
			home_top,cebian
		},
		data:function(){
			return{
				myche:this.$route.query,
				jobs:[],
			}
		},
		mounted() {
			this.useronline();
		},
		methods:{
			queryJob:function(){
				var o=this;
				$.ajax({
					url:"http://127.0.0.1:8081/java/ajax/queryJob",
					success:function(r){
						o.jobs=r;
					},
					xhrFields: {
					                  withCredentials: true //传递cookie,保持session的唯一性
					                },
					                crossDomain: true,
				})
			},
			//检测用户是否在线
			     useronline:function(){
			       var o = this;
			       $.ajax({
			         url: "http://127.0.0.1:8081/java/ajax/useronline",
			         success: function(r) {
									
			           if(r==""){
			             o.$router.push("/login");
			           }else{
			             o.queryJob();
						
			           }
			         },
			         xhrFields: {
			           withCredentials: true //传递cookie,保持session的唯一性
			         },
			         crossDomain: true,
			       })
			     },
				updateJob:function(){
					
				}
		}
	}
</script>

<style scoped="">
	.table{
		position: relative;
		right: -230px;
		bottom: 450px;
		/* margin-left: 200px;
		margin-top: -430px; */
		width: 85%;
	}
	#b1{
		position: relative;
		bottom: 480px;
		
	}
	tr td{
		border: 1px solid skyblue;
		cursor: pointer;
	}
	.tr1:hover{
		background-color: skyblue;
		cursor: pointer;
	}
	.tr2:hover{
		background-color: greenyellow;
	}
	.tr1{
		background-color:antiquewhite;
	}
	.tr2{
		background-color: floralwhite;
	}
</style>
