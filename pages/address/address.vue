<<template>
	<view class="choiceAddress">
		<view class="headerInfo">
			<view class="top">
				<text>请选择所在地区</text>
				<text class="cuIcon-roundclosefill" @tap="closeChoice"></text>
			</view>
			<!-- 已选择的信息 -->
			<view class="titleArea">
				<view class="has-choose-box flex-row pad-left">
					<view class="title" v-for="(item, index) in selectInfo" :key="index" :class="item.IsActive ? 'active' : ''" @tap="changeNavbar(index)">
						<text>{{ item.Name }}</text>
					</view>
				</view>
			</view>
		</view>
		<!-- 城市信息 -->
		<view class="cityInfo">
			<scroll-view scroll-y="true" id="city-item-box">
				<view class="cu-list menu" v-for="(pitem, index) in paintInfoList" v-show="pitem.IsActive" :key="pitem.Id">
					<view class="cu-item" v-for="item in pitem.Child" :key="item.ID" :class="item.ID === pitem.SelectId ? 'active' : ''">
						<view class="content" @tap="handleChoice(item, index)">
							<text class="cuIcon-roundcheck text-grey" v-if="item.ID === pitem.SelectId"></text>
							<text class="text-grey">{{ item.Name }}</text>
						</view>
					</view>
				</view>
			</scroll-view>
		</view>
	</view>
</template>
 
<script>
export default {
	data() {
		return {
			region: {},
			paintInfoList: [], //需要绘画的城市信息
			selectInfo: [
				{
					IsActive: true,
					ID: '-1',
					ParentId: '-1',
					Name: '请选择'
				}
			] //所选择的地址信息
		};
	},
	props: {
		regionInfo: {
			type: Array,
			required: true
		},
		callback: {
			type: Function,
			required: true
		}
	},
	methods: {
		closeChoice(){
			this.callback(true,this.selectInfo);
		},
		
		changeNavbar(index) {
			for (let item of this.selectInfo) {
				item.IsActive = false;
			}
			this.selectInfo[index].IsActive = true;
			for (let item of this.paintInfoList) {
				item.IsActive = false;
			}
			this.paintInfoList[index].IsActive = true;
		},
 
		handleChoice(item, index) {
			let tempIndex = index + 1;
			let selectItem = this.selectInfo[index];
			if (item.ID != selectItem.ID) {
				this.selectInfo.splice(tempIndex, this.selectInfo.length - 1);
				this.paintInfoList.splice(tempIndex, this.paintInfoList.length - 1);
				selectItem.ID = item.ID;
				selectItem.ParentId = item.ParentId;
				selectItem.Name = item.Name;
				selectItem.IsActive = false;
				this.paintInfoList[index].SelectId = item.ID;
				this.paintInfoList[index].IsActive = false;
				let tempArray = this.getRegionInfo(item.ID);
				if (tempArray !== null && tempArray !== undefined && tempArray.length > 0) {
					this.selectInfo.push({
						IsActive: true,
						ID: '-1',
						ParentId: '-1',
						Name: '请选择'
					});
					this.paintInfoList.push({
						Id: 'Y' + new Date().getTime(),
						SelectId: '',
						IsActive: true,
						Child: tempArray
					});
				} else {
					selectItem.IsActive = true;
					this.paintInfoList[index].IsActive = true;
					this.callback(true,this.selectInfo);
				}
			}
		},
 
		getRegionInfo(key) {
			let tempObj = this.region[key];
			let tempArray = []; //接收处理的数组
			if (tempObj === undefined) return tempArray;
			if (key === '86') {
				Object.keys(tempObj).forEach(keyName => {
					if (keyName === '910000') {
						tempArray.push({
							ID: '810000',
							ParentId: '-1',
							Name: '香港特别行政区'
						});
						tempArray.push({
							ID: '820000',
							ParentId: '-1',
							Name: '澳门特别行政区'
						});
					} else {
						tempArray.push({
							ID: keyName,
							ParentId: '-1',
							Name: tempObj[keyName]
						});
					}
				});
			} else {
				Object.keys(tempObj).forEach(keyName => {
					tempArray.push({
						ID: keyName,
						ParentId: key,
						Name: tempObj[keyName]
					});
				});
			}
			return tempArray;
		},
 
		init() {
			if (this.regionInfo.length > 0) {
				for (let item of this.regionInfo) {
					this.getRegionInfo(item);
				}
			}
		}
	},
	created() {
		uni.request({
			url: 'static/json/newRegion.json',
			success: res => {
				this.region = res.data;
				let tempArray = this.getRegionInfo('86');
				this.paintInfoList.push({
					Id: 'Y' + new Date().getTime(),
					IsActive: true,
					Child: tempArray
				});
				this.init();
			}
		});
	}
};
</script>
 
<style lang="scss">
.flex-row {
	display: flex;
	flex-direction: row;
}
.pad-left {
	padding-left: 30upx;
}
view {
	font-size: 26upx;
}
.choiceAddress {
	background-color: #ffffff;
	position: relative;
	.headerInfo {
		.top {
			height: 80upx;
			line-height: 80upx;
			text-align: center;
			font-size: 32upx;
			color: #8799a3;
			position: relative;
			.cuIcon-roundclosefill {
				position: absolute;
				top: 50%;
				transform: translateY(-50%);
				right: 20upx;
			}
		}
	}
}
 
.has-choose-box {
	height: 60upx;
	line-height: 60upx;
	box-shadow: 0 5upx 5upx #ccc;
	.title {
		margin-right: 50upx;
		border-bottom: 2upx solid #f5f5f5;
	}
	.title.active {
		color: #007aff;
		border-color: #007aff;
	}
}
 
#city-item-box {
	margin-top: 4upx;
	height: 500upx;
	.cu-list + .cu-list {
		margin-top: 0;
	}
	.cu-list.menu > .cu-item {
		min-height: 68upx;
	}
	.cu-list.menu > .cu-item.active {
		padding-left: 0;
		.cuIcon-roundcheck {
			margin-right: 0;
		}
		.text-grey,
		.line-grey,
		.lines-grey {
			color: #007aff !important;
		}
	}
}
</style>
