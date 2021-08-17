<template>
	<view class="comments-wrapper">
		<view class="comments-header">
			<view class="comments-header__logo">
				<image src="../../static/login.jpg" mode="aspectFill"></image>
			</view>
			<view class="comments-header__info">
				<view  class="title">{{comment_show.id}}</view>
				<!-- <view v-else class="title">{{comments.author.author_name}} <text class="reply-text">回复</text>{{comments.to}}</view> -->
				<view>{{comment_show.createdTime}}</view>
			</view>
		</view>
		<view class="comments-content">
			<view>{{comment_show.content}}</view>
			<view class="comments-info">
				<view class="comments-button">回复</view>
			</view>
			<view class="comments-reply" >
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			comment_show:{
				type:Object,
				default(){
					return{}
				}
			}
		},
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="scss">
	.comments-wrapper {
			margin: 15px 0;
	
			.comments-header {
				display: flex;
	
				.comments-header__logo {
					flex-shrink: 0;
					width: 30px;
					height: 30px;
					border-radius: 5px;
					overflow: hidden;
	
					image {
						width: 100%;
						height: 100%;
					}
				}
	
				.comments-header__info {
					display: flex;
					flex-direction: column;
					padding-left: 15px;
					font-size: 12px;
					color: #999;
					line-height: 1;
	
					.title {
						margin-bottom: 10px;
						font-size: 14px;
						color: #333;
	
						.reply-text {
							margin: 0 10px;
							font-weight: bold;
							color: #000;
						}
					}
				}
			}
	
			.comments-content {
				margin-top: 10px;
				font-size: 14px;
				color: #000;
	
				.comments-info {
					margin-top: 15px;
					display: flex;
	
					.comments-button {
						padding: 2px 10px;
						font-size: 12px;
						color: #999;
						border-radius: 20px;
						border: 1px #ccc solid;
					}
				}
	
				.comments-reply {
					display: flex;
					margin: 15px 0;
					padding: 0 10px;
					border: 1px #eee solid;
				}
	
			}
	
		}
</style>
