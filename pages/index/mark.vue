<template>
	<view>
		<view class="calendar-header">
			<view>日</view>
			<view>一</view>
			<view>二</view>
			<view>三</view>
			<view>四</view>
			<view>五</view>
			<view>六</view>
		</view>
		<view class="calendar-body">
			<view v-for="(week,index) in calendar.weeks" :key="index">
				<view class="calender-body-date-week">
					<view v-for="(day,i) in week" :key="i">
						<view class="date" :class="calendar.month == day.month?calendar.date == day.date?'date-current':'':'placeholder'">{{day.date}}</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				calShow: true, // 日历组件是否打开
				dateShow: false, // 日期是否选择
				selectDay: '', // 当前选择日期
				calendar: {
					"weeks": []
				}
			}
		},
		onLoad() {
			const db = wx.cloud.database({
				env: 'test-x3gmz'
			})
			db.collection('date').add({
				data: {
					username: this.username
				},
				success: res => {
					// 在返回结果中会包含新创建的记录的 _id
					console.log('数据插入成功', this)
					console.log('返回值', res)
				},
				fail: err => {
					console.error('[数据库] [新增记录] 失败：', err)
				}
			})

			/*
			let _date = new Date()
			let year = _date.getFullYear()
			let month = _date.getMonth() + 1
			let date = _date.getDate() //日期
			let day = _date.getDay() //星期几
			let calendar = [];
			let dates = {
				firstDay: new Date(year, month - 1, 1).getDay(),
				lastMonthDays: [], // 上个月末尾几天
				currentMonthDys: [], // 本月天数
				nextMonthDays: [], // 下个月开始几天
				endDay: new Date(year, month, 0).getDay(),
				weeks: []
			}
			// 循环上个月末尾几天添加到数组
			for (let i = dates.firstDay; i > 0; i--) {
				dates.lastMonthDays.push({
					date: new Date(year, month - 1, -i + 1).getDate(),
					month: month - 1
				})
			}
			// 循环本月天数添加到数组
			for (let i = 1; i <= new Date(year, month, 0).getDate(); i++) {
				dates.currentMonthDys.push({
					date: i,
					month: month
				})
			}
			// 循环下个月开始几天 添加到数组
			for (let i = 1; i < 7 - dates.endDay; i++) {
				dates.nextMonthDays.push({
					date: i,
					month: month + 1
				})
			}
			// 拼接数组  上个月开始几天 + 本月天数+ 下个月开始几天
			calendar = calendar.concat(dates.lastMonthDays, dates.currentMonthDys, dates.nextMonthDays)
			for (let i = 0; i < calendar.length; i++) {
				if (i % 7 == 0) {
					dates.weeks[parseInt(i / 7)] = new Array(7);
				}
				dates.weeks[parseInt(i / 7)][i % 7] = calendar[i]
			}

			this.calendar.weeks = dates.weeks
			this.calendar.year = year
			this.calendar.month = month
			this.calendar.date = date
			this.calendar.day = day
			// month = month < 10 ? "0" + month
			// date = date < 10 ? "0" + date

			// console.log(this.calendar);
			*/
		}
	}
</script>

<style>
	page {
		background: #FFFFFF;
	}

	.calendar-header {
		display: flex;
	}

	.calendar-header view {
		width: 100%;
		text-align: center;
		line-height: 80rpx;
		color: #52b8f5;
	}

	.calendar-body {
		display: flex;
		flex-wrap: wrap;
	}

	.calender-body-date-week {
		display: flex;
		width: 750rpx;
		border-bottom: 1px #f5f5f5 solid;
		justify-content: space-around;
	}

	.date {
		position: relative;
		width: 100rpx;
		text-align: center;
		color: #1c1c1c;
		background: #fff;
		line-height: 100rpx;
	}

	.placeholder {
		color: #a4a4a4;
	}

	.date-current {
		background: #52b8f5;
		color: #fff;
	}
</style>
