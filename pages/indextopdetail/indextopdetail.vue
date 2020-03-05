<template>
	<view class="indextopdetail">
		{{indextopdetailItem.img}}
		
	</view>
</template>

<script>
	export default{
		data(){
			return{
				indextopdetailItem: {}
			}
		},
		onLoad(option){
			console.log(option.item);
			this.indextopdetailItem = JSON.parse(option.item);
		}
	}
</script>

<style>
</style>
