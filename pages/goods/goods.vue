<template>
	<view class="goods_list">
		<view @goodsItemClick='goGoodsDetail(item.id)' class="goods_item" v-for="item in goods" :key="item.id">
			<image :src="item.goods_big_logo" mode=""></image>
			<view class="price">
				<text>￥{{item.goods_price}}</text>
				<text>￥{{item.goods_price -200}}</text>
			</view>
			<view class="name">
				{{item.goods_name}}
			</view>
		</view>
		<view class="isOver" v-if="flag">----- 已经到底部了 -----</view>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	export default {
		data() {
			return {
				goods: [],
				pagenum: 1,
				flag: false
			}
		},
		onLoad() {
			this.getGoodsList()
		},
		onReachBottom() {
			if(this.goods.length<this.goods.total) return this.flag=true
			this.pagenum++
			this.getGoodsList()
		},
		onPullDownRefresh() {
			this.pagenum = 1
			this.goods = []
			this.flag = false
			setTimeout(()=>{
			this.getGoodsList(()=>{
				uni.stopPullDownRefresh()
			})
			},1000)
		},
		components: {'goods-list': goodsList},
		methods: {
			async getGoodsList(callBack) {
				const res = await this.$myRequest({
						url: 'goods/search?pagenum=' + this.pagenum
				})
				this.goods = [...this.goods,...res.data.message.goods]
				callBack && callBack()
			},
			goGoodsDetail(id){
				uni.navigateTo({
					url: '/page/goods-detail/goods-detail?id='+id
				})
			}
		}
	}
</script>

<style lang="scss">
.goods_list {
		padding: 0 15rpx;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		background: #eee;
		.isOver{
			width: 100%;
			height: 50px;
			line-height: 50px;
			text-align: center;
			font-size: 28rpx;
		}
		.goods_item{
			background:#FFFFFF;
			width: 355rpx;
			margin: 10rpx 0;
			padding: 15rpx;
			box-sizing: border-box;
			image{
				width: 80%;
				height: 150px;
				display: block;
				margin: auto;
			}
			.price{
				color: $shop-color;
				font-size: 36rpx;
				margin: 20rpx 0 10rpx 0;
				text:nth-child(2){
					color: #ccc;
					font-size: 28rpx;
					margin-left: 17rpx;
					text-decoration: line-through;
				}
			}
			.name{
				font-size: 28rpx;
				line-height: 50rpx;
				padding-bottom: 15rpx;
				padding-top: 10rpx;
			}
		}
	}
</style>
