<template>
	<view class="content">
		<image src=../../static/timg.gif mode="widthFix"></image>
		<text class="title">做我女朋友</text>
		<view class="operate">
			<button type="primary" class="btn" @tap="agree">我愿意</button>
			<button type="warn" class="btn" @tap="disagree">坚决不行</button>
		</view>
		<view class="message" v-for="one in love" :key="one">{{one}}</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				love:[]
			}
		},
		onLoad() {
			this.back=uni.getBackgroundAudioManager()
			this.back.src="https://other-web-rh03-sycdn.kuwo.cn/5707c78d47ff5b37e2a907f6aa13aaaa/5d4ab842/resource/a2/21/9/2802372104.aac"
			this.back.title="音乐"
			this.back.play()
		},
		onShow() {
			this.love=[]
			this.timer={}
			let msg={
				2000: "以前我总是担心长大了会和谁在一起。其实我也老担心将来是和谁在一起，还好现在遇上了你，时间不早也不晚，还好上天给我预留了你，这么像我的你，让我这么喜欢的你。",
				4000: "",
				6000: "我要你知道，这个世界上有一个人会永远等着你，无论是在什么时候，无论你在什么地方，反正你知道总会有这样一个人。",
				8000: "",
				10000: "【“不行，差一年、一个月、一天、一个时辰，都不算一辈子”】",
				12000: "",
				14000: "",
				16000: "",
				18000: "",
				20000: ""
			}
			let ref=this;
			for(let key in msg){
				let t=setTimeout(function(){
					ref.love.push(msg[key])
					delete ref.timer[key]
				},key)
				ref.timer[key]=t
			}
		},
		onHide:function() {
			for(let key in this.timer){
				clearTimeout(this.timer[key])
			}
		},
		methods: {
			agree:function(){
				uni.showToast({
					icon:"none",
					title:"谢谢小姐姐的喜欢",
					duration:600
				})
			},
			disagree:function (){
				uni.showModal({
					title:"确定吗",
					content:"拒绝我你会后悔一辈子",
					cancelText:"拒绝",
					confirmText:"接受",
					confirmColor:"#DD524D",
					success:function(res){
						if(res.confirm){
							uni.showToast({
								icon:"none",
								title:"谢谢喜欢",
								duration:600
							})
						}
						else{
							uni.showToast({
								icon:"none",
								title:"你错过了5元红包",
								duration:600
							})
						}
					}
				})
			}
				
			

		}
	}
</script>

<style lang="less">
	@import url("index.less");
</style>
