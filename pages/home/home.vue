<template>
	<gui-page :fullPage="true" :customHeader="true" ref="guiPage" :isLoading="pageLoading">
		<view slot='gHeader'>
			<view class="gui-margin-top gui-bg-gray search-warp gui-border-box">
				<gui-search></gui-search>
			</view>
		</view>
		<view slot="gBody" class="gui-margin-top gui-flex1" style="background-color:#F8F8F8;">
			<!-- 分类导航 -->
			<view class="header gui-border-b gui-border-box gui-flex gui-columns gui-justify-content-center"
				id="myheader">
				<gui-switch-navigation :size="150" activeLineBg="linear-gradient(to right, #008AFF,#008AFF)"
					:items="navItems" @change="navchange"></gui-switch-navigation>
			</view>
			<!-- 滚动区域高度 = gBody - 自定义区域高度 -->
			<scroll-view :scroll-y="true" :show-scrollbar="false" :style="{height:mainHeight+'px'}"
				@touchstart="touchstart" @touchmove="touchmove" @touchend="touchend" @scrolltolower="loadmorefun"
				@scroll="scroll">
				<!-- 刷新组件 -->
				<gui-refresh @reload="reload" ref="refreshcom"></gui-refresh>
				<!-- 数据展示区域 -->
				<view>
					<gui-article-list :articles="newsList" @newstap="newstap"></gui-article-list>
				</view>
				<!-- 加载组件 -->
				<gui-loadmore ref="loadmorecom"></gui-loadmore>
			</scroll-view>
		</view>
	</gui-page>
</template>
<script>
	var graceJs = require('@/GraceUI5/js/grace.js');
	// 模拟 api 请求数据，格式见 article.js
	var artciles = require('@/GraceUI5/demoData/article.js');
	export default {
		data() {
			return {
				// 页面加载
				pageLoading: true,
				// 主体高度
				mainHeight: 200,
				// 滚动区域滚动距离
				scrollTop: 0,
				// 加载更多延迟
				loadMoreTimer: null,
				// 分类
				navItems: [{
						id: 1,
						name: '关注'
					}, {
						id: 2,
						name: '推荐'
					},
					{
						id: 3,
						name: '热榜'
					}, {
						id: 4,
						name: '前端'
					},
					{
						id: 5,
						name: '后端'
					}, {
						id: 6,
						name: '其他'
					}
				],
				// 当前展示的分类索引
				currentIndex: 0,
				// 新闻列表数据， 分类切换重新获取第一页
				newsList: [],
				// 页码
				page: 1
			}
		},
		mounted: function() {
			// 01. 获取页面主体高度
			graceJs.getRefs('guiPage', this, 0, (ref) => {
				ref.getDomSize('guiPageBody', (e) => {
					// 主体高度 = 页面高度 - 自定义区域高度
					graceJs.select('#myheader', (e2) => {
						// 如果自定义区域有 margin 尺寸获取不到请加上这个值，可以利用 uni.upx2px() 转换
						this.mainHeight = e.height - uni.upx2px(100);
						this.pageLoading = false;
						// 第一次加载数据
						this.getNews();
					});
				});
			});
		},
		methods: {
			navchange: function(index) {
				// 刷新当前分类对应的数据
				if (this.currentIndex != index) {
					this.page = 1;
					this.currentIndex = index;
					this.getNews();
					// 重置加载组件状态
					this.$refs.loadmorecom.stoploadmore();
				}
			},
			// 新闻加载函数
			// isReload 代表下拉刷新
			getNews: function(isReload) {
				if (this.page <= 1) {
					this.newsList = [];
					if (!isReload) {
						this.pageLoading = true;
					}
				}
				// 真实情况 url 地址类似如下格式 :
				// var url = 'http://您的api域名/**/**/?分类id='+this.navItems[this.currentIndex].id+'&页码='+this.page;
				// 连接 api 获取新闻数据
				// 模拟 api 加载数据
				setTimeout(() => {
					// 对演示数据随机刷新模拟数据刷新
					var demoArr = graceJs.arrayShuffle(artciles.articleList);
					if (this.page >= 2) {
						this.newsList = this.newsList.concat(demoArr);
						// 加载完成后停止加载动画
						this.$refs.loadmorecom.stoploadmore();
						// 假定第3页加载了全部数据，通知组件不再加载更多
						// 实际开发由接口返回值来决定
						if (this.page >= 3) {
							this.$refs.loadmorecom.nomore();
						}
					}
					// 第一页 有可能是第一次加载或者刷新
					else {
						this.newsList = [];
						this.newsList = demoArr;
						// 刷新
						if (isReload) {
							this.$refs.refreshcom.endReload();
						}
						this.pageLoading = false;
					}
					this.page++;
				}, 800);

			},
			scroll: function(e) {
				this.scrollTop = e.detail.scrollTop;
			},
			// 下拉刷新相关事件绑定
			touchstart: function(e) {
				if (this.scrollTop > 0) {
					return;
				}
				this.$refs.refreshcom.touchstart(e);
			},
			touchmove: function(e) {
				if (this.scrollTop > 0) {
					return;
				}
				this.$refs.refreshcom.touchmove(e);
			},
			touchend: function(e) {
				if (this.scrollTop > 0) {
					return;
				}
				this.$refs.refreshcom.touchend(e);
			},
			// 刷新事件
			reload: function() {
				this.page = 1;
				this.getNews(true);
				// 刷新时重置加载组件状态
				this.$refs.loadmorecom.stoploadmore();
			},
			// 加载更多事件
			loadmorefun: function() {
				// 获取加载组件状态看一下是否还能继续加载
				// 保证触底只执行一次加载
				if (this.loadMoreTimer != null) {
					clearTimeout(this.loadMoreTimer);
				}
				this.loadMoreTimer = setTimeout(() => {
					var status = this.$refs.loadmorecom.loadMoreStatus;
					if (status != 0) {
						return null;
					}
					this.$refs.loadmorecom.loading();
					// 此处开启加载动画执行加载数据的函数
					this.getNews();
				}, 80);
			},
			// 新闻点击
			newstap: function(e) {
				// 获取新闻 id
				var newsId = e;
				console.log(newsId);
				// 打开新闻详情页面
				//uni.navigateTo()
			}
		}
	}
</script>
<style>
	.header {
		padding: 15rpx 30rpx;
		height: 100rpx;
	}
</style>
