<template>
  <view class="webview">
    <web-view :src="url"></web-view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      url: '', // 从路由参数中获取文章链接
    };
  },
  onLoad(query) {
    if (query.url) {
      this.url = decodeURIComponent(query.url);
    }
  },
};
</script>
