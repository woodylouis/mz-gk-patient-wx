<template>
	<view>
		<view class="registration" v-for="(one, index) of list">
			<view class="calendar">
				<view class="month">{{ one.month }}月</view>
				<view class="day">{{ one.day }}日</view>
			</view>
			<view class="content">
				<view class="row">
					<text class="deptSubName">{{ one.name }}（{{ one.job }}）</text>
					<view class="more" @tap="moreHandle(one.id)">
						<text>more</text>
						<u-icon name="arrow-right" color="#aaa" size="14"></u-icon>
					</view>
				</view>
				<view class="row">
					<text class="address">地址：{{ one.location }}</text>
				</view>
				<view class="row">
					<text class="datetime">时间：{{ one.date }} {{ one.time }}</text>
				</view>
				<view class="unpaid" v-if="one.paymentStatus == 1 && !one.discarded">
					<u-button type="primary" size="small" @click="payHandle(one.id, index)">待支付</u-button>
				</view>
				<view class="paid" v-if="one.paymentStatus == 2">已支付</view>
				<view class="refund" v-if="one.paymentStatus == 3">已退款</view>
				<view class="discarded" v-if="one.paymentStatus == 4">已过期</view>
			</view>
		</view>
	</view>
</template>

<script>
let dayjs = require('dayjs');
const isBetween = require('dayjs/plugin/isBetween');
dayjs.extend(isBetween);
export default {
	data() {
		return {
			list: [],
			page: 1,
			length: 50,
			json: {
				'1': '08:00',
				'2': '08:30',
				'3': '09:00',
				'4': '09:30',
				'5': '10:00',
				'6': '10:30',
				'7': '11:00',
				'8': '11:30',
				'9': '13:00',
				'10': '13:30',
				'11': '14:00',
				'12': '14:30',
				'13': '15:00',
				'14': '15:30',
				'15': '16:00'
			},
			reload: true
		};
	},
	methods: {
		
	},
	onShow: function() {
		
	},
	onReachBottom: function() {
		
	}
};
</script>

<style lang="less">
@import url(registration_list.less);
</style>
