<template>
	<view class="u-search">
		<view class="u-content" :style="{
			backgroundColor: bgColor,
			borderRadius: shape == 'round' ? '100rpx' : '10rpx',
			border: borderStyle,
			height: height + 'rpx'
		}">
			<u-icon class="u-clear-icon" :size="30" name="search" color="#909399"></u-icon>
			<input confirm-type="search" @blur="blur" :value="value" @confirm="search" @input="inputChange" :disabled="disabled" @focus="getFocus" :focus="focus"
			 placeholder-class="u-placeholder-class" :placeholder="placeholder" class="u-input" type="text" :style="{
				 textAlign: inputAlign
			 }" />
			<view class="u-close-wrap" v-if="keyword && clearabled && focused" @touchstart="clear">
				<u-icon class="u-clear-icon" name="close" :size="16" color="#fff" @touchstart="clear"></u-icon>
			</view>
		</view>
		<view class="u-action" :class="[showActionBtn || show ? 'u-action-active' : '']" @tap="custom">
			{{actionAtext}}
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			// 搜索框形状，round-圆形，square-方形
			shape: {
				type: String,
				default: 'round'
			},
			// 搜索框背景色，默认值#f2f2f2
			bgColor: {
				type: String,
				default: '#f2f2f2'
			},
			// 占位提示文字
			placeholder: {
				type: String,
				default: '请输入关键字'
			},
			// 是否启用清除控件
			clearabled: {
				type: Boolean,
				default: true
			},
			// 是否自动聚焦
			focus: {
				type: Boolean,
				default: false
			},
			// 是否在搜索框右侧显示取消按钮
			showAction: {
				type: Boolean,
				default: true
			},
			// 取消按钮文字
			actionAtext: {
				type: String,
				default: '搜索'
			},
			// 输入框内容对齐方式，可选值为 left|center|right
			inputAlign: {
				type: String,
				default: 'left'
			},
			// 是否启用输入框
			disabled: {
				type: Boolean,
				default: false
			},
			// 开启showAction时，是否在input获取焦点时才显示
			animation: {
				type: Boolean,
				default: false
			},
			// 边框颜色，只要配置了颜色，才会有边框
			borderColor: {
				type: String,
				default: 'none'
			},
			// 输入框的初始化内容
			value: {
				type: String,
				default: ''
			},
			// 搜索框高度，单位rpx
			height: {
				type: [Number, String],
				default: 64
			}
		},
		data() {
			return {
				keyword: '',
				showClear: false, // 是否显示右边的清除图标
				show: false,
				// 标记input当前状态是否处于聚焦中，如果是，才会显示右侧的清除控件
				focused: this.focus, 
				// 绑定输入框的值
				// inputValue: this.value
			}
		},
		watch: {
			keyword(nVal) {
				// 双向绑定值，让v-model绑定的值双向变化
				this.$emit('input', nVal)
				// 触发change事件，事件效果和v-model双向绑定的效果一样，让用户多一个选择
				this.$emit('change', nVal)
			},
			value: {
				immediate: true,
				handler(nVal) {
					this.keyword = nVal;
				}
			}
		},
		computed: {
			showActionBtn() {
				if (!this.animation && this.showAction) return true;
				else return false;
			},
			// 样式，根据用户传入的颜色值生成，如果不传入，默认为none
			borderStyle() {
				if(this.borderColor) return `1px solid ${this.borderColor}`;
				else return 'none';
			}
		},
		methods: {
			// 目前HX2.6.9 v-model双向绑定无效，故监听input事件获取输入框内容的变化
			inputChange(e) {
				this.keyword = e.detail.value;
			},
			// 清空输入
			// 也可以作为用户通过this.$refs形式调用清空输入框内容
			clear() {
				this.keyword = '';
			},
			// 确定搜索
			search() {
				this.$emit('search', this.keyword);
				// 收起键盘
				uni.hideKeyboard();
			},
			// 点击右边自定义按钮的事件
			custom() {
				this.$emit('custom', this.keyword);
				// 收起键盘
				uni.hideKeyboard();
			},
			// 获取焦点
			getFocus() {
				this.focused = true;
				// 开启右侧搜索按钮展开的动画效果
				if (this.animation && this.showAction) this.show = true;
			},
			// 失去焦点
			blur() {
				this.focused = false;
				this.show = false;
			}
		}
	}
</script>

<style lang="scss" scoped>
	.u-search {
		display: flex;
		align-items: center;
	}

	.u-content {
		display: flex;
		align-items: center;
		padding: 0 18rpx;
		flex: 1;
	}
	
	.u-clear-icon {
		display: flex;
		align-items: center;
	}

	.u-input {
		flex: 1;
		font-size: 28rpx;
		line-height: 1;
		margin: 0 10rpx;
		color: $u-tips-color;
	}

	.u-close-wrap {
		width: 34rpx;
		height: 34rpx;
		display: flex;
		align-items: center;
		justify-content: center;
		background-color: rgb(200, 203, 204);
		border-radius: 50%;
	}

	.u-placeholder-class {
		color: $u-tips-color;
	}

	.u-action {
		font-size: 28rpx;
		color: $u-main-color;
		width: 0;
		overflow: hidden;
		transition: all 0.3s;
		white-space: nowrap;
		text-align: center;
	}
	
	.u-action-active {
		width: 80rpx;
		margin-left: 10rpx;
	}
</style>
