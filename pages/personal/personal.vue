<template>
	<view>
		<view class="gui-margin-top-large gui-padding">
			<text class="gui-h4 gui-bold gui-color-gray">个人中心</text>
		</view>
		<view class="gui-list gui-margin-top gui-padding">
			<view class="gui-list-items">
				<view class="gui-list-image ucenter-face gui-relative">
					<image class="gui-list-image ucenter-face-image"
						src="https://graceui.oss-cn-beijing.aliyuncs.com/faces/1.png" mode="widthFix"></image>
				</view>
				<view class="gui-list-body">
					<view class="gui-list-title">
						<text class="gui-list-title-text gui-primary-color">用户昵称</text>
					</view>
					<text class="gui-list-body-desc gui-color-gray gui-block-text">描述信息或签名信息</text>
				</view>
				<text class="gui-list-arrow-right gui-icons gui-color-gray">&#xe601;</text>
			</view>
		</view>
		<view class="ucenter-line"></view>
		<view>
			<gui-box-banner :items="items"></gui-box-banner>
		</view>
		<view class="ucenter-line"></view>
		<view class="gui-list gui-margin-top gui-padding">
			<view class="gui-list-items">
				<text class="gui-list-icon gui-icons gui-color-blue">&#xe60d;</text>
				<view class="gui-list-body gui-border-b">
					<view class="gui-list-title">
						<text class="gui-list-title-text">好友动态</text>
						<text class="gui-badge gui-bg-red gui-color-white">12</text>
					</view>
				</view>
				<text class="gui-list-arrow-right gui-icons">&#xe601;</text>
			</view>
			<view class="gui-list-items">
				<text class="gui-list-icon gui-icons gui-color-green">&#xe612;</text>
				<view class="gui-list-body gui-border-b">
					<view class="gui-list-title">
						<text class="gui-list-title-text">我的钱包</text>
					</view>
				</view>
				<text class="gui-list-arrow-right gui-icons">&#xe601;</text>
			</view>
			<view class="gui-list-items">
				<text class="gui-list-icon gui-icons gui-color-orange">&#xe624;</text>
				<view class="gui-list-body gui-border-b">
					<view class="gui-list-title">
						<text class="gui-list-title-text">我的文章</text>
					</view>
				</view>
				<text class="gui-list-arrow-right gui-icons">&#xe601;</text>
			</view>
			<view class="gui-list-items">
				<text class="gui-list-icon gui-icons gui-color-red">&#xe687;</text>
				<view class="gui-list-body">
					<view class="gui-list-title">
						<text class="gui-list-title-text">身份认证</text>
					</view>
				</view>
				<text class="gui-list-arrow-right gui-icons">&#xe601;</text>
			</view>
		</view>
		<view class="ucenter-line"></view>
		<view class="gui-list gui-margin-top gui-padding">
			<view class="gui-list-items">
				<text class="gui-list-icon gui-icons gui-color-yellow">&#xe613;</text>
				<view class="gui-list-body gui-border-b">
					<view class="gui-list-title">
						<text class="gui-list-title-text">账户设置</text>
					</view>
				</view>
				<text class="gui-list-arrow-right gui-icons">&#xe601;</text>
			</view>
			<view class="gui-list-items">
				<text class="gui-list-icon gui-icons gui-color-red">&#xe629;</text>
				<view class="gui-list-body">
					<view class="gui-list-title">
						<text class="gui-list-title-text">手机密保</text>
					</view>
				</view>
				<text class="gui-list-arrow-right gui-icons">&#xe601;</text>
			</view>
		</view>
		<view class="ucenter-line"></view>
		<view hover-class="gui-tap" @click="logout">
			<text class="gui-text-center gui-block-text gui-icons logoff gui-color-gray">&#xe62e; 退出登录</text>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				items: [
					[80, '', '动态'],
					[100, '', '好友'],
					[50, '', '私信'],
					['￥199', '', '余额']
				]
			}
		},
		methods: {
			logout() {
				console.log(111)
				uni.navigateTo({
					url: '/pages/login/login'
				})
			}
		}
	}
</script>
<style>
	.ucenter-face {
		width: 100rpx;
		height: 100rpx;
	}

	.ucenter-face-image {
		width: 100rpx;
		height: 100rpx;
	}

	.ucenter-line {
		height: 20rpx;
		background-color: #F6F7F8;
		margin: 16rpx 0;
	}

	.logoff {
		line-height: 88rpx;
		font-size: 28rpx;
	}

	.gui-list-title-text {
		line-height: 60rpx;
	}
</style>
