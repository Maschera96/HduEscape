<template>
	<view>
		<form>
			<view class="cu-form-group" style="margin-top: 20rpx;">
				<view class="title">姓名</view>
				<input style="width: 500rpx;" v-model='list.name' type="text" placeholder="姓名"></input> 
			</view>
			<view class="cu-form-group">
				<view class="title">学号</view>
				<input style="width: 500rpx;" v-model='list.number' type="text" placeholder="学号"></input> 
			</view>
			<view class="cu-form-group">
				<view class="title">学院</view>
				<input style="width: 500rpx;" v-model='list.college' type="text" placeholder="学院"></input> 
			</view>
			<view class="cu-form-group">
				<view class="title">班级</view>
				<input style="width: 500rpx;" v-model='list.classNumber' type="text" placeholder="班级"></input> 
			</view>
			<view class="cu-form-group">
				<view class="title">辅导员</view>
				<input style="width: 500rpx;" v-model='list.teacher' type="text" placeholder="辅导员"></input> 
			</view>
		</form>
		<view style="margin-top: 30rpx; font-size: 30rpx; color: #999999; padding-left: 10rpx;">*每条数据均为必填，后三条数据虽有默认值，但是可修改</view>
		<view style="margin-top: 15rpx; font-size: 30rpx; color: #999999; padding-left: 10rpx;">*新增缓存功能，不清缓存便可无需重复输入</view>
		<button type="primary" class="btn" style="margin-top: 80rpx; align-content: center;" @tap="goto()">提交</button>
		<!-- <button type="primary" class="btn" style="margin-top: 80rpx; align-content: center;" @tap="gotoMark()">打卡</button> -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: {
					name: null,
					number: null,
					college: '计算机学院',
					classNumber: '17059611',
					teacher: '张林达',
				}
			}
		},
		onLoad() {
			// this.list.name = wx.getStorageInfoSync('name') || null
			// this.list.number = wx.getStorageInfoSync('number') || null
			// this.list.college = wx.getStorageInfoSync('college') || '计算机学院'
			// this.list.classNumber = wx.getStorageInfoSync('classNumber') || '17059611'
			// this.list.teacher = wx.getStorageInfoSync('teacher') || '张林达'
			if(wx.getStorageSync('list')){
				this.list = wx.getStorageSync('list')
			}
		},
		methods: {
			goto(){
				for(let i in this.list){
					if(!this.list[i]){
						wx.showToast({
							title: '请全部填写',
							icon: 'none'
						})
						return
					}
				}
				
				wx.setStorageSync('list',this.list)
				getApp().globalData = this.list
				
				uni.navigateTo({
					url: './index'
				});
			},
			
			gotoMark(){
				uni.navigateTo({
					url: './mark'
				})
			}
		}
	}
</script>

<style>
	.cu-form-group {
		background-color: #ffffff;
		padding: 1rpx 30rpx;
		display: flex;
		align-items: center;
		min-height: 80rpx;
		justify-content: space-between;
		font-size: 33rpx;
	}
		
	.btn{
		width: 90%;
		height: 80rpx;
		line-height: 80rpx;
		border-radius: 10rpx;
		font-size: 35rpx;
	}
</style>
