## ��������
���ĵ�ָ������ Linux ϵͳ��������ΰ�װ��ʹ�� TcaplusDB PB��
## ���л���
Linux 2.6��Suse 12 64 λ��

## ǰ������
### Protobuf ��װ
�ڰ�װ��ʹ�� TcaplusDB Pb ǰ�谲װ Protobuf�����Ѱ�װ�ɺ��Դ˽ڡ�
Protobuf �� Google �Ƴ���һ�ֻ���������ݱ�׼����һ�����Ľṹ�����ݴ洢��ʽ��TcaplusDB ϵͳ֧��ʹ�� Protobuf ��ʽ�����ļ���.proto���������ݱ���ʹ�� TcaplusDB Pb API ֮ǰ����Ҫ�ڿ����������ϰ�װ Protobuf���ڴ��Ƽ�ʹ��Դ������� Protobuf ��װ����װ�������£�
1. ׼���Ʒ�����������
������Ҫ׼����װ�� CentOS6- x86_64 �� CentOS7-x86_64 �汾����ϵͳ�ķ�������Ϊ�˱��빹�� Protobuf����Ҫ��װ�����������װ���������в�ѯ��
 - autoconf
 - automake
 - libtool
 - curl (used to download gmock)
 - make
 - g++
 - unzip

2. ���� Protobuf[Դ�밲װ��](https://github.com/protocolbuffers/protobuf/releases)��
3. �����ʵ������װָ���汾��ProtoBuf��������protobuf 2.6.1�汾������
4. ��ѹԴ�밲װ����������Դ���Ŀ¼�£�����Ϊ�����в�����
```
tar -xzvf protobuf-2.6.1.tar.gz
cd ./protobuf-2.6.1
```
5. Configure ��ָ����װ·��ǰ׺���Ƽ���װ��·�� /usr/local/protobuf �£�����Ϊ�����в�����
```
./configure --prefix=/usr/local/protobuf
```
6. ���벢��װ������Ϊ�����в�����
```
make
make check
make install
```
6. ���ԣ�ʹ�� protoc ����鿴�Ƿ�װ�ɹ�������Ϊ�����в�����������ʾ����װ�ɹ���
```
# protoc --version
libprotoc 2.6.1
```

## ��������

### SDK ��װ
���Ƚ�SDK������������������Ȼ��ִ������ļ���װ��ָ����װĿ¼��
```
tar �Cxzf <��װ��·��> -C <��װĿ¼>��
```

### У��
��װ��ɺ󣬸�Ŀ¼�ṹ���±���ʾ��

| Ŀ¼���ļ� | ˵�� |
|---------|---------|
| include/tcaplus_service/ | TCAPLUS ���� API ͷ�ļ� |
| lib/libtcaplusserviceapi.a | TCAPLUS ���� API ���ļ� |
| include/tcaplus_service/protobuf/ | Protobuf API ͷ�ļ�|
| lib/libtcaplusprotobufapi.a | TCAPLUS Protobuf API ���ļ� |
| examples/tcaplus/ProtoBuf | TCAPLUS Protobuf API Ӧ��ʾ�� |

### ���� example ���� TcaplusDB
GameSvr ��Ϸ�������ж�Ӧ���ݷ����߼��Ŀ��������Բο� example �еĸ��ӿ�ʵ����

1. ��ѹ TcaplusDB Pb API ��������
```
tar -xzvf TcaplusPbApi3.36.0.152096.x86_64_release_20170712.tar.gz
```
2. ���� TcaplusDB ϵͳ������Ϣ��
	1. ���������������´������Ŀ¼��   
```
cd TcaplusPbApi3.36.0.152096.x86_64_release_20170712/release/x86_64/examples/tcaplus/C++_common_for_pb2
```

	2. ������������ vi common.h �޸� common.h ͷ�ļ�������ҵ������޸�����ͼƬ���ݡ�
	**DIR_URL_ARRAY��**��Ⱥ����IP��ַ�Ͷ˿ںš�
	**DIR_URL_COUNT��**�̶�ֵ������Ϊ1���ɡ�
	**TABLE_NAME��**��Ҫ���ʵ�Ŀ���
	**APP_ID��**��Ҫ���ʵĽ���ID��
	**ZONE_ID��**��д��Ҫ���ʵı����ID��
	**SIGNATURE��**��Ⱥ�������롣
	![](https://mc.qcloudimg.com/static/img/4eddaa926243031049ab2e019d8686ab/image.png)
3. �޸Ļ������������ļ���
�� TcaplusPbApi3.36.0.152096.x86_64_release_20170712/release/x86_64/examples/tcaplus Ŀ¼���зֱ�ͨ���첽��ʽ�Լ�Э�̷�ʽ����API�����ӣ�������Э�̷�ʽ���� Set �ӿ���������Ϊ����
���������������´������Ŀ¼��
```
cd TcaplusPbApi3.18.0.152096.x86_64_release_20170712/release/x86_64/examples/tcaplus/C++_pb2_coroutine_simpletable/SingleOperation/set
```
Э�̷�ʽ Set ���ӵ����д��붼�ڸ�Ŀ¼�С��޸� envcfg.env �ļ����� PROTOBUF_HOME ������������Ϊ���� protobuf �İ�װ·����--prefixָ���������� TCAPLUS_HOME ������������Ϊ Tcaplus Pb API ���� release/x86_64 Ŀ¼�ľ���·��������ͼ��
![](https://mc.qcloudimg.com/static/img/093250c857a6c77847fd14bd037dc7e9/image.png)
4. ���û���������
�ڴ���Ŀ¼��ִ�У�
```
source envcfg.env
bash conv.sh
```
5. ��������Ƴ���
ִ��`make`������� example �����ƣ�����ɹ����� mytest ��ִ���ļ���
![](https://mc.qcloudimg.com/static/img/9b4dd73cf2d3b93721d9782a76804d7f/mytest.png)
6. ִ�ж����Ƴ���
����������`./mytest` ��ִ�ж����Ƴ���ִ�н�����������б�׼�������ʾ��������������鿴����Ŀ¼�µ� tcaplus_pb.log ��־�ļ���
