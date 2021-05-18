<template>
	<view class="news_detail">
		<text class="title">标题</text>
		<view class="info">
			<text>发表时间：</text>
			<text>内容：</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id: 0,
				detail: {}
			}
		},
		methods: {
			async getNewDetail (){
				const res = await this.$myRequest({
					url: 'goods/detail/'+ this.id
				})
				this.detail = res.data.message[0]
			}
		},
		onLoad(options){
			this.id =options.id
			this.getNewDetail()
		}
	}
</script>

<style lang="scss">
.news_detail{
	font-size: 30rpx;
	padding: 0 20rpx;
	.title{
		text-align: center;
		width: 710rpx;
		display: block;
		margin: 20rpx 0;
	}
	.info{
		display: flex;
		justify-content: space-between;
	}
}
</style>
