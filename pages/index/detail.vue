<template>
	<view class="picture">
		<view class="box" style="top: 1003rpx;">{{list.name}}</view>
		<view class="box" style="top: 1104rpx;">{{list.number}}</view>
		<view class="box" style="top: 1205rpx;">{{list.college}}</view>
		<view class="box" style="top: 1306rpx;">{{list.classNumber}}</view>
		<view class="box" style="top: 1407rpx;">{{list.teacher}}</view>
		<view class="box" style="top: 867rpx; left: 0rpx; width: 100%; font-weight: 800; font-size: 29rpx; text-align: center;">{{time}}</view>
		<view class="box" style="top: 1920rpx; left: 82rpx; text-align: left; color: #c0c2c3;">{{date}}</view>
		<view class="box" style="top: 2150rpx; left: 82rpx; text-align: left; color: #c0c2c3;">{{date}}</view>
		<image :src="signImg" class="sign" mode="widthFix"></image>
		<image style="height: 100%; width: 100%;" src="../../static/detail_2.0.png"></image>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: {
					name: '张伟',
					number: '17054396',
					college: '计算机学院',
					classNumber: '17059611',
					teacher: '张林达',
				},
				time: null,
				date: null,
				signImg: null
			}
		},
		onLoad() {
			this.timeDifference()
			this.startCountDown()
			this.setDate()
			this.setSignNumber()
			this.list = getApp().globalData
			console.log(this.list);
		},
		methods: {
			goto() {
				uni.navigateTo({
					url: './detail'
				});
			},
			
			timeDifference() {
				let time = new Date()
				let month = time.getMonth() + 1
				let date = time.getDate()
				let hours = time.getHours()
				if(hours<10){hours = '0'+hours}
				let minutes = time.getMinutes()
				if(minutes<10){minutes = '0'+minutes}
				let seconds = time.getSeconds()
				if(seconds<10){seconds = '0'+seconds}
				let str = `当前时间：${month}月${date}日 下午${hours}:${minutes}:${seconds}`
				this.time = str
			},
			
			setDate() {
				let time = new Date()
				let year = time.getFullYear()
				let month = time.getMonth() + 1
				let date = time.getDate()
				let str = `${year}年${month}月${date}日`
				this.date = str
			},
			
			setSignNumber() {
				let time = new Date()
				this.signImg = `../../static/sign${time.getTime() % 2 + 1}.png`
			},
		
			startCountDown() {
				let that = this
				setTimeout(function() {
					that.timeDifference()
					that.startCountDown()
				}, 1000)
			}
		}
	}
</script>

<style>
	.picture {
		width: 750rpx;
		height: 3490rpx;
	}

	.box {
		position: absolute;
		left: 385rpx;
		/* top: 1003rpx; */
		width: 300rpx;
		height: 150rpx;
		font-size: 30rpx;
		color: #3d3a3d;
		text-align: right;
		z-index: 1;

		display: inline-block;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
	}
	
	.sign {
		width: 600rpx;
		position: absolute;
		top: 3075rpx;
		z-index: 3;
		margin: 0rpx 75rpx;
	}
</style>
