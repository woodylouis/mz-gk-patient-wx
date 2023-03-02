<template>
	<view>
		<view class="doctor">
			<u-avatar :src="photo" size="45"></u-avatar>
			<view class="info">
				<view class="row">
					<text class="name">{{ name }}</text>
					<text class="job">（{{ job }}）</text>
				</view>
				<view class="row">
					<text class="remark">{{ remark }}</text>
				</view>
				<view class="row">
					<rich-text class="desc">{{ description }}</rich-text>
				</view>
			</view>
		</view>
		<view class="schedule-container">
			<view>
				<text class="title">选择挂号时间</text>
				<u-grid :border="false" col="4">
					<u-grid-item v-for="one in schedule" :key="one.slot">
						<text
							:class="one.style"
							@click="clickScheduleHandler(one.workPlanId, one.scheduleId, one.slot)"
						>
							{{ one.range }}
						</text>
					</u-grid-item>
				</u-grid>
			</view>
			<u-parse :content="notice"></u-parse>
			<u-button type="primary" size="large" @click="submitHandler">挂号费{{ price }}元，去支付</u-button>
		</view>
	</view>
</template>

<script>
const dayjs = require('dayjs');
const isBetween = require('dayjs/plugin/isBetween');
dayjs.extend(isBetween);
export default {
	data() {
		return {
			workPlanId: null,
			scheduleId: null,
			date: '',
			deptSubId: null,
			doctorId: null,
			name: '',
			photo: '',
			job: '',
			remark: '',
			description: '',
			price: '',
			slot: null,
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
			schedule: [],
			notice: `
				<ol class='notice-list'>
					<li class='notice-item'>挂号平台提供次日起七天的预约服务，用户可预约中医院的大部分科室次日起至七天的就诊号源。</li>
					<li class='notice-item'>因为医生工作繁忙，可能更改或者取消预约时间，届时会第一时间通知您，请留意短信通知。</li>
					<li class='notice-item'>如果您在就诊当天不能前往医院取号就诊，请提前通过挂号平台取消预约，否则会因造成号源的浪费，请您谅解。</li>
				</ol>
			`
		};
	},
	methods: {
		
	},
	onLoad: function(options) {
		
	}
};
</script>

<style lang="less">
@import url(doctor_schedule.less);
</style>
