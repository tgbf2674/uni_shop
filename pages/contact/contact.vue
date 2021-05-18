<template>
	<view class="contact">
		<image class="img" src="../../static/guanyuwomen.jpg" mode=""></image>
		<view class="info">
		<view @click="phone">联系电话：400-123-1234 （点击拨打）</view>
		<view>商城地址：深圳市南山区西萨的JFK拉夫汉达4号大街134号时代广场</view>
		<map :makers="makers" :scale="scale" :latitude="latitude" :longitude="longitude" class="map" name=""></map>
	</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude: 113.926438,
				latitude: 22.541463,
				scale: 15,
				makers: [
					{
						longitude: 113.926438,
						latitude: 22.541463,
						iconPath: '/static/zuobiao.jpg',
						width: 30,
						height: 30
					}
				]
			}
		},
		methods: {
			phone(){
				uni.makePhoneCall({
					phoneNumber: '400-123-1234'
				})
			}
		}
	}
</script>

<style lang="scss">
	.contact{
		.img{
			width: 750rpx;
			height: 320rpx;
		}
		.info{
			padding: 10rpx 20rpx;
			font-size: 30rpx;
			view{
				line-height: 80rpx;
				border-bottom: 1px solid #eee;
			}
		}
		.map{
			width: 750rpx;
			height: 750rpx;
		}
	}
</style>
