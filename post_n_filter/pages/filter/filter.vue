<template>
	
	<view class="content">
	<!--要自定义导航栏，首先要取消系统自带的导航栏，需要在uni-app目的根目录的"pages.json"中设置-->
		<view class="bar">
			<u-button @click="show = true">筛选</u-button>
		</view>
		<view class="container">

		</view>
		
		<!--弹出层 进行筛选-->
		<u-popup :show="show" :round="20" mode="top" :safeAreaInsetTop="true" @close="close" @open="open">
			<view class="popup">
				<view id="popupTop">
					
					
				</view>
				<view id="popupBottom">
					<u-button type="default">取消</u-button>
					<u-button type="default">确认</u-button>
				</view>
			</view>
		</u-popup>

	</view>
</template>

<script>

	export default {
		
		data() {
			return {
				show: false,
				

				
			}
		},
		onLoad() {

		},
		methods: {
			open() {
				// console.log('open');
			},
			close() {
			    this.show = false
			    // console.log('close');
			},
			rightClick() {
	            console.log('rightClick');
	        },
		    leftClick() {
	            console.log('leftClick');
	        },
			checkboxChange(n) {
			            console.log('change', n);
			},
		}	
	}
</script>

<style>
	
</style>
