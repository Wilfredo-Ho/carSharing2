<template>
  	<div class="row">
  		<div class="sidebar col-md-2" ref="side">
  			<div class="btn-wrapper">
  				<div class="input-group">
  					<input type="text" class="form-control" placeholder="请输入车牌号或PNO码" v-model="searchText">
  					<span class="input-group-btn">
  						<button class="btn btn-primary" @click="clearInput" type="button"><icon name="search"></icon></button>
  					</span>
  				</div>
  				<div class="clear-wrapper" @click="clearInput">
  					<icon name="close" class="close-btn"></icon>
				</div>
  			</div>
  			<div class="tab">
  				<ul>
  					<router-link tag="li" :to="{path: '/member/list'}" class="item">会员列表</router-link>
					<router-link tag="li" :to="{path: '/member/verify'}" class="item">会员审核</router-link>
  				</ul>
  			</div>
  		</div>
  		<div class="content" :class="cont">
  			<div class="status">
  				<div class="btn-toggle">
  					<button class="btn btn-xs btn-gray" @click="toggle"><icon name="outdent"></icon></button>
  				</div>
  				<div class="breadcrumb">
  					<li>会员管理</li>
  					<li class="active">{{currentMenu}}</li>
  				</div>
  			</div>
  			<div class="page-wrapper">
  				<router-view></router-view>
  			</div>
  		</div>
  	</div>
  
</template> 
 
<script> 
export default { 

  data () { 
    return { 
 		searchText: "",
 		cont: 'col-md-10',
 		currentMenu: '会员列表'
    }
  },
  methods: {
  	clearInput () {
  		this.searchText = '';
  	},
  	toggle () {
  		let sidename = this.$refs.side.className;
  		if(sidename.indexOf('collapse')<0){
  			this.$refs.side.className = 'collapse'
  			this.cont = 'col-md-12'
  		}else{
  			this.$refs.side.className = 'sidebar col-md-2'
  			this.cont = 'col-md-10'
  		}
  	},
  	nameToggle(){
  		// 获取当前路由
  		let val = this.$route.path;
  		if(val.indexOf('list')<0){
  			this.currentMenu = "会员列表"
  		}else{
  			this.currentMenu = "会员审核"
  		}
  	}
  },
  watch: {
  	// 监听路由变化
  	"$route": "nameToggle"
  }
}
</script> 
 
<style scoped>
ul{
	list-style: none;
}
.row{
	margin: 0;
} 
.sidebar{
	
}
.btn-wrapper{
	position: relative;
}
.btn-wrapper .close-btn{
	position: absolute;
	top: 20%;
	right: 18%;
	z-index: 10;
	color: #DDDDDD;
}
.tab{
	margin-top: 8px;
}
ul{
	padding: 0;
}
.item{
	height:62px;
	line-height: 62px;
	text-align: center;
	background-color: #f8f8f8;
	font-size: 18px;
	color: #5fc0ed;
	cursor: pointer;
}
.item.active{
	background-color: #f0f0f0;
	color: #768595;
	border-left: 8px solid #2a80c9;
}
.content{
	padding:0;
}
.status{

}
.btn-toggle{
	display: inline-block;
	border: 1px solid #e3e3e3;
	border-bottom: 0;
	border-top: 0;
}
.btn-gray{
	background-color: #fff;
}
.breadcrumb{
	display: inline-block;
	background-color: #fff;
	margin-bottom: 0;
}
.page-wrapper{
	background-color: #ecf2f7;
}
.clearfix{
	display: none;
}
</style> 