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
			<swiper-item v-for="(item,topindex) in swiperList" :key="topindex">
				<navigator class="swiper-item index-bg1" :url="'../indextopdetail/indextopdetail?item=' + JSON.stringify(item)">
					<image :src="item.img" style="width: 100%;"></image>
				</navigator>
			</swiper-item>
			<!-- <swiper-item>
				<view class="swiper-item index-bg2" @click="goLinks()"></view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item index-bg3" @click="goLinks()"></view>
			</swiper-item> -->
		</swiper>
		<!-- 产品icon -->
		<view class="nav">
			<swiper class="middle" :duration="500" :disable-touch="true" @change="changeSwiper">
				<swiper-item v-for="(item1,index1) in 2" :key="index1">
					<!-- swpiper-item这里 2应该写成 Math.ceil(producticon.lenght/8),但是会报错?--> 
					<view class="swiper-item index-bg2">
						<navigator class="swiper-item icon" v-for="(item2,index2) in 8" :key="index2"
							:url="'../indexnavdetail/indexnavdetail?id=' + producticon[(index2 + swiperCurrent*8)].id"
						>
							<image v-if="producticon[(index2 + swiperCurrent*8)].image" :src="producticon[(index2 + swiperCurrent*8)].image"></image>
							<!-- image这里,可以写成 :src="'../../static/tabbar/porduct_icon/' + (item + swiperCurrent*8) +'.png'" -->
							<text>{{producticon[(index2 + swiperCurrent*8)].name}}</text>
						</navigator>
					</view>
				</swiper-item>
			</swiper>
			 <!-- 轮播指示点样式修改 -->
			  <view class="dots">
				  <block v-for="(item,index) in 2" :key="item">
					  <view class="dot" :class="index==swiperCurrent ? ' active' : ''"></view>
				  </block>
			  </view>
		</view>
		
		<!-- 3d轮播 -->
		<!-- #ifdef H5 -->
		<!-- <view class="threed">
			<bw-img-upload style="width:100%"></bw-img-upload>
			<bw-swiper :swiperList="swiperList" style="width:710rpx" displayMultipleItems="3"
				
				swiperType="true"
			></bw-swiper>
		</view> -->
		<!-- #endif -->
		


		
	</view>
</template>

<script>
	import producticonJson from "./json/producticon.json"
	import uniNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue"
	import uniSearchBar from "@/components/uni-search-bar/uni-search-bar.vue"
	// import bwSwiper from '@/components/bw-swiper/bw-swiper.vue'
	
	export default {
		data() {
			return {
				swiperCurrent: 0,
				producticon: producticonJson,
				swiperList:[ // 滑块视图容器数据 
				    // 数据格式 :imageKey="xx" :textKey="yy" [{xx: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big25011.jpg',yy:'加油'}] 提示文字可要可不要
				    // 或者 [{img: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big25011.jpg',text:'加油'}] 提示文字可要可不要, 同时数据要把大括号改成中括号
					{img: '../../static/tabbar/bar/1.png',text:'1'},
					{img: '../../static/tabbar/bar/2.png',text:'2'},
					{img: '../../static/tabbar/bar/3.png',text:'3'}
				],
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
			searchClick(){
			}
		},
		components: {
			uniNavBar,
			uniSearchBar,
			// bwSwiper
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
				}
			}
		}
		
		/* 产品icon */
		.nav{
			position: relative;
			.middle {
				height: 260rpx;
				.swiper-item.index-bg2{
					height: 220rpx;
					background-color: #fedcba;
					margin: 10rpx 20rpx;
					padding: 20rpx 0 0;
					border-radius: 10rpx;
					display: flex;
					flex-wrap: wrap;
					.swiper-item.icon{
						width: 25%;
						height: 100rpx;
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
							-webkit-transform: translate(-50%,-50%);
						}
						text{
							font-size: 22rpx;
							position: absolute;
							top: 68%;
							left: 50%;
							transform: translate(-50%,-50%);
							-webkit-transform: translate(-50%,-50%);
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
		
		/* 3d */
		.threed{
			margin: 10rpx 20rpx;
		}
	
	
	
	}

</style>
