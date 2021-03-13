<template>
	<view class="stationery">
		<view class="stationery_infor">
			<view>
				1.填写捐赠信息
			</view>
			<text>
				
				2.信息填写成功后我们将与你取得联系
				3.由您指定上门取件时间
			</text>
		</view>
		<view class="stationery_type">
			<image src="./../../static/wenju.jpg"></image>
		</view>
		<view class="stationery_btn">
			<button type="default" @click="jumpTodonate">立即捐赠</button>
		</view>
	</view>
</template>

<script>
	export default {
		methods:{
			jumpTodonate(){
				uni.navigateTo({
					url:"/pages/donate/donate"
				})
			}
		}
	} 
</script>

<style lang="scss">
	.stationery{
		position:relative;
		.stationery_infor{
			background-color:#FF8C69;
			color:#fff;
			height:300rpx;
			border-bottom-left-radius:32rpx;
			border-bottom-right-radius:32rpx;
			font-weight: bold;
			view{
				// background-color: #eee;
				width:200px;
				height:40px;
				line-height: 40px;
				margin-left: 10px;
				border-radius: 5px;
			}
		}
		.stationery_type{
			position:absolute;
			top:270rpx;
			right:30rpx;
			border-radius:10px;
			background-color:#FCFCFC;
			width: 670rpx;
			padding: 40rpx 8rpx;
			display:flex;
			justify-content: center;
			align-items: center;
			border:1px solid #eee;
			// border:10px solid rgba(250, 250, 210, 0.5);
			.recover_title{
				font-size: 40rpx;
				
			}
			.recover_pro{
				margin-top:30rpx;
			}
		}
		.stationery_btn{
			position: fixed;
			bottom:0;
			height: 80px;
			width:100%;
			border:1px solid #eee;
	
			button{
				position: absolute;
				bottom: 15px;
				right:30px;
				background-color: #FF8C69;
				width: 450rpx;
				height:50px;
				color:#fff;
				text-align:center;
				}
		}
	}
	
</style>

