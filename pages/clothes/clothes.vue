<template>
	<view class="clothes">
		<view class="clothes_infor">
			<view>
				1.填写捐赠信息
			</view>
			<text>
				
				2.信息填写成功后我们将与你取得联系
				3.由您指定上门取件时间
			</text>
		</view>
		<view class="clothes_type">
			<view class="recover_title">回收种类</view>
			<view class="recover_pro">
				<view>
					<view class="iconfont icon-yifu"></view>
					<text>衣服</text>
				</view>
				<view>
					<view class="iconfont icon-kuzi"></view>
					<text>裤子</text>
				</view>
				<view>
					<view class="iconfont icon-xiezi"></view>
					<text>鞋子</text>
				</view>
				<view>
					<view class="iconfont icon-maozi"></view>
					<text>帽子</text>
				</view>
				<view>
					<view class="iconfont icon-beizi"></view>
					<text>被子</text>
				</view>	
			</view>
		</view>
		<view class="clothes_btn">
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
	.clothes{
		position:relative;
		.clothes_infor{
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
		.clothes_type{
			position:absolute;
			top:270rpx;
			right:30rpx;
			border-radius:10px;
			background-color:#FCFCFC;
			width: 670rpx;
			padding: 40rpx 8rpx;
			
			border:1px solid #eee;
			// border:10px solid rgba(250, 250, 210, 0.5);
			.recover_title{
				font-size: 40rpx;
				
			}
			.recover_pro{
				display: flex;
				margin-top:30rpx;
				view {
					flex:1;
					font-size: 60rpx;
					text {
						font-size: 30rpx;
					}
				}
			}
		}
		.clothes_btn{
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
