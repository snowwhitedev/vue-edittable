<template>
	<table class="edit-table" cellpadding="0" cellspacing="0">
		<thead>
			<slot name="columns">
				<th v-for="column in columns" :key="column.text" :width="column.width">
					{{column.text}}
				</th>
			</slot>
			<!-- <tr>
			<th v-for="(col, ii) in columns" :key="ii">{{ col.text }}</th>
			</tr> -->
		</thead>
		<tbody v-click-outside="onBlurBody">
			<tr v-for="(row, rowIndex) in rows" :key="rowIndex">
				<td v-for="column in columns" :key="column.text" :class="{activeCell:isFocused(rowIndex, column.field)}">
					<!-- <input type="text" :value="row[column.field]" /> -->
					<edit-table-cell v-model="row[column.field]" 
						@input="cellInput()"
						@onClick="onActiveCell(rowIndex, column.field)" 
						:inputStatus="isFocused(rowIndex, column.field)" 
						> </edit-table-cell>
				</td>
			</tr>
		</tbody>
	</table>
</template>

<script>
import EditTableCell from '@/components/EditTableCell';
import ClickOutside from 'vue-click-outside';
export default {
	name: 'EditTable',
	components:{
		EditTableCell
	},
	props: {
		columns: Array,
		rows: Array
	},
	directives:{
		ClickOutside
	},
	data(){
		return{
			activeRow: '',
			activeCol: ''
		}
		
	},
	created(){
		let iii = 10;
	},
	methods:{
		cellInput(val){
			this.$emit("changedTable");
		},
		onActiveCell(rowIndex, colField){
			this.activeRow = rowIndex;
			this.activeCol = colField;
		},
		onBlurBody(){
			this.activeRow = '';
			this.activeCol = '';
		},
		isFocused(row, col){
			
			if (this.activeRow === row && this.activeCol === col){
				return true;
			}
			return false;
		}
	}
}
</script>

<style scoped>
table.edit-table{
	width: 100%;
	border: 1px solid #cccccc;
	
}
table.edit-table th{
	border: 0.5px solid #cccccc;
	padding: 8px 10px;
	
}
table.edit-table td{
	border: 0.5px solid #cccccc;
	padding: 5px 10px;
}
table.edit-table td.activeCell{
	border: 2px solid green;
}
</style>
