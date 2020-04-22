<template>
	<div class="sample-data">
		<edit-table :columns="labels" :rows="data" @changedTable="()=>{submitDisabled=false;}"></edit-table>
		<div class="form-action">
			<button class="btn submit" type="submit" :disabled="submitDisabled">Submit</button>
		</div>
		
	</div>
</template>

<script>
import EditTable from '@/components/EditTable.vue';
export default {
	name: "SampleData",
	components:{
		EditTable
	},
	data(){
		return{
			labels: [
				{ text:"Index", field:"idx", width:"8%"},
				{ text:"Title", field:"title", width:"23%"},
				{ text:"Data1", field:"data1", width:"23%"},
				{ text:"Data2", field:"data2", width:"23%"},
				{ text:"Amount", field:"amount", width:"23%"},
			],
			data: [],
			submitDisabled: true
		}
	},

	created(){
		this.fakeFetch().then((items) => {
			this.data = items;
		});
	},
	methods:{
		fakeFetch() {
			return new Promise((resolve, reject) => {
				const count = 5;
				let result = [];
				for (let ii = 0; ii < count; ii++) {
					result.push({
						idx : ii,
						title: "Title" + ii,
						data1: "Data1<>" + ii,
						data2: "Data2<>" + ii,
						amount: 100.5 + parseFloat(ii * 1000)
					});
				}
				resolve(result);
			})
		}
	}
}
</script>

<style scoped>
.sample-data{
	width: 80%;
	margin: 30px auto;
}
.btn.submit{
	height: 60px;
	width: 120px;
	border-radius: 30px;
	border: 2px solid #1ECD97;
	font-size: 18px;
	text-align: center;
	color: #1ECD97
}
.btn.submit:hover{
	background: #1ECD97;
	color: white;
	cursor: pointer;
}
.btn.submit:disabled{
	background: #cccccc;
	border: 2px solid #999999;
}
.btn.submit:disabled:hover{
	background: #cccccc;
	cursor: no-drop;
	color: #1ECD97;

}
.form-action{
	margin-top: 30px;
	display: flex;
	justify-content: flex-end;
}
</style>