# Gemini-Feishu

快速让你的飞书机器人可以使用Gemini

项目思路来自[ChatGPT-Feishu](https://github.com/bestony/ChatGPT-Feishu)



## 一、创建、配置飞书应用

### 1. 创建飞书应用，并获取到 APPID 和 Secret

通过[飞书开放平台后台](https://open.feishu.cn/app)，创建一个`企业自建应用`，设置好名称、描述、图标。

<img src="https://tg-image.com/file/efe0a0d5ba78b309181ee.jpg" alt="" width="450">

应用创建完成后，可以在`凭证与基础信息`中查看到App ID和App Secret，在下面的步骤中我们会用上。

<img src="https://tg-image.com/file/b9ffb55c277cf8276cd6a.jpg" alt="" width="450">

### 2. 添加应用能力

要实现机器人的对话功能，我们需要为创建的应用`添加应用能力`，开启会话场景下的`发送和接受消息`，添加完成后可以在左边`添加应用能力`下看到多了一个`机器人`

<img src="https://tg-image.com/file/f11f43bba3c65bc7b8784.jpg" alt="" width="450">

<img src="https://tg-image.com/file/c631cd096943eadbb344e.jpg" alt="" width="450">

### 3.开启需要权限

点击`机器人`后，会看到一个提示我们开启权限的提示，点击左边菜单栏的`权限管理`,开启以下权限

- im:message 获取与发送单聊、群聊消息
- im:message.group_at_msg 获取用户在群组中@机器人的消息 权限
- im:message.group_at_msg:readonly 接收群聊中@机器人消息事件
- im:message.p2p_msg 获取用户发给机器人的单聊消息
- im:message.p2p_msg:readonly 读取用户发给机器人的单聊消息
- im:message:send_as_bot 以应用的身份发消息

### 4.配置事件与回调

在`事件与回调`中配置订阅方式，以便将事件发送至开发者服务器；添加请求地址后，就可以`添加事件`, 在事件中我们选择`im.message.receive_v1`添加即可。

> 开发者服务器可等[步骤三](#三创建后端服务)完成后，再来填写

<img src="https://tg-image.com/file/010c8e9b5153813a1eeb5.jpg" alt="" width="450">

<img src="https://tg-image.com/file/6bd5794121f72c4e4c106.jpg" alt="" width="450">

## 二、申请Gemini API key

访问[Google AI Studio](https://aistudio.google.com/app/apikey)创建API key

<img src="https://tg-image.com/file/3e7479af4f93a9f487f05.png" alt="" width="450">

## 三、创建后端服务

这里我们选择了一个可以白嫖的服务[AirCode](https://aircode.io/dashboard)

### 1. 访问 [AirCode](https://aircode.io/dashboard) ，创建一个新的项目

登录 [AirCode](https://aircode.io/dashboard) ，创建一个新的 Node.js 的项目，项目名可以根据你的需要填写

<img src="https://tg-image.com/file/77b7c4bb269c16ddbfe6c.jpg" alt="" width="450">

<img src="https://tg-image.com/file/96051f859c9bac3d69afa.png" alt="" width="450">

### 2. 复制项目下的 index.js 的源码内容，并粘贴到 Aircode 当中

### 3. 安装所需依赖

这个开发过程中，我们使用了飞书开放平台官方提供的 SDK，以及 axios 来完成调用。点击页面左下角的包管理器，安装 `@larksuiteoapi/node-sdk` 和 `@google/generative-ai`。

<img src="https://tg-image.com/file/4a8a97293c5d855d199b2.png" alt="" width="450">

### 4. 配置环境变量

我们需要配置四个必须的环境变量 `APPID` 、`SECRET`、`BOTNAME`和`API_KEY`

APPID，SECRET 填写在飞书开放平台获取到的APPID，SECRET，BOTNAME 填写你应用的名字。

API_KEY 填写我们在[步骤二](#二申请gemini-api-key)中创建的API key

> 配置环境变量可能会失败，可以多 deploy 几次，确保配置成功。

<img src="https://tg-image.com/file/5aedc99d8676cc884ae67.png" alt="" width="450">

## 四、发布应用

上述这些都配置完成后，你的机器人就配置好了，接下来只需要在飞书开放平台后台找到应用发布，创建一个全新的版本并发布版本即可。
