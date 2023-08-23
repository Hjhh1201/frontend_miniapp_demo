<template>
  <view>
	
	<!-- 添加搜索框 -->
	
	    <!-- 添加搜索框和搜索按钮 -->
	    <view class="search-bar">
	      <input v-model="searchKeyword" placeholder="输入关键字搜索">
	      <button class="search-button" @click="handleSearchButtonClick">搜索</button>
	    </view>
		
		<view>筛选</view>
		    <view class="category-selector">
		          <view class="category-label">选择分类1：</view>
		          <view class="category-picker-container">
		            <picker class="category-picker" :value="selectedCategoryIndex1" :range="categories1" mode="selector" @change="handleCategoryChange1">
		              <view class="picker-content">{{ categories1[selectedCategoryIndex1] }}</view>
		            </picker>
		          </view>
		        </view>
		        <view class="category-selector">
		          <view class="category-label">选择分类2：</view>
		          <view class="category-picker-container">
		            <picker class="category-picker" :value="selectedCategoryIndex2" :range="categories2" mode="selector" @change="handleCategoryChange2">
		              <view class="picker-content">{{ categories2[selectedCategoryIndex2] }}</view>
		            </picker>
		          </view>
		        </view>
		        <view class="category-selector">
		          <view class="category-label">选择分类3：</view>
		          <view class="category-picker-container">
		            <picker class="category-picker" :value="selectedCategoryIndex3" :range="categories3" mode="selector" @change="handleCategoryChange3">
		              <view class="picker-content">{{ categories3[selectedCategoryIndex3] }}</view>
		            </picker>
		          </view>
		        </view>
			
		<!-- 添加排序按钮 -->
		    <view class="sort-buttons">
			  <button @click="sortByClicks">热度</button>
		      <button @click="sortByTime">时间</button>
		      
		    </view>
		
	

	<view class="news-list">
    
        <view class="news-item" v-for="news in filteredNewsList" :key="news.info_id" @click="navigateToDetail(news.info_id)">
          <!-- <image class="news-image" :src="news.picture" mode="aspectFill"></image> -->
          <view class="news-title" @click="navigateToDetail(news.info_id)">{{ news.title }}</view>
        </view>
	</view>
	
</view>
    
</template>

<script>
export default {
  data() {
    return {
      newsList: [{
		  info_id:1,
		  url:'shjsh',
		  title:'666',
		  brief:'888',
		  picture:'7',
		  time:'2022-09-09',
		  click:2
	  },{
		  info_id:2,
		  url:'shjsh',
		  title:'89',
		  brief:'8882',
		  picture:'7',
		  time:'2022-09-06',
		  click:2000
	  },{
		  info_id:3,
		  url:'shjsh',
		  title:'99999999最近',
		  brief:'8882',
		  picture:'7',
		  time:'2022-09-27',
		  click:200
	  },{
		  info_id:3,
		  url:'shjsh',
		  title:'99999999',
		  brief:'8882',
		  picture:'7',
		  time:'2022-09-06',
		  click:200
	  }], // 资讯数据从后端获取并赋值给这个数组
      sortBy: 'clicks', // 初始按点击数排序
	  searchKeyword: '',        // 搜索关键字
	  keyword: '',
	  filterNewsList: [],     // 过滤后的资讯列表
	  categories1: ['全部', '商学院', '人文学院','理工学院'], // 第一个下拉框的分类数据
	  selectedCategoryIndex1: 0, // 第一个下拉框的当前选中的分类索引
	  categories2: ['全部', '学分活动', '专家讲座','校内拓展','社团组织'], // 第二个下拉框的分类数据
	  selectedCategoryIndex2: 0, // 第二个下拉框的当前选中的分类索引
	  categories3: ['全部', '新生', '课程','申研'], // 第三个下拉框的分类数据
	  selectedCategoryIndex3: 0, // 第三个下拉框的当前选中的分类索引
    };
  },
  computed: {
    // sortedNews() {
    //   if (this.sortBy === 'clicks') {
    //     return this.newsList.slice().sort((a, b) => b.click - a.click);
    //   } else if (this.sortBy === 'time') {
    //     return this.newsList.slice().sort((a, b) => new Date(b.time) - new Date(a.time));
    //   }
    //   return this.newsList;
    // },
	filteredNewsList(){
		
		//调取后端接口，获得根据分类筛选后的结构，返回给filterNewList
		// ...
		
		
		// 完成过滤
		if (this.keyword === '') {
		  this.filterNewsList=this.newsList;
		} else {
		  this.filterNewsList = this.newsList.filter(news => {
		    return news.title.includes(this.keyword);
		  });
		}
		
		
		
		// 对过滤后的list完成排序
		if (this.sortBy === 'clicks') {
		  return this.filterNewsList.slice().sort((a, b) => b.click - a.click);
		} else if (this.sortBy === 'time') {
		  return this.filterNewsList.slice().sort((a, b) => new Date(b.time) - new Date(a.time));
		}
		return this.filterNewsList;
		
	}
  },
  methods: {
    sortByClicks() {
      this.sortBy = 'clicks';
	  
    },
    sortByTime() {
      this.sortBy = 'time';
	  
    },
	
	handleSearchButtonClick() {
	    this.handleSearch(); // 执行搜索操作
	  },
	  
	handleSearch() {
	    this.keyword=this.searchKeyword;
	    
	  },
	  
	handleCategoryChange1(event) {
	    this.selectedCategoryIndex1 = event.detail.value;
	    
	  },
	
	  handleCategoryChange2(event) {
	    this.selectedCategoryIndex2 = event.detail.value;
	    
	  },
	
	  handleCategoryChange3(event) {
	    this.selectedCategoryIndex3 = event.detail.value;
	    
	  },
	 // applySorting() {
	 //    const sortedNewsList = [...this.filteredNewsList];
	 //    sortedNewsList.sort((a, b) => {
	 //      if (this.sortBy === 'time') {
	 //        return new Date(b.time) - new Date(a.time);
	 //      } else if (this.sortBy === 'clicks') {
	 //        return b.clicks - a.clicks;
	 //      }
	 //    });
	 //    this.filteredNewsList = sortedNewsList;
	 //  },
	 //  handleSearch() {
	 //      this.filteredNewsList = this.newsList.filter(news => {
	 //        return news.title.includes(this.searchKeyword);
	 //      });
	 //      this.applySorting(); // 在过滤后应用排序
		  
	 //    },
    navigateToDetail(infoId) {
      uni.navigateTo({
        url: '/pages/detail/detail?infoId=' + infoId,
      });
    }
  },
};
</script>

<style scoped>
/* ...（其他样式） */
.search-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 15px;
}

input {
  flex: 1;
  padding: 6px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.search-button {
  padding: 2px 4px; /* 调整按钮的内边距 */
  background-color: #dbe9e9;
  border: none;
  border-radius: 3px;
  color: #333;
  cursor: pointer;
}
.page {
  background-color: #f5f5f5; /* 设置背景色 */
}

.sort-buttons {
  width: 100px;
  height: 40px;
  font-size: 1px;
  display: flex;
  justify-content: center;
  margin: 8px; /* 调整按钮上下外边距 */
}

button {
  margin: 0 3px; /* 调整按钮左右外边距 */
  padding: 2px 4px; /* 调整按钮内边距 */
  background-color: #dbe9e9;
  border: none;
  border-radius: 3px;
  color: #333;
  cursor: pointer;
}

.news-list {
  padding: 10px;
  background-color: #fff; /* 资讯列表背景色 */
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* 添加阴影效果 */
}

.news-item {
  display: flex;
  align-items: center;
  margin-bottom: 8px;
  cursor: pointer;
  padding: 8px;
  border-radius: 5px;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.news-image {
  width: 80px;
  height: 80px;
  margin-right: 8px;
  border-radius: 5px;
}

.news-title {
  font-size: 18px;
  color: #333;
}
</style>
