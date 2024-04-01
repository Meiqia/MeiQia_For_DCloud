
<template>
	<view class="content">
		<button type="primary" @click="openMeiQiaChatView()">打开默认的美洽聊天页面</button>
		<button type="primary" @click="openMeiQiaMessageForm()">打开美洽留言页面</button>
		<button type="primary" @click="preSendTextMessage()">预发送文字消息</button>
		<button type="primary" @click="setPreSendProductCardMessage()">发送商品卡片</button>
		<button type="primary" @click="setClientInfo()">配置个人信息</button>
		<button type="primary" @click="getUnreadMessages()">获取未读消息</button>
		<button type="primary" @click="getUnreadMessagesWithCustomizedId()">获取自定义id未读消息</button>
		<button type="primary" @click="endCurrentConversation()">结束当前对话</button>
		<button type="primary" @click="switchAppkey()">切换appkey登录</button>
		<button type="primary" @click="configMeiQiaChatStyle()">聊天页面 UI 样式</button>
		<button type="primary" @click="setLocalizedLanguage()">设置当前语言</button>
	</view>
</template>

<script>
    // 首先需要通过 uni.requireNativePlugin("ModuleName") 获取 module 
    var mqModule = uni.requireNativePlugin("MeiQia-ChatPlugin");
    export default {
        methods: {
            openMeiQiaChatView() {
                // 调用同步方法
                mqModule.initChatViewManger();
				mqModule.showMeiQiaChatView();
            },
			
			openMeiQiaMessageForm() {
			    // 调用同步方法
			    mqModule.showMQMessageForm();
			},
			
			preSendTextMessage() {
			    // 调用同步方法
			    mqModule.initChatViewManger();
			    mqModule.setPreSendTextMessage("订单号是:48611123");
				mqModule.showMeiQiaChatView();
			},
			
			setPreSendProductCardMessage() {
				mqModule.initChatViewManger();
				mqModule.setPreSendProductCardMessage({
				pictureUrl : "https://file.pisen.com.cn/QJW3C1000WEB/Product/201701/16305409655404.jpg", 	
				title: "456456123",
				description:"描述的内容啊",
				productUrl:"https://meiqia.com",
				salesCount:50
				});
				mqModule.setLinkTapCallback((url) => {
					console.log(url);
					// 退出美洽客服页面
					mqModule.dismiss();
				})
				mqModule.showMeiQiaChatView();
			},
			
			setClientInfo() {
				mqModule.initChatViewManger();
				mqModule.setClientInfo({
				clientInfo:{
					age:"22",
					weixin: "5545666",
					qq: "45665445"
					}, 
				override: true});
				mqModule.showMeiQiaChatView();
			},
			
			getUnreadMessages() {
				mqModule.getUnreadMessages((result) => {
					console.log(result);
					uni.showToast({
						title: '调用获取未读数' + result.length,
						icon:'none'
					});
				});
			},
			
			getUnreadMessagesWithCustomizedId() {				
				mqModule.getUnreadMessagesWithCustomizedId("111111", (result) => {
					console.log(result);
					uni.showToast({
						title: '调用获取未读数' + result.length,
						icon:'none'
					});
				});
			},

			endCurrentConversation() {
				mqModule.endCurrentConversation((result) => {
					console.log('结束对话 ==== ' + result);
					if (result) {
						console.log('结束成功');
					}else {
						console.log('结束失败');
					}
				});
			},

			switchAppkey() {
				mqModule.switchAppkey('22222', (result) => {
					console.log('clientId：' + result);
					if (result.length > 0) {
						console.log('切换成功');
					}else {
						console.log('切换失败');
					}
				});
			},

			configMeiQiaChatStyle() {
				mqModule.initChatViewManger();
				mqModule.configChatViewStyle({
				  "navBarBackgroundColor": "#ffffff", // 设置导航栏的背景色；
				  "navBarTitleTxtColor": "#000000", // 设置导航栏上的 title 的颜色；
				  "enableShowClientAvatar": true, // 是否支持当前用户头像的显示
				  "incomingMsgTextColor": "#FF5C5E", // 设置客服发送过来的message的文字颜色；
				  "incomingBubbleColor": "#00CE7D", // 设置客服发送过来的message气泡颜色；
				  "outgoingMsgTextColor": "#17C7D1", // 设置用户发送出去的message的文字颜色
				  "outgoingBubbleColor": "#FFB652", // 设置用户发送出去的message气泡颜色；
				  "backgroundColor": "#303D42", // 聊天窗口背景色；
				  //以下配置暂时只支持ios
				  "eventTextColor": "#ffffff", // 设置事件流的显示文字的颜色；
				  "navTitleFont": 15, // 设置导航栏上的title的字体大小
				  "enableRoundAvatar": false, // 是否开启圆形头像；
				  "enableIncomingAvatar": true, // 是否支持左边头像的显示
				});
				mqModule.showMeiQiaChatView();
			},
			
			setLocalizedLanguage() {
			    testModule.setLocalizedLanguage('ja');
			}
		}
    }
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		justify-content: center;
		margin: 100rpx;
		margin-top: 20rpx;
	}
		
	button{
		margin: 5rpx;
	}
	
</style>