<template>
	<div>
		<home_top></home_top>
		<cebian></cebian>
		
		 
		
		<!-- Button trigger modal -->
		
		<button id="b1" type="button" class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal">
		  信息添加
		</button>
		<!-- Modal -->
		<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel">
		  <div class="modal-dialog" role="document">
		    <div class="modal-content">
		      <div class="modal-header">
		        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
		        <h4 class="modal-title" id="myModalLabel">信息添加</h4>
		      </div>
		      <div class="modal-body">
		       
			   <div class="form-group">
			      <label for="name"></label>
			      <input v-model="cname" type="text" class="form-control" id="name" placeholder="请输入车主姓名">
			    </div>
			   						
			   						<div class="form-group">
			   						   <label for="name"></label>
			   						   <input v-model="cphone" type="number" class="form-control" id="name" placeholder="请输入车主电话">
			   						 </div>
			   		
			   						<div class="form-group">
			   						   <label for="name"></label>
			   						   <input v-model="type" type="text" class="form-control" id="name" placeholder="请输入车辆种类">
			   						 </div>
			   		
			   						<div class="form-group">
			   						   <label for="name"></label>
			   						   <input v-model="chepai" type="text" class="form-control" id="name" placeholder="请输入车主车牌号">
			   						 </div>
			   						
			   						<div class="form-group">
			   						   <label for="name"></label>
			   						   <input v-model="maobing" type="text" class="form-control" id="name" placeholder="请输入车辆故障现象">
			   						 </div>
			   						
			
		      </div>
		      <div class="modal-footer">
		        <button type="button" class="btn btn-default" data-dismiss="modal">关闭</button>
		        <button @click="luru()" type="button" class="btn btn-primary">录入并保存</button>
		      </div>
		    </div>
		  </div>
		</div>
		
		<div>
			
		 	<table class="table table-danger table-hover">
				<tr>
					<td>编号</td>
					<td>车主姓名</td>
					<td>车主电话</td>
					<td>车辆种类</td>
					<td>车牌</td>
					<td>进厂时间</td>
					<td>车辆故障现象</td>
				</tr>
				
				<tr class="tr1" v-for="v,s in myche" v-if="s%2!=0"  @click="jumpMyche(v)">
					<td>{{v.cid}}</td>
					<td>{{v.cname}}</td>
					<td>{{v.cphone}}</td>
					<td>{{v.type}}</td>
					<td>{{v.chepai}}</td>
					<td>{{v.cdate.substr(0,10)}}</td>
					<td>{{v.maobing}}</td>
					
				</tr>
				<tr class="tr2" v-else  @click="jumpMyche(v)">
					<td>{{v.cid}}</td>
					<td>{{v.cname}}</td>
					<td>{{v.cphone}}</td>
					<td>{{v.type}}</td>
					<td>{{v.chepai}}</td>
					<td>{{v.cdate.substr(0,10)}}</td>
					<td>{{v.maobing}}</td>
					
				</tr>
			</table>
			
		</div>
		
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
				cname:"",
				cphone:"",
				type:"",
				chepai:"",
				maobing:"",
				myche:[],
			}
		},
		mounted() {
			this.useronline()
		},
		methods:{
			jumpMyche:function(myche){
			        this.$router.push({path:"/caozuo",query:myche})
			      },
			//添加车辆信息
			luru:function(){
				var o=this;
				$.ajax({
					url:"http://127.0.0.1:8081/java/ajax/luru",
					data:{cname:o.cname,cphone:o.cphone,type:o.type,chepai:o.chepai,maobing:o.maobing},
					success:function(r){
						if(r>0){
							alert("录入成功");
							o.$router.go(0)
						}
						
					},
					xhrFields: {
					                  withCredentials: true //传递cookie,保持session的唯一性
					                },
					                crossDomain: true,
				})
			},
			queryCheliang:function(){
				var o=this;
				$.ajax({
					url:"http://127.0.0.1:8081/java/ajax/queryCheliang",
					
					success:function(r){
						o.myche=r;
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
			              o.queryCheliang();
			
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

<style scoped="">
	.col-sm-2{
		
	}
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
	tr{
		
	}
</style>
