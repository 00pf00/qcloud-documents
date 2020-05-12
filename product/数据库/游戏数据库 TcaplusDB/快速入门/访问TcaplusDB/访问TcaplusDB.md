TcaplusDB���ݿ���ͨ�����ַ�ʽ���з��ʶ�ȡ���������SDK���߰���RESTFul�ӿڣ��ͻ��˹��ߡ�

## SDK����֧�� C++�Լ�JAVA�������ԣ�
- ͨ��[C++ SDK�ӿ�]()����TcaplusDB����

## RESTFul API�ӿ�
- ͨ��[RESTFul API�ӿ�]()����TcaplusDB����


## ͨ�� client ���߷��� TcaplusDB ��

tcaplus_client ��һ�� TcaplusDB ����ʵĿͻ��˹��ߣ���ͨ���±��е��������ӽ������ء�

Linux x86_64 ƽ̨�� TcaplusServiceAPI ������������64λ Linux �汾�� tcaplus_client ���ߣ�Windows x64 ƽ̨�� TcaplusServiceAPI ������������64λ Windows �汾�� tcaplus_client ���ߣ�����ʾ������ Linux x86_64 �汾�Ĺ��߽��С�

| �汾 | ����ϵͳ|���ذ��� | 
|---------|---------|---------|
| 3.36.0.192960 | Linux |[TTcaplusPbApi3.36.0.192960.x86_64](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/TcaplusPbApi3.36.0.192960.x86_64_release_20200115.tar.gz) |

>?��ز�����Ҫ���û���Ѷ���˺��������ͬVPC���磬ͬ�������Ʒ����� CVM �н��С�

### ��װ�ͻ��˹���
�������TcaplusServiceApi��װ���󣬽���ͨ���ϴ������ϴ�����TcaplusDB��ȺͬһVPC��ͬһ�������Ʒ������С�
1. �ϴ���ɺ�ִ�����������ѹ��װ����
```
tar -xf TcaplusServiceApi3.32.0.191008.x86_64_release_20190409.tar.gz -C tcaplus
```
2. ��ѹ��ɺ󣬽�����tcaplus��binĿ¼�У��������ִ��Ȩ��:
```
cd tcaplus/release/x86_64/bin
chmod +x tcaplus_client
```
3. ֱ��ִ�� ./tcaplus_client �������ʾ�������ݿ�����Ĳ�����Ϣ���û����Ը����Լ��ļ�Ⱥ��Ϣ������д��
>!����ʾ���� app_id����Ⱥ����ID,App����Ⱥ��
>����ʾ���� zone�������顣

```
# ./tcaplus_client
--------------------------------------------------------------------------------
 invalid parameters, please start the client as following:
    ./tcaplus_client -a app_id -z zone_id -s signature -d dir_server_url [-t table_name] [-l log_file.xml] [-T tdr_file.tdr] [-e execute_command]
    the params in [] are optional, and theire order is not important.
    -a(--ap_id)    App ID
    -z(--zone_id)    ZONE ID
	-s(--signature)    PASSWORD
    -d(--dir)    dir server addr
    -t(--table)    table to add
    -l(--log)    log file name that must be client_log.xml, and log class name be client
    -T(--tdr)    tdr filename 
    -e(--execute)    content following should be with qoutes.
    e.g. ./tcaplus_client -a 2 -z 3 -s "test@Password1" -d 172.25.40.181:9999 -T table_test.tdr 
--------------------------------------------------------------------------------
```

### ���� TcaplusDB

ʹ���������� TcaplusDB�������о����У����ʵ���Ϣ���£������ڱ����IDΪ1�ı�����д����˱� tb_online��
- ��Ⱥ����ID��2
- �������룺test@Password1
- ������ַ:�����˿ڣ�10.125.32.21:9999
- �����ID��1

```
./tcaplus_client -a 2 -z 1 -s "test@Password1" -d 10.125.32.21:9999
+------------------------------------------------------------------------------+
|    tcaplus_client x86_64  build at Wed Jan 18 22:08:38 CST 2017              |
|                                                                              |
|    Welcome!                                                                  |
+------------------------------------------------------------------------------+

tcaplus>
```

����ʾ��֮������ help���ɿ�����һ���İ�����Ϣ��ͨ�� `> help ��������` ���Բ鿴����ʹ�÷�����

```
tcaplus>help
--------------------------------------------------------------------------------
    show                 get server status related information. executing help show for details.
    dir                  add dir server url. if no dir_server_url added ,
                         commands will fail when executing.
    desc                 output current table struction description
    count                output table row count
    select               query data
    update               update record. if record does not exist then add it or update it if exists.
    insert               insert a new record (not implemented)
    delete               delete record(s)
    bson                 execute bson query
    dump                 dump records from tcaplus to file with csv format
    load                 load records from csv file and import the records to tcplus
    clean                clean table
    quit                 exit the client
    help                 follow a command to get details.
                         e.g. help show, help dir etc.
    note: tdr mode means starting client with -T, and none tdr mode starting client without -T
--------------------------------------------------------------------------------
```


������ʾ�ֱ������������ִ�з��������á�
### desc ����
�鿴��Ķ�����Ϣ��Ƕ���ֶ�ֻ�ܿ���������ΪǶ�����ͣ������޷��鿴Ƕ�׽ṹ��Ķ��塣
ʹ���﷨Ϊ��desc ����;
```
tcaplus>desc game_players;
TableName:game_players
TableType:PROTOBUF
-------------------------------------------------------------------------
| Field                         Type                          Key       |
-------------------------------------------------------------------------
| player_id                     int64                         key       |
| player_email                  string                        key       |
| player_name                   string                                  |
| game_server_id                int32                                   |
| login_timestamp               string                                  |
| logout_timestamp              string                                  |
| is_online                     int8                                    |
| pay                           message                                 |
-------------------------------------------------------------------------
```

### count ����
�鿴���¼������ʹ���﷨Ϊ��count ������
```
tcaplus>count t1;
-------------------------------------------
| TableName                     COUNT(*)  |
-------------------------------------------
| t1                            15        |
-------------------------------------------
```

### ��������
ʹ��dump�����ָ�������еļ�¼�������ļ��ĸ�ʽ��json��ʽ��
ʹ���﷨��dump * from ���� into �ļ�����
```
tcaplus>dump * from player into player.txt;
--------------------------------------------------------------------------------
      dump from table("player") success. total record number is 4
--------------------------------------------------------------------------------
```
### ��������
ʹ��load�����csv�ļ��е���ָ����ļ�¼���޷�ֱ�ӵ���dump�������ļ���
ʹ���﷨��load ���� from �ļ�;
```
tcaplus>load hehe from test1;
--------------------------------------------------------------------------------
      1 records loaded successfully.
--------------------------------------------------------------------------------
```
### ��ձ�����
��Ϊ��ȫԭ�򣬵�ǰ�ͻ��˹��߲�֧��ֱ����������ݡ�����������ű����ݣ���ͨ������̨[�����](https://console.cloud.tencent.com/tcaplusdb/table)���ܽ��С�