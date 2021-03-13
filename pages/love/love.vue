<template>
	<view class="love-wrapper">
		<view class="search-wrapper">
			<view class="search-icon-wrapper">
				<image src="./../../static/icon-search.png" class="sear-icon"></image>
			</view>
			<input tpe="text"  class="search-text" focus placeholder="搜索(最长10个关键字)捐赠地区名字" maxlength="10" 
			confirm-type="search" @input="getData"/>
		</view>
		<view class="img-wrapper" >
			<view class="img-item" v-for="item in list" :key="item.id">
				<image class="img-show" :src="item.img" @click="toDetail(item.id)"></image>
			</view>
		</view>
	</view>
	
</template>

<script>
	export default{
		data(){
			return {
				condition:'',
				img:'./../../static/love.jpg',
				list:[]
			}
		},
		methods:{
			toDetail(id,){
				uni.navigateTo({
					url:"../detail/detail?id="+id	
				})
			},
			getData(){
				uni.request({
					url:"http://81.71.6.187:9890/areas",
					method:"GET",
					success:(res)=>{
						// debugger
						console.log(res.data)
						if(res.data.code ==20000){
							var list = res.data.result
							this.list =list
						}
						
					}
				})
			}
		},
		onLoad() {
			this.getData()
		}
	}
</script>

<style lang="scss">
	.love-wrapper{
		.search-wrapper{
			display: flex;
			flex-direction: row;
			padding:20rpx;
			width:750rpx;
			position:fixed;
			top:0rpx;
			background-color:#fff;
			z-index:1000;
			.search-icon-wrapper{
				background-color: #eaeaea;
				display:flex;
				flex-direction: column;
				justify-content: center;
				padding:0rpx 10rpx;
				.sear-icon{
					width:50rpx;
					height:50rpx;
				}
			}
			.search-text{
				width:600rpx;
				height:60rpx;
				font-size:30rpx;
				// padding:
				background-color: #eaeaea;
			}
		}
		//图片展示
		.img-wrapper{
			display:flex;
			flex-direction: row;
			justify-content: flex-start;
			flex-wrap: wrap;
			margin-top:80rpx;
			padding:6rpx 15rpx 0rpx 15rpx;
			.img-item{
				padding:10rpx 15rpx;
				.img-show{
					width:325rpx;
					height:325rpx;
				}
			}
		}
	}
	
</style>
