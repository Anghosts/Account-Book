<template>
	<view class="container">
		<view class="header">
			<view class="bottom">
				<view class="month-expend">
					<text class="month">{{setMonth}}</text>
					<text class="expend">月 · 支出</text>
				</view>
				<view class="expend-price">0.00</view>
				<view class="income-price">
					<text class="income">本月收入</text>
					<text class="price">0.00</text>
				</view>
			</view>
		</view>
		
		<uni-list class="date-list">
			<uni-list-item :title="item.title" :note="item.date" link v-for="(item,index) in dateList" :key="index">
				<template v-slot:footer>
					<view class="expend-income">
						<text class="expend">{{item.expend | tofixed}}</text>
						<text class="income">{{item.income | tofixed}}</text>
					</view>
				</template>
			</uni-list-item>
		</uni-list>
			
		<view class="bottom-nav">
			<button class="plus-btn" hover-class="plus-btn-hover">记一笔</button>
		</view>
	</view>
</template>

<script>
	import dayjs from 'dayjs'
	
	export default {
		data() {
			return {
				dateList: [{
					title: '今天',
					date: '',
					expend: 0,
					income: 0
				}, {
					title: '本周',
					date: '',
					expend: 0,
					income: 0
				}, {
					title: '本月',
					date: '',
					expend: 0,
					income: 0
				}, {
					title: '本年',
					date: '',
					expend: 0,
					income: 0
				}, ]
			}
		},
		methods: {
			// 今天
			today() {
				this.dateList[0].date = dayjs().format('M月D日');
			},
			// 本周
			week() {
				let start = dayjs().day(1).format('M月D日');
				let end = dayjs().day(7).format('M月D日');
				this.dateList[1].date = `${start} - ${end}`
			},
			// 本月
			month() {
				let start = dayjs().startOf('month').format('M月D日');
				let end = dayjs().endOf('month').format('M月D日');
				this.dateList[2].date = `${start} - ${end}`
			},
			// 本年
			year() {
				this.dateList[3].date = dayjs().format('YYYY年');
			}
		},
		computed: {
			// 本月
			setMonth() {
				const date = new Date()
				return date.getMonth() + 1
			},
		},
		filters: {
			// 把数字处理为带两位小数点的数字
			tofixed(num) {
				return Number(num).toFixed(2)
			}
		},
		onLoad() {
			this.today()
			this.week()
			this.month()
			this.year()
		}
	}
</script>

<style lang="scss">
	.container {
		font-size: 14px;
		
		.header {
			display: flex;
			align-items: flex-end;
			height: 130px;
			padding: 20px;
			color: #fff;
			background-color: #666;
			
			.bottom {
				.month-expend {
					.month {
						margin-right: 3px;
						font-size: 24px;
					}
					.expend {
						color: #bbb;
					}
				}
				
				.expend-price {
					font-size: 30px;
				}
				
				.income-price {
					margin-top: 5px;
					.income {
						margin-right: 5px;
						color: #bbb;
					}
					.price {
						font-size: 14px;
					}
				}
			}
		}
		
		.date-list {
			.expend-income {
				display: flex;
				flex-direction: column;
				font-size: 14px;
				.expend {
					color: #d66854;
				}
				.income {
					color: #3bb28d;
				}
			}
		}
		
		.bottom-nav {
			position: fixed;
			bottom: 0;
			left: 0;
			right: 0;
			display: flex;
			justify-content: center;
			align-items: center;
			height: 50px;
			border-top: 1px solid #f2f2f2;
			background-color: #fff;
			
			.plus-btn {
				height: 40px;
				width: 100px;
				text-align: center;
				line-height: 40px;
				border-radius: 20px;
				font-size: 14px;
				color: #fff;
				// background-color: #ff8541;
				background: linear-gradient(75deg, #ff9966 0%, #ff5e62 100%);
			}
			.plus-btn-hover {
				background: linear-gradient(75deg, #ffaa77 0%, #ff6f73 100%);
			}
		}
	}
</style>
