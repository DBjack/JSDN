<template>
	<view>
		<view class="gui-margin gui-margin-top">
			<text class="gui-h5 gui-color-gray gui-bold">消息列表</text>
		</view>
		<view class="my-list">
			<navigator class="gui-list-items">
				<view class="gui-list-image gui-relative">
					<image class="gui-list-image" 
					src="https://cmsuse.oss-cn-beijing.aliyuncs.com/g5/15.png"></image>
					<view class="gui-badge-point"></view>
				</view>
				<view class="gui-list-body gui-border-b">
					<view class="gui-list-title">
						<text class="gui-list-title-text gui-primary-color">标题信息</text>
						<text class="gui-list-title-desc gui-color-gray">08/18/2020</text>
					</view>
					<text class="gui-list-body-desc gui-color-gray">描述信息</text>
				</view>
				<text class="gui-list-arrow-right gui-icons gui-color-gray-light">&#xe601;</text>
			</navigator>
			<navigator class="gui-list-items">
				<text class="gui-list-icon gui-icons gui-color-red">&#xe6cf;</text>
				<view class="gui-list-body gui-border-b">
					<view class="gui-list-title">
						<text class="gui-list-title-text gui-primary-color">标题信息</text>
						<text class="gui-list-title-desc gui-color-gray">08/18/2020</text>
					</view>
					<text class="gui-list-body-desc gui-color-gray">描述信息</text>
				</view>
				<text class="gui-list-arrow-right gui-icons gui-color-gray-light">&#xe601;</text>
			</navigator>
			<navigator class="gui-list-items">
				<text class="gui-list-icon gui-icons gui-color-green">&#xe666;</text>
				<view class="gui-list-body gui-border-b">
					<view class="gui-list-title">
						<text class="gui-list-title-text gui-list-one-line gui-primary-color">单行模式</text>
						<text class="gui-list-title-desc gui-color-gray">08/18/2020</text>
					</view>
				</view>
				<text class="gui-list-arrow-right gui-icons gui-color-gray-light">&#xe601;</text>
			</navigator>
			<navigator class="gui-list-items">
				<text class="gui-list-icon gui-icons gui-color-blue">&#xe61f;</text>
				<view class="gui-list-body gui-border-b">
					<view class="gui-list-title">
						<text class="gui-list-title-text gui-primary-color gui-list-one-line gui-ellipsis" 
						style="width:320rpx; height:60rpx;">标题文本文字很多，溢出省略</text>
					</view>
				</view>
				<text class="gui-list-arrow-right gui-icons gui-color-gray-light">&#xe601;</text>
			</navigator>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>
<style>
.my-list{margin:30rpx 0; padding:0 30rpx;}
</style>