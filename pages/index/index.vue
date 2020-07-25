<template>
	<view class="picture">
		<view class="box" @tap="goto"></view>
		<image style="height: 100%; width: 100%;" src="../../static/liulan.png"></image>
		<!-- <view class="text-area">
			<text class="title">{{title}}</text>
		</view> -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad() {

		},
		methods: {
			goto(){
				uni.navigateTo({
					url: './detail'
				});
			}
		}
	}
</script>

<style>
	.picture{
		width: 750rpx;
		height: 1400rpx;
	}
	.box{
		position: absolute;
		left: 570rpx;
		top: 393rpx;
		width: 115rpx;
		height: 75rpx;
		/* background-color: #F0AD4E; */
		z-index: 1;
	}
</style>
