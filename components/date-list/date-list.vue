<template>
	<view class="date-list">
		<view class="left-item">
			<text class="tips-date">{{title}}</text>
			<text class="date">{{date}}</text>
		</view>
		<view class="right-item">
			<view class="expend-income">
				<text class="expend">{{expend | tofixed}}</text>
				<text class="income">{{income | tofixed}}</text>
			</view>
			<uni-icons type="forward" color="gray"></uni-icons>
		</view>
	</view>
</template>

<script>
	export default {
		name:"date-list",
		data() {
			return {
				
			};
		},
		props: {
			title: {
				type: String,
				default: '今天'
			},
			date: {
				type: String,
				default: '1月1日'
			},
			expend: {
				type: Number,
				default: 0
			},
			income: {
				type: Number,
				default: 0
			}
		},
		filters: {
			// 把数字处理为带两位小数点的数字
			tofixed(num) {
				return Number(num).toFixed(2)
			}
		},
	}
</script>

<style lang="scss">
.date-list {
	display: flex;
	justify-content: space-between;
	padding: 15px 20px;
	padding-right: 10px;
	border-bottom: 1px solid #e3e3e3;
	
	.left-item {
		display: flex;
		flex-direction: column;
		
		.tips-date {
			font-size: 17px;
		}
		.date {
			color: gray;
		}
	}
	
	.right-item {
		display: flex;
		justify-content: space-between;
		align-items: center;
		
		.expend-income {
			display: flex;
			flex-direction: column;
			margin-right: 5px;
			.expend {
				color: #d66854;
			}
			.income {
				color: #3bb28d;
			}
		}
	}
}
</style>