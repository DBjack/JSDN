<template>
	<gui-page :fullPage="true" :isLoading="pageLoading" ref="guiPage">
		<view slot="gBody" class="gui-flex1 gui-flex gui-columns">
			<!-- 局部选项卡 使用 切换导航 + swiper 实现 -->
			<view class="demo-nav">
				<gui-switch-navigation :items="tabs" :size="150" :currentIndex="currentIndex" @change="navchange"></gui-switch-navigation>
			</view>
			<swiper :current="currentIndex" @change="swiperChange" 
			:style="{height:mainHeight+'px', width:'750rpx'}">
				<!-- 轮播项目数量对应 上面的选项标签 -->
				<swiper-item>
					<!-- 使用滚动区域来实现主体内容区域 -->
					<scroll-view :scroll-y="true" class="gui-bg-gray" :style="{height:mainHeight+'px'}">
						<text class="gui-block-text gui-text gui-color-gray gui-text-center demo-text">one</text>
					</scroll-view>
				</swiper-item>
				<swiper-item>
					<!-- 使用滚动区域来实现主体内容区域 -->
					<scroll-view :scroll-y="true" class="gui-bg-blue" :style="{height:mainHeight+'px'}">
						<text class="gui-block-text gui-text gui-color-gray gui-text-center demo-text">two</text>
					</scroll-view>
				</swiper-item>
				<swiper-item>
					<!-- 使用滚动区域来实现主体内容区域 -->
					<scroll-view :scroll-y="true" class="gui-bg-green" :style="{height:mainHeight+'px'}">
						<text class="gui-block-text gui-text gui-color-gray gui-text-center demo-text">Three</text>
					</scroll-view>
				</swiper-item>
				<swiper-item>
					<!-- 使用滚动区域来实现主体内容区域 -->
					<scroll-view :scroll-y="true" class="gui-bg-red" :style="{height:mainHeight+'px'}">
						<text class="gui-block-text gui-text gui-color-gray gui-text-center demo-text">four</text>
					</scroll-view>
				</swiper-item>
				<swiper-item>
					<!-- 使用滚动区域来实现主体内容区域 -->
					<scroll-view :scroll-y="true" class="gui-bg-yellow" :style="{height:mainHeight+'px'}">
						<text class="gui-block-text gui-text gui-color-gray gui-text-center demo-text">five</text>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</gui-page>
</template>
<script>
var graceJS = require('@/GraceUI5/js/grace.js');
export default {
	data() {
		return {
			// 全屏 loading
			pageLoading : true,
			// 选项卡标签
			tabs : [{id:1,name:'One'},{id:2,name:'Two'},{id:3,name:'Three'},{id:4,name:'Four'},{id:5,name:'Five'}],
			// 选中选项的 索引
			currentIndex : 0,
			// 核心区域高度 
			mainHeight   : 200
		}
	},
	mounted:function(){
		// 01. 获取页面主体高度
		console.log('onload')
		graceJS.getRefs('guiPage', this, 0, (ref)=>{
			ref.getDomSize('guiPageBody', (e)=>{
				console.log(e);
				// 02. 导航的高度
				// 可以 使用 graceJS.select() 函数动态获取， 也可以使用 uni.upx2px 转换已知高度
				// 轮播主体高度 = 页面高度 - 导航高度
				this.mainHeight  = e.height - uni.upx2px(100);
				this.pageLoading = false;
			});
		});
	},
	methods: {
		navchange:function(index){
			this.currentIndex = index;
		},
		swiperChange : function(e){
			var index = e.detail.current;
			this.currentIndex = index;
		}
	}
}
</script>
<style>
.demo-nav{padding:15rpx 30rpx;}
.demo-text{line-height:200rpx; padding-bottom:3000px;}
</style>