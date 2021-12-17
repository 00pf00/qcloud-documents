## 操作场景

本文通过一个demo进行 gRPC-Go 应用接入微服务引擎托管的 PolarisMesh 治理中心的全流程操作演示，帮助您快速了解如何使用服务治理中心。

## 前提条件

- 已创建PolarisMesh服务治理中心，请参考[创建PolarisMesh治理中心](https://cloud.tencent.com/document/product/1364/65866)。
- 下载github的[demo源码](https://github.com/polarismesh/grpc-go-polaris/tree/main/examples/quickstart)到本地并解压。
- 本地编译构建打包机器环境已安装了[Go](https://go.dev/doc/devel/release)，并且能够使用Go mod拉取依赖。
- 【虚拟机部署】已创建CVM虚拟机，请参考[创建CVM虚拟机](https://cloud.tencent.com/document/product/213/2936)
- 【容器化部署】已创建TKE容器集群，请参考[创建 TKE 集群](https://cloud.tencent.com/document/product/457/32189)。

## 操作步骤

1. 登录微服务引擎控制台
  - 登录[腾讯云控制台](https://cloud.tencent.com/)
  - 单击左上角云产品，搜索”微服务引擎”，选择并进入微服务引擎控制台。
    ![console](https://qcloudimg.tencent-cloud.cn/raw/7f7daff61aff9aface98161c61a56239.png)
2. 获取微服务引擎服务治理中心地址
  - 点击左边栏polarismesh按钮，进入polarismesh引擎列表：![pm_icon](https://qcloudimg.tencent-cloud.cn/raw/bdd06200187fff733eb1222f794a014a.png)
  - 点击页面上方下拉列表，选择地域：![region_icon](https://qcloudimg.tencent-cloud.cn/raw/b5153fa452844ee19e24436e11b2376e.png)
  - 在引擎列表中，选择已经创建好的polarismesh服务治理中心引擎，点击进入：![instance_icon](https://qcloudimg.tencent-cloud.cn/raw/c75a4b2c7b53a6cb2bec33bde7fa8c99.png)
  - 进入“基本信息”页，查看访问地址，gRPC-Go 应用访问使用gRPC端口（8091）：
    ![access](https://qcloudimg.tencent-cloud.cn/raw/561460943b0404c44c29d2c0dd09c56f.png)
3. 修改demo中的注册中心地址。
  - 在下载到本地的demo源码目录下，分别找到
“\examples\quickstart\provider\polaris.yaml”和“\examples\quickstart\consumer\polaris.yaml”两个文件。
  - 添加微服务引擎服务治理中心地址到项目配置文件中（以“\examples\quickstart\provider\polaris.yaml”为例）。
```yml
global:
  serverConnector:
    addresses:
    - 192.168.100.9:8091
```

4. 将源码编译成可执行程序。
  - 分别在`consumer`和`provider`这2个目录下，打开cmd命令，执行以下命令，对项目进行编译：
    - 编译consumer：`CGO_ENABLED=0 go build -ldflags "-s -w" -o consumer`
    - 编译provider：`CGO_ENABLED=0 go build -ldflags "-s -w" -o provider`
  - 编译成功后，生成如表1所示的2个二进制包。
    表1 软件包列表

| 软件包所在目录                                         | 软件包名称                                  | 说明       |
| ------------------------------------------------------ | ------------------------------------------- | ---------- |
| \examples\quickstart\provider | provider | 服务生产者 |
| \examples\quickstart\consumer | consumer | 服务消费者 |

5. 【虚拟机部署】部署provider和consumer微服务。
 - 上传二进制以及配置文件至 CVM 实例。
 - 执行启动命令进行启动：
```shell
nohup [二进制名称] &
```

6. 【容器化部署】部署provider和consumer微服务。
 - 编写dockerfile生成镜像，参考：
```
FROM golang:alpine
WORKDIR /root
ADD . /root
ENTRYPOINT ./[二进制名称]
```
 - 通过TKE部署并运行镜像

7. 确认部署结果。
 - 进入前面提到的微服务治理中心实例页面。
 - 选择“服务管理 > 服务列表”，查看微服务EchoServerGRPC（provider）的实例数量：
   - 若实例数量值不为0，则表示已经成功接入微服务引擎。
   
   - 若实例数量为0，或者找不到EchoServerGRPC服务名，则表示微服务应用接入微服务引擎失败。
   
     ![grpc_service_list](https://qcloudimg.tencent-cloud.cn/raw/7e1194b2c16e3fbbe7e70445e33f7836.png)
   
 - 调用consumer的HTTP接口
   - 执行http调用，其中${app.port}替换为consumer的监听端口（默认为16011），${add.address}则替换为consumer暴露的地址。
    ```
    curl -L -X GET 'http://${add.address}:${app.port}/echo?value=hello_world'
    预期返回值：echo: hello_world
    ```

