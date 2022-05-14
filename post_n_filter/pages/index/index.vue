<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<navigator url="/pages/edit/edit">
			<u-button type="info">发布</u-button>
		</navigator>
		<navigator url="/pages/filter/filter">
			<u-button type="info">筛选</u-button>
		</navigator>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			}
		},
		onLoad() {

		},
		methods: {
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 100rpx;
		width: 100rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}


</style>
