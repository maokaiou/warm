<template>
	<view class="content">
		<view class="update-message">
			<view class="update-text">所在地区：</view>
			<view class="update-input">
				<input @tap="openAddres" v-model="address"/>
			</view>
			<!-- <image src="../../static/" class="jt"></image> -->
		</view>
		<textarea class="detail" placeholder-style="color:#ccc;" placeholder="详细地址:如教学楼,宿舍" v-model="details_content"/>
		<simple-address ref="simpleAddress" :pickerValueDefault="cityPickerValueDefault" @onConfirm="onConfirm" themeColor='#333'></simple-address>
		<button @click="submitAddress">确认</button>
	</view>
</template>

<script>
	import simpleAddress from "@/components/simple-address/simple-address.nvue"
	export default {
		data() {
			return {
				cityPickerValueDefault: [0, 0, 1],//弹框的初始值
				pickerText:'',
				address:'北京市-市辖区-西城区',//初始值,
				details_content:''
			}
		},
		components: {
			simpleAddress
		},
		methods: {
			openAddres() {
				this.$refs.simpleAddress.open();
			},
			onConfirm(e) {
				this.pickerText = JSON.stringify(e);//这个步骤只是为了让大家看到返回的数据
				this.address=e.label;//把选择的地址回显到input框中
				// console.log(e.label)
				// console.log(JSON.stringify(e))
			},
			bindTextAreaBlur: function (e) {
			    console.log(e.detail.value)
			},
			// 提交地址
			submitAddress(){
				var me =this
				var userInfor = uni.getStorageSync('globalUser')
				var address_total = me.address + ' ' + me.details_content
				
				uni.request({
					url:"http://81.71.6.187:9890/address",
					method:"POST",
					data:{
						uid:userInfor.id,
						content:address_total 
					},
					success(res) {
						if(res.data.code === 20000){
							uni.showToast({
								title:"添加成功",
								icon:""
							})
							
						}
					}
				})
			}

		}
	}
</script>

<style>
	page{background-color: #f1f1f1;}
	/* 提示 */
	.mind{color: #ccc;font-size: 24upx;margin:3%;}
	text{margin:1%;}
	/* 所在地区 */
	.update-message{background-color: #fff;height:95upx;line-height: 95upx;font-size: 32upx;display: flex;border-bottom:2upx solid #e4e4e4;}
	/* 文字 */
	.update-text{flex: 3;text-align: center;}
	/* 右侧input框 */
	.update-input{flex: 7;display: flex;padding: 3.5%;}
	/* 箭头 */
	.jt{height:30upx;width:30upx;margin: auto;margin-right: 20upx;}
	/* 详情 */
	.detail{background-color: #fff;width: 100%;height: 200upx;padding: 2%;}
</style>
			