<template>
	<view class="view_box">
		<view class="title-box">
			<view class="title-left">
				<view class="left_block" />
				{{ title }}
			</view>
			<view class="title-right">
				<slot name="right"></slot>
			</view>
		</view>
		<view :col="3" class="book_info_wrap">
			<view
				span="4"
				v-for="(item, idx) in items"
				:key="item.title + idx + 'guess'"
				class="book_info_item"
			>
				<view class="note_box">
					<img :src="item.url" alt="">
					<view class="book_title">{{ item.title }}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			items: {
				type: Array,
				default: []
			},
			title: {
				type: String,
				default: ''
			}
		},
		data() {
			return {
			};
		}
	}
</script>

<style lang="scss">
	.view_box {
		background: #fff;
		margin-bottom: 3px;
	}
	.notes_wrap {
		display: flex;
		flex-wrap: wrap;
	}
	.note_box {
		img {
			max-width: 100%;
			max-height: 100%;
		}
	}
	.book_info_wrap {
		position: relative;
		display: flex;
		flex-wrap: wrap;
		padding: 10px 0;
		.book_info_item {
			width: 33.3333%;
			border: none;
		}
		.u-grid-item-box {
			border: none;
		}
		img {
			width: 200rpx;
			height: 280rpx;
		}
		.note_box {
			height: 350rpx;
			display: flex;
			align-items: center;
			flex-direction: column;
			justify-content: center;
		}
		.book_title {
			white-space: nowrap;
			overflow: hidden;
			text-overflow: ellipsis;
			max-width: 78%;
			color: #616161;
			line-height: 24px;
		}
		@media only screen and (-webkit-min-device-pixel-ratio: 1.0) {
			&::after {
				content: '';
				width: 100%;
				position: absolute;
				top: 0;
				left: 0;
				border-top: 1px solid #eaeaea;
				-webkit-transform-origin: top left;
			}
		}
		@media only screen and (-webkit-min-device-pixel-ratio: 2.0) {
			&::after {
				content: '';
				width: 200%;
				position: absolute;
				top: 0;
				left: 0;
				border-top: 1px solid #eaeaea;
				-webkit-transform: scale(0.5, 0.5);
				transform: scale(0.5, 0.5);
				-webkit-transform-origin: top left;
			}
		}
		
		/* 3倍屏 */
		@media only screen and (-webkit-min-device-pixel-ratio: 3.0) {
			&::after {
				content: '';
				width: 300%;
				position: absolute;
				top: 0;
				left: 0;
				border-top: 1px solid #eaeaea;
				-webkit-transform: scale(0.3333333333333);
				transform: scale(0.5, 0.5);
				-webkit-transform-origin: top left;
			}
		}
	}
</style>
