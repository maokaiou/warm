<template>
	<view class="myself">
		<view class="myself_theme">
			<view v-if="userIsLogin">
				<image src="./../../static/login.jpg" mode="widthFix"></image>
			</view>
			<view v-else>
				<image src="./../../static/nologin.png" mode="widthFix"></image>
			</view>	
			
			<view class="infor-wrapper" v-if="userIsLogin">
				<view class="username">{{userInfo.username}}</view>
				<view class="nav_infor">ID:{{userInfo.flagId}}</view>
			</view>
			
			<view v-else>
				<view class="regist-login" @click="jumpRegLogin">注册/登录</view>	
			</view>
				<!-- <navigator url="./../../registLogin/registLogin" v-else>
					
				</navigator> -->
			
			<view class="set-wrapper" v-if="userIsLogin">
				<image src="./../../static/shezhi.png" mode="widthFix" @tap="jumpTomySet"></image>
			</view>
		</view>
		<view class="heng">
			<view class="contact_we" @tap="jumpToContact">
				<view  class="contaddr">
					联系我们
				</view>
				<view class="arrow-block contact-icon">
					<image src="../../static/icons/icon-arrow.png" class="set-icon"></image>
				</view>
			</view>
			<view class="address" @tap="jumpToAddress" v-if="userIsLogin">
				<view class="addr-icon">
					<image src="./../../static/icons/icon-address.png" class="set-icon" ></image>
				</view>
				<view class="contaddr">取货地址</view>
				<view class="arrow-block addr-arrow">
					<image src="../../static/icons/icon-arrow.png" class="set-icon"></image>
				</view>
			</view>
			<view class="donate-product-wrapper" @tap="jumpToDonate" v-if="userIsLogin">
				<view class="doante-icon">
					<image src="./../../static/icons/icon-address.png" class="set-icon" ></image>
				</view>
				<view class="donate-product-words">已捐物品</view>
				<view class="arrow-block donate-arrow">
					<image src="../../static/icons/icon-arrow.png" class="set-icon"></image>
				</view>
			</view>
		</view>	
		<!-- <view class="function_gather">
			<view class="function-item-wraper">
				<image clss="function-icon" :src=""></image>
				<view class="function-text"></view>
			</view>
		</view> -->
	</view>
</template>

<script>
	export default{
		data(){
			return {
				userIsLogin:false, // 用户是否登录
				userInfo:{}, //用户信息
				function_icons:[
					{
						icon:"",
						name:"募捐"
					},
					{
						icon:"",
						name:""
					}
				]
			}
		},
		onShow() {
			var userInfor = uni.getStorageSync("globalUser")
			if(userInfor !== null && userInfor !=="" && userInfor !== undefined){
				this.userIsLogin = true;
				this.userInfo = userInfor
			}
			else{
				this.userIsLogin = false;
				this.userInfo = {}
			}
		},
		methods:{
			jumpRegLogin(){
				uni.navigateTo({
					url:"../registLogin/registLogin"
				})
			},
			jumpTomySet(){
				// console.log("ihao")
				// debugger
				uni.navigateTo({
					url:"../myset/myset"
				})
				
			},
			jumpToContact(){
				uni.navigateTo({
					url:"../contact/contact"
				})
			},
			jumpToAddress(){
				uni.navigateTo({
					url:"../address/address"
				})
			},
			jumpToDonate(){
				uni.navigateTo({
					url:"../donate/donate"
				})
			}
		}
	}
</script>

<style lang="scss">
	.myself {
		.myself_theme{
			position:relative;
			background-color:#FF8C69;
			color:#fff;
			height:300rpx;
			font-size:30rpx;
			border-bottom-left-radius:32rpx;
			border-bottom-right-radius:32rpx;
			display: flex;
			flex-direction: row;
			align-items: center;
			padding-left: 40rpx;;
			image{
					width:140rpx;
					height:140rpx;
					border-radius:70rpx;
					flex-shrink:0
				}
			.infor-wrapper{
			margin-left:40rpx;
			display:flex;
			flex-direction: column;
				.username{
					color:#6a5018;
					font-weight: bold;
				}
				.nav_infor{
					color:#a38162;
					margin-top: 10rpx;
				}
			}
			.regist-login{
				margin-left:50rpx;
				font-size:40rpx;
				color:#6a5018;
				font-weight: bold;
			}
			.set-wrapper{
				width:50rpx;
				position:absolute;
				top:15rpx;
				right:14rpx;
				image{
					width:100%
				}
			}
		}
		.heng{
			.contact_we{
				position: relative;
				display:flex; 
				border:1px solid #eee;
				.contaddr{
					height:60px;
					
					line-height: 60px;
					padding-left:40px;
					
					&::before{
						position: absolute;
						top:20px;
						left:10px;
						content:' ';
						display:inline-block;
					    width:20px;
				   	    height:20px;
					    background:url('./../../static/icon-contact.png') no-repeat center;
				        background-size:contain;
					}
				}
				.contact-icon{
					position:absolute;
					right:60rpx;
					height:60px;
					line-height: 60px;
				}
			}
			.address{
				display:flex;
				justify-content: center;
				align-items: center;
				height:60px;
				border-bottom: 1px solid #eee;
				.addr-icon{
					width:8%;
					height:60px;
					display:flex;
					flex-direction:row;
					align-items: center;
					justify-content: flex-end;
					
				}
				.contaddr{
					width:72%;
					height:60px;
					line-height: 60px;
					padding-left: 20rpx;
				}
				.addr-arrow{
					width:20%;
					height:60px;
				}
			}
			.donate-product-wrapper{
				display:flex;
				justify-content: center;
				align-items: center;
				height:60px;
				border-bottom: 1px solid #eee;
				.doante-icon{
					width:8%;
					height:60px;
					display:flex;
					flex-direction:row;
					align-items: center;
					justify-content: flex-end;
					
				}
				.donate-product-words{
					width:72%;
					height:60px;
					line-height: 60px;
					padding-left: 20rpx;
				}
				.donate-arrow{
					width:20%;
					height:60px;
				}
			}
		}
	}
</style>
