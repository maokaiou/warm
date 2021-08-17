<template>
	<view class="uni-steps" style="margin-top:20upx;">
		<view :class="[direction==='column'?'uni-steps__column':'uni-steps__row']">
			<view :class="[direction==='column'?'uni-steps__column-container':'uni-steps__row-container']">
				<view :class="[direction==='column'?'uni-steps__column-line-item':'uni-steps__row-line-item']" v-for="(item,index) in options"
				 :key="index" @click="toStep(item)">
					<view :class="[direction==='column'?'uni-steps__column-line':'uni-steps__row-line',direction==='column'?'uni-steps__column-line--before':'uni-steps__row-line--before']"
					 :style="{backgroundColor:index<=active&&index!==0?activeColor:index===0?'transparent':deactiveColor}"></view>
					<view :class="[direction==='column'?'uni-steps__column-check':'uni-steps__row-check']" v-if="index === active">
						<uni-icons :color="activeColor" type="checkbox-filled" size="30"></uni-icons>
					</view>
					<view :class="[direction==='column'?'uni-steps__column-circle':'uni-steps__row-circle']" v-else>
						{{index + 1}}
					</view>
					<view :class="[direction==='column'?'uni-steps__column-line':'uni-steps__row-line',direction==='column'?'uni-steps__column-line--after':'uni-steps__row-line--after']"
					 :style="{backgroundColor:index<active&&index!==options.length-1?activeColor:index===options.length-1?'transparent':deactiveColor}"></view>
				</view>
			</view>
			<view :class="[direction==='column'?'uni-steps__column-text-container':'uni-steps__row-text-container']" style="margin-top:20upx;">
				<view v-for="(item,index) in options" :key="index" :class="[direction==='column'?'uni-steps__column-text':'uni-steps__row-text']">
					<text :style="{color:index<=active?activeColor:deactiveColor}" :class="[direction==='column'?'uni-steps__column-title':'uni-steps__row-title']">{{item.title}}</text>
					<text :style="{color:index<=active?activeColor:deactiveColor}" :class="[direction==='column'?'uni-steps__column-desc':'uni-steps__row-desc']">{{item.desc}}</text>
				</view>
			</view>
		</view>
	</view>
</template>


<script>
	import uniIcons from '../uni-icons/uni-icons.vue'
	export default {
		name: 'UniSteps',
		components: {
			uniIcons
		},
		props: {
			direction: {
				// 排列方向 row column
				type: String,
				default: 'row'
			},
			activeColor: {
				// 激活状态颜色
				type: String,
				default: '#1aad19'
			},
			deactiveColor: {
				// 未激活状态颜色
				type: String,
				default: '#999999'
			},
			active: {
				// 当前步骤
			type: Number,
				default: 0
			},
			options: {
				type: Array,
				default () {
					return []
				}
			} // 数据
		},
		data() {
			return {}
		},
		methods:{
			toStep(item){
				this.$emit('selectStep',item);
			}
		}
	}
</script>
				
<style lang="scss" scoped>
	.uni-steps {
		/* #ifndef APP-NVUE */
		display: flex;
		width: 100%;
		/* #endif */
		/* #ifdef APP-NVUE */
		flex: 1;
		/* #endif */
		flex-direction: column;
	}

	.uni-steps__row {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
	}

	.uni-steps__column {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row-reverse;
	}
.uni-steps__row-text-container {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
	}

	.uni-steps__column-text-container {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		flex: 1;
	}

	.uni-steps__row-text {
		/* #ifndef APP-NVUE */
		display: inline-flex;
		/* #endif */
		flex: 1;
		flex-direction: column;
	}

	.uni-steps__column-text {
		padding: 12upx 0upx;
		border-bottom-style: solid;
		border-bottom-width: 2upx;
		border-bottom-color: $uni-border-color;
/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
	}

	.uni-steps__row-title {
		font-size: $uni-font-size-base;
		line-height: 32upx;
		text-align: center;
	}

	.uni-steps__column-title {
		font-size: $uni-font-size-base;
		text-align: left;
		line-height: 36upx;
	}

	.uni-steps__row-desc {
		font-size: 24upx;
		line-height: 28upx;
		text-align: center;
	}

	.uni-steps__column-desc {
		font-size: $uni-font-size-sm;
		text-align: left;
		line-height: 36upx;
	}

	.uni-steps__row-container {
		height:60upx;
		border:1px soild red;
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
	}

	.uni-steps__column-container {
		/* #ifndef APP-NVUE */
		display: inline-flex;
		/* #endif */
		width: 60upx;
		flex-direction: column;
	}

	.uni-steps__row-line-item {
		/* #ifndef APP-NVUE */
		display: inline-flex;
		/* #endif */
		flex-direction: row;
		flex: 1;
		height: 60upx;
		line-height: 60upx;
		align-items: center;
		justify-content: center;
	}

	.uni-steps__column-line-item {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		flex: 1;
		align-items: center;
		justify-content: center;
	}

	.uni-steps__row-line {
		flex: 1;
		height: 2upx;
		background-color: $uni-text-color-grey;
	}

	.uni-steps__column-line {
		width: 2upx;
		background-color: $uni-text-color-grey;
	}

	.uni-steps__row-line--after {
		transform: translateX(1px);
	}

	.uni-steps__column-line--after {
		flex: 1;
		transform: translate(0px, 1px);
	}

	.uni-steps__row-line--before {
		transform: translateX(-1px);
	}

	.uni-steps__column-line--before {
		height: 12upx;
		transform: translate(0px, -1px);
	}

	.uni-steps__row-circle {
		border:1px solid #999999;
		background:transparent;
		width:60upx;
		height:60upx;
		border-radius: 50%;
		text-align: center;
		line-height: 54upx;
	}

	.uni-steps__column-circle {
		width: 10upx;
		height: 10upx;
		border-radius: 200upx;
		background-color: $uni-text-color-grey;
		margin: 8upx 0upx 10upx 0upx;
	}

	.uni-steps__row-check {
		margin: 0upx 12upx;
	}

	.uni-steps__column-check {
		height: 28upx;
		line-height: 28upx;
		margin: 4upx 0upx;
	}
</style>
