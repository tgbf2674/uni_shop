<template>
	<view class="pics">
		<scroll-view scroll-y="true" class="left">
			<view @click="leftClickHandle(index,item.cat_id)" :class="active1 === index? 'active': '' " v-for="(item,index) in cateList" :key="item.cat_id">{{item.cat_name}}</view>
		</scroll-view>
		<scroll-view scroll-y="true" class="right">
			<view v-for="(item,index) in rightData" :key="index" class="item">
				<image @click="previewImage(item.img_url)" :src="item.img_url" mode=""></image>
				<text>{{item.title}}</text>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cateList: [],
				active1: '',
				rightData: [
					{
						title: '欧式风格继承了巴洛克风格中豪华、动感、多变的视觉效果',
						zhaiyao: '继上编欧式客厅装修效果图之后，今天，小编为大家带来的是一组不同类型的欧式卧室装修效果图。欧式卧室的设计风格按不同的地域文化可分为北欧卧室、简欧卧室和传统欧式卧室。在中国，因为欧式风格继承了巴洛克风格中豪华、动感、多变的视觉效果，也吸取了洛可可风格中唯美、律…"',
						img_url: '../../static/123.jpg'
					}
				]
			}
		},
		onLoad() {
			this.getPicsCate()
		},
		methods: {
			async getPicsCate() {
				const res = await this.$myRequest({
					url: 'categories'
				})
				this.cateList = res.data.message
			},
			async leftClickHandle (index){
				this.active1 = index
			},
			previewImage(current) {
				const url = this.rightData.map(item=>{
					return item.img_url
				})
				uni.previewImage({
					current,
					urls: url
				})
			}
		}
	}
</script>

<style lang="scss">
	page{
		height: 100%;
	}
	.pics{
	height: 100%;
	display: flex;
	.left{
		height: 100%;
		width: 200rpx;
		view{
			height: 60px;
			line-height: 60px;
			color: #333;
			text-align: center;
			font-size: 30rpx;
			border-top: 1px solid #eee;
		}
		.active{
			background: $shop-color;
			color: #FFFFFF;
		}
	}
	.right{
		height: 100%;
		width: 550rpx;
		margin: 0 auto;
		.item{
			image{
				width: 530rpx;
				height: 530rpx;
				border-radius: 5px;
			}
		}
	}
	}
</style>
