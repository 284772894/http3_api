#��Ŀ�������

* ����python3���Զ����ӿڲ��Կ��
* ���ö�ÿ��ӿڲ�����ϵķ�ʽ�����������,���õ�PICT��ϲ�������,�������Լ����ú�PICT�����л���

## ��ϲ��Խ���

�ø��ٵ���ϸ������������ø����ʲ����٣���ϲ��Եķ��ࣺ
* ��������ϲ��ԣ�Ҳ����Բ��ԡ�ȫ��ż���ԣ����ɵĲ��Լ����Ը���������������������ȡֵ��ϡ��������ϣ������������Ա�¶����������������ͬ���ö�������ȱ�ݡ�
* ��������ϲ������ɵĲ��Լ����Ը�������n�ͱ���������ȡֵ��ϡ��������ϣ��ò������������Է�������n�����ع�ͬ����������ȱ�ݡ�

�ϺõĲ�����ϵ�ԭ�����
* ÿ�����ӵ�ˮƽֵ���ܱ����Ե���
* �����������ӵĸ���ˮƽֵ��϶��ܱ����Ե�����ͽ���Բ��Է���
	* ����վ�г������еĿ�����ϲ��Թ��ߣ� http://www.pairwise.org/tools.asp
* �����һ���ӿ��е���������������12�鲻ͬ��ϣ�1�������в������Դ˽ӿ���֤ͨ��������11�ζ��ǽӿ�Ϊʧ�ܵ������

## ʹ�÷�ʽ

```
python httpRequest.py
```

## �������ܽ���

* ��ÿ���������Э��ѹ��ķ�ʽ����ѹ��
* yaml��������
* ֧�ֵ�½�ɹ��󷵻�token����user_id�������ӿ�ʹ��,����Ӳ�����Ҫ������ܲ�����������չ���Լ�ȥ��װ
* ������ü��ӿںͷ������ݿ�ķ�ʽ���м��
	* �����������ֱ�ӷ������ݿ⣬������쳣����ֱ�Ӷ�ȡ�ӿڷ���ֵ
* ע��˿����ʱ����̽���׶Σ�Ŀ����ʵ��ƽ̨��

### ��������

* api.yaml

```
---
title: XXXX�ӿڲ���
host: rap.taobao.org
port: 80
protocol: http://
header: {"Accept":"text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8","User-Agent":"Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.59 Safari/537.36"}
database: {"databaseName":userinfo,"host":"127.0.0.1", "user": "root", "password": "", "port": 3306, "charset": "utf8"} #�������ݿ�
api_list:
- id: 1001
  name: ��½
  method: post
  url: /mockjs/11463/login
  stress: 2
  hope_sql: {"findKey": "findBySql", "sql": "select * from info", "params": { }} #ע��findKey��ֵ��Ҫ��Ӧȫ�ֱ��������ֵ
  params:
  - "user_name:user_name:error:0:send_keys:333:type:str,user_name:error:1,user_name:error:2,user_name:error:3:send_keys:22222:type:str"
  - "pwd:pwd:error:0:send_keys:111:type:str,pwd:error:1,pwd:error:2,pwd:error:3:send_keys:32321:type:str"
  is_first: 1 # Ԥ���ĵ�½�ӿ�
  login_key: user_id # ���ظ������ӿ�ʹ�õ�key
- id: 1002
  ...
  get_login_param: 1 # ��Ҫ��½�ӿڷ��ع����Ĳ���
  
```

- ע��������Ϣerror��ֵ 0������1�޴˲�����2������ֵΪ�գ�3�����ݿ��в���.0��3�����ݿ⣬1,2ֱ�Ӷ�ȡ�ӿڷ�����Ϣ

### �������

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
* ���յ�Ŀ����������ƽ̨��
