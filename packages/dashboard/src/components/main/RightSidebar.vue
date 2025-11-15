<template>
  <div class=" fit">
    <q-table
      class="fit"
	title="示例数据"
      :rows="rows"
      :columns="columns"
      row-key="name"

      :hide-pagination="true"
      :rows-per-page-options="[0]"
      :flat="true"
    >
      <slot name="top-right">
        <q-btn dense flat round icon="menu" />
      </slot>
    </q-table>
  </div>
</template>

<script>
import { useMainStore } from "stores/main-store";
import { defineComponent } from "vue";

export default defineComponent({
	name: "RightSidebar",
	data: () => ({
		columns: [
			{
				name: "name",
				required: true,
				label: "甜点 (每100g)",
				align: "left",
				field: (row) => row.name,
				format: (val) => `${val}`,
				sortable: true,
			},
			{
				name: "calories",
				align: "center",
				label: "卡路里",
				field: "calories",
				sortable: true,
			},
			{ name: "fat", label: "脂肪 (g)", field: "fat", sortable: true },
			{ name: "carbs", label: "碳水 (g)", field: "carbs" },
			{ name: "protein", label: "蛋白质 (g)", field: "protein" },
			{ name: "sodium", label: "钠 (mg)", field: "sodium" },
			{
				name: "calcium",
				label: "钙 (%)",
				field: "calcium",
				sortable: true,
				sort: (a, b) => Number.parseInt(a, 10) - Number.parseInt(b, 10),
			},
			{
				name: "iron",
				label: "铁 (%)",
				field: "iron",
				sortable: true,
				sort: (a, b) => Number.parseInt(a, 10) - Number.parseInt(b, 10),
			},
		],
		rows: [
			{
				name: "冻酸奶",
				calories: 159,
				fat: 6.0,
				carbs: 24,
				protein: 4.0,
				sodium: 87,
				calcium: "14%",
				iron: "1%",
			},
			{
				name: "冰淇淋夹心",
				calories: 237,
				fat: 9.0,
				carbs: 37,
				protein: 4.3,
				sodium: 129,
				calcium: "8%",
				iron: "1%",
			},
			{
				name: "闪电泡芙",
				calories: 262,
				fat: 16.0,
				carbs: 23,
				protein: 6.0,
				sodium: 337,
				calcium: "6%",
				iron: "7%",
			},
			{
				name: "纸杯蛋糕",
				calories: 305,
				fat: 3.7,
				carbs: 67,
				protein: 4.3,
				sodium: 413,
				calcium: "3%",
				iron: "8%",
			},
			{
				name: "姜饼",
				calories: 356,
				fat: 16.0,
				carbs: 49,
				protein: 3.9,
				sodium: 327,
				calcium: "7%",
				iron: "16%",
			},
			{
				name: "软心豆粒糖",
				calories: 375,
				fat: 0.0,
				carbs: 94,
				protein: 0.0,
				sodium: 50,
				calcium: "0%",
				iron: "0%",
			},
			{
				name: "棒棒糖",
				calories: 392,
				fat: 0.2,
				carbs: 98,
				protein: 0,
				sodium: 38,
				calcium: "0%",
				iron: "2%",
			},
			{
				name: "蜂巢糖",
				calories: 408,
				fat: 3.2,
				carbs: 87,
				protein: 6.5,
				sodium: 562,
				calcium: "0%",
				iron: "45%",
			},
			{
				name: "甜甜圈",
				calories: 452,
				fat: 25.0,
				carbs: 51,
				protein: 4.9,
				sodium: 326,
				calcium: "2%",
				iron: "22%",
			},
			{
				name: "奇巧巧克力",
				calories: 518,
				fat: 26.0,
				carbs: 65,
				protein: 7,
				sodium: 54,
				calcium: "12%",
				iron: "6%",
			},
		],
	}),
	methods: {
		openFileDetails: (row) => {
			// this.$emit('updateDrawer', true)  // TODO: enable
			// console.log(row)
		},
	},
	computed: {
		selectedBucket: function () {
			return this.$route.params.bucket;
		},
		selectedApp: function () {
			return this.$route.name.split("-")[0];
		},
	},
	mounted() {
		this.$bus.on("openFileDetails", this.openFileDetails);
	},
	beforeUnmount() {
		this.$bus.off("openFileDetails");
	},
	setup() {
		const mainStore = useMainStore();

		return {
			mainStore,
		};
	},
});
</script>
