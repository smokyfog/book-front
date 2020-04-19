<script>
	export default {
		onLaunch: function() {
			console.log('App Launch');
			// #ifdef APP-NVUE
			plus.screen.lockOrientation('portrait-primary');
			var domModule = weex.requireModule('dom');
			domModule.addRule('fontFace', {
				'fontFamily': "texticons",
				'src': "url('./static/text-icon.ttf')"
			});
			// #endif
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="scss">
	/*每个页面公共css */
	.title-box {
		display: flex;
		justify-content: space-between;
		padding: 8px;
		.title-left {
			display: flex;
			align-items: center;
			font-weight: 400;
			font-size: 14px;
			color: #4d4d51;
			.left_block {
				height: 13px;
				width: 3px;
				margin-right: 5px;
				background-color: #2B85E4;
			}
		}
		.title-right {
			color: #0078e0;
			font-size: 12px;
			font-weight: 400;
		}
	}
</style>
