<template>
	<view class="detail-wrapper">
		<view class="support-total">
			<image src="./../../static/love.jpg" class="photo" mode="widthFix"></image>
			<view class="support-item">
				已筹集：
				<text>￥300</text>
			</view>
		</view>
		<view class="xiangmu-detail">
			<view class="detail-title">
				项目详情
			</view>
			<view class="detail-content">在资源有限的环境中,对于学生们渴望知识改变命运,我们了解到孩子们正需要补充教材,继续筹集到足够的资金为孩子们的学习保驾护航</view>
		</view>
		<view class="donate-money">
			<button>捐钱</button>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				
			}
		},
		onLoad(option) {
			console.log(option)
		}
	}
	
</script>

<style lang="scss">
	.detail-wrapper{
		.support-total{
			padding-bottom: 15rpx;
			border-bottom: 20rpx solid #F2F2F2;
			.photo{
				width:100%;
			}
			.support-item{
				color:#999999;
				padding:20rpx 0rpx 20rpx 20rpx;
				text{
					color:#FF8C69;
				}
			}
		}
		.donate-money{
			position: fixed;
			bottom:0;
			height: 120rpx;
			width:100%;
			border:1px solid #eee;
			button{
				position:absolute;
				top:20rpx;
				left:75rpx;
				width:600rpx;
				height:80rpx;
				line-height: 80rpx;
				color:#fff;
				background-color:#FF8C69 ;
			}
		}
		.xiangmu-detail{
			color:#999999;
			.detail-title{
				color:#333;
				font-weight: bold;
			}
		}
	}
</style>

