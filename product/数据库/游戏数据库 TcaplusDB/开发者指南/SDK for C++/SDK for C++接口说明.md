## ���
TcaplusDB ���� API ��Ӧ�÷�����Ϸ���ݿ� TcaplusDB �����ݷ�����ڣ���Ӧ�ô�ȡ��Ϸ���ݿ� TcaplusDB ��ҵ�����ݵı�̽ӿڡ���ǰ TcaplusDB ��Ҫʹ�û��� Google Protocol Buffer��Protobuf�� ��ͨѶ������Ԫ����Э�顣


## ����
���ڿ���̨��ͨҵ�񴴽����󣬿���̨������Ϣҳ���ṩ����ID,�������룬����IPV4��ַ���Լ� Protobuf �����ҳ��ʾ�Ѿ������ı����ƺͱ����ID����Ϣ��ʹ��TcaplusDB C++ API��Ӧ�ÿ��Բ������ڴ˼�Ⱥ�µĶ����

## ģ��
������ Protobuf Э����������� TcaplusDB �淶�ı��ѱ����Ԫ�ļ����� TcaplusDB ����̨����ϵͳ�н��д����±���޸��Ѿ����ڵı��ɹ��󼴿�ͨ�� TcaplusDB Protobuf API ���б����ݼ�¼�Ķ�д��������ǰ TcaplusDB Protobuf API ֧�ֵĲ������±�

| ���� | �������� |
|---------|---------|
| GET | ���ݵ������ֶλ�õ��� Value ��Ϣ |
| BATCHGET | ���ݶ�����ֶλ�ö��� Value ��Ϣ |
| ADD | ����һ�����ݡ�����ֶζ�Ӧ��¼�����򱨴� |
| SET | �ֶζ�Ӧ��¼������������ݣ���������������� |
| DEL| �����ֶ�ɾ����Ӧ�ļ�¼ |
| FIELDINC | ָ���ֶε�ֵ�������ͣ�����ָ��ֵ |
| FIELDSET | ����ָ���ֶΣ�������������ֵ |
| FIELDGET | ��ȡָ���ֶΣ�������������ֵ |
| INDEXGET | ָ���������ֶν���������ѯ |
| TRAVERSE | ָ����������ȫ����� |

## TcaplusDB SDK Լ��
TcaplusDB ��Ҫ�����������ֶε���Ϣ����չ tcaplusservice.optionv1.proto ������ TcaplusDB ϵͳ�У���ֻ�����Զ����ʱ���ã������±���޸��Ѿ����ڵı�ʱ�����ϴ���ϵͳ�Ѿ����á������������£�
```
extend google.protobuf.MessageOptions
{
    optional string tcaplus_primary_key             = 60000; //����������
    repeated string tcaplus_index                   = 60001; //����������
    optional string tcaplus_field_cipher_suite      = 60002; //�������ֶ�ʹ�õļ����㷨
    optional string tcaplus_record_cipher_suite     = 60003; //�������ֶ�ʹ�õļ����㷨����ʱδʹ��
    optional string tcaplus_cipher_md5              = 60004; //���ڷ���cipher �ֶ���ϢժҪ
    optional string tcaplus_sharding_key            = 60005; //Tcaplus sharding key
}

extend google.protobuf.FieldOptions
{
    optional uint32 tcaplus_size                    = 60000; // �ֶδ�С����ʱδʹ��
    optional string tcaplus_desc                    = 60001; // �ֶ�����
    optional bool tcaplus_crypto                    = 60002; // �Ƿ�����ֶΣ������㷨��tcaplus_field_cipher_suite����
}
```
�����ļ�����Ŀ¼ release\x86_64\include\tcaplus_pb_api\tcaplusservice.optionv1.proto ���ҵ���
1. ����Ҫ����ĸ���»��߿�ͷ�����ܳ���31���ֶΣ������г����֣���ĸ���»���֮��������ֶΡ�
2. ���ֶε�����Ҫ����ĸ���»���������protobuf �Ѿ����ơ�
3. �������4���ֶΣ������� required ���ͣ�����󳤶Ȳ��ܳ���1022�ֽڡ�
4. �ֶ�ֵ������ܳ���256KB, ͬʱ������¼������ܳ���256KB��
5. ���������ֶΣ�������һ�� ��ͨ�ֶΡ�
6. ��Ĭ���� generic ���͡������ⲻ��ʾ generic ���͡�
7. �����ֶε�ǰֻ���� protobuf �涨�ı������ͣ�Scalar Value Type�������ܰ��������������ͣ��Զ������͵ȡ�

## ���ýӿ�˵��
```
 @brief �����û������req�е�index���ƣ�msgֵ��offset�Լ�limit��ͨ��������ȡ�����¼��ֵ��䵽res�е�vec�ṹ�У��������ܼ�¼���Լ�ʣ���¼����
 @param [INOUT] req   �û������req
 @param [INOUT] res   �û������res
 @retval <0   ʧ�ܣ����ض�Ӧ�Ĵ����롣
 @retval 0    �ɹ���
```
**int Get(::google::protobuf::Message &msg);**
```
  @brief �����û������ msgs �е� �ֶ�ֵ��������ȡ msg ��Ϣ���ֶ�ֵ������䵽 msgs ��.
  @param [INOUT] msgs �û������ �ֶ��б�����ָ���ֶ�� msgs ��
  @retval <0   ʧ�ܣ����ض�Ӧ�Ĵ����롣
  @retval 0    �ɹ���������һ���ֶβ�ѯ�ɹ��Ż᷵�� 0��
```
**int BatchGet(std::vector< ::google::protobuf::Message * > &msgs);**

```
 @brief �����û������msg�е��ֶΣ�����msg���ݼ�¼������ֶδ��ڱ����˳���
 @param [INOUT] msg   �û�������ֶ�ֵ���Լ���Ҫ��������ݼ�¼msg��
 @retval <0   ʧ�ܣ����ض�Ӧ�Ĵ����롣
 @retval 0    �ɹ���
```
**int Add(::google::protobuf::Message \*msg);**

```
 @brief �����û������msg�е��ֶΣ������¼���ڸ���ָ����¼��ֵ���������ָ����¼��
 @param [INOUT] msg   �û�������ֶ�ֵ���Լ���Ҫ���õ����ݼ�¼msg��
 @retval <0   ʧ�ܣ����ض�Ӧ�Ĵ����롣
 @retval 0    �ɹ���
```
**int Set(const ::google::protobuf::Message &msg);**

```
  @brief �����û������ msg �е��ֶ�ֵ��ɾ�� msg��       
  @param [IN] msg   �û�������ֶ�ֵ������ָ���ֶ�� msg �С�
  @retval <0   ʧ�ܣ����ض�Ӧ�Ĵ����롣
  @retval 0    �ɹ���������һ���ֶβ�ѯ�ɹ��Ż᷵�� 0��
```
**int Del(const ::google::protobuf::Message &msg);**
```
 @brief �����û������msg�е��ֶ�ֵ��values����ֵ����dottedpathsָ�����ֶ����ƣ�����msgָ���ֶε�ֵ���ֶ�Ϊ��ֵ�ͱ�����
 @param [INOUT] msg   ���ݼ�¼msg�������û�������ֶ�ֵ�����������ֶεĽ��ֵ���µ�msg��
 @param [IN] dottedpaths �ֶ����Ƶĵ��Ƕ���ַ�����
 @retval <0   ʧ�ܣ����ض�Ӧ�Ĵ����롣��ʾû���κ��ֶθ���
 @retval 0    �ɹ���ȫ���ֶθ��³ɹ���
```
**int FieldInc(::google::protobuf::Message &msg, const std::set &dottedpaths);**
```
 @brief �����û������msg�е��ֶ�ֵ����dottedpathsָ�����ֶ����ƣ���ȡָ���ֶε�ֵ������䵽msg�С�
 @param [INOUT] msg   ���ݼ�¼msg�������û�������ֶ�ֵ������ָ���ֶ��msg��
 @param [IN] dottedpaths �ֶ����Ƶĵ��Ƕ���ַ�����
 @param [OUT] failedpaths ���ز���ʧ�ܵ��ֶ����Ƶĵ��Ƕ���ַ�����
 @retval <0   ʧ�ܣ����ض�Ӧ�Ĵ����롣
 @retval 0    �ɹ���������һ���ֶβ�ѯ�ɹ��Ż᷵��0��
```
**int FieldGet(const std::set<std::string> &dottedpaths, ::google::protobuf::Message \*msg, std::set<std::string> \*failedpaths);**
```
 @brief �����û������ msg �е� �ֶ�ֵ���� dottedpaths ָ�����ֶ����ƣ�����ָ���ֶε�ֵ������˲����ڵ�ֵ��׷�ӽ�ȥ��
 @param [IN] msg �û������ �ֶ�ֵ������ָ���ֶ�� msg �С�
 @param [IN] dottedpaths �ֶ����Ƶĵ��Ƕ���ַ�������
 @retval <0   ʧ�ܣ����ض�Ӧ�Ĵ����롣��ʾû���κ��ֶθ��¡�
 @retval 0    �ɹ���ȫ���ֶθ��³ɹ���
```
**int FieldSet(::google::protobuf::Message &msg, const std::set &dottedpaths);**
```
 @brief �����û������req�е�index���ƣ�msgֵ��offset�Լ�limit��ͨ��������ȡ�����¼��ֵ��䵽res�е�vec�ṹ�У��������ܼ�¼���Լ�ʣ���¼����
 @param [INOUT] req   �û������req
 @param [INOUT] res   �û������res
 @retval <0   ʧ�ܣ����ض�Ӧ�Ĵ����롣
 @retval 0    �ɹ���
```
**int Get(NS_TCAPLUS_PROTOBUF_API::IndexGetRequest& req, NS_TCAPLUS_PROTOBUF_API::IndexGetResponse \*res);**
```
 @brief ��������Ϣ����䵽msg�С�
 @param [INOUT] msg   ����ָ���ֶ��msg��
 @param [INOUT] cb   �ص�����
 @retval <0   ʧ�ܣ����ض�Ӧ�Ĵ����롣
 @retval 0    �����ɹ���ɡ�
```
**int Traverse(::google::protobuf::Message \*msg, TcaplusTraverseCallback \*cb);**

## ������Լ��
### Get ����Լ��
1. ���ܲ�ѯ�ض��汾�ŵļ�¼��
1. �������ѯ���ֶ�ԭ��¼�в����ڣ���᷵���ֶ�Ĭ��ֵ��

### BatchGet ����Լ��
1. ������ѯ�������뾭�� tcaproxy ������Ϣ·�ɴ���tcapsvr ���̲�֧��������ѯ������
1. һ��������ѯ���󷵻�һ��������ѯ�����������ѯ�ĳ�ʱʱ��Ϊ10�롣
1. ������ѯ�����¼��ͬ�����м�¼������ѯ�����ڻ��߲�ѯʧ�ܵļ�¼Ҳ���ڽ�����д���һ���յļ�¼�������Ҫͨ�� FetchRecord ���м�¼��ȡ��
1. ������ѯ������ܴ�С���ܳ���256K�����򳬹���С��¼���ݻ��޷����أ��᷵�ؿռ�¼���ݡ�
1. ������ѯ��������ص�˳��������ļ�¼˳�򲻱�֤һ�¡�

### FieldInc ����Լ��
1. message ��ָ���� �ֶεļ�¼�����Ǵ��ڡ�
1. dottedpaths ��ָ�����ֶα�������ֵ���͡�
1. dottedpaths ���� set �е�Ԫ�ظ��������������128����
1. dottedpaths ���� set �е�ÿ��Ԫ�صĳ��Ȳ��ܳ���1023�ֽڡ�
1. dottedpaths ���� set �еĵڸ�Ԫ�ش�����ֶ�Ƕ�ײ��ܳ���32��

### FieldGet ����Լ��
1. dottedpaths ���� set �е�Ԫ�ظ��������������128����
1. dottedpaths ���� set �е�ÿ��Ԫ�صĳ��Ȳ��ܳ���1023�ֽڡ�
1. dottedpaths ���� set �еĵڸ�Ԫ�ش�����ֶ�Ƕ�ײ��ܳ���32��

### FieldSet ����Լ��
1. dottedpaths ���� set �е�Ԫ�ظ��������������128����
1. dottedpaths ���� set �е�ÿ��Ԫ�صĳ��Ȳ��ܳ���1023�ֽڡ�
1. dottedpaths ���� set �еĵڸ�Ԫ�ش�����ֶ�Ƕ�ײ��ܳ���32��


## SDK Դ�ļ�Ŀ¼�ṹ

    `-- release
        `-- x86_64
            |-- docs                                   �ĵ�Ŀ¼
            |   `-- tcaplus
            |       `-- readme.txt                     ��C++ SDK��ʹ������ָ���ļ�
            |-- examples                               ��C++ SDKʹ�õ�����Ŀ¼����ͬ�����첽���󲿷�,����ֱ���޸�ʹ��
            |-- include                                ��C++ SDK��ͷ�ļ�Ŀ¼
            |   `-- tcaplus_pb_api                     TcaplusDB PB APIͷ�ļ���
            |       |-- cipher_suite_base.h            ���ݼ������㷨�׼�����
            |       |-- default_aes_cipher_suite.h     ���ݼ������㷨�׼�Ĭ��ʵ����
            |       |-- tcaplus_async_pb_api.h         �첽ģʽ���ͷ�ļ���ʹ���첽ģʽ���е�TcaplusAsyncPbApi��
            |       |-- tcaplus_coroutine_pb_api.h     Э��ģʽ���ͷ�ļ���ʹ��Э��ģʽ���е�TcaplusCoroutinePbApi��
            |       |-- tcaplus_error_code.h           ������ͷ�ļ��������漰�Ĵ�����������������ҵ���Ӧ�Ķ��弰����
            |       |-- tcaplus_protobuf_api.h         API����ͷ�ļ�������������ͷ�ļ���ֻ��������һ���ļ����㿪��
            |       |-- tcaplus_protobuf_define.h      �����ṹ�ͺ궨��ͷ�ļ�������ClientOptions�ṹ��MESSAGE_OPTION_*�궨��
            |       |-- tcaplusservice.optionv1.pb.h   Tcaplus���������Protobufͷ�ļ�
            |       `-- tcaplusservice.optionv1.proto  Tcaplus���������protoԴ�ļ�, �Զ����ʱ��������ļ�
            |-- lib                                    ��C++ SDK�Ŀ��ļ�Ŀ¼
            |   `-- libtcaplusprotobufapi.a            ��C++ SDK�Ŀ��ļ�, �����������ӿ������
            `-- version                                ��C++ SDK�İ汾��¼�ļ�