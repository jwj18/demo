<template>
	<view>
		<view id="header">
			<view class="weather-wrap">
				<img class="weather_icon" :src="weather_icon"/>
				<text class="weather-text">{{weather_text}}</text>
			</view>
			<view>
				<img class="log_pic" :src="log_pic_url"/>
			</view>	
			<text class="countdown">{{countdown}}</text>		
		</view>
		<view id="guide">
			<view v-for="(item,index) in guide" :key="index" class="guide-wrap">
				<img :src="item.icon" class="guide-icon">
				<text class="guide-text">{{item.txt}}</text>
			</view>
		</view>
		<view class="title_background">
			<view class="background-left"></view>
			<view class="background-right">
				<text>精选背景</text>
			</view>
		</view>
		<!--  -->
		<!-- <wfalls-flow :list="bgImgList" ref="wfalls" @finishLoad="getLoadNum"></wfalls-flow>    -->
		
		<view class="bgImg-wrap">
			<view class="upload">
				<img src="@/static/img/icon_upload_pic@2x.png" alt="">
				<text>自己传图</text>
			</view>
			<view
				v-for="(item,index) in bgImgList"
				:key="index"
				class="bgImg"
			>	
				<img :src="item" class="bgImg-wrap-img">
			</view>
			<view class="more">
				<text>更多美图</text>
			</view>
		</view>
		<view class="title_read">
			<view class="read-left"></view>
			<view class="read-right">
				<text>精选阅读</text>
			</view>
		</view>
		<view class="read-wrap">
			<view v-for="(item,index) in readData" :key="index" class="content">
				<view class="content-left">
					<img :src="item.icon" class="content-icon">
				</view>
				<view class="content-right">
					<text class="content-text1">{{item.title}}</text>
					<text class="content-text2">{{item.date}}</text>
				</view>
			</view>
		</view>
	</view>
	
	
		
	
</template>

<script>
	 import wfallsFlow from '@/components/wfalls-flow/wfalls-flow'
	export default {
	  components: { wfallsFlow  },
		data() {
			return {
				weather_icon: "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/icon_weather.png",
				weather_text: "",
				log_pic_url: "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/log_pic.png?1=1",//实际运用中，图片由后端返回
				
				//精刚导航栏数据 
				guide: [
				    {icon: "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/icon_guide1.png", txt: "换图"},
				    {icon: "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/icon_guide2.png", txt: "提醒"},
				    {icon: "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/icon_guide3.png", txt: "积分"},
				    {icon: "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/icon_guide4.png", txt: "成就"},
				],
				
				//精选图片数据
				bgImgList: ["https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/bg_img1.png", "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/bg_img2.png", "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/bg_img3.png", "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/bg_img4.png", "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/bg_img5.png", "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/bg_img6.png", "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/bg_img7.png"],
				// bgImgList: [{key: 'https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/bg_img1.png', label: 'https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/bg_img1.png'}],
				//精选阅读数据
				readData: [
				    {
				        icon: "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/read_pic1.png",
				        title: "好的界面设计并不始于图片，而是始于对人的理解",
				        date: "2021-06-12"
				    },
				    {
				        icon: "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/read_pic2.png",
				        title: "将已知的事物陌生化，更是一种创造",
				        date: "2021-06-10"
				    },
				    {
				        icon: "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/read_pic3.png",
				        title: "不要在你家里放一件你不知其用，或你认为不美的东西",
				        date: "2021-06-08"
				    },
				],
				
				//底部导航栏数据
				tabbar: [
				    {icon: "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/icon_tabbar1.png", txt: "早安"},
				    {icon: "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/icon_tabbar2.png", txt: "排名"},
				    {icon: "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/icon_tabbar3.png", txt: "统计"},
				    {icon: "https://xunmi-fe-test.oss-cn-shanghai.aliyuncs.com/img/icon_tabbar4.png", txt: "我的"},
				],
				
				//todo:html中需要的变量，请在此处定义
				countdown:"距离打卡结束倒计时 02:02:02"
				
			}
		},
		created: function () {
		    //获取天气文本
		    this.getWeatherText();
			this.getTimeText();
		},
		methods: {
			getWeatherText() {
			    this.weather_text = "江干区，小雨，气温24～31℃"
			},
			getTimeText(){
				const time = new Date();
				console.log(time)
			}
			
			//todo:如有需要，你可以在这里编写method，实现交互或者对变量赋值
		}
	}
</script>

<style scoped>
	#header{
		width: 688rpx;
		margin:0 auto;
	}
	/* 天气预报样式 */
	.weather-wrap{
		margin-top: 27rpx;
		margin-bottom: 12rpx;
	}
	.weather_icon {
	    width: 31rpx;
	    height: 23rpx;
		line-height: 38rpx;
	    /* vertical-align: -2px; */
	}
	
	.weather-text {		
		font-size: 27rpx;
		font-weight: 400;
		color: #4F4F4F;
		line-height: 38rpx;
	}
	
	/*打卡海报图样式*/
	
	.log_pic {
	    width: 100%;
		
	}
	
	/* todo:在这里往下继续编写css */
	
	/* 定时器样式 */
	.countdown{
		font-size: 27rpx;
		font-weight: 400;
		color: #000000;
		line-height: 38rpx;
		margin-left: 160rpx;
		margin-top: 15rpx;
		
	}
	/* guide样式 */
	#guide{
		width: 688rpx;
		margin:50rpx auto;
		display: flex;
		justify-content: space-around;
	}
	.guide-wrap{
		display: flex;
		flex-direction: column;
		text-align: center;
	}
	.guide-icon{
		width: 63rpx;
		height: 63rpx;
	}
	.guide-text{
		font-size: 23rpx;
		font-weight: 400;
		color: #4F4F4F;
		line-height: 33rpx;
		padding: 8rpx;
	}
	
	.title_background{
		display: flex;
		margin-bottom: 27rpx;
	}
	.background-left{
		margin-top: 6rpx;
		width: 12rpx;
		height: 67rpx;
		background-color: #F3CF56;
	}
	.background-right{
		width: 312rpx;
		height: 48rpx;
		margin-left: 15rpx;
		font-size: 35rpx;
		font-weight: 400;
		color: #4F4F4F;
		line-height: 48rpx;
		padding-top: 12rpx;
		padding-left: 17rpx;
		padding-bottom: 17rpx;
		background-color: #F3CF56;
		background-image: linear-gradient(90deg, rgba(243, 207, 86, 0.24) 0%, rgba(255, 255, 255, 0.5) 100%);
		border-radius: 10rpx;
	}
	
	.bgImg-wrap{
		width: 688rpx;
		margin:0 auto;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		position: relative;
	}
	.bgImg{
		width: 331rpx;
		height: 331rpx;
		margin-bottom: 31rpx;
		/* float: left; */
	}
	.bgImg:nth-of-type(3){
		margin-top: 183rpx;
	}
	.bgImg:nth-of-type(4){
		margin-top: -183rpx;
	 }
	.bgImg:nth-of-type(6){
		margin-top: -183rpx;
	}
	.bgImg:nth-of-type(8){
		margin-top: -183rpx;
	}
	.bgImg-wrap-img{
		width: 331rpx;
		height: 331rpx;
	}
  
	.upload{
		/* box-sizing: border-box; */
		width: 331rpx;
		height: 148rpx;
		background: rgba(243, 207, 86, 0.05);
		border-radius: 10rpx;
		border: 2rpx solid #F3CF56;
		margin: 4rpx 0 31rpx;
		font-size: 35rpx;
		font-family: PingFangSC-Regular, PingFang SC;
		font-weight: 400;
		color: #F3CF56;
		line-height: 48rpx;
		position: absolute;
		right: 0;
		top: 0;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.upload img{
		width: 54rpx;
		height: 48rpx;
		vertical-align: middle;
	}
	.upload text{
		font-size: 35rpx;
		font-family: PingFangSC-Regular, PingFang SC;
		font-weight: 400;
		color: #F3CF56;
		line-height: 48rpx;
	}
	.more{
		width: 331rpx;
		height: 133rpx;
		background: #F3CF56;
		border-radius: 10rpx;
		font-size: 35rpx;
		font-family: PingFangSC-Regular, PingFang SC;
		font-weight: 400;
		color: #FFFFFF;
		line-height: 48rpx;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	
	/* 精选阅读样式 */
	.title_read{
		margin-top: 46rpx;
		display: flex;
	}
	.read-left{
		margin-top: 6rpx;
		width: 12rpx;
		height: 67rpx;
		background-color: #F3CF56;
	}
	.read-right{
		width: 312rpx;
		height: 48rpx;
		margin-left: 15rpx;
		font-size: 35rpx;
		font-weight: 400;
		color: #4F4F4F;
		line-height: 48rpx;
		padding-top: 12rpx;
		padding-left: 17rpx;
		padding-bottom: 17rpx;
		background-color: #F3CF56;
		background-image: linear-gradient(90deg, rgba(243, 207, 86, 0.24) 0%, rgba(255, 255, 255, 0.5) 100%);
		border-radius: 10rpx;
	}
	/* 精选阅读 内容区样式 */
	.read-wrap{
		width: 688rpx;
		margin:0 auto 77rpx;
		padding-top: 4rpx;
	}
	
	.content{
		display: flex;
		margin-top: 23rpx;
	}
	.content-icon{
		width: 246rpx;
		height: 154rpx;
	}
	.content-right{
		margin-left: 23rpx;
		padding-top: 15rpx;
		display: flex;
		flex-direction: column;
	}
	.content-text1{
		font-size: 31rpx;
		font-family: PingFangSC-Regular, PingFang SC;
		font-weight: 400;
		color: #4F4F4F;
		line-height: 42rpx;
	}
	.content-text2{
		margin: 15rpx 2rpx 12rpx 298rpx;
		font-size: 23rpx;
		font-family: Helvetica;
		color: #757575;
		line-height: 27rpx;
	}
	
	
</style>
