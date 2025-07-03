<template>
  <view class="navbar">
    <view 
      class="nav-item" 
      :class="{ active: currentIndex === 0 }" 
      @click="currentIndex = 0"
    >特价</view>
    <view 
      class="nav-item" 
      :class="{ active: currentIndex === 1 }" 
      @click="currentIndex = 1"
    >首页</view>
    <view 
      class="nav-item" 
      :class="{ active: currentIndex === 2 }" 
      @click="currentIndex = 2"
    >秒送</view>
    <view 
      class="nav-item" 
      :class="{ active: currentIndex === 3 }" 
      @click="currentIndex = 3"
    >外卖</view>
    <view 
      class="nav-item" 
      :class="{ active: currentIndex === 4 }" 
      @click="currentIndex = 4"
    >新品</view>
	<view class="ad-container">
	  <image class="ad-image" src="/static/img/@V]9072X24Z6H6T1AUE0I~O.png"></image>
	</view>
  </view>
  
  <Search
    v-model="value"
    show-action
    
    :placeholder="currentPlaceholder"
    @search="onSearch"
  >
    <!-- 自定义左侧图标 -->
    <template #left-icon>
      <Icon name="scan" />
    </template>
	
	
    <template #action >
		<div style="display: flex;">
			<img src="/static/img/照相机.png" style="width: 58rpx;height: 64rpx;margin-right: 20px;"/>
		<div @click="onClickButton" >
		  
		  搜索
		</div>
		</div>
    </template>
  </Search>
  
<view class="swiper_navbar">
	 <text class="text-item" style="font-weight: bold;">推荐</text>
<Swipe :loop="false" :width="65" :show-indicators="false" style="width: 486rpx;padding: 0 0;">
  <SwipeItem v-for="(item,index) in items" :key="index">{{item}}</SwipeItem>
</Swipe>
	<Icon name="wap-nav" />
    <text class="text-item">分类</text>
</view>

<view class="container618">
	<view class="duanwu">
		<text class="text1">空调补贴</text>
		<img class="air_cond" src="/static/img/空调.png"/>
		<text class="text2">立减35%</text>
	</view>
	
	<view class="liquor">
		 <img class="air_cond" src="/static/img/酒.png"/>
	</view>
	
	<view class="actice618">
		<text class="text1_618">618周年庆</text>
		<text class="text2_618">明晚8点开启</text>
		<text class="text3_618">白亿补贴4折起</text>
	</view>
	
	<view class="yuan1000">
		<text class="text1">买车养车</text>
		<img class="air_cond" src="/static/img/自行车.png"/>
		<text class="text2">不止5折</text>
	</view>
</view>

<Swipe :loop="false" :width="90" :show-indicators="false"  style="width: 100%;height:175rpx; padding: 20rpx 0;">
 <SwipeItem v-for="(text, index) in box_text" :key="index"  >
    <view class="swiper_ad">
      <text class="swiper_ad_text1">{{ text }}</text>
      <text>{{ box_script[index] }}</text>
    </view>
  </SwipeItem>
</Swipe>

<Products></Products>
<TabBar></TabBar>
</template>

<script setup>
import { ref,computed,onMounted,onUnmounted } from 'vue';
import { Button,Search,Icon,Swipe, SwipeItem,Tabbar, TabbarItem } from 'vant';

const items = ref(['国家补贴', '食品', '手机', '酒饮', '数码','女装','男装'])

const currentIndex = ref(1); // 默认选中首页，索引从0开始
const search_text = ref(['九阳电热水壶', '九阳保温烧水壶', '容声水壶', '长虹电水壶'])
const index = ref(0);
const box_text = ref(['618', '30', '日', '晚','8','点'])
const box_script = ref(['秒杀', '京东快递', '领卷', '京东到家','京东校园','借款'])

const currentPlaceholder = computed(() => search_text.value[index.value]);

let intervalId;

onMounted(() => {
  intervalId = setInterval(() => {
    index.value = (index.value + 1) % search_text.value.length;
  }, 3000);
});

onUnmounted(() => {
  clearInterval(intervalId);
});

const onClickButton = () => {
  console.log('点击了搜索按钮');
};


</script>

<style lang="scss" scoped>
.navbar {
  display: flex;
  background-color: #ff4d4f; /* 红色背景 */
  padding: 0 0;
  width: 100%;
  height: 95rpx;
  
}

.nav-item {
  flex: 1;
  text-align: center;
  color: white;
  padding: 10px 0;
  cursor: pointer;
}

.nav-item.active {
  border-bottom: 2px solid white; /* 选中项下划线 */
}

.ad-container {
  flex: 0 0 auto; /* 自动宽度 */
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: 10px; /* 添加左边距 */
  z-index: 10; /* 设置 z-index */
}

.ad-image {
  width: 271rpx; /* 增加宽度 */
  height: 100%;
}

.swiper_navbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 734rpx;
  height: 64rpx;
 
 
}

.text-item {
  
  text-align: center;
  color: #333;
  
  padding: 0 0;
  width: 104 rpx
}

.van-swipe-item {
  width: 104rpx;
  text-align: center;
}

.container618{
	width: 100%;
	height: 248rpx;
	background-color: red;
	display: flex;
	border-radius: 20rpx; /* 设置圆角半径 */
	.duanwu{
		  display: flex;
		  flex-direction: column; /* 改为垂直排列 */
		  justify-content: flex-start; /* 从顶部开始排列 */
		  align-items: center; /* 水平居中对齐 */
		  background-color: white;
		  width: 20%; /* 根据需要调整 */
		  height: 199rpx; /* 根据需要调整 */
		  margin: 20rpx; /* 上下左右间距都为10rpx */
		  border-radius: 20rpx;
		  .text1{
			    font-size: 12px; /* 缩小字体大小，可根据需要调整 */
			    font-weight: bold; /* 加粗字体 */
			    margin-top: 0; /* 与顶部的间距 */
		  }
		  .air_cond{
				font-size: 12px; /* 缩小字体大小，可根据需要调整 */
				font-weight: bold; /* 加粗字体 */
				margin-top: 50rpx; /* 与顶部的间距 */
		  }
		  .text2{
		  			    font-size: 12px; /* 缩小字体大小，可根据需要调整 */
		  			    font-weight: bold; /* 加粗字体 */
						width:90%;
		  			    margin-top: 40rpx; /* 与顶部的间距 */
						background-color: red;
						color: white;
						text-align: center;
						border-radius: 20rpx;
		  }
	}
	.actice618{
		  display: flex;
		  flex-direction: column; /* 改为垂直排列 */
		  justify-content: flex-start; /* 从顶部开始排列 */
		  align-items: center;
		  width: 40%; /* 根据需要调整 */
		  height: 199rpx; /* 根据需要调整 */
		  margin: 20rpx; /* 上下左右间距都为10rpx */
		  border-radius: 20rpx;
		  .text1_618{
				 position: relative; /* 设置为相对定位 */
			  font-size: 18px; /* 缩小字体大小，可根据需要调整 */
			  font-weight: bold; /* 加粗字体 */
			  width:90%;
			  margin-top: 0; /* 与顶部的间距 */
			  background-color: red;
			  color: white;
			  text-align: center;
			  border-radius: 20rpx;
		  }
		  .text2_618{
		  				 position: relative; /* 设置为相对定位 */
		  			  font-size: 20px; /* 缩小字体大小，可根据需要调整 */
		  			  font-weight: bold; /* 加粗字体 */
		  			  width:90%;
		  			  margin-top: 30rpx; /* 与顶部的间距 */
		  			  background-color: red;
		  			  color: white;
		  			  text-align: center;
		  			  border-radius: 20rpx;
		  }
		  .text3_618{
		  				 position: relative; /* 设置为相对定位 */
		  			  font-size: 15px; /* 缩小字体大小，可根据需要调整 */
		  			  font-weight: bold; /* 加粗字体 */
		  			  width:90%;
		  			  margin-top: 20rpx; /* 与顶部的间距 */
		  			  background-color: white;
		  			  color: red;
		  			  text-align: center;
		  			  border-radius: 20rpx;
		  }
		
	}
	.yuan1000{
		  display: flex;
		  flex-direction: column; /* 改为垂直排列 */
		  justify-content: flex-start; /* 从顶部开始排列 */
		  align-items: center; /* 水平居中对齐 */
		  background-color: white;
		  width: 20%; /* 根据需要调整 */
		  height: 199rpx; /* 根据需要调整 */
		  margin: 20rpx; /* 上下左右间距都为10rpx */
		  border-radius: 20rpx;
		  .text1{
			    font-size: 12px; /* 缩小字体大小，可根据需要调整 */
			    font-weight: bold; /* 加粗字体 */
			    margin-top: 0; /* 与顶部的间距 */
		  }
		  .air_cond{
				font-size: 12px; /* 缩小字体大小，可根据需要调整 */
				font-weight: bold; /* 加粗字体 */
				margin-top: 50rpx; /* 与顶部的间距 */
		  }
		  .text2{
		  			    font-size: 12px; /* 缩小字体大小，可根据需要调整 */
		  			    font-weight: bold; /* 加粗字体 */
						width:90%;
		  			    margin-top: 2rpx; /* 与顶部的间距 */
						background-color: red;
						color: white;
						text-align: center;
						border-radius: 20rpx;
		  }
	}
	.liquor{
		  display: flex;
		  justify-content: center;
		  background-color: white;
		  align-items: center;
		  width: 20%; /* 根据需要调整 */
		  height: 199rpx; /* 根据需要调整 */
		  margin: 20rpx; /* 上下左右间距都为10rpx */
		  border-radius: 20rpx;
	}
}

.swiper_ad{
	display: flex;
	flex-direction: column; /* 改为垂直排列 */
	justify-content: flex-start; /* 从顶部开始排列 */
	align-items: center; /* 水平居中对齐 */
	
	.swiper_ad_text1{
		background-color: red;
		color: white;
		width: 84rpx;
		height: 89rpx;
		text-align: center;
		font-weight: bold;
		line-height: 89rpx;
		border-radius: 20rpx;
		font-size: 50rpx; /* 设置字体大小为 30rpx */
	}
	
}


</style>