<template>
	<view>
		<view v-for="item in list" @click="navigator(item.goods_id)" :key="item.goods_id" class="news_item">
			<image :src="item.goods_small_logo" mode=""></image>
		<view class="right">
		<view class="tit">
			{{item.goods_name}}
		</view>
		<view class="info">
			<text>商品重量：{{item.goods_weight}}</text>
			<text>商品价格：{{item.goods_price}}</text>
		</view>
		</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:['list'],
		data() {
			return {
				
			}
		},
		filters: {
			formatDate(date) {
				const newdate = new Date(date)
				const year = newdate.getFullYear()
				const mouth =newdate.getMonth().toString().padStart(2,0)
				const day = newdate.getDay().toString().padStart(2,0)
				console.log(year,mouth,day)
			}
		},
		methods: {
			navigator (id) {
				this.$emit('itemClick',id)
			}
		}
	}
</script>

<style lang="scss">
.news_item{
			display: flex;
			padding: 10rpx 20rpx;
			border-bottom: 1px solid $shop-color;
			image{
				min-width: 200rpx;
				max-width: 200rpx;
				height: 150rpx;
			}
			.right{
				margin-left: 15rpx;
				display: flex;
				flex-direction: column;
				justify-content: space-between;
			.tit{
				font-size: 30rpx;
			}	
			.info{
				font-size: 24rpx;
				text:nth-child(2){
					margin-left: 20rpx;
				}
			}
			}
		}
</style>
