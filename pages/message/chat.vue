<template>
	<view>
		<!-- IM 消息展示区 -->
		<gui-im-message :msgs="msgs" 
		group="group1" userid="10000"></gui-im-message>
		<!-- 底部提交区 -->
		<gui-im-input 
		@chooseImage="chooseImage" 
		@sendText="sendText" 
		@sendVoice="sendVoice"></gui-im-input>
	</view>
</template>
<script>
// 模拟消息数据
var msgsData = require('@/GraceUI5/demoData/immessages.js');
export default {
	data() {
		return {
			msgs : msgsData.msgs
		}
	},
	methods: {
		// 01 发送文本消息
		sendText    : function (msg) {
			//提交给 IM 服务返回消息数据，添加到消息列表中
			//模拟IM 服务端返回消息
			var msg = {
				group         : 'group1',
				uindex        : '10000',
				uname         : '老兵张嘎',
				contentType   : 'txt',
				uface         : 'https://cmsuse.oss-cn-beijing.aliyuncs.com/g5/13.png',
				content       : msg,
				date          : '刚刚'
			}
			this.msgs.push(msg);
			this.pageScroll();
		},
		// 02 选择图片
		chooseImage : function (img) {
			console.log('选择图片');
			// 选择后返回临时图片
			// 请提交给 IM 服务器上传，上传后会产生真实图片地址，
			// 具体逻辑视 IM 后端情况来实现
			// 然后 IM 服务返回消息数据，添加到消息列表中
			// 模拟IM 服务端返回消息
			var msg = {
				group         : 'group1',
				uindex        : '10000',
				uname         : '老兵张嘎',
				contentType   : 'img',
				uface         : 'https://cmsuse.oss-cn-beijing.aliyuncs.com/g5/13.png',
				content       : img,
				date          : '刚刚'
			}
			this.msgs.push(msg);
			this.pageScroll();
		},
		// 03 发送语音消息
		sendVoice  : function (voice, vlength) {
			console.log(voice);
			// 录音后返回临时语音文件
			// 请提交给 IM 服务器上传，上传后会产生真实语音文件地址，
			// 具体逻辑视 IM 后端情况来实现
			// 然后 IM 服务返回消息数据，添加到消息列表中
			// 模拟IM 服务端返回消息
			var msg = {
				group         : 'group1',
				uindex        : '10000',
				uname         : '老兵张嘎',
				contentType   : 'voice',
				uface         : 'https://cmsuse.oss-cn-beijing.aliyuncs.com/g5/13.png',
				content       : voice,
				length        : vlength,
				date          : '刚刚'
			}
			this.msgs.push(msg);
			this.pageScroll();
		},
		// 滚动条滚动 [ 有新消息可以自动滚动到底部 ]
		pageScroll : function () {
			setTimeout(()=>{
				uni.pageScrollTo({
					scrollTop:999999+Math.random(),
					duration:100
				})
			},200);
		}
	},
}
</script>
<style>
page{background-color:#F7FBFE;}
</style>