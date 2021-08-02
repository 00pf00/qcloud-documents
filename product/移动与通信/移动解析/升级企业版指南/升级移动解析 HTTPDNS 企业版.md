
## 背景
移动解析 HTTPDNS 以 HTTP 协议替代传统域名解析，解决⼩程序在不同⽹络环境中⾯临的域名劫持、⽹络接⼊异常的问题。由于近⼏年解析量增涨导致⼤量的资源消耗，为提升客户服务质量，进⽽推出企业版，并且免费的 HTTPDNS 解析能⼒将会在**2022年1⽉1⽇0时**停⽌服务。
因此，为避免影响业务，请尽快完成接⼊ IP 切换。

## 企业版功能特性
HTTPDNS ⾮企业版仅提供基础的域名解析服务，以下功能特性均为企业版独享。

<table>
<thead>
  <tr>
    <th>功能特性</th>
    <th>说明<br></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>⽆限请求 </td>
    <td>⾮企业版，测试使⽤时，单个 IP 请求上限100QPS，单个域名上限1000QPS。</td>
  </tr>
  <tr>
    <td>境外节点 </td>
    <td>近⼏年重点扩充企业版的境外节点，建⽴基于 BGP Anycast ⽹络架构的⾼防集群。<br></td>
  </tr>
  <tr>
    <td>解析联动加速 </td>
    <td>⾯向权威解析托管在 DNSPod 的域名有加成的缓存加速能⼒。</td>
  </tr>
  <tr>
    <td>HTTP SDK 方式接入 HTTPDNS</td>
    <td>通过 SDK 实现快速接入，可兼容 IOS/Android 多平台移动应⽤。<br></td>
  </tr>
  <tr>
    <td>DES、AES、HTTPS <br>数据加密</td>
    <td>使⽤ DES、AES 、HTTPS 加密，可以防⽌明⽂请求在传输过程中被恶意篡改。<br></td>
  </tr>
  <tr>
    <td>新特性支持</td>
    <td>所有正在研发的新功能特性只在企业版上发布。</td>
  </tr>
  <tr>
    <td>预警提醒</td>
    <td>告警通知。</td>
  </tr>
  <tr>
    <td>域名管理</td>
    <td>在控制台中管理客户域名。<br></td>
  </tr>
  <tr>
    <td>报表统计 </td>
    <td>统计和查看域名解析量的变化情况。<br></td>
  </tr>
  <tr>
    <td>服务升级</td>
    <td>针对重点客户的数据审计分析，⾏业解决⽅案⽀持。<br></td>
  </tr>
  <tr>
    <td>SLA 保障</td>
    <td>承诺99.99%服务可⽤性。<br></td>
  </tr>
</tbody>
</table>

>?
>- ECS（EDNS-Client-Subnet）协议在 DNS 请求包中附加请求域名解析的用户 IP 地址，DNS 服务器可以根据该地址返回用户更容快速访问的服务器 IP 地址。
>- 移动解析 HTTPDNS 公共服务已经不再维持 ECS IP 库的常态化更新，仅保持每周更新一次。
>
## 迁移指引
>?针对在**2021年9⽉30⽇23:59:59前**以及**2021年10⽉31⽇23:59:59前**迁移 HTTPDNS 企业版的客户，分别提供相关补贴政策。具体可查看 [过渡期补贴政策说明](https://cloud.tencent.com/document/product/379/59288)。
>
### 步骤1：开通移动解析HTTPDNS
详细操作请参见：[开通移动解析 HTTPDNS](https://cloud.tencent.com/document/product/379/54577)。

### 步骤2：添加域名
详细操作请参见：[添加域名](https://cloud.tencent.com/document/product/379/54588)。

### 步骤3：接入移动解析 HTTPDNS 企业版

请根据您的业务与使用情况选择接入新 IP 的方式：

#### 已经使用移动解析 HTTPDNS 企业版服务，但目前接入的是119.29.29.29
无需在控制台进行任何操作。
您只需在业务代码中将接入 IP 切换为 `119.29.29.99`（HTTPS 加密方式）或者 `119.29.29.98`（AES/DES 加密方式）。

#### 使用免授权方式访问119.29.29.29，没有授权 ID，直接通过 HTTP 请求服务
1. 在 [移动解析 HTTPDNS 控制台](https://console.cloud.tencent.com/httpdns) 开通服务，详情请查看 [开通移动解析 HTTPDNS](https://cloud.tencent.com/document/product/379/54577)。
2. 开通成功后，您将获得相关授权信息进行调用服务，此过程不会影响 `119.29.29.29` 的使用。为确保您的业务正常运行，开通后建议您逐步切量，将请求从 `119.29.29.29` 切换至 `119.29.29.99/98`。详情请查看 [接入移动解析 HTTPDNS](https://cloud.tencent.com/document/product/379/3522)。

#### 使用授权方式访问119.29.29.29，但未开通过移动解析 HTTPDNS 企业版服务，有授权 ID，但没有控制台权限
1. 在 [移动解析 HTTPDNS 控制台](https://console.cloud.tencent.com/httpdns) 开通服务，开通过程中将已有授权 ID 进行绑定，详情请查看 [开通移动解析 HTTPDNS](https://cloud.tencent.com/document/product/379/54577)。
2. 绑定成功后，您只需在业务代码中将接入 IP 切换为 `119.29.29.99`（HTTPS  加密方式）或者 `119.29.29.98`（AES/DES 加密方式）。详情请查看 [接入移动解析 HTTPDNS](https://cloud.tencent.com/document/product/379/3522)。





