<template>
	<div id="index-view">
		<van-sticky>
			<!-- 搜索框 -->
			<wj-search show-innerleft disabled @click="toSearchHandler"></wj-search>
		</van-sticky>

		<!-- 导航分类 -->
		<van-tabs 
		 sticky offset-top="555" 
		 v-model:active="active"
		 title-active-color="#CC3A8C"
		 title-inactive-color="#666"
		 line-width="30"
		 >
			<van-tab
			 v-for="item in catList"
			 :key="item.cat_id"
			 :title="item.cat_name"
			 :name="item.cat_id"
			 >
			  <!--动态切换组件 具体分类的内容 使用组件渲染 is属性值为组件名！-->
				<component 
				 :id="item.cat_id" 
				 :name="item.cat_name" 
				 :is="active == '0000' ? 'HomeContent' : 'OtherContent'"
				></component>
				<!-- <home-content 
				 :name="item.cat_name"
				 :id="item.cat_id"
				></home-content> -->
			</van-tab>
		</van-tabs>

	</div>
</template>

<script>
	// 引入组件
	import WjSearch from '../components/WjSearch.vue'
	import HomeContent from '../components/home/HomeContent.vue'
	import OtherContent from '../components/home/OtherContent.vue'

	export default {
		components : {
			WjSearch,
			HomeContent,
			OtherContent
		},

		data(){
			return {
				active : '0000',
				catList : []
			}
		},

		async created(){
			this.catList = await this.api.getCatData();
			this.catList.unshift({cat_id : '0000', cat_name : '首页'});
		},

		methods : {
			toSearchHandler(){
				//跳转到搜索页面
				console.log(this.$router)
				this.$router.push('/search');
			}
		}
	}
</script>


<style lang="less" scoped>
	.logo{
    color: var(--baseColor);
    font-size: 12px;
    border-right: 1px solid #666;
    padding-right: 8px;
  }
</style>
