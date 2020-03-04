<template>
	<view class="index">	
		<!-- 搜索框 -->
		<uni-nav-bar @clickLeft="goCamera" @clickRight="goVip">
			<view class="uni-nav-bar index-lf" slot="left"></view>
			<!-- <image slot="left" src="../../static/tabbar/richscan_icon.png" :style="{'width' : 20 + 'rpx'}"></image> -->
			<uni-search-bar :radius="50" cancelButton="none" :style="{'width': 560 + 'rpx'}"
				@confirm="search" @input="input" ></uni-search-bar>
			<navigator class="uni-nav-bar index-rg" slot="right" url="../vip/vip"></navigator>	
		</uni-nav-bar>
		<!-- 轮播图 -->
		<swiper class="top" :interval="3000" :duration="true" indicator-active-color="#ffffff" :circular="true" :disable-touch="true" :indicator-dots="true" :autoplay="true">
			<swiper-item>
				<view class="swiper-item index-bg1" @click="goLinks()"></view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item index-bg2" @click="goLinks()"></view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item index-bg3" @click="goLinks()"></view>
			</swiper-item>
		</swiper>
		<!-- 产品icon -->
		<view class="nav">
			<swiper class="middle" :duration="500" :disable-touch="true" @change="changeSwiper">
				<swiper-item>
					<view class="swiper-item index-bg4">
						<view class="swiper-item icon" v-for="(item,index) in 8" :key="index">
							<image :src="'../../static/tabbar/porduct_icon/' + item +'.png'"></image>
							<text>产品</text>
						</view>
					</view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item index-bg5"></view>
				</swiper-item>
			</swiper>
			 <!-- 轮播指示点样式修改 -->
			  <view class="dots">
				  <block v-for="(item,index) in 2" :key="item">
					  <view class="dot" :class="index==swiperCurrent ? ' active' : ''"></view>
				  </block>
			  </view>
		</view>
		
	</view>
</template>

<script>
	import uniNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue"
	import uniSearchBar from '@/components/uni-search-bar/uni-search-bar.vue'
	export default {
		data() {
			return {
				swiperCurrent: 0,
			}
		},
		onLoad() {
		},
		methods: {
			goCamera(){
				uni.scanCode({			
				    success: function (res) {		
				        console.log('条码类型：' + res.scanType);			
				        console.log('条码内容：' + res.result);			
				    }			
				});
			},
			 changeSwiper(e) {
	             this.swiperCurrent = e.detail.current;
			 },
			goVip(){
			},
			input(){
			},
			search(){
			},
			goLinks(){
			},
			searchClick(){
			}
		},
		components: {
			uniNavBar,
			uniSearchBar
		}
	}
</script>

<style lang='scss'>
	.index {
		box-sizing: border-box;
		/* 搜索框 */
		uni-nav-bar {	
			.uni-nav-bar.index-lf {
				width: 56rpx;
				height: 56rpx;
				background-image: url('../../static/tabbar/richscan_icon.png');
				background-size: 56rpx;
			}			
			.uni-nav-bar.index-rg {
				width: 56rpx;
				height: 56rpx;
				background-image: url('../../static/tabbar/t30.png');
				background-size: 56rpx;
			}
		}
		
		/* 轮播图 */
		.top {
			width: 100%;
			height: 200rpx;
			swiper-item {
				.swiper-item.index-bg1 {
					width: 100%;
					height: 200rpx;
					background-color: #007AFF;
				}
				.swiper-item.index-bg2 {
					width: 100%;
					height: 200rpx;
					background-color: #4CD964;
				}
				.swiper-item.index-bg3 {
					width: 100%;
					height: 200rpx;
					background-color: #F0AD4E;
				}
			}
		}
		
		/* 产品icon */
		.nav{
			position: relative;
			.middle {
				height: 240rpx;
				.swiper-item.index-bg4{
					height: 220rpx;
					background-color: #fedcba;
					margin: 20rpx;
					display: flex;
					flex-wrap: wrap;
					.swiper-item.icon{
						width: 25%;
						height: 110rpx;
						display: flex;
						/* flex-direction: column; *//* 上下对齐 */
						position: relative;
						image{
							width: 48rpx;
							height: 48rpx;
							position: absolute;
							top: 28%;
							left: 50%;
							transform: translate(-50%,-50%);
						}
						text{
							font-size: 20rpx;
							/* text-align: center; */
							position: absolute;
							top: 68%;
							left: 50%;
							transform: translate(-50%,-50%);
						}
					}
				}
				.swiper-item.index-bg5 {
					height: 220rpx;
					background-color: #abcdef;
				}
			}
			.dots {
			          position: absolute;
			          bottom: 20rpx;
			          left: 50%;
			           /* 这里一定要注意兼容不然很可能踩坑 */
			          transform: translate(-50%, 0);
			          -webkit-transform: translate(-50%, 0);        
			          z-index: 99;
			          display: flex;
			          flex-direction: row;
			          justify-content: center;
			
			          .dot {
			              width: 24rpx;
			              height: 8rpx;
			              transition: all .6s;
			              background: rgba(0, 0, 0, .3);
			              margin-right: 10rpx;
			          }
			
			          .active {
			              width: 24rpx;
			              height: 8rpx;
			              background: rgba(255, 255, 255, .8);
			          }
			      }
		}
	}
	/* uni-swiper-dots.uni-swiper-dots-horizontal */
	/* uni-swiper .uni-swiper-dot-active */
	swiper .uni-swiper-dot{
		width: 20rpx !important;
		height: 80rpx !important;
		border-radius: 50%;
	}
		/* uni-swiper .uni-swiper-dot */
</style>
