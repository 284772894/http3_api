# ��Ŀ�������

* ����python3���Զ����ӿڲ��Կ��
* ���ö�ÿ��ӿڲ�����ϵķ�ʽ�����������,���õ�PICT��ϲ�������,�������Լ����ú�PICT�����л���

## ��ϲ��Խ���

�ø��ٵ���ϸ������������ø����ʲ����٣���ϲ��Եķ���

* ��������ϲ��ԣ�Ҳ����Բ��ԡ�ȫ��ż���ԣ����ɵĲ��Լ����Ը���������������������ȡֵ��ϡ��������ϣ������������Ա�¶����������������ͬ���ö�������ȱ�ݡ�
* ��������ϲ������ɵĲ��Լ����Ը�������n�ͱ���������ȡֵ��ϡ��������ϣ��ò������������Է�������n�����ع�ͬ����������ȱ�ݡ�

�ϺõĲ�����ϵ�ԭ�����:

* ÿ�����ӵ�ˮƽֵ���ܱ����Ե���
* �����������ӵĸ���ˮƽֵ��϶��ܱ����Ե�����ͽ���Բ��Է���
	* ����վ�г������еĿ�����ϲ��Թ��ߣ� http://www.pairwise.org/tools.asp
* �����һ���ӿ��е���������������12�鲻ͬ��ϣ�1�������в������Դ˽ӿ���֤ͨ��������11�ζ��ǽӿ�Ϊʧ�ܵ������

## ʹ�÷�ʽ

```
python httpRequest.py
```

## �������ܽ���

* ��ÿ�����asyncio+aiohttp ����ѹ������
* yaml��������
* ������ü��ӿںͷ������ݿ�ķ�ʽ���м��
	* �����������ֱ�ӷ������ݿ⣬������쳣����ֱ�Ӷ�ȡ�ӿڷ���ֵ

* �ӿڵĲ����Ļ��ܹ����ṩ���Լ��ڴ����еĴ����д���
* �ӿ�����������������׼����ʱ����д���ã�ÿ���ӿڶ��Ƕ�������

### ��������

* api.yaml

```
---
title: XXXX�ӿڲ���
host: int.dpool.sina.com.cn
port: 80
protocol: http://
header: {"Accept":"text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8","User-Agent":"Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.59 Safari/537.36"}
database: {"databaseName":userinfo,"host":"1111", "user": "root", "password": "111", "port": 3306, "charset": "utf8"}
api_list:
- id: 1001
  name: �õ�ip�Ĺ�����
  method: get
  url: /iplookup/iplookup.php
  stress: 1
  hope_sql: {"findKey": "findBySql", "sql": "select * from 1111", "params": { }}
  params:
  - "ip:ip:error:0:send_keys:218.4.255.255:type:str,ip:error:1,ip:error:2,ip:error:3:send_keys:22222:type:str"
  - "format:format:error:0:send_keys:json:type:str,format:error:1,format:error:2,format:error:3:send_keys:32321:type:str"
- id: 1002
  stress: 1
  method: post
  name: �õ�������Ϣ
  url: /iplookup/iplookup.php
  hope_sql: {"findKey": "findBySql", "sql": "select * from info", "params": { }}
  params:
   - "ip:ip:error:0:send_keys:218.4.255.255:type:str,ip:error:1,ip:error:2,ip:error:3:send_keys:22222:type:str"
   - "format2:format2:error:0:send_keys:json:type:str,format2:error:1,format2:error:2,format2:error:3:send_keys:32321:type:str
  
```

- ע��������Ϣerror��ֵ 0������1�޴˲�����2������ֵΪ�գ�3�����ݿ��в���.0��3�����ݿ⣬1,2ֱ�Ӷ�ȡ�ӿڷ�����Ϣ

### �������

����չ

```
 #{'method': 'post', 'success': 32, 'stress': 2, 'failed': 0, 'url': '/mockjs/11463/login', 'name': '��½', 'sum': 16}
    '''
    sum ��ʾ�˽ӿ���16�����
    stress: ��ʾÿ�����ѹ������
    method: ���󷽷�
    success: �ɹ��������
    failed:ʧ���������
    url:�������ַ
    name:�ӿ�����
    '''
```



# ����

* �����򵥰ѽ����¼��excel�У����ʼ�
* �����ĿӴ������̽���׶�

