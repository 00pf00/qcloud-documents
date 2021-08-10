## �������
��Ǩ������ѡ������Ǩ��ʱ����Ҫ�������������м�飬����У��ʧ�ܡ�

- Դ��Ŀ�������汾����ҪΪ PostgreSQL 10.x ֮ǰ��
- Դʵ���� `wal_level`����Ϊ `logical`��
- Ŀ���`max_replication_slots` ��`max_wal_senders` ������Ҫ���ڴ�Ǩ�Ƶ����ݿ�������
- Ŀ��ʵ���� `max_worker_processes` ������� `max_logical_replication_workers` ��ֵ��
- ��Ǩ�Ʊ��в��ܴ���unlogged table�������޷�Ǩ�ơ�

## �޻�����
����汾������Ҫ���������汾���޸Ĳ��� `wal_level`��`max_replication_slots`��`max_worker_processes` �� `max_wal_senders` �ķ������¡�

1. ��¼Դ���ݿ⡣

> ˵����
>
> - ��Դ���ݿ�Ϊ�Խ����ݿ⣬��Ҫ��¼�����ݿ�����з������ϣ��������ݿ�������Ŀ¼�У�һ��Ϊ$PGDATA��
> - ��Դ���ݿ�Ϊ���������ݿ⣬��ʹ�������ƽ̨�Ĳ����޸ķ�����
> - ����Ҫ�޸�Ŀ��ʵ���Ĳ��������ύ��������

2. �ҵ� postgresql.conf �ļ����򿪴��ļ����޸�`wal_level`��

```
wal_level = logical
```

3. �޸���ɺ��������ݿ�ʵ����
4. ��¼�����ݿ�ʵ���У�ʹ����������鿴����ֵ�Ƿ�������ȷ��

  ```
postgres=> select name,setting from pg_settings where name='wal_level';
   name    | setting 
-----------+---------
 wal_level | logical
(1 row)
postgres=> select name,setting from pg_settings where name='max_replication_slots';
         name          | setting 
-----------------------+---------
 max_replication_slots | 10
(1 row)
postgres=> select name,setting from pg_settings where name='max_wal_senders';
      name       | setting 
-----------------+---------
 max_wal_senders | 10
(1 row)
  ```

5. ����ִ��У������