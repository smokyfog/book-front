<template>
	<view class="home-page wrap">
		<u-swiper
			:height="300"
			:list="list"
			:title="title"
			:effect3d="effect3d"
			:indicator-pos="indicatorPos"
			:mode="mode"
			:interval="3000"
			@click="click"
			class="swiper_wrap"
		/>
		<BasicNote
			title="猜你喜欢"
			:items="guess_likes"
		>
			<template v-slot:right>
				<view>换一换</view>
			</template>
		</BasicNote>
		<u-row>
			<u-col span="9">
				<view class="demo-layout bg-purple-light">2</view>
			</u-col>
		</u-row>
	</view>
</template>

<script>
	import BasicNote from '../../components/note_basic/note_basic.vue'
	export default {
		components: {
			BasicNote
		},
		data() {
			return {
				list: [{
						image: 'http://cdn.uviewui.com/uview/swiper/1.jpg',
						title: '昨夜星辰昨夜风，画楼西畔桂堂东'
					},
					{
						image: 'http://cdn.uviewui.com/uview/swiper/2.jpg',
						title: '身无彩凤双飞翼，心有灵犀一点通'
					},
					{
						image: 'http://cdn.uviewui.com/uview/swiper/3.jpg',
						title: '谁念西风独自凉，萧萧黄叶闭疏窗，沉思往事立残阳'
					}
				],
				guess_likes: [
					{
						url: "https://img.cn6154.com/uploadimg/img/2018/0602/1527935559656.jpg",
						title: "九宫歌"
					},
					{
						url: "https://img.cn6154.com/uploadimg/img/2018/0602/1527935559656.jpg",
						title: "九宫歌"
					},
					{
						url: "https://img.cn6154.com/uploadimg/img/2018/0602/1527935559656.jpg",
						title: "九宫歌"
					},
					{
						url: "https://img.cn6154.com/uploadimg/img/2018/0602/1527935559656.jpg",
						title: "九宫歌"
					},
					{
						url: "https://img.cn6154.com/uploadimg/img/2018/0602/1527935559656.jpg",
						title: "九宫歌"
					},
					{
						url: "https://img.cn6154.com/uploadimg/img/2018/0602/1527935559656.jpg",
						title: "九宫歌"
					}
				],
				title: false,
				mode: 'round',
				indicatorPos: 'bottomCenter',
				effect3d: false,
			}
		}
	}
</script>

<style scoped lang="scss">
	.home-page {
		background: #f5f5f5;
	}
</style>