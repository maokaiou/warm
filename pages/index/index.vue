<template>
	<view class="home">
		<swiper indicator-dots autoplay circular duration=100>
			<swiper-item>
				<image src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fwww.hpa.net.cn%2Fbinger%2Fimages2%2F2016%2F12%2F26%2F201612261242382885_9019.jpg&refer=http%3A%2F%2Fwww.hpa.net.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1616897532&t=69cf4e08ea187b8b9d2947a65570a34d"></image>
			</swiper-item>
			<swiper-item>
				<image src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fphotocdn.sohu.com%2F20160201%2Fmp57477904_1454297808206_1_th.png&refer=http%3A%2F%2Fphotocdn.sohu.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1616897532&t=edbe70b82f9b31faca4158ed0ec1c30c"></image>
			</swiper-item>
		</swiper>
		<!-- 捐赠项目 -->
		<view class="xiangmu">
			<view class="xiangmu_title">回收项目</view>
			<view class="xiangmu_type">
				<navigator class="xiangmu_type1" url="./../book/book">
					<text>书籍类</text>
				</navigator>
				<navigator  class="xiangmu_type2" url="./../clothes/clothes">
					<text>服饰类</text>
				</navigator>
				<navigator  class="xiangmu_type2" url="./../stationery/stationery">
					<text>文具类</text>
				</navigator>
				<navigator  class="xiangmu_type2" url="./../toy/toy">
					<text>玩具类</text>
				</navigator>
			</view>
		</view>
		
		<!-- 合作企业 -->
		<view class="jigoulogo">
			<view class="tit">合作教育机构</view>
			<view  class="scroll_left">
				<view class="logo-item" v-for="item in qylogo">
					<image :src="item.bkgrd" mode="widthFix"></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				qylogo:[
				  {
					  bkgrd: "../../static/logo/school.jpg"
				  },
				  {
				  	   bkgrd: "../../static/logo/school.jpg"
				  },
				  {
				  		bkgrd: "../../static/logo/school.jpg"
				  },
				  {
				  		bkgrd: "../../static/logo/school.jpg"
				  }
				  
				]
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style lang="scss">
	.home{
		swiper {
			width: 750rpx;
			height:380rpx;
			image{
				height: 100%;
				width: 100%;
			}
		}
		.xiangmu{
			margin-top:30rpx;
			border:1px solid #eee;
			padding-top:10px;
			padding-bottom: 10px;
			.xiangmu_title{
				fontsize: 60rpx;
				font-weight: bold;
				color:#4F4F4F;
				margin-bottom: 20rpx;
			}
			.xiangmu_type{
				// 清除浮动
				overflow: hidden;
				color:#333;
				font-size:40rpx;
				.xiangmu_type1{
					float:left;
					width:240rpx;
					height:410rpx;
					background-color: #1AAD19;
					border-radius: 30rpx;
					margin-left:10px;
					margin-right:8px;
					background: url('./../../static/huishou/photo_shuji.jpg') no-repeat center;
					background-size:cover;
				}
				.xiangmu_type2{
					float:left;
					width:200rpx;
					height:200rpx;
					background-color: #5989B9;
					border-radius: 20rpx;
					&:nth-last-child(1){
						width:430rpx;
						background: url('./../../static/huishou/photo_wanju.jpg') no-repeat center;
						background-size:cover;
					},
					&:nth-last-child(2){
						margin-left:10px;
						border-bottom: 10rpx solid #fff;
						background: url('./../../static/huishou/photo_wenju.jpg') no-repeat center;
						background-size:cover;
					}
					&:nth-last-child(3){
						border-bottom: 10rpx solid #fff;
						background: url('./../../static/huishou/photo_fuzhuang.jpg') no-repeat center;
						background-size:cover;
				    }
				}
			}
		}
		.jigoulogo{
			// height: 150rpx;
			margin-top: 40rpx;
			padding-bottom: 8rpx;
			border-top:1px solid #eee;
			.tit {
				fontsize: 60rpx;
				font-weight: bold;
				color:#4F4F4F;
			}
			.scroll_left {
				display:flex;
				// flex-direction: column;
				margin-top:20rpx;
				.logo-item {
					width:200rpx;
					padding:0rpx 20rpx;
					
					image {
						width: 100%;
						height:100%;
					}
				}
			}
		}
		
	}
</style>
