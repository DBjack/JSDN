<template>
	<gui-page :customFooter='true'>
		<!-- 页面主体 -->
		<view slot="gBody">
			<Home v-if="curNav == 0"></Home>
			<Message v-if="curNav === 1"></Message>
			<Personal v-if="curNav == 4"></Personal>
		</view>
		
		<view slot='gFooter'>
			<tabBar @navChange='navChange'></tabBar>
		</view>
	</gui-page>
</template>
<script>
import Swiper from '../swiper/swiper.nvue'
import tabBar from '../../components/tabBar/tabBar.nvue'
import scroll from '../scroll/scroll.nvue'
import Home from '../home/home.vue'
import Message from '../message/message.vue'
import Personal from '../personal/personal.vue'


export default {
	components:{ Swiper, tabBar,scroll,Home,Personal,Message },
	data() {
		return {
			search: '',
			curNav: 0,
		}
	},
	methods: {
		navChange(index) {
			this.curNav = index
		}
	}
}
</script>