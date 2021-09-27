# MeiQia_For_DCloud

> 请您首先把文档全部仔细阅读完毕,再进行您的开发, 如还有疑问，欢迎加入 美洽 SDK 开发 QQ 群：515344099

# Appkey的获取方法

使用管理员权限账号登陆美洽，在 设置 --> SDK 页面中，选择 添加 App 配置 ，根据提示配置 App 信息，然后添加 APP 即可得到 appkey 用于配置。

# 插件接口总览

|方法名|说明|
|---|---|
|initChatViewManger()|初始化美洽聊天页面管理器|
|configChatViewStyle(:)|美洽UI样式配置|
|setPreSendTextMessage(:)|预发送文本信息|
|setPreSendProductCardMessage(:)|预发送商品卡片信息|
|enableSendVoiceMessage(:)|是否支持发送语音信息|
|enableSendImageMessage(:)|是否支持发送图片信息|
|enableMessageSound(:)|是否开启接收/发送消息的声音|
|setScheduledAgentId(:)|指定分配客服|
|setScheduledGroupId(:)|指定分配客服组|
|setNotScheduledAgentId(:)|设置不分配给指定的客服|
|setLoginCustomizedId(:)|使用开发者自定义的id上线|
|setClientInfo(:)|设置顾客的自定义信息|
|showMeiQiaChatView()|跳转到聊天页面|
|showMQMessageForm()|打开美洽留言界面|

# 插件接口使用详解

## 项目中引用插件

```js
const mqModule = uni.requireNativePlugin("MeiQiaChatPlugin");
```

## 打开默认的美洽聊天页面

```js
openMeiQiaChatView() {
                mqModule.initChatViewManger();
                mqModule.showMeiQiaChatView();
            },
```
>说明：美洽所有业务和配置方法都在initChatViewManger()，调用以后才能调用，最后使用showMeiQiaChatView()跳转到聊天页面。

## 配置聊天页面UI样式

```js
configMeiQiaChatStyle() {
    mqModule.initChatViewManger();
    
    mqModule.configChatViewStyle({
      "incomingMsgTextColor": "#ffffff", // 设置发送过来的message的文字颜色(左边)；
      "incomingBubbleColor": "#ffffff", // 设置发送过来的message气泡颜色(左边)
      "outgoingMsgTextColor": "#ffffff", // 设置发送出去的message的文字颜色(右边)
      "outgoingBubbleColor": "#ffffff", // 设置发送出去的message气泡颜色（右边）
      "eventTextColor": "#ffffff", // 设置事件流的显示文字的颜色
      "navBarColor": "#ffffff", // 设置导航栏的背景色；
      "navTitleFont": 15.0, // 设置导航栏上的title的字体大小；
      "navTitleColor": "#ffffff", // 设置导航栏上的title的颜色；
      "backgroundColo": "#ffffff", // 聊天窗口背景色
      "enableRoundAvatar": true, // 是否开启圆形头像
      "enableIncomingAvatar": true, // 是否支持左边头像的显示
      "enableOutgoingAvatar": true, // 是否支持当前用户头像的显示
    });

    mqModule.showMeiQiaChatView();
  }
```

## 设置预发送文本消息

```js
preSendTextMessage() {
                mqModule.initChatViewManger();
                mqModule.setPreSendTextMessage("订单号是:48611123");
                mqModule.showMeiQiaChatView();
            },
```

## 设置预发送商品卡片信息消息

```js
preSendProductCardMessage() {
                
                mqModule.initChatViewManger();
                mqModule.setPreSendProductCardMessage({
                pictureUrl : "https://file.pisen.com.cn/QJW3C1000WEB/Product/201701/16305409655404.jpg", // 商品图片的链接  
                title: "商品的标题",
                description:"商品描述的内容啊",
                productUrl:"https://meiqia.com", // 商品链接
                salesCount:50 // 商品销售量
                });
                
                mqModule.showMeiQiaChatView();
            },
```

## 设置是否支持发送语音信息

```js
enableSendVoiceMessage() {
                mqModule.initChatViewManger();
                mqModule.enableSendVoiceMessage(false); // 默认支持
                mqModule.showMeiQiaChatView();
            },
```
>说明：是否发送语音、图片，默认都是支持的。 接收/发送消息的声音，也是默认开启的。


## 设置指定分配的客服

```js
configScheduledAgentId() {
                
                mqModule.initChatViewManger();
                mqModule.setScheduledAgentId("客服id");
                mqModule.showMeiQiaChatView();
            },
```


## 设置指定分配的客服组

```js
configScheduledAgentId() {
                
                mqModule.initChatViewManger();
                mqModule.setScheduledGroupId("客服组id");
                mqModule.showMeiQiaChatView();
            },
```
>说明：如果设置了分配给客服id，以分配给客服id为优先


## 设置不分配给指定的客服

```js
configNotScheduledAgentId() {
                
                mqModule.initChatViewManger();
                mqModule.setNotScheduledAgentId("客服id");
                mqModule.showMeiQiaChatView();
            },
```

## 使用开发者自定义的id上线

```js
configLoginCustomizedId() {
                
                mqModule.initChatViewManger();
                mqModule.setLoginCustomizedId("顾客自定义id");
                mqModule.showMeiQiaChatView();
            },
```

## 设置顾客的自定义信息

```js
configClientInfo() {
                
                mqModule.initChatViewManger();
                mqModule.setClientInfo({
                clientInfo:{
                    age:"22",
                    weixin: "5545666",
                    name: "美洽用户"
                    }, 
                override: true});
                mqModule.showMeiQiaChatView();
            },
```
>说明：clientInfo: 顾客配置信息；  override：是否强制更新，如果不设置此值为 true，设置只有第一次有效。

以下字段是美洽定义好的，开发者可通过上方提到的接口，直接对下方的字段进行设置：

|Key|说明|
|---|---|
|name|真实姓名|
|gender|性别|
|age|年龄|
|tel|电话|
|weixin|微信|
|weibo|微博|
|address|地址|
|email|邮件|
|weibo|微博|
|avatar|头像 URL|
|tags|标签，数组形式，且必须是企业中已经存在的标签|
|source|顾客来源|
|comment|备注|

>如果还要添加更多的自定义字段，请到工作台的 设置页面 -> 顾客 -> 顾客管理 -> 顾客名片字段 -> 自定义字段  中添加想要的字段。


## 使用美洽留言页面

```js
openMeiQiaMessageForm() {
                mqModule.showMQMessageForm();
            },
```
>不用调用initChatViewManger，直接就可以跳转。
