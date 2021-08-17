
<template>
	<view class="donate-wrapper">
		<view class="donate_address_wrapper">
			<view class="donate-address">
				<navigator url="../adr/address_show/address_show" class="choose_address">选择取货地址</navigator>
			</view>
		</view>
		<view class="step">
			<uni-steps :options="steps" direction="column" :active="2" class="step_item"></uni-steps>
		</view>
		<view class="confirm_order">
			<view class="order_item_wrapper">
				<view class="ordere_item" @click="submitOrder">确认订单</view>
			</view>
		</view>
	</view>
</template>
<script>
	import uniSteps from '@/components/uni-steps/uni-steps.vue'
	export default {
		data(){
			return {
				steps:[
					{title: '填写信息',index:0}, 
					{title: '填写取货地址',index:1}, 
					{title: '捐赠成功等待取货',index:2}, 
					{title: '生成订单',index:3}
				]
			}
		},
		components:{
			uniSteps
		},
		methods:{
			submitOrder(){
				console.log("zhuabjie")
				var userInfor = uni.getStorageSync('globalUser')
				const a = uni.getStorageInfoSync("globalAddress")
				console.log(a)
				uni.request({	
					url:"http://81.71.6.187:9890/area-resource",
					method:'POST',
					data:{
						"detail":a,//取货地址
						"uid": userInfor.id    ,// 用户id
						"rname":"书籍 "  //捐赠类型
					},
					success(res) {
						console.log(res)
					}
				})
			}
			
		}
	}
</script>
<style lang="scss">
	.donate-wrapper{
		position: relative;
		height:100%;
		.donate_address_wrapper{
			display: flex;
			justify-content: center;
			align-items: center;
			padding:10px 0px;
			.donate-address{
				height:40px;
				line-height: 40px;
				text-align: center;
				width:200px;
				background-color: #ff3333;
				border:1px solid #f0f0f0;
				color:#fff;
				
				.choose_address{
					font-size:13px;
				}
			}
		}
		.step{
			display:flex;
			padding:20px 10px;
			border-top: 8px #f5f5f5 solid;
			.step_item{
				height:300px;
				width:100%;
				.uni-steps{
					.uni-steps__column{
						//左边框
						.uni-steps__column-text-container{
							
							padding:10px 0px;
							.uni-steps__column-text{
								height:40px;
								line-height: 20px;
								.uni-steps__column-title{
									// 标题
									font-size:12px;
								}
							}
						}
						// 右边框
						
						.uni-steps__column-container{
							display:flex;
							flex-direction: column;
							.uni-steps__column-line-item{
								height:40px;
								padding:10px 0px;
							}
						}
						
					}
				}
			}
		}
		.confirm_order{
			position: fixed;
			bottom: 0;
			left: 0;
			display: flex;
			align-items: center;
			justify-content: center;
			width:100%;
			height: 60px;
			border-top: 8px #f5f5f5 solid;
			box-sizing: border-box;
			.order_item_wrapper{
				width:150px;
				height:30px;
				line-height: 30px;
				text-align: center;
				background-color: #ff3333;
				border:1px solid #f0f0f0;
				color:#fff;
				margin:0 auto;
				.order_item{
					
				}
			}
		}
	}
</style>