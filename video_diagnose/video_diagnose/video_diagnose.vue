<template>
	<view><trtc-room id="trtc-room" :config="trtcConfig"></trtc-room></view>
</template>

<script>
import dayjs from 'dayjs';
export default {
	data() {
		return {
			trtcConfig: {
				sdkAppID: this.tencent.trtc.appid,
				userID: null, // 用户唯一标识符
				userSig: null,
				template: 'grid' // 画面排版模式
			},
			roomId: null,
			expectEnd: null
		};
	},
	methods: {

	},
	onLoad: function(options) {
		
	},
	onShow: function() {
		
	}
};
</script>

<style lang="less">
@import url('video_diagnose.less');
</style>
