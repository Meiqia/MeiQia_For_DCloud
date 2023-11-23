
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
	</view>
</template>

<script>
    // 首先需要通过 uni.requireNativePlugin("ModuleName") 获取 module 
    var testModule = uni.requireNativePlugin("MeiQia-ChatPlugin");
    export default {
        methods: {
            
            openMeiQiaChatView() {
                // 调用同步方法
                testModule.initChatViewManger();
				testModule.showMeiQiaChatView();
            },
			
			openMeiQiaMessageForm() {
			    // 调用同步方法
			    testModule.showMQMessageForm();
			},
			
			preSendTextMessage() {
			    // 调用同步方法
			    testModule.initChatViewManger();
			    testModule.setPreSendTextMessage("订单号是:48611123");
				testModule.showMeiQiaChatView();
			},
			
			setPreSendProductCardMessage() {
				
				testModule.initChatViewManger();
				testModule.setPreSendProductCardMessage({
				pictureUrl : "https://file.pisen.com.cn/QJW3C1000WEB/Product/201701/16305409655404.jpg", 	
				title: "456456123",
				description:"描述的内容啊",
				productUrl:"https://meiqia.com",
				salesCount:50
				});
				testModule.setLinkTapCallback((url) => {
					console.log(url);
					// 退出美洽客服页面
					testModule.dismiss();
				})
				testModule.showMeiQiaChatView();
			},
			
			setClientInfo() {
				
				testModule.initChatViewManger();
				testModule.setClientInfo({
				clientInfo:{
					age:"22",
					weixin: "5545666",
					qq: "45665445"
					}, 
				override: true});
				testModule.showMeiQiaChatView();
			},
			
			getUnreadMessages() {
				
				testModule.getUnreadMessages((result) => {
					console.log(result);
					uni.showToast({
						title: '调用获取未读数' + result.length,
						icon:'none'
					});
				});
			},
			
			getUnreadMessagesWithCustomizedId() {				
				testModule.getUnreadMessagesWithCustomizedId("111111", (result) => {
					console.log(result);
					uni.showToast({
						title: '调用获取未读数' + result.length,
						icon:'none'
					});
				});
			},
			
			endCurrentConversation() {
				testModule.endCurrentConversation((result) => {
					console.log('结束对话 ==== ' + result);
					if (result) {
						console.log('结束成功');
					}else {
						console.log('结束失败');
					}
				});
			},
			
			switchAppkey() {
				testModule.switchAppkey('5318abacb9406122d4970f17c80f5ec3', (result) => {
					console.log('clientId：' + result);
					if (result.length > 0) {
						console.log('切换成功');
					}else { 
						console.log('切换失败');
					}
				});
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