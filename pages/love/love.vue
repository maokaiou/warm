<template>
	<view class="love-wrapper">
		<view class="search-wrapper">
			<view class="search-icon-wrapper">
				<image src="./../../static/icon-search.png" class="sear-icon"></image>
			</view>
			<input tpe="text"  class="search-text" focus placeholder="搜索(最长10个关键字)捐赠地区名字" maxlength="10" 
			confirm-type="search" @input="getData"/>
		</view>
		<view class="show-wrapper" >
			<view class="show-item" v-for="item in list" :key="item.id">
					<view class="show-img">
						<image :src="item.img" @click="toDetail(item.id)" mode="scaleToFill"></image>
					</view>
					<view class="show-address">
					三下乡:{{item.address}}</view>
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
							console.log(this.list)
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
		.show-wrapper{
			display:flex;
			flex-direction: row;
			justify-content: space-between;
			align-items: center;
			flex-wrap: wrap;
			margin-top:80rpx;
			padding:7px 10px;
			// padding:6rpx 15rpx 0rpx 15rpx;
			height:140px;
			.show-item{	
				width:45%;
				border:6px solid #F0F0F0;
				.show-img{
					display:flex;
					justify-content: center;
					margin-bottom: 10px;
					image{
						// width:100px;
						height:100px;
					}
				}
				.show-address{
					width:100px;
					color:#555555;
					font-size: 10px;
					font-weight: bold;
					word-wrap:break-word
				}
			}
		}
	}
	
</style>
