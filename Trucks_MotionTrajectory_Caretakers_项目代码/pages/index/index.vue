<template>
	<view class="content">
		<!-- 按钮-左侧弹出菜单 -->
		<view class="VievButton" id="mainMenu" @click="showDrawer()">
			<img class='VievButtonImg' src="/static/Vector.png" alt="" srcset="">
		</view>
		<!-- 按钮-显示自己位置 -->
		<view class="radiusVievButton" id="myPosition" @click="move_to_location()">
			<img class='VievButtonImg' src="@/static/Crosshair.png" alt="" srcset="">
		</view>
		<!-- 窗口-左侧菜单 -->
		<uni-drawer 
		ref="mainMenu_drawer" 
		mode="left" 
		:mask-click="true"
		width="300"
		>
			<scroll-view style="height: 100%;" scroll-y="true">
				
			</scroll-view>
		</uni-drawer>
		<!-- 组件-地图 -->
		<map 
		id="Map"
		class="map"
		:longitude="longitude"
		:latitude="latitude"
		:show-compass="true"
		:show-location="true"
		@updated='move_to_location()'
		></map>
	</view>
</template>
<script>
	export default {
		name: 'TrucksMap',
		data() {
			return {
				longitude:113.790475,
				latitude:34.795507
			}
		},
		methods: {
			move_to_location() {
				uni.createMapContext('Map').moveToLocation();			
			},
			showDrawer() {
				this.$refs.mainMenu_drawer.open();
			},
			closeDrawer() {
				this.$refs.mainMenu_drawer.close();
			},
		}
	}
</script>

<style>
	.content {
		width: 750rpx;
		height: auto;
	}

	.map {
		width: 750rpx;
		height: 100vh;
	}

	.VievButton {
		width: 80rpx;
		height: 80rpx;
		background-color: white;
		border-radius: 5rpx;
		border: 0.5px inside #e4e4e4;
		box-shadow: 0px 1px 6px rgba(216, 216, 216, 0.5);
		display: grid; //生成3*3网格布局
		grid-template-columns: 20% 60% 20%;
		grid-template-rows: 20% 60% 20%;
	}

	.VievButtonImg {
		width: 100%;
		height: 100%;
		grid-row-start: 2; // 上边框是第二根网格线
		grid-column-start: 2; // 左边框是第二根网格线
		grid-row-end: 3; // 下边框是第三根网格线
		grid-column-end: 3; // 右边框是第三根网格线
	}

	.radiusVievButton {
		width: 80rpx;
		height: 80rpx;
		background-color: white;
		border-radius: 50%;
		border: 0.5px inside #e4e4e4;
		box-shadow: 0px 1px 6px rgba(216, 216, 216, 50%);
		display: grid; //生成3*3网格布局
		grid-template-columns: 10% 80% 10%;
		grid-template-rows: 10% 80% 10%;
	}

	#myPosition {
		z-index: 1;
		position: fixed;
		top: 75vh;
		right: 5vw;
	}

	#mainMenu {
		z-index: 1;
		position: fixed;
		top: 75vh;
		left: 5vw;
	}
</style>
