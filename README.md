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

* ȫ�ֱ���

```
PICT_PARAMS = "d:/params.txt" # ���������ŵ�ַtxt
PICT_PARAMS_RESULT = "d:/t2.txt" # ������Ժ��·��excel
# ���ݿ�ĳ����ֶ�
FIND_BY_SQL = "findBySql" # ����sql����
COUNT_BY_SQL = "countBySql" # �Զ���sql ͳ��Ӱ������
INSERT = "insert" # ����
UPDATE_BY_ATTR = "updateByAttr" # ��������
DELETE_BY_ATTR = "deleteByAttr" # ɾ������
FIND_BY_ATTR = "findByAttr" # ����������ѯһ����¼
FIND_ALL_BY_ATTR = "findAllByAttr"  #����������ѯ������¼
COUNT = "count" # ͳ����
EXIST = "exist" # �Ƿ���ڸü�¼
#�ӿڼ򵥵��е�erro����
NORMAL = "0" # �������������Ե��������ҵ�
DEFAULT = "1" # �޴˲���
EMPTY = "2" # ����Ϊ��ֵ����name=''
DROP = "3" # ���ݿ����Ҳ����˲���
# �ӿ�ͳ��
LOGIN_KEY = ""  # ��½�󷵻ص�key
LOGIN_VALUE = ""  # ��½�󷵻ص�value
RESULT = {"info": []} # �������
```

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
  # ע�������error,��Ӧȫ�ֱ��������error
  is_first: 1 # Ԥ���ĵ�½�ӿ�
  login_key: user_id # ���ظ������ӿ�ʹ�õ�key
- id: 1002
  ...
  get_login_param: 1 # ��Ҫ��½�ӿڷ��ع����Ĳ���
  
```


## �������

* ��ڴ���

```
from DAL import httpConfig as hc
from DAL import gevents, dbConnection, httpParams
from common import operateYaml
from DAL.pairs import *
PATH = lambda p: os.path.abspath(
    os.path.join(os.path.dirname(__file__), p)
)
def myRequest(**kwargs):
  # {"appStatus": {"errorCode": 0,"message": "�����ɹ�"},"content": {"nickname":"18576759587","user_id": 30}} �ӿڶ���Ĺ���
  # ����ֻ�ǿ��ǵ��˵�½�󷵻�token,user_id�ⷽ�������

    method = kwargs["param_req"]["method"]
    get_login_params = 0 # ��ʶ�����˷��ض��ٸ�������user_id,token��������������չ
    param = httpParams.params_filter(kwargs["param_result"])  # ��������Ĵ�����������и��ּ��ܿɴӴ˴���չ
    # get_login_param��ʾ�˽ӿ���Ҫ��½��������id(token),һ���½�ɹ��󷵻ص��ֶ�
    if kwargs["param_req"].get("is_first", "false") == "false" and kwargs["param_req"].get("get_login_param", "false") != "false":
        param[Const.LOGIN_KEY]= Const.LOGIN_VALUE
        get_login_params += 1
    if kwargs["param_req"]["method"] == Const.HTTP_POST:
        really_result = kwargs["http_config"].post(dict_post=kwargs["param_req"], param=param) # ����post����
    elif kwargs["param_req"]["method"] == Const.HTTP_GET:
        really_result = kwargs["http_config"].get(dict_get=kwargs["param_req"], param=param)  # ����get����
    if really_result.get("status_code") == 200:
        print("����%s�ɹ���" %method)
        if kwargs["param_req"].get("is_first", "false") != "false" :
            # ��Ҫ�ӿڷ��ع�����login_key����token,user_id���ȣ���ʱ�Ͳ��ò����ݿ���Ϊ���㣬����Ϊֱ�Ӷ�ȡ��Ӧ���
            if really_result["appStatus"]["errorCode"] == 0:
                Const.LOGIN_KEY = kwargs["param_req"]["login_key"]
                Const.LOGIN_VALUE = really_result["content"][Const.LOGIN_KEY]
                print("%s�ӿ���֤ͨ��,�������ݿ�" %method)
                kwargs["result"]["success"] += 1
            else:
                print("%s�ӿڲ���ʧ��,�������ݿ�~" %method)
                kwargs["result"]["failed"] += 1

        #���ʵ�ʵĲ������쳣,is_first��ʾ�Ƿǵ�½�ӿڣ��Ͳ������ݿ�.
        elif len(kwargs["param_result"].keys()) != len(param) - get_login_params:
            #���ݽӿڷ��ص�errorCode�жϣ�����errorCode=2��ʾ�����쳣
            if really_result["appStatus"]["errorCode"] == 2:
                print("%s�ӿ��쳣�������ͨ��" % method)
                kwargs["result"]["success"] += 1
            else:
                print("%s�ӿ��쳣�������ʧ��" % method)
                kwargs["result"]["failed"] += 1
            return
        else: #ֱ�Ӳ�ѯ���ݿ���Ϊ����
            check_sql_key = kwargs["param_req"]["hope_sql"]["findKey"]  # ���������key,����ת����ͬ�����ݿ��ѯ���
            kwargs["param_req"]["hope_sql"]["params"] = param  # �Ѿ�����õ���������������ݿ�sql�����������Ϊ��params{"a":"b"}
            for item in kwargs["param_result"]:
                #  error: 0������1�޴˲�����2������ֵΪ�գ�3�����ݿ��в���.0��3�����ݿ⣬1,2ֱ�Ӷ�ȡ�ӿڷ�����Ϣ
                error = kwargs["param_result"][item]["error"]
                if error == Const.NORMAL or error == Const.DROP:
                    if kwargs["check_sql"].findKeySql(check_sql_key, **kwargs["param_req"]["hope_sql"]):
                        print("%s���ݿ�ӿ���֤�ɹ�" %method)
                        kwargs["result"]["success"] += 1
                    else:
                        print("%s���ݿ�ӿ���֤ʧ��" %method)
                        kwargs["result"]["failed"] += 1
                    return
                elif error == Const.DEFAULT or error == Const.EMPTY:
                    if really_result["appStatus"]["errorCode"] == 2: # �ӿڷ��ص�2Ϊ�����쳣
                        print("%s�ӿ��쳣�������ɹ�" %method)
                        kwargs["result"]["success"] += 1
                    else:
                        print("%s�ӿ��쳣�������ʧ��" % method)
                        kwargs["result"]["failed"] += 1
                    return
    else:
        print("������ʧ��,״̬��Ϊ:%s" % really_result.get("status_code"))
def gevent_request(**kwargs):
    for i in kwargs["api_config"]:  # ��ȡ�����ӿڵ����ã�api.ymal
        # ���ɲ���
        pict_param(params=i["params"], pict_params=Const.PICT_PARAMS,
                   pict_params_result=Const.PICT_PARAMS_RESULT)
        # ��ȡ����
        get_param = read_pict_param(Const.PICT_PARAMS_RESULT)
        count = len(get_param) # ���ݲ�ͬ���������ѭ������
        green_let = []
        req = {}
        for key in i:
            if key != "params":  # ����������������������Ѿ��������
                req[key] = i[key]
        result = {}  # ͳ������
        result["name"] = req["name"]  # �ӿ�����
        result["method"] = req["method"]
        result["url"] = req["url"]
        result["sum"] = count
        result["stress"] = req["stress"]
        result["success"] = 0
        result["failed"] = 0
        kwargs["result"] = result
        for k in range(0, count):
            kwargs["param_result"] = get_param[k]  # �ӿ��в�ͬ�Ĳ�����ϣ���dict����
            kwargs["param_req"] = req  #ÿ���������ϲ���֮��Ĳ�����������ֻ�������url,method,������
            for item in range(kwargs["param_req"]["stress"]):  # ѹ������,����Э��ȥѹ��
                green_let.append(gevents.requestGevent(myRequest(**kwargs)))
            for k in range(0, kwargs["param_req"]["stress"]):
                green_let[k].start()
            for k in range(0, kwargs["param_req"]["stress"]):
                green_let[k].join()
        Const.RESULT["info"].append(kwargs["result"])
def get_config(api_ymal):
    '''
    �õ�api.ymal�е����õĽӿ���Ϣ
    :param api_ymal:
    :return:
    '''
    http_config = {} # http��Ϣ�ļ�¼
    api_config = [] # api�ļ�¼��¼
    get_api_list = operateYaml.getYam(api_ymal)
    for key in get_api_list:
        if type(get_api_list[key]) != list:
            http_config[key] = get_api_list[key]
        else:
            api_config = get_api_list[key]
    return http_config, api_config

if __name__ == "__main__":
    start_time = time.time()
    get_api_config = get_config(PATH("api.ymal"))
    http_conf = hc.ConfigHttp(dict_http=get_api_config[0]) # http���������
    apiConfigs = get_api_config[1]
    check_sql = dbConnection. MySQLet(host=get_api_config[0]["database"]["host"], user=get_api_config[0]["database"]["user"],
                                     password=get_api_config[0]["database"]["password"], charset=get_api_config[0]["database"]["charset"],
                                     database=get_api_config[0]["database"]["databaseName"], port=get_api_config[0]["database"]["port"])
    gevent_request(http_config=http_conf, api_config=get_api_config[1], check_sql=check_sql)
    check_sql.close()
    end_time = time.time()
    print("�����ѣ�""%.2f" % (end_time - start_time))
    print(Const.RESULT)

   
```

* �������

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
