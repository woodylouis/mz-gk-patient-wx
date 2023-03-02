<template>
	<view>
		<view class="main-container">
			<view>
				<u-count-down :time="time" format="mm:ss" autoStart @change="onChange">
					<view class="time">
						<text class="desc">距离问诊{{ startOrEnd }}</text>
						<text :class="startOrEnd == '结束' ? 'minute red' : 'minute'">{{ timeData.minutes }}</text>
						<text class="unit">分</text>
						<text :class="startOrEnd == '结束' ? 'second red' : 'second'">{{ timeData.seconds }}</text>
						<text class="unit">秒</text>
					</view>
				</u-count-down>
			</view>

			<view class="title">请上传诊断材料</view>
			<view class="files">
				<u-upload
					:fileList="fileList"
					@afterRead="afterRead"
					@delete="deleteImage"
					multiple
					:maxSize="2 * 1024 * 1024"
					:maxCount="20"
					:previewFullImage="true"
				></u-upload>
			</view>
			<view class="operate">
				<view class="btn red" @tap="deleteAllImageHandle">清空诊断材料</view>
				<view :class="enableBtn ? 'btn green' : 'btn gray'" @click="enterHandle">进入问诊室</view>
			</view>
		</view>
		<view class="desc-container">
			<view class="title">视频问诊说明</view>
			<view class="desc">
				<text class="num">1.</text>
				<text>
					在视频问诊之前以先上传相关的诊断材料照片，但是最多不能超过20张照片，而且每张照片不能超过2M体积。
				</text>
			</view>
			<view class="desc">
				<text class="num">2.</text>
				<text>
					视频问诊开始的时候，您可以点击【进入问诊室】按钮开始视频问诊。在视频问诊开始之前，请耐心等待。
				</text>
			</view>
			<view class="desc">
				<text class="num">3.</text>
				<text>
					建议您的手机连接WIFI网络，以保证最佳问诊质量。在问诊期间不要随便走动，避免网络信号波动，影响问诊音视频质量。
				</text>
			</view>
			<view class="desc">
				<text class="num">4.</text>
				<text>
					视频问诊仅作为初步诊断，存在误诊几率，不能以此当做准确诊断。建议您结合线下门诊的诊断结果及时就医。
				</text>
			</view>
			<view class="desc">
				<text class="num">5.</text>
				<text>
					如果遇到医疗系统技术故障或者其他不可抗力因素，无法进行视频问诊。请拨打【800-12388】客户热线，联系客服人员予以解决或者退款。
				</text>
			</view>
		</view>
	</view>
</template>

<script>
import dayjs from 'dayjs';
export default {
	data() {
		return {
			videoDiagnoseId: null,
			expectStart: null,
			expectEnd: null,
			doctorId: null,
			startOrEnd: '开始',
			enableBtn: false,
			time: null,
			timeData: {},
			fileList: []
		};
	},
	methods: {
		
	},
	onLoad: function(options) {
		
	}
};
</script>

<style lang="less">
@import url('prepare_diagnose.less');
</style>
