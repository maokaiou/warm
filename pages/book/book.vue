<template>
	<view class="book">
		<view class="book_infor">
			<view>
				1.填写捐赠信息
			</view>
			<text>
				
				2.信息填写成功后我们将与你取得联系
				3.由您指定上门取件时间
			</text>
		</view>
		<view class="book_type">
			<view class="recover_title">回收种类</view>
			<view class="recover_pro">
					<view class="imgs-item" v-for="item in imgs">
						<image class="book_img" :src=item.bk mode="widthFix"></image>
						<view class="book_name">{{item.title}}</view>
					</view>	
					<!-- <image src="../../static/book/jiaocai.jpg"></image> -->
				
			</view>
		</view>
		<view class="book_btn">
			<button type="default" @click="jumpTodonate">立即捐赠</button>
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return{
				imgs:[
					{	
						title: "教材教辅类",
						bk:"./../../static/book/jiaocai.jpg"
					},
					{
						title: "科普图书类",
						bk:"./../../static/book/kepu.jpg"
					},
					{
						title: "课外拓展类",
						bk:"./../../static/book/kewai.jpg"
					},
					{
						title: "文学作品类",
						bk:" ./../../static/book/wenxue.jpg"
					}
				]
			}
		},
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
	.book{
		position:relative;
		.book_infor{
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
		.book_type{
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
				display:flex;
				flex-direction: row;
				padding:20rpx 0rpx 20rpx 0rpx;
				.imgs-item{
					flex:1;
					.book_img{
						width:150rpx;
						// height:100rpx;
						
					}
					.book_name{
						font-size:30rpx;
					}
					
				}
			}
		}
		.book_btn{
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
