<template>
	<view>
		<view class="header-container">
			<view class="dept_sub">
				<text @click="showDeptSubPickerHandler">{{ deptSub }}</text>
				<u-icon name="arrow-down-fill" color="#b5b5b5" size="14"></u-icon>
			</view>
			<view class="job">
				<text @click="showJobPickerHandler">{{ job }}</text>
				<u-icon name="arrow-down-fill" color="#b5b5b5" size="14"></u-icon>
			</view>
		</view>
		<view class="doctor-container">
			<view class="doctor" v-for="one in doctor">
				<u-avatar :src="one.photo" size="45"></u-avatar>
				<view class="info">
					<view class="row">
						<text class="name">{{ one.name }}</text>
						<text class="job">{{ one.job }}</text>
						<button class="btn" @tap="createVideoDiagnoseHandle(one.doctorId)">问诊</button>
					</view>
					<view class="row">
						<text class="remark">{{ one.remark }}</text>
					</view>
					<view class="row">
						<rich-text class="desc">{{ one.description }}</rich-text>
					</view>
					<view class="row">
						<u-icon
							name="rmb-circle-fill"
							color="#ff0000"
							size="18"
							:label="one.price"
							labelColor="#ff0000"
							labelSize="18"
							top="1"
						></u-icon>

						<u-icon
							name="clock-fill"
							color="#a0a0a0"
							size="18"
							label="问诊15分钟"
							labelColor="#a0a0a0"
							labelSize="16"
							top="1"
						></u-icon>
					</view>
				</view>
			</view>
			<view v-if="doctor.length == 0">
				<u-empty mode="search" icon="http://cdn.uviewui.com/uview/empty/search.png"></u-empty>
			</view>
		</view>
		<u-picker
			:show="showDeptSubPicker"
			ref="DeptSubPicker"
			:columns="deptSubColumns"
			@confirm="confirmDeptSub"
			@change="changeDeptSub"
			@cancel="cancelDeptSub"
		></u-picker>

		<u-picker
			:show="showJobPicker"
			ref="JobPicker"
			:columns="jobColumns"
			@confirm="confirmJob"
			@cancel="cancelJob"
		></u-picker>
	</view>
</template>

<script>
let dayjs = require('dayjs');
export default {
	data() {
		return {
			deptSub: '全部诊室',
			showDeptSubPicker: false,
			deptSubColumns: [],
			deptSubColumnData: [],

			job: '全部医师',
			showJobPicker: false,
			jobColumns: [['全部医师', '主任医师', '副主任医师', '主治医师', '副主治医师']],

			doctor: []
		};
	},
	methods: {
		
	},
	onLoad: function() {
		
	}
};
</script>

<style lang="less">
@import url('doctor_list.less');
</style>
