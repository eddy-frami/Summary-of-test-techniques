# 一：脚本录制流程
1. 创建脚本
2. 选择协议，设置录制选项
3. 开始录制
4. 插入命令
5. 停止录制
# 二：录制脚本具体操作
- ## 可以使用ld自带应用web tools作为录制时的网站
1. 启用web service服务：hploadrunner--samples--web--start web servers  
2. 环境配置  
首页设置为空白页；删除ie缓存；设置--高级--不启用“第三方浏览器扩展”  
- ## 参数化
1. 设置参数。选择要设置的参数值例如values=v1，将v1设置成参数。选中v1，右键，选择“replace with a parameter”,设置参数名，例如设置为“name”,那么将values的取值就从name里面取值。values={name}  
2. 设置参数化字段的属性。右键选中{name}，选择parameter property  
3. 用例执行次数设置  
vuser--run-time setting  
4.取值策略  
**select next row(参数取值策略)**  
顺序：从上到下依次取值  
随机：随机取值  
唯一：多个用户执行，每个用户取值唯一  
**update value on(参数更新值策略)**  
每次迭代更新：每迭代一次更新一次  
每取值一次更新：每次取值都更新  
只更新一次：只取一个值，不会更新   
**顺序取值与唯一取值的区别**  
顺序取值：  
user1：1 2 3  
user2：1 2 3  
user3：1 2 3  
唯一取值：  
user1：1 2 3                          
user2：4 5 6  
user3：7 8 9   
- ## 生成大量参数数据方法
1.excel生成  
2.数据库导出  
3.编程生成  
> i = 1  
> myfile = open("/Users/suyun/Desktop/pytest/data.txt",mode="w")  
> myfile.write("username,password,mailbox\n")  
> while i<50:  
> myfile.write("vu"+str(i)+",123456,mail"+str(i)+"@123.com\n")  
> i=i+1  
> myfile.close()  
> myopen = open("/Users/suyun/Desktop/pytest/data.txt",mode="r")  
> mylines = myopen.readlines()  
> myopen.close()  
> print(mylines)

- ## 参数赋值、取值
1.替换参数（和excel中查找和替换的用法一样，将文件中所有位置都替换）。路径：edit--replace 弹出框中，"find what"为要被替代的值，"replace with"为赋予的参数名。例如要将脚本中所有"127.0.0.1"都用""{ip}"来替换。  
2.赋值、取值函数
- 字符串、整数保存在参数中  
lr_save_string("127.0.0.1","ip"),将字符串""127.0.0.1"用“ip”来表示。  
lr_save_int(5,"param")将整型数字用变量替换  
再运行脚本就能正常运行。  
- 从参数中取出内容  
lr_eval_string("{}")  
char *tmp="hello";  
lr_save_string("777","page"); //将常量777保存为参数page  
lr_output_message(lr_eval_string("{page}"));  //获取并输出参数page的当前值  
lr_save_string(tmp,"page");     //将变量保存为参数,tmp为变量  
lr_output_message(lr_eval_string("{page}"));  
执行结果：  
777  
hello  
- ## 关联
1. 手工关联
2. 录制后自动关联
3. 录制过程中自动关联

---
### 手工关联
1. 举例说明。假设现在要录一个请求首页信息+登陆的场景，首先请求首页信息时，浏览器会在请求之后给一个响应，响应信息里面包含sessionid，每次请求都会返回不同的sessionid，之前的sessionid就会失效。登陆时会将最新的sessionid一起上送给服务端。  
2. 录制这个场景的脚本时，登陆上送给服务端的sessionid是录制脚本时的sessionid，如果下次拿着这个脚本回放时，会重新请求首页+登陆，此时登陆的sessionid应该是本次脚本回放时服务端返回的sessionid。但是上送的却是录制脚本时的sessionid，这就会造成上送的sessionid失效，不是最新的sessionid。  
3. 解决的方法是，在录制脚本时，请求首页之前，加一个注册函数Web_reg_save_param（"param参数名","LB=左边界值","RB=右边界值",LAST）,这样把这个注册函数后面服务器响应值中，符合左右边界值的响应值，放在"param参数名"中，然后在之后用到这个值的地方，例如登陆时上送的sessionid，用参数名代替上送的值，这样就可以上送给服务端最新的参数值了。
4. 注册函数Web_reg_save_param像这种以Web_reg_开头的函数一般是注册函数，使用位置为，使用在背部或消息包对应请求之前。
5. 使用方法：value=123&&*替换成value={param参数名}  

Web_reg_save_param的其他参数：  
1. SaveoffSet=7，从左边界后的第7位开始  
1. SaveLen=20，符合左右边界条件的长度20位的字符  
1. ORD=2，响应体中可能有很多处都符合条件，取第2处的值。  

---
### 录制后自动关联
1. 