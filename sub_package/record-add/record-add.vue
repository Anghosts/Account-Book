<template>
	<view class="record-add-container">
		<view class="header-bar">
			<view class="btns">
				<uni-segmented-control 
					:current="current" 
					:values="items" 
					@clickItem="onClickItem" 
					style-type="text" 
					active-color="#ff5e62"
				/>
			</view>
			<view class="content">
				<view v-if="current === 0">
					<uni-forms :modelValue="baseFormData">
						<uni-forms-item label="金额">
							<uni-easyinput v-model="baseFormData.name" placeholder="0.00" />
						</uni-forms-item>
						<uni-forms-item label="分类">
							<uni-data-picker placeholder="请选择分类" popup-title="请选择分类" :localdata="classifyDataTree" v-model="classify">
							</uni-data-picker>
						</uni-forms-item>
						<uni-forms-item label="账户">
							<uni-data-picker placeholder="请选择支付方式" popup-title="请选择支付方式" :localdata="accountDataTree" v-model="account">
							</uni-data-picker>
						</uni-forms-item>
						<uni-forms-item label="时间">
							<uni-datetime-picker type="datetime" return-type="timestamp" v-model="baseFormData.datetimesingle"/>
						</uni-forms-item>
						<uni-forms-item label="备注">
							<uni-easyinput type="textarea" v-model="baseFormData.introduction" placeholder="备注" />
						</uni-forms-item>
					</uni-forms>
				</view>
				<view v-if="current === 1"><text class="content-text">选项卡2的内容</text></view>
			</view>
		</view>
	</view>
	
</template>

<script>
	export default {
		data() {
			return {
				items: ['支出', '收入'],
				current: 0,
				baseFormData: {
					name: '',
					age: '',
					introduction: '',
					sex: 2,
					hobby: [5],
					datetimesingle: 1627529992399
				},
				classify: '1-1',
				classifyDataTree: [{
					text: '食品酒水',
					value: '1-0',
					children: [{
						text: '早午晚餐',
						value: '1-1'
					}, {
						text: '水果零食',
						value: '1-2'
					}]
				}, {
					text: '居家物业',
					value: '2-0',
					children: [{
						text: '日常用品',
						value: '2-1'
					}]
				}],
				account: '2-1',
				accountDataTree: [{
					text: '食品酒水',
						value: '1-0',
						children: [{
							text: '早午晚餐',
							value: '1-1'
						}, {
							text: '水果零食',
							value: '1-2'
						}]
					}, {
						text: '居家物业',
						value: '2-0',
						children: [{
							text: '日常用品',
							value: '2-1'
						}]
				}]
			};
		},
		methods: {
			onClickItem(e) {
				if (this.current !== e.currentIndex) {
					this.current = e.currentIndex
				}
			},
		}
	}
</script>

<style lang="scss">
.record-add-container {
	.header-bar {
		background-color: #fff;
		
		.content {
			padding: 15px;
		}
	}
}
</style>
