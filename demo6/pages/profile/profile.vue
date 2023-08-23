<template>
  <view class="profile">
    <view class="profile-info">
      <text class="profile-name">用户名: {{ userName }}</text>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      userName: 'John Doe', // 用户名
    };
  },
};
</script>

<style scoped>
.profile {
  padding: 20px;
}

.profile-info {
  padding: 20px;
  border: 1px solid #ccc;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.profile-name {
  font-size: 20px;
  color: #333;
}
</style>
