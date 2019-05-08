## 开发准备

### SDK 获取

实时流式语音识别的 iOS SDK 的下载地址：[iOS SDK](https://github.com/heavensword/resources/blob/master/sdk/QCloudSDK.zip)

更多示例可参考 Demo：[iOS Demo](https://main.qcloudimg.com/raw/522db7adc9be319ea591d15e5cbec49c/iOSDemo.zip)

### 开发准备

-  QCloudSDK支持*iOS 9.0*及以上版本
-  实时流式语音识别，需要手机能够连接网络（GPRS、3G 或 Wi-Fi 网络等）
-  从控制台获取 APP ID、SecretID、SecretKey，详情参考 [基本概念](https://cloud.tencent.com/document/product/441/6194)


### SDK 配置

#### SDK 导入

iOS SDK 压缩包名称为： QCloudSDK.zip。压缩包中包含了一个` libWXVoiceSpeex.a` 静态库和`QCloudSDK.framework`。

#### 工程配置

在工程` info.plist` 添加以下设置:

1. 设置NSAppTransportSecurity策略，添加如下内容:
```objective-c
   <key>NSAppTransportSecurity</key>
   <dict>
        <key>NSAllowsArbitraryLoads</key>
        <true/> 
   </dict>
```
2. 申请系统的麦克风的权限，添加如下内容:
```objective-c
   <key>NSMicrophoneUsageDescription</key>
   <string>需要使用了的麦克风采集音频</string>
```
3. 在工程中添加依赖库，在build Phases Link Binary With Libraries中添加以下库：

   -  AVFoundation.framework
   -  AudioToolbox.framework
   -  QCloudSDK.framework
   -  libWXVoiceSpeex.a
   
添加完如图所示：
![](https://github.com/heavensword/resources/blob/master/images/framework.png?raw=true)

#### **QCloudRealTimeRecognizer**初始化说明
***QCloudRealTimeRecognizer***是实时语音识别类，提供两种初始化方法。
```objective-c
/**
 * 初始化方法，调用者使用内置录音器采集音频
 * @param config 配置参数，详见QCloudConfig定义
 */
- (instancetype)initWithConfig:(QCloudConfig *)config;

/**
 * 初始化方法，调用者传递语音数据调用此初始化方法
 * @param config 配置参数，详见QCloudConfig定义
 * @param dataSource 语音数据数据源，必须实现QCloudAudioDataSource协议
 */
- (instancetype)initWithConfig:(QCloudConfig *)config dataSource:(id<QCloudAudioDataSource>)dataSource;
```

#### **QCloudConfig**初始化方法说明

```objective-c
/**
 * 初始化方法
 * @param appid     腾讯云appId     基本概念见https://cloud.tencent.com/document/product/441/6194
 * @param secretId  腾讯云secretId  基本概念见https://cloud.tencent.com/document/product/441/6194
 * @param secretKey 腾讯云secretKey 基本概念见https://cloud.tencent.com/document/product/441/6194
 * @param projectId 腾讯云projectId 基本概念见https://cloud.tencent.com/document/product/441/6194
 */
- (instancetype)initWithAppId:(NSString *)appid
                     secretId:(NSString *)secretId
                    secretKey:(NSString *)secretKey
                    projectId:(NSString *)projectId;
```

## 示例
### 使用内置录音器采集语音识别示例
#### 1.引入***QCloudSDK***的头文件，将使用***QCloudSDK***的文件名后缀有*.m->.mm*
```objective-c
#import<QCloudSDK/QCloudSDK.h>
```
#### 2.创建***QCloudConfig***实例
```objective-c
 //1.创建QCloudConfig实例
 QCloudConfig *config = [[QCloudConfig alloc] initWithAppId:kQDAppId 
  						  secretId:kQDSecretId 
					         secretKey:kQDSecretKey 
					         projectId:kQDProjectId];
 config.sliceTime = 600;                             	           //语音分片时常600ms
 config.enableDetectVolume = _volumeDetectSwitch.on;                //是否检测音量
 config.endRecognizeWhenDetectSilence = _silenceDetectEndSwitch.on; //是否检测到静音停止识别
```
#### 3.创建***QCloudRealTimeRecognizer***实例
```objective-c
 QCloudRealTimeRecognizer *recognizer = [[QCloudRealTimeRecognizer alloc] initWithConfig:config];;
```
#### 4.设置delegate，实现[***QCloudRealTimeRecognizerDelegate***](#QCloudRealTimeRecognizerDelegate)方法
```objective-c
recognizer.delegate = self;
```
#### 5.开始识别
```objective-c
 [recognizer start];
```
#### 6.结束识别
```objective-c
 [recognizer stop];
```

### 调用者提供语音数据示例
#### 1.引入***QCloudSDK***的头文件，将使用***QCloudSDK***的文件名后缀有*.m->.mm*
```objective-c
#import<QCloudSDK/QCloudSDK.h>
```
#### 2.创建***QCloudConfig***实例
```objective-c
 //1.创建QCloudConfig实例
 QCloudConfig *config = [[QCloudConfig alloc] initWithAppId:kQDAppId 
  						  secretId:kQDSecretId 
					         secretKey:kQDSecretKey 
					         projectId:kQDProjectId];
 config.sliceTime = 600;                             	           //语音分片时常600ms
 config.enableDetectVolume = _volumeDetectSwitch.on;                //是否检测音量
 config.endRecognizeWhenDetectSilence = _silenceDetectEndSwitch.on; //是否检测到静音停止识别
```
#### 3.自定义***QCloudDemoAudioDataSource***，***QCloudDemoAudioDataSource***实现[***QCloudAudioDataSource***](#QCloudAudioDataSource)协议
```objective-c
 QCloudDemoAudioDataSource *dataSource = [[QCloudDemoAudioDataSource alloc] init];
```
#### 4.创建***QCloudRealTimeRecognizer***实例
```objective-c
 QCloudRealTimeRecognizer *recognizer = [[QCloudRealTimeRecognizer alloc] initWithConfig:config];;
```
#### 5.设置delegate，实现[***QCloudRealTimeRecognizerDelegate***](#QCloudRealTimeRecognizerDelegate)方法
```objective-c
recognizer.delegate = self;
```
#### 6.开始识别
```objective-c
 [recognizer start];
```
#### 7.结束识别
```objective-c
 [recognizer stop];
```

#### <div id="QCloudRealTimeRecognizerDelegate">***QCloudRealTimeRecognizerDelegate***方法说明</div>
```objective-c
/**
 * 一次实时录音识别，分为多个flow，每个flow可形象的理解为一句话，一次识别中可以包括多句话。
  * 每个flow包含多个seq语音数据包，每个flow的seq从0开始
 */
@protocol QCloudRealTimeRecognizerDelegate <NSObject>

@required
/**
 * 每个语音包分片识别结果
 * @param response 语音分片的识别结果
 */
- (void)realTimeRecognizerOnSliceRecognize:(QCloudRealTimeRecognizer *)recognizer response:(QCloudRealTimeResponse *)response;

@optional
/**
 * 一次识别成功回调
 @param recognizer 实时语音识别实例
 @param result 一次识别出的总文本
 */
- (void)realTimeRecognizerDidFinish:(QCloudRealTimeRecognizer *)recognizer result:(NSString *)result;
/**
 * 一次识别失败回调
 * @param recognizer 实时语音识别实例
 * @param error 错误信息
 */
- (void)realTimeRecognizerDidError:(QCloudRealTimeRecognizer *)recognizer error:(NSError *)error;


//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
/**
 * 开始录音回调
 * @param recognizer 实时语音识别实例
 * @param error 开启录音失败，错误信息
 */
- (void)realTimeRecognizerDidStartRecord:(QCloudRealTimeRecognizer *)recognizer error:(NSError *)error;
/**
 * 结束录音回调
 * @param recognizer 实时语音识别实例
 */
- (void)realTimeRecognizerDidStopRecord:(QCloudRealTimeRecognizer *)recognizer;
/**
 * 录音音量实时回调用
 * @param recognizer 实时语音识别实例
 * @param volume 声音音量，取值范围（-40-0)
 */
- (void)realTimeRecognizerDidUpdateVolume:(QCloudRealTimeRecognizer *)recognizer volume:(float)volume;


//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
/**
 * 语音流的开始识别
 * @param recognizer 实时语音识别实例
 * @param voiceId 语音流对应的voiceId，唯一标识
 * @param seq flow的序列号
 */
- (void)realTimeRecognizerOnFlowRecognizeStart:(QCloudRealTimeRecognizer *)recognizer voiceId:(NSString *)voiceId seq:(NSInteger)seq;
/**
 * 语音流的结束识别
 * @param recognizer 实时语音识别实例
 * @param voiceId 语音流对应的voiceId，唯一标识
 * @param seq flow的序列号
 */
- (void)realTimeRecognizerOnFlowRecognizeEnd:(QCloudRealTimeRecognizer *)recognizer voiceId:(NSString *)voiceId seq:(NSInteger)seq;


//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
/**
 * 语音流开始识别
 * @param recognizer 实时语音识别实例
 * @param voiceId 语音流对应的voiceId，唯一标识
 * @param seq flow的序列号
 */
- (void)realTimeRecognizerOnFlowStart:(QCloudRealTimeRecognizer *)recognizer voiceId:(NSString *)voiceId seq:(NSInteger)seq;
/**
 * 语音流结束识别
 * @param recognizer 实时语音识别实例
 * @param voiceId 语音流对应的voiceId，唯一标识
 * @param seq flow的序列号
 */
- (void)realTimeRecognizerOnFlowEnd:(QCloudRealTimeRecognizer *)recognizer voiceId:(NSString *)voiceId seq:(NSInteger)seq;

@end
```
#### <div id="QCloudAudioDataSource">***QCloudAudioDataSource***初始化说明</div>
```objective-c
/**
 * 语音数据数据源，如果调用者需要自己提供语音数据需要, 调用者实现此协议中所有方法
 * 提供符合以下要求的语音数据:
 * 采样率：16k
 * 音频格式：pcm
 * 编码：16bit位深的单声道
 */
@protocol QCloudAudioDataSource <NSObject>

@required

/**
 * 标识data source是否开始工作，执行完start后需要设置成YES， 执行完stop后需要设置成NO
 */
@property (nonatomic, assign) BOOL running;

/**
 * SDK会调用start方法，实现此协议的类需要初始化数据源。
 */
- (void)start:(void(^)(BOOL didStart, NSError *error))completion;
/**
 * SDK会调用stop方法，实现此协议的类需要停止提供数据
 */
- (void)stop;
/**
 * SDK会调用实现此协议的对象的此方法读取语音数据, 如果语音数据不足expectLength，则直接返回nil。
 * @param expectLength 期望读取的字节数，如果返回的NSData不足expectLength个字节，SDK会抛出异常。
 */
- (nullable NSData *)readData:(NSInteger)expectLength;

@end

```
