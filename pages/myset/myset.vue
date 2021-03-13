<template>
	<view class="mySet-wrapper">
		<view class="my-infor">
		<!-- 	头像 -->
			<view class="header-sculpture infor-list">
				<view class="left-title">头像</view>
				<view class="right-wrapper">
					<image src="../../static/login.jpg" class="touxiang"></image>
					<view class='arrow-block'>
						<image src="../../static/icons/icon-arrow.png" class="set-icon"></image>
					</view>
				</view>
				
			</view>
			<!-- 用户名 -->
			<view class="username infor-list">
				<view class="left-title">用户名</view>
				<view class="right-wrapper">
					<view class="user-infor">{{userInfor.username}}</view>
					<view class='arrow-block'>
						<image src="../../static/icons/icon-arrow.png" class="set-icon"></image>
					</view>
				</view>
			</view>
			<!-- 学校 -->
			<view class="school infor-list">
				<view class="left-title">学校</view>
				<view class="right-wrapper">
					<view class="school-infor">湖南工学院</view>
					<view class='arrow-block'>
						<image src="../../static/icons/icon-arrow.png" class="set-icon"></image>
					</view>
				</view>	
			</view>
			<!-- 生日 -->
			<view class="birthday infor-list">
				<view class="left-title">生日</view>
				<view class="right-wrapper">
					<view class="birth-infor">2021-3-8</view>
					<view class='arrow-block'>
						<image src="../../static/icons/icon-arrow.png" class="set-icon"></image>
					</view>
				</view>
				
			</view>
			<!-- 性别 -->
			<view class="sex infor-list">
				<view class="left-title">性别</view>
				
				<view class="right-wrapper">
					<view class="sex-infor">女</view>
					<view class='arrow-block'>
						<image src="../../static/icons/icon-arrow.png" class="set-icon"></image>
					</view>
				</view>
			</view>
		
			<view class="footer-set">
				<view class="footer-item">清除缓存</view>
				<view class="footer-item">退出登录</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				userInfor:{}
			}
		},
		onShow() {
			var userInfor = uni.getStorageSync("globalUser")
			console.log(userInfor)
			this.userInfor = userInfor
		}
	}
	
</script>

<style lang="scss">
	page{
		width:100%;
		height:100%;
		.mySet-wrapper{
			// position: relative;
			width:100%;
			height: 100%;
			background-color: #F5F5F5;
			.my-infor{
			background-color: #FFFFFF;
				.header-sculpture{
					.touxiang{
						width:50rpx;
						height:50rpx;
						border-radius: 25rpx;
						border:1px solid #909090;
					}
				}
			}
			.footer-set{
				position:fixed;
				bottom: 0px;
				display:flex;
				flex-direction: column;
				width:100%;
				color:#999999;
				background-color: #FFFFFF;
				.footer-item{
					line-height: 80rpx;
					border-top:1px solid #C0C0C0;
					text-align: center;
				}
				
			}
		}
	}	

	
</style>
