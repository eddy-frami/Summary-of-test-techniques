# 一：python发送get请求
1. 导入第三方模块requests
2. 使用requests的get参数，发送get请求
3. 请求的参数值可以放在url中，使用&分隔；也可以使用get的param中  
> 例如：  
> import requests  
> url1 = 'http://ws.webxml.com.cn/WebServices/WeatherWS.asmx/getSupportCityString'  
> paras1 = {'theRegionCode': 3113}  
> response = requests.get(url=url1, params= paras1)  
> print(response.text)

# 二：python发送post请求
1. 使用requests的post参数，发送post请求
2. 请求的参数值放在post的第二个参数data中（注意与get的区别）  

---
请求体格式为键值对格式，用字典表示请求体内容
>  例1：  
>  import requests  
>  url1 = 'http://ws.webxml.com.cn/WebServices/WeatherWS.asmx/getSupportCityString'  
>  data1 = {"theRegionCode": 3113}  
>  response = requests.post(url=url1, data=data1, headers={'Content-Type' : 'application/x-www-form-urlencoded'})  
>  print(response.text)

---
请求体格式为json字符串格式  
> 例2：  
> import requests  
> url2 = 'http://139.199.132.220:8000/event/weather/getWeather/'  
> data2 = '{"theCityCode": 1}'  
> response = requests.post(url=url2, data=data2, headers={'Content-Type':'application/json'})  
> print(response.text)

---
如果请求体格式为json字符串格式，但是不想拼json字符串，也可以用字典格式，data2使用字典，在post的第二个参数不用data，而是用json=data2，即可
> data2 = {"theCityCode": 1}  
> response = requests.post(url=url2, **json**=data2, headers={'Content-Type':'application/json'})

# 三：获取响应体中的数据
1.获取响应状态码
> print(response.status_code)  
>
> >打印结果为200
---
2.获取响应体的headers  
> print(response.headers)

---
3.获取响应报文中的内容  
> 
# 四：批量跑用例，使用单元测试框架

1. 导入第三方库unittest
2. 将每个用例都新建为类中的方法，类继承unittest中的testcase

---
get1
> import requests  
> import unittest  
> class Case01(unittest.TestCase):  
> def testcase01(self):  
>    url1 = 'http://ws.webxml.com.cn/WebServices/WeatherWS.asmx/getSupportCityString' 
>    paras1 = {'theRegionCode': 3113}  
>    response = requests.get(url=url1, params=paras1)  
>    print(response.text)

---
get2
> import requests  
> import unittest  
> class Case02(unittest.TestCase):  
> def testcase02(self):  
>    url1 = 'http://ws.webxml.com.cn/WebServices/WeatherWS.asmx/getSupportCityString'  
>    data1 = {"theRegionCode": 3113}  
>    response = requests.post(url=url1, data=data1, headers={'Content-Type': 'application/x-www-form-urlencoded'})  
>    print(response.text)

---
run
> import unittest  
> from get1 import Case01    
> from get2 import Case02  
> suite=unittest.TestSuite()  
> suite.addTest(Case01('testcase01'))  
> suite.addTest(Case02('testcase02'))  
> unittest.TextTestRunner().run(suite)  

# 五：生成文档
1，使用第三方库HTMLTestRunnerCN
2.HTMLTestRunnerCN.HTMLTestRunner().run(suite)去跑批量跑用例，就可以生成测试报告
3.测试报告输出的路径，可以用HTMLTestRunnerCN.HTMLTestRunner()的stream参数
> st=open('./文件地址',wb)  
> HTMLTestRunnerCN.HTMLTestRunner(stream=str,title='文件名',tester='测试人员').run(suite)