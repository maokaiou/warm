<template>
	<view class="address-show">
		<view class="address-wrapper">
			<view class="address-item" v-for="item in addressList" :key="item.id">
				<view class="address-content">{{item.content}}</view>
				<view class="address">
					<view class="choose_true" @click="set_default(item.id)" >
						
						<image src="../../../static/icons/no_moren.png" mode="widthFix"></image>
						<view  class="text">设为默认</view>
					</view>
					<view class="icon-item" @click="delAddress(item.id)">
						<uni-icons type="trash-filled" color="#FF8C69"></uni-icons>
					</view>	
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				addressList:[],
				address_id:0
			}
		},
		methods: {
			// 更新收货地址
			getUpdateAddress(){
				var me = this
				var userInfor = uni.getStorageSync('globalUser')
				console.log(userInfor)
				uni.request({
					url:"http://81.71.6.187:9890/address/user/"+userInfor.id,
					success(res) {
						console.log(res)
						if( res.data.code === 20000){
							me.addressList = res.data.result
						}
					}
				})
			},
			// 设为默认
			set_default(e){
				uni.request({
					url:"http://81.71.6.187:9890/address/"+e,
					success(res) {
						if(res.data.code === 20000){
							const gloAddress = res.data.result
							uni.setStorageSync("globalAddress",gloAddress)
						}
					}
				})
				
			},
			// 删除指定地址
			delAddress(e){
				uni.request({
					url:"http://81.71.6.187:9890/address"+e,
					success(res) {
						if(res.data.code === 20000){
							uni.showToast({
								title:"删除成功",
								icon:"none"
							})
						}
					}
				})
			}
		},
		onLoad() {
			this.getUpdateAddress()
		}
	}
</script>

<style lang="scss">
	.address-show{
		.address-wrapper{
			.address-item{
				// padding:8px 5px;
				
				// border-top:4px solid #e4e4e4;
				border-bottom:6px solid #f0f0f0;
				margin-top:8px;
				align-items: center;
				
				.address-content{
					padding:8px 5px;
					word-wrap:break-word;
					font-size:14px;
				}
				.address{
					border-top: 1px solid #f0f0f0;
					display:flex;
					align-items: center;
					justify-content: space-between;
					height:25px;
					padding: 4px 10px;
					.choose_true{
						display: flex;
						width:100px;
						image{
							width:22px;
						}
					}
					.icon-item{
						
					}
				}
			}
		}
	}

</style>
