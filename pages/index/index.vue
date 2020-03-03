<template>
	<view class="index">	
		<uni-nav-bar @clickLeft="goCamera" @clickRight="goVip">
			<view class="uni-nav-bar index-lf" slot="left"></view>
			<!-- <image slot="left" src="../../static/tabbar/richscan_icon.png" :style="{'width' : 20 + 'rpx'}"></image> -->
			<uni-search-bar :radius="50" cancelButton="none" :style="{'width': 560 + 'rpx'}"
				@confirm="search" @input="input" ></uni-search-bar>
			<view class="uni-nav-bar index-rg" slot="right"></view>
		</uni-nav-bar>
		<swiper :interval="3000" :duration="true" indicator-active-color="#ffffff" :circular="true" :disable-touch="true" :indicator-dots="true" :autoplay="true">
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
	</view>
</template>

<script>
	import uniNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue"
	import uniSearchBar from '@/components/uni-search-bar/uni-search-bar.vue'
	export default {
		data() {
			return {
			}
		},
		onLoad() {
		},
		methods: {
			goCamera(){
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
		
		swiper {
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
	}
</style>
