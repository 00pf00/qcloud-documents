## 接入架构
腾讯云互动课堂解决方案为用户提供强大的能力支持，用户只需完成业务层逻辑和接口调用，即可快速搭建一个全平台的在线互动课堂产品。
![](https://main.qcloudimg.com/raw/1924c82283cd5e15da0518d97154e0bb.png)

## 接入操作
调用 TICSDK 登录/登出接口前，用户需先在自己的开发者服务器生成所需的 identifier 和 userSig。
#### 生成 identifier 和 userSig 
![](https://main.qcloudimg.com/raw/e5e4e33ea06db665a249844f928f0094.png)
1. 登录开发者服务器，使用腾讯云提供的工具生成登录 TICSDK 所需的 userSig，将 userSig 返回终端。
>?执行此操作可在腾讯云后台注册生成一个帐号，用户名为用户登录开发者服务器的用户名，密码为生成的 userSig。
2. 终端获取后，使用用户名（即 identifier）和 userSig 调用 TICSDK 的登录接口，腾讯云后台校验登录信息的正确性，返回登录结果。
>?在开发调试阶段，可使用实时音视频控制台生成的 identifier 和 userSig 用于测试开发，详细操作请参考 [生成签名](https://cloud.tencent.com/document/product/647/17275)。

#### 调用接口
调用 TICSDK 接口接入，详细接口介绍请参见 [客户端 SDK 集成](https://cloud.tencent.com/document/product/680/17883)。

#### 界面布局
用户需完成自己的产品的界面布局。

#### 课堂管理
由于课堂 ID (roomID) 从外部传入，TICSDK 无法维护 roomID，因此用户在调用 TICSDK 接口创建课堂时，需维护 roomID 的唯一性。
>?创建重复的课堂 TICSDK 将会返回创建失败及错误信息，根据具体业务用户需维护当前的课堂列表。






