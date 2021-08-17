<template>
	<view class="detail-wrapper">
		<view class="support-total">
			<image :src="areasInfor.img" class="photo" mode="widthFix"></image>
			<view class="support-item">
				需要筹集：
				<text>￥600</text>
			</view>
		</view>
		<view class="xiangmu-detail">
			<view class="detail-title">
				项目详情
			</view>
			<view class="detail-content">
				<rich-text :nodes="areasInfor.content"></rich-text>
			</view>
		</view>
		<!-- <view class="donate-money">
			<button>捐钱</button>
		</view> -->
		<view class="detail-content">
			<view class="xiangmu-detail">
				<!-- <view class="detail-title">
					项目详情
				</view> -->
				<!-- <view class="xiangmu-content">在资源有限的环境中,对于学生们渴望知识改变命运,我们了解到孩子们正需要补充教材,继续筹集到足够的资金为孩子们的学习保驾护航</view> -->
			</view>
			<view class="detail-comment">
				<view class="comment-title">最新评论</view>
				<view class="comment-content" v-for="item in commentsList">
					<comments :comment_show="item"></comments>
				</view>
			</view>
		</view>
		<view class="detail-bottom">
			<view class="detail-bottom__input" @click="openComments">
				<text>谈谈你的看法</text>
				<uni-icons type="compose" size="16" color="#F07373"></uni-icons>
			</view>
			<view class="detail-bottom__icons">
				<view class="detail-bottom__icons-box">
					<uni-icons type="chat" size="22" color="#F07373"></uni-icons>
				</view>
				<view class="detail-bottom__icons-box">
					<uni-icons type="hand-thumbsup" size="22" color="#F07373"></uni-icons>
				</view>
				<view class="detail-bottom__icons-box" >
					<uni-icons  type="heart" size="22" color="#F07373"></uni-icons>
				</view>
			</view>
		</view>
		
		<uni-popup tyep="bottom" ref="popup" :maskClick="false">
			<view class="popup-body-wrapper">
				<view class="popup-header">
					<text class="popup-text-item" @click="closePopup">取消</text>
					<text class="popup-text-item" @click="releaseContent">发布</text>
				</view>
				<view class="popup-content">
					<textarea fixed="true" v-model="comment" placeholder="请输入内容" maxlength="150" ></textarea>
					<view class="content-count">{{comment.length}}/150</view>
				</view>
			</view>
			
		</uni-popup>
	</view>
</template>

<script>
	import comments from '../../components/comments/comments.vue'
	export default{
		components:{
			comments
		},
		data(){
			return{
				comment:"",
				aid:{},
				commentsList:[],
				areasInfor:{} // 地区信息
			}
		},
		onLoad(options) {
			// option中接受上一级页面的值
			// console.log(options.id)
			 this.aid =JSON.parse(options.id)
			 // 更新评论
			 this.updateComments()
			 // 获取信息
			 this.getAreasInfor()
		},
		methods:{
			// 获取地区信息
			getAreasInfor(){
				var me = this
				uni.request({
					url:"http://81.71.6.187:9890/areas/"+me.aid,
					success(res) {
						if(res.data.code === 20000){
							me.areasInfor = res.data.result
							console.log(res.data.result)
						}
						
					}
				})
			},
			// 打开PopuP弹框
			openComments(){
				this.comment =""
				this.$refs.popup.open()
			},
			// 关闭PopUp弹框
			closePopup(){
				this.comment=""
				 this.$refs.popup.close()
			},
			// 发表评论
			releaseContent(){
				var me =this
				if(!me.comment){
					uni.showToast({
						title:'请输入评论内容',
						icon:"none"
					})
					return
				}
				uni.showLoading()
				uni.request({
					url:"http://81.71.6.187:9890/comments",
					method:'POST',
					data:{
						aid:me.aid,
						content:me.comment
					},
					success:(res)=>{
						uni.hideLoading()
						if(res.data.code === 20000){
							
							 this.$refs.popup.close()
						}
					}
				})
				
			},
			// 根据aid更新评论
			updateComments(){
				var me =this
				// console.log(me.aid)
				uni.request({
					url:"http://81.71.6.187:9890/comments/area/"+me.aid,
					success:(res)=> {
						console.log(res)
						if(res.data.code === 20000){
							this.commentsList = res.data.result
							console.log(this.commentsList)
						}
						
						
					}
				})
			}
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
		// .donate-money{
		// 	position: fixed;
		// 	bottom:0;
		// 	height: 120rpx;
		// 	width:100%;
		// 	border:1px solid #eee;
		// 	button{
		// 		position:absolute;
		// 		top:20rpx;
		// 		left:75rpx;
		// 		width:600rpx;
		// 		height:80rpx;
		// 		line-height: 80rpx;
		// 		color:#fff;
		// 		background-color:#FF8C69 ;
		// 	}
		// }
		.detail-content{
			margin-top: 20px;
			.xiangmu-detail{
				color:#999999;
				.detail-title{
					color:#333;
					font-weight: bold;
					margin-bottom: 5px;
				}
				.xiangmu-content{
					padding:0 14px;
				}
			}
			.detail-comment {
				margin-top: 30px;
				.comment-title {
					padding: 10px 15px;
					font-size: 14px;
					color: #666;
					border-bottom: 1px #f5f5ff solid;
				}
				.comment-content {
					padding: 0 15px;
					border-top: 1px #eee solid;
				}
			}
		}
		
		.detail-bottom {
				position: fixed;
				bottom: 0;
				left: 0;
				display: flex;
				align-items: center;
				width: 100%;
				height: 44px;
				border-top: 1px #f5f5f5 solid;
				background-color: #fff;
				box-sizing: border-box;
		
				.detail-bottom__input {
					display: flex;
					justify-content: space-between;
					align-items: center;
					margin-left: 10px;
					padding: 0 10px;
					width: 100%;
					height: 30px;
					border: 1px #ddd solid;
					border-radius: 5px;
		
					text {
						font-size: 14px;
						color: #999;
					}
				}
		
				.detail-bottom__icons {
					display: flex;
					flex-shrink: 0;
					padding: 0 10px;
		
					.detail-bottom__icons-box {
						position: relative;
						display: flex;
						align-items: center;
						justify-content: center;
						width: 44px;
					}
				}
			}
	}
		.popup-body-wrapper{
			background-color: #fff;
			width:100%;
			.popup-header{
				display:flex;
				justify-content: space-between;
				color:#666;
				border-bottom: 1px solid #f5f5f5;
				.popup-text-item{
					height:45px;
					line-height: 45px;
					padding:0 15px;
				}
			}
			.popup-content{
				width:100%;
				// background-color: #fff;
				.content-count{
					display:flex;
					justify-content: flex-end;
					font-size: 14px;
					color: #999;
				}
			}
		}
</style>

