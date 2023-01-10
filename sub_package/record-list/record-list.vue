<template>
	<view class="record-list-container">
		<template v-if="scene === '今天'">
			<view class="record-item" v-for="record in recordList" :key="record.id">
				<view class="record-item-title">
					<text class="day">{{record.day}}日</text>
					<text class="date">{{record.date | toDate}}</text>
					<text class="week">{{record.week.replace('星期', '周')}}</text>
				</view>
				<uni-list :border="false">
					<uni-list-item
						:title="record.behavior" 
						:note="record.time + ' · ' + record.pay" 
						:rightText="record.expend || record.income" 
						:border="false"
					>
						<template v-slot:footer>
							<text :class="record.expend ? 'expend' : 'income'">
								{{(record.expend || record.income) | tofixed}}
							</text>
						</template>
					</uni-list-item>
					<uni-list-item 
						:title="recordItem.behavior"
						:note="recordItem.time + ' · ' + recordItem.pay" 
						v-for="recordItem in record.childes" 
						:key="recordItem.id"
						:border="false"
					>
						<template v-slot:footer>
							<text :class="recordItem.expend ? 'expend' : 'income'">
								{{(recordItem.expend || recordItem.income) | tofixed}}
							</text>
						</template>
					</uni-list-item>
				</uni-list>
			</view>
		</template>
		<view class="empty" v-else>
			无记录
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				scene: '',	// 场景值
				recordList: [{
					id: 1,
					date: '2023-1-8',
					day: '8',
					time: '20:35',
					week: '星期日',
					expend: 10,
					income: 0,
					pay: '微信支付',
					behavior: '生活用品',
					childes: [{
						id: 2,
						date: '2023-1-8',
						day: '8',
						time: '13:52',
						week: '星期日',
						expend: 0,
						income: 100,
						pay: '支付宝',
						behavior: '卖废品'
					}]
				}, {
					id: 3,
					date: '2023-1-7',
					day: '7',
					time: '8:36',
					week: '星期六',
					expend: 10,
					income: 0,
					pay: '微信支付',
					behavior: '生活用品',
					childes: [{
						id: 4,
						date: '2023-1-8',
						day: '8',
						time: '8:36',
						week: '星期六',
						expend: 10,
						income: 0,
						pay: '微信支付',
						behavior: '生活用品'
					}]
				},]
			};
		},
		filters: {
			// 把日期格式转换为 YYYY.MM
			toDate(date) {
				return date.split('-').slice(0,2).join('.')
			},
			// 把数字处理为带两位小数点的数字
			tofixed(num) {
				return Number(num).toFixed(2)
			}
		},
		onLoad(options) {
			this.scene = options.scene
		}
	}
</script>

<style lang="scss">
.record-list-container {
	.record-item {
		border-bottom: 3px solid #f2f2f2;
		.record-item-title {
			padding: 5px 15px;
			background-color: white;
			.day {
				margin-right: 3px;
				font-size: 18px;
			}
			.date,
			.week {
				margin-right: 5px;
				font-size: 12px;
				color: #999;
			}
		}
		
		.expend {
			color: #3bb28d;
		}
		.income {
			color: #d66854;
		}
	}
	
	.empty {
		text-align: center;
	}
}
</style>
