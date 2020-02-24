## 操作场景
本文档将向您介绍如何在 Notebook 中访问 COS 进行文件的下载操作，其他操作请参考 [COS SDK](https://cloud.tencent.com/document/product/436/12269) 文档。

## 操作详情
#### 导入依赖包
```
import os
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from ti.utils import get_temporary_secret_and_token

#### 指定本地文件路径，可根据需要修改。
local_file = "/home/tione/notebook/data"

#### 用户的存储桶，修改为存放所需数据文件的存储桶，存储桶获取参考腾讯云对象存储
bucket="user_bucket"

#### 用户的数据，修改为对应的数据文件路径，文件路径获取参考腾讯云对象存储
data_key="user_data_key"

#### 获取用户临时密钥
secret_id, secret_key, token = get_temporary_secret_and_token()
config = CosConfig(Region=os.environ.get('REGION'), SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme='https')
client = CosS3Client(config)

####  获取文件到本地
response = client.get_object(
    Bucket=bucket,
    Key=data_key,
)
response['Body'].get_stream_to_file(local_file)
```
