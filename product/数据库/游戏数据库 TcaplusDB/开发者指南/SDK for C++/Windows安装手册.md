
## ��������
����Ϊ����������� Windows(x64) ϵͳ�ϲ��� Tcaplus Protobuf API��

## ���л���
- ����ϵͳ��Microsoft Windows x86\_64
- ���뻷����Microsoft Visual Studio 2015 (VC14.0)

## ��������
### ���������
1. ������������ Tcaplus Protobuf API ��������μ� [SDK ����](https://cloud.tencent.com/document/product/596/31925)��
2. ��ѹ����������������Ľṹ��
```
Tcaplus_PbAPI_3.32.0.171987_Win64Vc14MT_Release_20180413
|-- cfg                                                 # ����Ŀ¼
|-- docs                                                # �ĵ�Ŀ¼
|   `-- tcaplus
|-- include                                             # ����ͷ�ļ�Ŀ¼
|   `-- tcaplus_pb_api
|-- lib                                                 # ��Ŀ¼
|    |-- Debug
|    `-- Release
|-- examples                                            # ʾ��Ŀ¼
   `-- tcaplus
       |-- C++_common_for_pb2                           # ʾ������ͷ�ļ�Ŀ¼
       |-- C++_pb2_asyncmode_simpletable                # �첽ģʽ��pb�򵥱�ʾ��
       |-- C++_pb2_coroutine_simpletable                # Э��ģʽ��pb�򵥱�ʾ��
```

### ׼��
1. ��ȷ���Ѿ��� [��Ѷ�� TcaplusDB](https://cloud.tencent.com/product/tcaplus) ��ͨ����Ϸҵ�񣬲����Ѿ���ȡ����Ӧ�� App ��Ϣ�����磺AppId��ZoneId��AppKey����
2. ��ѹ������������װ��������`TSF4G_BASE-2.7.28.164975_Win64Vc14Mt_Release.zip`������Ϊ����ʵ����  [Windows ƽ̨����������](https://cloud.tencent.com/document/product/596/31925#windows-.E5.B9.B3.E5.8F.B0.E4.BE.9D.E8.B5.96.E5.8C.85.E4.B8.8B.E8.BD.BD) �ṩ��������Ϊ׼��
���谲װ�ĸ�·���� `D:\Tencent\tsf4gMT`������ļ����ᱻ��װ�� `D:\Tencent\tsf4gMT\win64vc14MT`·���¡�
3. ���벢��װ`Porotbuf-3.5.1`��
  - [Դ���ַ](https://github.com/google/protobuf/releases/) 
  - [���밲װָ��](https://github.com/google/protobuf/tree/master/cmake) 
  - ���谲װ·��Ϊ `D:\protobuf-3.5.1`
4. ���벢��װ`OpenSSL-1.1.0f`��
  - [Դ�����ַ](https://www.openssl.org/source/) 
  - [���밲װָ��](https://wiki.openssl.org/index.php/Compilation_and_Installation) 
  - ���谲װ·��Ϊ `D:\openssl-1.1.0f`
5. ���û���������
  - `TSF4G_HOME="D:\Tencent\tsf4gMT"`
  - `PROTOBUF_HOME="D:\protobuf-3.5.1"`
  - `OPENSSL_HOME="D:\openssl-1.1.0f"`

### ����
1. ��ѹ�� Tcaplus Pb API ��װ����
2. �� `examples/tcaplus/C++_common_for_pb2/common.h` �ļ������� App ��Ϣ��
  - Tcapdir ������ַ�б� - `DIR_URL_ARRAY`
  - Tcapdir ������ַ���� - `DIR_URL_COUNT`
  - �û�������ʹ��֮ǰ�û���ҪԤ��ʹ��ʾ��Ŀ¼�е� table_test.xml �ļ������� - `TABLE_NAME`
  - �û�ҵ�� ID - `APP_ID`
  - �û�ҵ������ ID - `ZONE_ID`
  - �û�ҵ������ - `SIGNATURE`

 ```C
 //examples/tcaplus/C++_common_for_pb2/common.h
  /******************�û��Զ���****************************/
  // Tcapdir ������ַ�б�
  static const char DIR_URL_ARRAY[][TCAPLUS_MAX_STRING_LENGTH] =
  {
  	"tcp://10.125.32.21:9999"
  };
  // Tcapdir ������ַ����
  static const int32_t DIR_URL_COUNT = 1;
  // �û�����
  static const char * TABLE_NAME = "tb_online";
  // �û�ҵ��ID
  static const int32_t APP_ID = 4;
  // �û�ҵ������ID
  static const int32_t ZONE_ID = 1;
  // �û�ҵ������
  static const char * SIGNATURE = "8e24269ba91f433ca7e89b1cbb77368e";
  /******************�û��Զ���******************************/
  ```

3. �� `examples\tcaplus\C++_pb2_coroutine_simpletable\SingleOperation\set`Ϊ����
```
set/
|-- main.cpp                              # ʾ������������
|-- readme.txt
|-- table_test.proto                        # T����proto�ļ�,����ҪԤ�ȴ���
|-- pb_co_set.sln                           # ��ĿVisualSudio��������ļ�
|-- pb_co_set.vcxproj                       # ��ĿVisualSudio�����ļ�
|-- proto_generate.cmd                      # ����proto�ļ��ű�
`-- tlogconf.xml
```
  * ���ȣ�ȷ���Ѿ�ʹ��`table_test.proto`��Ŀ�� App �д�����ɹ���
  * ִ��`proto_generate.cmd`�ű����ڵ�ǰ·�������������ļ���
    * `table_test.pb.cc`
    * `table_test.pb.h`
  * �� Microsoft Visual Studio 2015 �д���Ŀ�ļ�`pb_co_set.sln`��
  * ���ɽ��������
  * ���û�д����������`examples\tcaplus\C++_pb2_coroutine_simpletable\SingleOperation\set/x64`·���½������ɿ�ִ���ļ�`pb_co_set.exe`��


### ����
1. ����`pb_co_set.exe`��`tlogconf.xml`�����ļ���ͬһĿ¼�¡�
2. �л�`administrator`��ݲ�ʹ�� cmd.exe �� powershell.exe ���п�ִ���ļ�`pb_co_set.exe`��
3. ��������
4. �����Ҫ�˽�������ϸ��Ϣ����鿴��־�ļ�`tcaplus_pb.log`��
5. �����Ҫ����`*_crypto`ʾ������ȷ��`libcrypto-1_1-x64.dll`�ļ���ϵͳ Path ·����,����ļ��ܹ��� openssl �ı���Ŀ¼���ҵ���
![Output](https://main.qcloudimg.com/raw/40627a3a2dff8a4a4aeea57cda2bb8bb.png)


## Tcaplus Pb API �����б�

Tcaplus Pb API ֧�ֶ������Ͳ�����֧���첽��Э��ģʽ���û�������ʾ�����ҵ���Ӧ���÷��������� Tcaplus Pb API �����б�

|����                          | ����  |
| ------------------------------- | ------------ |
|SET           |ͨ��ָ��һ����¼������������һ����¼�������¼����ִ�и��ǲ���������ִ�в�������� |
|GET          |��һ�� Tcaplus pb ����ͨ��ָ��һ����¼����������ѯһ����¼��������ݼ�¼�����ڣ����᷵�ش���|
|ADD           |ͨ��ָ��һ����¼������������һ����¼�������¼���ڷ��ش���|
|DELETE         |ͨ��ָ��һ����¼����������ɾ���˼�¼��������ݲ������򷵻ش���|
|BATCHGET              |��һ�� Tcaplus pb ����ͨ��ָ������������ѯ������¼��|
|TRAVERSE           |����һ�� Tcaplus pb �������ض�����¼��|
|FIELDGET        |��һ�� Tcaplus pb ����ͨ��ָ��һ����¼����������ѯһ����¼��������ֻ��ѯ�ʹ����û�ָ�����ֶε�ֵ���������紫��������������ݼ�¼�����ڣ����᷵�ش���|
|FIELDSET   |ͨ��ָ��һ����¼�����������޸�ָ���ֶΣ�ֻ����ָ���ֶε�ֵ����������������������ݼ�¼���ڣ���ִ�и��²��������򽫻᷵�ش���|
|FIELDINC      |ͨ��ָ��һ����¼������������ָ�����ֶν��������������������ֽ�֧�� int32��int64��uint32 �� uint64 �����ֶΡ������� FIELDSET ���ơ�|
|GETBYPARTKEY  |ͨ��ָ��������������ѯ���������Ķ������ݣ��������ϱ����ڽ����ʱ�򴴽�������������᷵�ش���|
