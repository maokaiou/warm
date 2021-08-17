<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	@font-face {font-family: "iconfont";
	  src: url('~@/static/fonts/iconfont.eot?t=1614585994869'); /* IE9 */
	  src: url('~@/static/fonts/iconfont.eot?t=1614585994869#iefix') format('embedded-opentype'), /* IE6-IE8 */
	  url('data:application/x-font-woff2;charset=utf-8;base64,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') format('woff2'),
	  url('~@/static/fonts/iconfont.woff?t=1614585994869') format('woff'),
	  url('~@/static/fonts/iconfont.ttf?t=1614585994869') format('truetype'), /* chrome, firefox, opera, Safari, Android, iOS 4.2+ */
	  url('~@/static/fonts/iconfont.svg?t=1614585994869#iconfont') format('svg'); /* iOS 4.1- */
	}
	
	.iconfont {
	  font-family: "iconfont" !important;
	  font-size: 16px;
	  font-style: normal;
	  color:#FF8C69;
	  -webkit-font-smoothing: antialiased;
	  -moz-osx-font-smoothing: grayscale;
	}
	
	.icon-beizi:before {
	  content: "\e616";
	}
	
	.icon-maozi:before {
	  content: "\e619";
	}
	
	.icon-yifu:before {
	  content: "\e604";
	}
	
	.icon-xiezi:before {
	  content: "\e502";
	}
	
	.icon-kuzi:before {
	  content: "\e62e";
	}
	
	/* 用户设置 */
	.infor-list{
		height:90rpx;
		width:600rpx;
		margin:0px auto;
		color:#555555;
		display:flex;
		flex-direction: row;
		justify-content:center;
		align-items: center;
		border-bottom: 1px solid #d3d3d3;
	}
	.arrow-block{
		display:flex;
		flex-direction: row;
	/* 	justify-content: flex-end; */
	justify-content:center;
	align-items: center;
		margin-left:15rpx;
	}
	.set-icon{
		width:30rpx;
		height:30rpx;
	}
	.left-title{
		width:20%
	}
	.right-wrapper{
		display: flex;
		width:80%;
		flex-direction: row;
		justify-content: flex-end;
	}
	/* 我的 */
	
</style>
