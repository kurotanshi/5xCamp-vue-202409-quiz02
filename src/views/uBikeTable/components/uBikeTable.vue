<script setup>
const props = defineProps({
	dataSource: Array,
	searchText: String,
	isSortDesc: Boolean,
	currentSort: String
});

const emit = defineEmits(['setSort']);

// 指定排序
const setSort = sortType => {
	emit('setSort', sortType);
};

// 關鍵字 Highlight
const keywordsHighlight = (text, keyword) => {
  if(keyword === '') return text;
  const reg = new RegExp(keyword, 'gi');
  return text.replace(reg, `<span style="color: red;">${keyword}</span>`);
};

</script>

<template>
	<table class="table table-striped">
		<thead>
			<tr>
				<th class="pointer" @click="setSort('sno')">
					#
					<span v-show="currentSort === 'sno'">
						<i class="fa" :class="isSortDesc ? 'fa-sort-desc' : 'fa-sort-asc'" aria-hidden="true"></i>
					</span>
				</th>
				<th>
					場站名稱
				</th>
				<th>
					場站區域
				</th>
				<th @click="setSort('available_return_bikes')" class="pointer">
					目前可用車輛
					<span v-show="currentSort === 'available_return_bikes'">
						<i class="fa" :class="isSortDesc ? 'fa-sort-desc' : 'fa-sort-asc'" aria-hidden="true"></i>
					</span>
				</th>
				<th @click="setSort('total')" class="pointer">
					總停車格
					<span v-show="currentSort === 'total'">
						<i class="fa" :class="isSortDesc ? 'fa-sort-desc' : 'fa-sort-asc'" aria-hidden="true"></i>
					</span>
				</th>
				<th>
					資料更新時間
				</th>
			</tr>
		</thead>
		<tbody>
			<tr v-for="s in dataSource" :key="s.sno">
				<td>{{ s.sno }}</td>
				<td v-html="keywordsHighlight(s.sna, searchText)"></td>
				<td>{{ s.sarea }}</td>
				<td>{{ s.available_return_bikes }}</td>
				<td>{{ s.total }}</td>
				<td>{{ (s.mday) }}</td>
			</tr>
		</tbody>
	</table>
</template>

<style lang="scss" scoped>
.pointer {
  cursor: pointer;
}

@media (max-width: 768px) {
  .sno {
    max-width: 50px; word-wrap: break-word;
  }
  .table td, .table th {
    padding: .5rem .25rem;
  }
}
</style>