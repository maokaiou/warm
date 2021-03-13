<template>
	<view class="contact">
		<view class="contact_theme">
			<view>
				联系我们
			</view>
		</view>
		<view class="infor">
			<view @click="call_phone">联系电话：19973826395 (点击拨号)</view>
			<view>地址：湖南省衡阳市珠晖区湖南工学院</view>
			<map  class="map" :latitude="latitude" :longitude="longitude" :scale="scale" :markers="markers"></map>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				latitude:26.883613,
				longitude:112.691683,
				scale: 13,
				markers:[
					{
						longitude:112.691683,
						
						latitude:26.883613,
						iconPath:"./../../static/logo/school.jpg",
						width:50,
						height:50,
						title:"湖南工学院"
						
					}
				]
			}
		},
		methods:{
			call_phone(){
				uni.makePhoneCall({
					phoneNumber:"19973826395"
				})
			}
		}
	}
</script>
<style lang="scss">
	.contact {
		.contact_theme{
			position: relative;
			background-color:#FF8C69;
			color:#fff;
			height:300rpx;
			font-size:20px;
			border-bottom-left-radius:32rpx;
			border-bottom-right-radius:32rpx;
			font-weight: bold;
			
			view{
				position: absolute;
				top:40px;
				left:30px;
			}
		}
		.infor {
			font-size: 30rpx;
			margin-top:20px;
			view {
				height:70rpx;
				border-bottom: 2rpx solid #eee;
				line-height: 70rpx;
				padding: 10rpx 20rpx; 
			}
			.map {
				margin-top:20px;
				width: 750rpx;
				height: 750rpx;
			}
		}
	}
</style>
