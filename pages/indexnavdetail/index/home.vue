<template>
	<view class="index-wrapper">
		<!-- 轮播图 -->
		<view class="swiper-wrapper">
			<view class="swiper-box">
				<swiper class="swiper-content" :autoplay="true" :interval="3000" :circular="true" @change="changeSwiper">
					<swiper-item class="swiper-item" v-for="imgs in swiperList" :key="imgs.id">
						<image class="swiper-img" :src="imgs.img"></image>
					</swiper-item>
				</swiper>
				<view class="indicator">
					<view class="dots" v-for="(swiper, index) in swiperList" :class="[currentSwiper >= index ? 'on' : '']" :key="index"></view>
				</view>
			</view>
		</view>
		<!-- 分类列表 -->
		<view class="category-wrapper">
			<view class="category-content" v-for="categorys in categoryList" :key="categorys.id">
				<image class="category-img" :src="categorys.img"></image>
				<text class="category-name">{{categorys.name}}</text>
			</view>
		</view>
		<!-- banner -->
		<view class="banner-wrapper">
			<image class="banner" src="/static/img/banner.jpg"></image>
		</view>
		<!-- 优惠专区 -->
		<view class="discount-wrapper">
			<view class="discount-title">
				<text class="title">优惠专区</text>
			</view>
			<view class="discount-content">
				<view class="discount-item" v-for="(promote,index) in Promotion" :key="index">
					<view class="item-title">
						<text>{{promote.title}}</text>
					</view>
					<view class="item-contnet">
						<view class="item-left">
							<view class="discript">{{promote.ad}}</view>
							<view class="into">点击进入</view>
						</view>
						<view class="item-right">
							<image class="shopImg" :src="promote.img"></image>
						</view>
					</view>
				</view>
			</view>
		</view>
		<!-- 产品列表 -->
		<view class="goodsList-wrapper">
			<view class="goodsTitle">
				<view class="line"></view>
				<view class="title">商品列表</view>
				<view class="line"></view>
			</view>
			<view class="goodsBox">
				<goods-list :goodsList="goodsList" @change="goGoodsdetail"></goods-list>
			</view>
		</view>
		<!-- 加载更多 -->
		<uni-load-more :status="status" />
	</view>
</template>

<script>
	// import mpvueCityPicker from '@/components/mpvue-citypicker/mpvueCityPicker.vue'
	import goodsList from '../../../components/goodsList/goodslist.vue'
	import uniLoadMore from '../../../components/uni-load-more/uni-load-more.vue'

	export default {
		components: {
			goodsList,
			uniLoadMore
		},
		data() {
			return {
				// 轮播图片
				swiperList: [{
						id: 1,
						src: 'url1',
						img: '/static/img/1.jpg'
					},
					{
						id: 2,
						src: 'url2',
						img: '/static/img/2.jpg'
					},
					{
						id: 3,
						src: 'url3',
						img: '/static/img/3.jpg'
					}
				],
				currentSwiper: 0,
				// 分类菜单
				categoryList: [{
						id: 1,
						name: '办公',
						img: '/static/img/category/1.png'
					},
					{
						id: 2,
						name: '家电',
						img: '/static/img/category/2.png'
					},
					{
						id: 3,
						name: '服饰',
						img: '/static/img/category/3.png'
					},
					{
						id: 4,
						name: '日用',
						img: '/static/img/category/4.png'
					},
					{
						id: 5,
						name: '蔬果',
						img: '/static/img/category/5.png'
					},
					{
						id: 6,
						name: '运动',
						img: '/static/img/category/6.png'
					},
					{
						id: 7,
						name: '书籍',
						img: '/static/img/category/7.png'
					},
					{
						id: 8,
						name: '文具',
						img: '/static/img/category/8.png'
					}
				],
				Promotion: [],
				goodsList: [{
						goods_id: 0,
						img: '/static/img/goods/p1.jpg',
						name: '商品名称',
						price: 168,
						slogan: 1558
					},
					{
						goods_id: 1,
						img: '/static/img/goods/p2.jpg',
						name: '商品名称商品名',
						price: 167,
						slogan: 1038
					},
					{
						goods_id: 2,
						img: '/static/img/goods/p3.jpg',
						name: '商品名称商品名称商品名称商品名称商品名称',
						price: 17,
						slogan: 1228
					},
					{
						goods_id: 3,
						img: '/static/img/goods/p4.jpg',
						name: '商品名称商品名称商',
						price: 167,
						slogan: 1058
					},
					{
						goods_id: 4,
						img: '/static/img/goods/p5.jpg',
						name: '商品名称商品名称商品名',
						price: 107,
						slogan: 558
					},
					{
						goods_id: 5,
						img: '/static/img/goods/p6.jpg',
						name: '商品名名称商品品名称商品名称',
						price: 177,
						slogan: 58
					},
					{
						goods_id: 6,
						img: '/static/img/goods/p7.jpg',
						name: '商品名称商品名称商品名称商商品名称',
						price: 18,
						slogan: 1800
					},
					{
						goods_id: 7,
						img: '/static/img/goods/p8.jpg',
						name: '商品名称商品名称商品名称商商品名称商品名称商品名称商品名',
						price: 144,
						slogan: 13526
					},
					{
						goods_id: 8,
						img: '/static/img/goods/p9.jpg',
						name: '商品名称商品名称商品名称商品名称商品名称',
						price: 123,
						slogan: 1000
					},
					{
						goods_id: 9,
						img: '/static/img/goods/p10.jpg',
						name: '商品名称商品名称商品名称商品名',
						price: 186,
						slogan: 3008
					}
				],
				status: 'loading',
			}
		},
		onLoad() {
			this.loadPromotion();
		},
		onPullDownRefresh() {
			console.log('下拉了');
		},
		onReachBottom() {
			this.goodsList = this.goodsList.concat(this.goodsList);
		},
		methods: {
			
			//跳轉詳情頁
			goGoodsdetail(){
				uni.navigateBack({
					url: '../indexnavdetail.vue'
				})
			},
			changeSwiper(e) {
				this.currentSwiper = e.detail.current;
			},
			//加载Promotion 并设定倒计时,,实际应用中应该是ajax加载此数据。
			loadPromotion() {
				let cutTime = new Date();
				let yy = cutTime.getFullYear(),
					mm = cutTime.getMonth() + 1,
					dd = cutTime.getDate();
				let tmpcountdown = yy + '/' + mm + '/' + dd + ' 23:59:59';
				let tmpPromotion = [{
						title: '整点秒杀',
						ad: '整天秒杀专区',
						img: '/static/img/s1.jpg',
						countdown: false
					},
					{
						title: '限时抢购',
						ad: '每天23点上线',
						img: '/static/img/s2.jpg',
						countdown: tmpcountdown
					} //countdown为目标时间，程序会获取当前时间倒数
				];
				//检查倒计时
				for (let i = 0; i < tmpPromotion.length; i++) {
					let row = tmpPromotion[i];
					if (row.countdown) {
						let h = '00',
							m = '00',
							s = '00';
						let currentTime = new Date();
						let cutoffTime = new Date(tmpcountdown);
						if (!(currentTime >= cutoffTime)) {
							let countTime = parseInt(
								(cutoffTime.getTime() - currentTime.getTime()) / 1000
							);
							h = parseInt(countTime / 3600);
							m = parseInt((countTime % 3600) / 60);
							s = countTime % 60;
							h = h < 10 ? '0' + h : h;
							m = m < 10 ? '0' + m : m;
							s = s < 10 ? '0' + s : s;
						}
						tmpPromotion[i].countdown = {
							h: h,
							m: m,
							s: s
						};
					}
				}
				this.Promotion = tmpPromotion;
			},
		}
	}
</script>

<style lang="less" scoped>
	@import "../../../common/css/uni.css";

	.index-wrapper {
		font-size: 25rpx;

		.swiper-wrapper {
			width: 100%;
			display: flex;
			justify-content: center;
			box-sizing: border-box;
			padding: 0 30rpx;
			margin-top: 10rpx;

			.swiper-box {
				width: 100%;
				height: 32vw;
				overflow: hidden;
				border-radius: 15rpx;
				box-shadow: 0rpx 8rpx 25rpx rgba(0, 0, 0, 0.2);
				//兼容ios，微信小程序
				position: relative;
				z-index: 1;

				.swiper-content {
					width: 100%;
					height: 32vw;
					background-color: aqua;

					.swiper-item {
						.swiper-img {
							width: 100%;
							height: 32vw;
						}
					}
				}

				.indicator {
					width: 120rpx;
					height: 5rpx;
					display: flex;
					flex-direction: row;
					position: absolute;
					left: 10rpx;
					bottom: 10rpx;
					background-color: #efefef;
					overflow: hidden;
					border-radius: 2rpx;

					.dots {
						width: 40rpx;
						height: 100%;

						&.on {
							background-color: aqua;
						}
					}
				}
			}
		}

		.category-wrapper {
			display: flex;
			flex-direction: row;
			flex-flow: wrap;
			padding: 20rpx;
			position: relative;

			&::after {
				content: '';
				position: absolute;
				left: 20rpx;
				right: 20rpx;
				bottom: 0;
				border-bottom: 1px solid #efefef;
			}

			.category-content {
				display: flex;
				width: 25%;
				height: 150rpx;
				flex-direction: column;
				justify-content: center;
				align-items: center;

				.category-img {
					width: 68rpx;
					height: 68rpx;
					margin-bottom: 5rpx;
				}

				.category-name {
					font-size: 12px;
					color: #3c3c3c;
				}
			}
		}

		.banner-wrapper {
			display: flex;
			width: 100%;
			height: 200rpx;
			align-items: center;
			justify-content: center;

			.banner {
				width: 685rpx;
				height: 150rpx;
			}
		}

		.discount-wrapper {
			padding: 0 40rpx;
			margin-bottom: 30rpx;

			.discount-title {
				margin-bottom: 10rpx;

				.title {
					font-size: 35rpx;
					font-weight: bold;
				}
			}

			.discount-content {
				display: flex;
				flex-direction: row;
				justify-content: space-between;

				.discount-item {
					display: flex;
					width: 48%;
					height: 200rpx;
					background-color: #ebf9f9;
					border-radius: 10rpx;
					padding: 10rpx;
					box-sizing: border-box;
					flex-direction: column;

					.item-title {
						font-size: 26rpx;
						font-weight: bold;
					}

					.item-contnet {
						flex: 1;
						display: flex;
						flex-direction: row;

						.item-left {
							flex: 1;
							height: 100%;
							display: flex;
							flex-direction: column;
							justify-content: space-between;
							color: #acb0b0;
						}

						.item-right {
							.shopImg {
								width: 140rpx;
								height: 140rpx;
							}
						}
					}
				}
			}
		}

		.goodsList-wrapper {
			padding: 0 40rpx;

			.goodsTitle {
				display: flex;
				flex-direction: row;
				justify-content: center;
				align-items: center;
				margin-bottom: 20rpx;

				.title {
					font-size: 35rpx;
					color: coral;
					margin: 0 20rpx;
				}

				.line {
					width: 30rpx;
					height: 1px;
					background-color: coral;
				}
			}

			.goodsBox {}
		}
	}
</style>
