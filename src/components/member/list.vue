<template>
  	<div class="list-wrapper">
  		<div class="search">
  			
  		</div>
  		<div class="table-wrapper">
  			<table data-toggle="table" data-url="listData">
          <thead>
            <tr>
              <th v-for="item in listCol" :data-field="item.field">{{item.title}}</th>
            </tr>
          </thead>   
        </table>
  		</div>
  	</div>
  
</template> 
 
<script> 
const OK_STATUS = 0;
// import BootstrapTable from 'vue-bootstrap-table'

export default { 

  data () { 
    return { 
 		listCol: [
 			{
 				field: "id",
 				title: "用户ID"
 			},
 			{
 				field: "name",
 				title: "姓名"
 			}
 		],
 		listData: [
			{
				id: 0,
				name: "Miss Yang"
			},
			{
				id: 1,
				name: "Mr He"
			}
 		],
 		option: {}
    }; 
  },
  methods:{
  	tableInit(obj, res){
  		console.log(res)
		obj.boostrapTable({
			columns: this.listCol,

		})  		
  	}
  },
  created () {
  	this.$http.get('/api/memberList').then((res) => {
  		if(res.body.errno === OK_STATUS){
  			// 初始化bootstrap table
  			// this.listData = res.body.data;
  		}
  	}, (err) => {
  		alert(err);
  	})
  }
}; 
</script> 
 
<style scoped> 
  .table-wrapper{
  	height:300px;
  	border-bottom: 1px solid #000;
  }
</style> 