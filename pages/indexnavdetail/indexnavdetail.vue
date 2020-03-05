<template>
	<view class="indexnavdetail">
		{{indexnavdetailId}}
	</view>
</template>

<script>
	export default{
		data(){
			return{
				indexnavdetailId: 0,
			}
		},
		onLoad(option){
			//console.log(option);
			this.indexnavdetailId = option.id;
		}
	}
</script>

<style>
	.indexnavdetail{
		font-size: 80rpx;
		color: #007AFF;
		text-align: center;
	}
</style>
