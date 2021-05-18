<template>
	<view class="home">
		<swiper :circular="true" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="item in swiper" :key='item.id'>
					<image :src="item.image_src"></image>
			</swiper-item>
		</swiper>
		<!-- 导航区域 -->
		<view class="nav">
			<view class="nav_item" v-for="(item,index) in navs" :key="index" @click="navItemClick(item.path)">
				<view :class="item.icon"></view>
				<text>{{item.title}}</text>
			</view>
		</view>
		<!-- 推荐商品 -->
		<view class="hot_goods">
			<view class="tit">推荐商品</view>
			<goods-list @goodsItemClick='goGoodsDetail' :goods="goods"></goods-list>
		</view>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	export default {
		data() {
			return {
				swiper: [],
				goods: [{
					id: '1',
					url: '../../static/hotshop/123.jpg',
					prePrice: 2599,
					nowPrice: 2199,
					detail: '华为（HUAWEI）荣耀6Plus 16G双4G版'
				},
				{
					id: '2',
					url: '../../static/hotshop/iphone.jpg',
					prePrice: 6599,
					nowPrice: 6199,
					detail: '苹果X（iphone）X 16G双4G版'
				},
				{
					id: '3',
					url: '../../static/hotshop/iphone1.jpg',
					prePrice: 5599,
					nowPrice: 5199,
					detail: '苹果11（iphone）11 绿色 16G双4G版'
				},
				{
					id: '4',
					url: '../../static/hotshop/lg.jpg',
					prePrice: 4599,
					nowPrice: 4199,
					detail: 'lg（lg）荣耀6Plus  16G双4G版'
				},
				{
					id: '5',
					url: '../../static/hotshop/viov.jpg',
					prePrice: 3599,
					nowPrice: 3199,
					detail: 'vivo（vivo）荣耀6Plus  16G双4G版'
				},
				{
					id: '6',
					url: '../../static/hotshop/xiaomi.jpg',
					prePrice: 4599,
					nowPrice: 4199,
					detail: 'xiaomi（xiaomi）xiaomi8Plus  16G双4G版'
				},
				],
				navs: [
					{
						icon: 'iconfont icon-ziyuan',
						title: '小小超市',
						path: '/pages/goods/goods'
					},
					{
						icon: 'iconfont icon-guanyuwomen',
						title: '联系我们',
						path: '/pages/contact/contact'
					},
					{
						icon: 'iconfont icon-tupian',
						title: '社区图片',
						path: '/pages/pics/pics'
					},
					{
						icon: 'iconfont icon-shipin',
						title: '学习视频',
						path: '/pages/videos/videos'
					}
				]
			}
		},
		onLoad() {
			this.getSwipers()
		},
		components: {
			"goods-list" : goodsList
		},
		methods: {
			async getSwipers(){
				const res = await this.$myRequest({
					url: 'home/swiperdata'
				})
				this.swiper = res.data.message
			},
			navItemClick (path) {
				uni.navigateTo({
					url: path
				})
			},
			/* 导航到商品详情页 */
			goGoodsDetail(id){
				uni.navigateTo({
					url: '/pages/goods-detail/goods-detail?id='+id
				})
			}
		}
	}
</script>

<style lang="scss">
	.home{
		swiper{
			width: 750rpx;
			height: 380rpx;
			image{
				height: 100%;
				width: 100%;
			}
		}
		.nav{
			display: flex;
			.nav_item{
				width: 25%;
				text-align: center;
				view{
					width: 120rpx;
					height: 120rpx;
					background-color: $shop-color;
					border-radius: 50%;
					margin: 10px auto;
					line-height: 120rpx;
					color: #FFFFFF;
					font-size: 44rpx;
				}
				text{
					font-size: 30rpx;
				}
			}
		}
		.hot_goods{
			background: #eee;
			overflow: hidden;
			margin-top: 10px;
			.tit{
				height: 50px;
				line-height: 50px;
				color: $shop-color;
				text-align: center;
				letter-spacing: 20rpx;
				background: #FFFFFF;
				margin: 7rpx 0;
			}
			.goods_list {
				padding: 0 15rpx;
				display: flex;
				flex-wrap: wrap;
				justify-content: space-between;
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
		}
	}
</style>
