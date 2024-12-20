# MeiQia_For_DCloud

> 请您首先把文档全部仔细阅读完毕,再进行您的开发, 如还有疑问，欢迎加入 美洽 SDK 开发 QQ 群：515344099

# AppKey 的获取方法

使用管理员权限账号登陆美洽，在 设置 --> SDK 页面中，选择 添加 App 配置 ，根据提示配置 App 信息，然后添加 APP 即可得到 appkey 用于配置。

# 插件接口总览

|方法名|说明|
|---|---|
|initChatViewManger()|初始化美洽聊天页面管理器|
|configChatViewStyle()|美洽UI样式配置|
|setPreSendTextMessage()|预发送文本信息|
|setPreSendProductCardMessage()|预发送商品卡片信息|
|enableSendVoiceMessage()|是否支持发送语音信息|
|enablePhotoLibraryEdit()|是否支持相册选择图片可裁剪|
|setScheduledAgentId()|指定分配客服|
|setScheduledGroupId()|指定分配客服组|
|setScheduledRule()|指定分配客服/客服组，该客服/客服组不在线，如何转接的规则|
|setLoginCustomizedId()|使用开发者自定义的id上线|
|setClientInfo()|设置顾客的自定义信息|
|getUnreadMessages()|获取当前未读消息|
|showMeiQiaChatView()|跳转到聊天页面|
|showMQMessageForm()|打开美洽留言界面|
|dismiss()|退出聊天页面|
|setLinkTapCallback()|监听对话中的链接点击|
|getUnreadMessagesWithCustomizedId()|根据 customizedId 获取未读消息|
|endCurrentConversation()|结束当前对话|
|switchAppkey()|切换appkey登录|
|setLocalizedLanguage()|设置当前语言|
|setNoReallocate()|已指定分配客服后，下次指定分配是否需要重新分配 设置接口|

# 插件接口使用详解

## 设置 AppKey
添加插件的时候，需要将从美洽获取到的 appkey 填入配置中

## 项目中引用插件

```js
// 务必先生成自定义基座，然后运行的时候使用自定义基座，否则会出现找不到插件的错误
const mqModule = uni.requireNativePlugin("MeiQia-ChatPlugin");
```

## 打开默认的美洽聊天页面

```js
openMeiQiaChatView() {
    mqModule.initChatViewManger();
    mqModule.showMeiQiaChatView();
},
```
>说明：美洽所有业务和配置方法都在initChatViewManger()，调用以后才能调用，最后使用showMeiQiaChatView()跳转到聊天页面。

## 配置聊天页面 UI 样式

```js
configMeiQiaChatStyle() {
    mqModule.initChatViewManger();
    mqModule.configChatViewStyle({
      "navBarBackgroundColor": "#ffffff", // 设置导航栏的背景色；
      "navBarTitleTxtColor": "#ffffff", // 设置导航栏上的 title 的颜色；
      "enableShowClientAvatar": true, // 是否支持当前用户头像的显示
      //以下配置暂时只支持ios
      "incomingMsgTextColor": "#ffffff", // 设置客服发送过来的message的文字颜色；
      "incomingBubbleColor": "#ffffff", // 设置客服发送过来的message气泡颜色；
      "outgoingMsgTextColor": "#ffffff", // 设置用户发送出去的message的文字颜色
      "outgoingBubbleColor": "#ffffff", // 设置用户发送出去的message气泡颜色；
      "eventTextColor": "#ffffff", // 设置事件流的显示文字的颜色；
      "navTitleFont": 15, // 设置导航栏上的title的字体大小
      "backgroundColor": "#ffffff", // 聊天窗口背景色；
      "enableRoundAvatar": false, // 是否开启圆形头像；
      "enableIncomingAvatar": true, // 是否支持左边头像的显示
    });

    mqModule.showMeiQiaChatView();
  }
```

## 设置预发送文本消息

```js
preSendTextMessage() {
    mqModule.initChatViewManger();
    mqModule.setPreSendTextMessage("预发送内容");
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
    description:"商品描述的内容",
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

## 是否支持相册选择图片可裁剪，只支持iOS

```js
enablePhotoLibraryEdit() {
    mqModule.initChatViewManger();
    mqModule.enablePhotoLibraryEdit(false); // 默认支持
    mqModule.showMeiQiaChatView();
},
```
>说明：这个方法是针对iOS的


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

## 设置指定分配的客服/客服组的转接规则

```js
configScheduledAgentId() {
    mqModule.initChatViewManger();
    mqModule.setScheduledGroupId("客服组id");
    mqModule.setScheduledRule(1);  //不转接给任何人
    mqModule.showMeiQiaChatView();
},
```
>说明：指定分配客服/客服组，该客服/客服组不在线，如何转接的规则
>
>setScheduledRule的value值：
> vaule == 1； //不转接给任何人
> vaule == 2； //转接给组内的人
> vaule == 3； //转接给企业其他随机一个人
> 
> 不调用setScheduledRule方法，默认就是按照 vaule == 3的规则分配

## 已指定分配客服后，下次指定分配是否需要重新分配 设置接口

```js
configSetNoReallocate() {
    mqModule.initChatViewManger();
    mqModule.setNoReallocate(false);
    mqModule.showMeiQiaChatView();
},
```
>说明：默认关闭。开启后，在已分配客服的情况下，下次触发分配，不再重新分配客服

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
|comment|备注|

>如果还要添加更多的自定义字段，请到工作台的 设置页面 -> 顾客 -> 顾客管理 -> 顾客名片字段 -> 自定义字段  中添加想要的字段。

## 获取当前未读消息

```js
getUnreadMessages() {
    testModule.getUnreadMessages((result) => {
        uni.showToast({
            title: '调用获取未读消息' + result,
            icon:'none'
        });
    });
}
```
>返回未读消息的数组，数据结构大体是：

```js
[{
    "id": "26136869504",
    "agent_id": "1525407",
    "content_type": "text",
    "conversation_id": "3682151000",
    "type": "message",
    "action": "message",
    "track_id": "2BF3IyEcxfbjuF9Pdo9NlkAtwGt",
    "created_on": "1656487957.360000",
    "message_user_name": "客服某某",
    "message_avatar": "https:/xxx.jpg",
    "from_type": "agent",
    "content": "23132"
}, {
    "id": "26136869068",
    "agent_id": "1525407",
    "content_type": "text",
    "conversation_id": "3682151000",
    "type": "message",
    "action": "message",
    "track_id": "2BF3IyEcxfbjuF9Pdo9NlkAtwGt",
    "created_on": "1656487955.565000",
    "message_user_name": "客服某某",
    "message_avatar": "https://xxx.jpg",
    "from_type": "agent",
    "content": "112323123"
}]
```

## 关闭对话页

```js
dismiss() {
    testModule.dismiss();
}
```

## 监听对话中的链接点击

```js
// ios 目前只支持商品卡片的点击回调
// 开发者自己处理 url 点击，注意：设置监听回调后,将不再跳转网页.如果需要跳转,开发者需要自行处理
setLinkTapCallback() {
    testModule.setLinkTapCallback((url) => {
        console.log('url = ' + url);
    });
}
```

## 使用美洽留言页面

```js
openMeiQiaMessageForm() {
    mqModule.showMQMessageForm();
},
```
>不用调用initChatViewManger，直接就可以跳转。

## 根据 customizedId 获取未读消息

```js
getUnreadMessagesWithCustomizedId() {
    testModule.getUnreadMessagesWithCustomizedId("111111", (result) => {
        uni.showToast({
            title: '调用获取未读消息' + result,
            icon:'none'
        });
    });
}
```

## 结束当前对话

```js
endCurrentConversation() {
    testModule.endCurrentConversation((result) => {
        console.log('结束对话 ==== ' + result);
        if (result) {
            console.log('结束成功');
        }else {
            console.log('结束失败');
        }
    });
```

## 切换appkey登录

```js
switchAppkey() {
    testModule.switchAppkey('22222', (result) => {
        console.log('clientId：' + result);
        if (result.length > 0) {
            console.log('切换成功');
        }else { 
            console.log('切换失败');
        }
    });
}
```

## 设置当前语言

>配置本地化语言(仅iOS支持)，目前支持：中文简体、中文繁体、英文、马来语、印尼语，日语、泰语、越南语、葡萄牙语、印地语、西班牙语、俄语，韩语，不支持的语言默认显示为英文 如："en" ，"zh-Hans"，"zh-Hant"，"ms"， "id",  "ja"，"th"，"vi"，"pt"，"hi"， "es"，"ru"，"ko"（不调用此方法，则随系统语言变化）

```js
setLocalizedLanguage() {
    testModule.setLocalizedLanguage('ms');
}
```

## iOS离线推送说明

首先需要设置服务器地址，请使用美洽管理员帐号登录 [美洽](http://www.meiqia.com)，在「设置」 -\> 「SDK」中设置。

### 推送消息数据结构

当有消息需要推送时，美洽服务器会向开发者设置的服务器地址发送推送消息，方法类型为 *POST*，数据格式为 *JSON* 。

发送的请求格式介绍：

request.header.authorization 为数据签名。

request.body 为消息数据，数据结构为：

|Key|说明|
|---|---|
|id|消息 id|
|messageId|当前对话的会话 id|
|content|消息内容|
|messageTime|发送时间|
|fromName|发送人姓名|
|deviceToken|发送对象设备的 deviceToken，格式为字符串|
|clientId|发送对象的顾客 id|
|customizedId|开发者传的自定义 id|
|contentType|消息内容类型 - text/photo/audio|
|deviceOS|设备系统|
|customizedData|开发者上传的自定义的属性|
|type|消息类型 - mesage 普通消息 / welcome 欢迎消息 / ending 结束消息 / remark 评价消息 / 留言消息|

>注意：开发者需要自己请求注册推送，让用户授权
