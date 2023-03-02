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
		//查询某个诊室7天出诊情况
		searchCanRegisterInDateRange: function(ref, deptSubId) {
		    let startDate = dayjs().format('YYYY-MM-DD');
		    let endDate = dayjs().add(6, 'day').format('YYYY-MM-DD');
		    let data = {
		        deptSubId: deptSubId,
		        startDate: startDate,
		        endDate: endDate
		    };
		    ref.ajax(ref.api.searchCanRegisterInDateRange, 'POST', data,
		        function(resp) {
		            let result = resp.data.result;
		            //定义工具数组
		            let array = ['日', '一', '二', '三', '四', '五', '六'];
		            for (let one of result) {
		                //把星期几的阿拉伯数字转换成汉字数字
		                let day = array[dayjs(one.date).day()];
		                one.day = day;
		                one.dateOfMonth = dayjs(one.date).date();
		            }
		            ref.dateList = result;
		        },
		        false
		    );
		},
		
		//查找某天科室医生出诊列表
		searchDeptSubDoctorPlanInDay: function(ref) {
		    let data = {
		        deptSubId: ref.deptSubId,
		        date: ref.date
		    };
		
		    ref.ajax(ref.api.searchDeptSubDoctorPlanInDay, 'POST', data,
		        function(resp) {
		            let result = resp.data.result;
		            //把头像相对路径合成绝对路径
		            for (let one of result) {
		                one.photo = `${ref.minioUrl}/${one.photo}`;
		            }
		            ref.doctorList = result;
		            if (result.length == 0) {
		                ref.showEmpty = true;
		            } else {
		                ref.showEmpty = false;
		            }
		        },
		        false
		    );
		},

	},
	onLoad: function(options) {
	    let that = this;
	    //取出URL参数
	    let deptSubId = options.deptSubId;
	    let deptSubName = options.deptSubName;
	
	    that.deptSubId = deptSubId;
	    //设置当前页面标题栏文字
	    uni.setNavigationBarTitle({
	        title: deptSubName
	    });
	  
	    that.searchCanRegisterInDateRange(that,deptSubId)
	    that.searchDeptSubDoctorPlanInDay(that);
	}

};
</script>

<style lang="less">
@import url(dept_sub_plan.less);
</style>
