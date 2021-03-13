<template>
	<view class="regist-login">
		<form @submit="submitForm">
			<view class="img-wrapper">
				<image src="../../static/nologin.png"></image>
			</view>
			<view class="infor-wrapper">
				<label class="infor-item">用户名</label>
				<input type="text" value="" name="username" class="input" placeholder="请输入用户名" v-model="username"/>
			</view>
			<view class="infor-wrapper">
				<label class="infor-item">密码</label>
				<input type="text" value="" name="password" class="input" placeholder="请输入密码"  password="true" v-model="password" />
			</view>
			<view class='btn-wrapper'>
				<button type="primary" form-type="submit">登录</button>
				<view @click="regist">注册</view>
				<!-- <button type="primary" form-type="submit">注册</button> -->
			</view>
		</form>
		
		<view class="third">
			<view class="line-wrapper">
				<view class="line"></view>
			</view>
			<view class="third-words">第三方账号登录</view>
			<view class="line-wrapper">
				<view class="line"></view>
			</view>
		</view>
		<view class="third-icon-wrapper">
			<image src="../../static/icons/icon-weixin.png" class="third-icon" @click="wxLogin"></image>
			<!-- <button open-type="getUserInfo" @getuserinfo="wxLogin"></button> -->
		</view>
		
	</view>
</template>

<script>
	export default{
		data(){
			return {
				username:'',
				password:'',
				userInfo:{}
			}
		},
		methods:{
			// 登录事件
			submitForm(e){
				
				var username=e.detail.value.username
				var password=e.detail.value.password
				// 发起登录请求
				uni.request({
					url:'http://81.71.6.187:9890/users/login',
					method:'POST',
					data:{
						"username":username,
						"password":password
					},
					success:(res)=>{
						if(res.data.code == 20000 ){
							var userInfor = res.data.result
							uni.showToast({
								title:"登录成功跳转页面",
								duration:4000
							})
							// console.log(userInfor)
							// 将用户信息存储到缓冲区域
							uni.setStorageSync('globalUser',userInfor)
							uni.switchTab({
								url:"../myself/myself"
							})
						}
						else if (res.data.code == 20004){
							uni.showToast({
								title:"检查所填信息",
								duration: 2000,
								image:"./../../static/icons/error.png"
							})
						}
						else if(res.data.code == 20002){
							uni.showToast({
								title: "用户信息非法",
								duration: 2000,
								image:"./../../static/icons/no.png"
							})
						}
						
					}
				})
				
			},
			// 注册事件
			regist(){
				uni.request({
					url:"http://81.71.6.187:9890/users/register",
					method:"POST",
					data:{
						"username":this.username,
						"password":this.password
					},
					success:(res)=>{
						// console.log(res.data)
						// debugger
						if(res.data.code ==20000){
							console.log(res.data)
							uni.showToast({
								title:"注册成功",
								duration: 2000,
								image:"../../static/icons/success.png"
							})
						}
						else if(res.data.code ==20003){
							uni.showToast({
								title:"用户名已存在",
								duration: 2000,
								image:"../../static/icons/error.png"
							})
						}
						else if(res.data.code == 20002){
							uni.showToast({
								title:"提交信息非法",
								duration: 2000,
								image:"../../static/icons/no.png"
							})
						}
						
						
					}
				})
			},
			wxLogin(){
				let me = this
				console.log(me)
				uni.getUserInfo({
					provider:"weixin",
					success:function(loginRes) {
						let userInfo= loginRes.userInfo
							me.userInfo=userInfo
						
						 console.log(me.userInfo)
					}
				})
				// let userInfor = e.detail.userInfo
				uni.login({
					provider: 'weixin',
					  success: (loginRes)=> {
						 // 获取微信登录的code(授权码)
					    let code = loginRes.code
				// 		console.log(this.userInfo)
				
						uni.request({
							url:"http://81.71.6.187:9890/users/wx-login",
							mehtod:"POST",
							data:{
								code:code
							},
							success:(userResult)=>{
								console.log(userResult)
								if(userResult.data.code == 20000){
									uni.setStorageSync("global")
									uni.switchTab({
										url:"../myself/myself"
									})
								}
							}
						})
					  }
				})
				
			}
		
		}
	}
</script>

<style lang="scss">
	.regist-login{
		.img-wrapper{
			height:150px;
			display:flex;
			justify-content: center;
			align-items: center;
			
			image{
				width:150rpx;
				height:150rpx;
				border-radius:75rpx;
				border:1px solid #CDC5BF;
			}
		}
		.infor-wrapper{
			display:flex;
			flex-direction: row;
			justify-content: center;
			height:100rpx;
			align-items: center;
			border-bottom: 1px solid #dbdbda;
			// width:400rpx;
			.infor-item{
				color:#808080;
			}
			.input{
				height:80rpx;
				line-height: 90rpx;
				width:500rpx;
				margin-left:30rpx;
			}
		}
		.btn-wrapper{
			display:flex;
			flex-direction: row;
			button{
				margin-top:60rpx;
				width:400rpx;
				height:100rpx;
				background-color:#FF8C69;
			}
			view{
				width:200rpx;
				display:flex;
				align-items: flex-end;
				text-decoration: underline;
				color:#CFCFCF;
			}
		}
		.third{
			display:flex;
			line-height:60rpx;
			margin-top:30rpx;
			.third-words{
				font-size:30rpx;
				color:#909090;
				width:36%;
				
				text-align: center;
			}
			.line-wrapper{
				width:32%;
				display:flex;
				flex-direction: row;
				justify-content: flex-end;
				align-items: center;
				&:last-child{
					justify-content: flex-start;
				}
				.line{
					width:120rpx;
					border-bottom:1px solid #CFCFCF;
					
				}
			}
		}
		.third-icon-wrapper{
			display: flex;
			align-items: center;
			justify-content: center;
			height:70rpx;
			.third-icon{
				width:45rpx;
				height:45rpx;
			}
			button{
				width:30rpx;
				height:30rpx;
			}
		}
	}
</style>
