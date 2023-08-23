<template>
  <view>
    <!-- <image class="detail-image" :src="news.picture" mode="aspectFit"></image> -->
    <view class="detail-title">{{ news.title }}</view>
    <view class="detail-brief">{{ news.brief }}</view>
	 <!-- 添加按钮，点击后跳转 -->
	<button class="read-article-button" @click="openArticle">阅读原文</button>
  </view>
</template>

<script>
export default {
  data() {
    return {
      news: {}, // 资讯详情从后端获取并赋值给这个对象
    };
  },
  onLoad(options) {
    const infoId = options.infoId;
	
    // 调用后端API，获取资讯详情数据，并赋值给this.news
	this.news={
		id:infoId,
		title:'666',
		brief:'888',
		url:'https://mp.weixin.qq.com/s/Yk2rHoosMHeOH_PLrDEl8g'
	}
  },
  methods: {
	  openArticle() {
	        // 执行跳转操作，使用 uni.navigateTo 或 uni.redirectTo
	        // 例如使用 uni.navigateTo：
	        uni.navigateTo({
	          url: '/pages/webview/webview?url=' + encodeURIComponent(this.news.url)
	        });
	      },
  }
};
</script>

<style scoped>
.detail-image {
  width: 100%;
  height: 300px;
}

.detail-title {
  font-size: 18px;
  font-weight: bold;
  margin: 10px;
}

.detail-brief {
  font-size: 14px;
  color: #666;
  margin: 10px;
}
</style>
