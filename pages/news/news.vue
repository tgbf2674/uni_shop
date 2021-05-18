<template>
	<view class="news">
		<news-item @itemClick="goDetail" :list="goodsList"></news-item>
	</view>
</template>

<script>
	import newsList from '../../components/news-item/news-item.vue'
	export default {
		data() {
			return {
				goodsList:[]
			}
		},
		components: {
			'news-item': newsList
		},
		onLoad() {
			this.getGoods()
		},
		methods: {
			async getGoods(){
				const res = await this.$myRequest({
					url: 'goods/search'
				})
				this.goodsList = res.data.message.goods
			},
			goDetail(id){
				uni.navigateTo({
					url: '/pages/news-detail/news-detail?id=' +id
				})
			}
		}
	}
</script>

<style lang="scss">
	.news{
		
	}
</style>
