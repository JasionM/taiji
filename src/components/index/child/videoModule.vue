<template>
	<div id="videoModule">
		<img src="./../../../assets/video_bg.png" class="bg_pic">
		<div class="container">
			<div class="main">
				<div class="top_info">
					<div class="title">
						<h3>首推视频</h3>
						<h3>{{currentVideo.title}}</h3>
					</div>
					<div class="intro">
						<p v-for="info in currentVideo.content.split(';')">{{info}}</p>
						<!-- <p>陈式太极拳“四大金刚”之一的陈正雷老师独家授权并参与拍摄的教学视频库，由赏析视频，教学视频与动作库三部分组成</p>
						<p>并邀请陈正雷大师亲自示范</p>
						<p>陈正雷大师若干弟子全程参与课程拍摄和文字整理，保证了教学视频的科学，系统及标准化</p> -->

					</div>
				</div>
				<div class="video_swipe">
					<videoSwiper :videoList="videoList"></videoSwiper>
				</div>
				<div class="bottom">
					<button type="button" @click="gotoVideoGroup">进入视频区</button>
				</div>
			</div>
		</div>
		<transition name="fade">
			<videoPlayPage :url="url" :poster="poster" :title="title" v-if="showVideoPlay"></videoPlayPage>
		</transition>
	</div>
</template>
<script>
	import videoPlayPage from "./../../public/videoPlayPage.vue";
	import videoSwiper from "./videoSwiper.vue";
	export default {
	  	name: '',
	  	props: ["videoList"],
	  	data () {
		    return {
				url: "",
				poster: "",
				showVideoPlay: false,
				currentVideo:{},
				startIndex: 1,
				title: "",
		    }
		},
		components: {
			videoSwiper,
			videoPlayPage
		},
		computed: {
			swiper() {
		     	return this.$refs.mySwiper.swiper;
		    }
		},
		mounted: function () {
			let windowHeight = $(window).height() < 893?893:$(window).height();
			$("#videoModule").height(windowHeight);
		},
		created: function () {
			console.log("created");
			this.init();
			this.getCurrentVideoInfo(this.startIndex);
		},
		methods: {
			init () {
				console.log("init");
			},
			playVideo(url,poster, title){
				this.url = url;
				this.title = title;
				this.poster = poster;
				this.showVideoPlay = true;
			},
			gotoVideoGroup(){
				this.$router.push({
					name: "videoGroup"
				})
			},
			getCurrentVideoInfo(index){
				this.currentVideo = this.videoList[index];
			},
			close(){
				this.showVideoPlay = false;
			}
		}
	}
</script>
<style type="text/css" lang="less">
	#videoModule{
		position: relative;
		overflow: hidden;
		h3,p{
			margin: 0;
		}
		img.bg_pic{
			position: absolute;
			top: 50%;
			margin-top: -556px;
			left: 50%;
			margin-left: -960px;
		}
		.fade-enter-active, .fade-leave-active {
		  	transition: opacity .5s;
		}
		.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
		  opacity: 0;
		}
		div.container{
			position: absolute;
			top: 0;
			left: 0;
			width: 100%;
			height: 100%;
			background: rgba(0,0,0,.7);
			div.main{
				width: 1200px;
				margin: 0 auto;
				div.top_info{
					text-align: center;
					color: #fff;
					margin-top: 50px;
					margin-bottom: 27px;
					div.title{
						h3{
							font-size: 26px;
							line-height: 53px;
						}
					}
					div.intro{
						p{
							font-size: 14px;
							line-height: 23px;
							
						}
					}
				}
				div.video_swipe{
					height: 438px;
				}
				div.bottom{
					text-align: center;
					margin-top: 50px;
					button{
						height: 78px;
						width: 256px;
						line-height: 78px;
						border: 1px solid #fff;
						font-size: 30px;
						color: #fff;
						// opacity: .9;
						background: rgba(0,0,0,0);
						cursor: pointer;
						transition: all .5s;
						&:hover{
							background-color: #eee;
							color: #333;
						}
					}
				}
			}
		}
	}
</style>