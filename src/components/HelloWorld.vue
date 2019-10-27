<template>

	<table class="recommend_table" cellspacing="0">
    <tr>
        <th>姓名</th>
        <th @click="sort('age')">年龄</th>
        <th >性别</th>
    </tr>
    <tr v-for="(item,index) in list" :key="index">
        <td>{{item.name}}</td>
        <td>{{item.age}}</td>
        <td>{{item.sex}}</td>
    </tr>
	</table>
</template>

<script>
import axios from 'axios'
export default {
name: 'HelloWorld',
data() {
  return{
    list:[],
    sortType:'age'
  } 
},
methods:{
	getData(){
		let that = this
		axios.get('http://localhost:8080/data.json')
		.then(function (res) {
			console.log(res);
			that.list=res.data.data;
		})
		.catch(function (error) {
			console.log(error);
		})
	},
	sort(type) {
		this.sortType = type;
        this.list.sort(this.compare(type));
	},
	compare(attr) {
		return function(a,b){
			var val1 = a[attr];
			var val2 = b[attr];
			return val1 - val2;
		}
	}
},
mounted(){
	this.getData();
},

}
</script>


<style scoped>
li{color:#000}
li:hover{color:red}
li:nth-child(odd){background:blue}
li:nth-child(even){background:green}
</style>
