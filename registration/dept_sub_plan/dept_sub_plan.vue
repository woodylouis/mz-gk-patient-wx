<template>
	<view>
		<view class="date-container">
			<view class="item" v-for="one in dateList">
				<text class="day">{{ one.day }}</text>
				<view :class="one.date == date ? 'selector active' : 'selector'" @tap="clickDataHandle(one.date)">
					<text class="date">{{ one.dateOfMonth }}</text>
					<text :class="one.status == '无号' ? 'status gray' : 'status'">{{ one.status }}</text>
				</view>
			</view>
		</view>
		<view class="doctor" v-for="one in doctorList">
			<u-avatar :src="one.photo" size="45"></u-avatar>
			<view class="info">
				<view class="row">
					<text class="name">{{ one.name }}</text>
					<text class="job">（{{ one.job }}）</text>
					<button class="btn" @tap="clickBtnHandle(one.id, date)">挂号</button>
				</view>
				<view class="row">
					<text class="num">总量:{{ one.maximum }}</text>
					<text class="price">￥{{ one.price }}</text>
				</view>
				<view class="row">
					<rich-text class="desc">{{ one.description }}</rich-text>
				</view>
			</view>
		</view>
		<u-empty
			v-if="showEmpty"
			mode="list"
			text="无医生出诊记录"
			width="150"
			icon="http://cdn.uviewui.com/uview/empty/order.png"
		></u-empty>
	</view>
</template>

<script>
let dayjs = require('dayjs');
export default {
	data() {
		return {
			deptSubId: null,
			showEmpty: false,
			date: dayjs().format('YYYY-MM-DD'),
			dateList: [],
			doctorList: []
		};
	},
	methods: {
		
	},
	onLoad: function(options) {
		
	}
};
</script>

<style lang="less">
@import url(dept_sub_plan.less);
</style>
