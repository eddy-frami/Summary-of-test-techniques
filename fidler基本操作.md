1.响应信息  
1）返回码
1**  中间状态，请求被接受  
2** 请求被成功处理  
3** 重定向相关  
4** 客户端错误  
5** 服务端错误  

2.工具栏  
1）replay 重新播放、重放。  

	选中抓到的请求，点击”replay“一次，就会重发一次请求  
	快捷键R，也可以重放。选中之后，点击r键  
	shift+r，可以设置重放次数  

2）删除请求  

	选中，delete键  
	选中，右键选择remove  
	选中要保留的请求，shift+delete可以删掉其他请求
	工具栏的叉号，有”remove“和”remove all“选项
	ctrl+x，删除所有请求
	工具栏edit--》remove--》all  session，删除所有请求
	
3）go 断点，程序在某一步停下来
 
4）stream 流模式，  

	区别于缓冲模式，发出去或者接收的东西会在代理那里缓冲一下再发出去；
	流模式是没有缓冲的，直接出去很顺畅。一般不用，一般缓冲模式

5）decode 解码。

6）any session。  

	打靶，点击之后可以在屏幕上任选要监控的软件，例如浏览器、qq等，再次点击取消

7）find 
 
	    查找请求、响应中的相关信息，快速定位
	ctrl+f

8) save  
  
	  保存会话。点击之后会把所有会话，保存成文件，后缀saz，开发点击之后可以直接用fiddler打开

9）browse 快速打开某浏览器

10）clear cache 清除缓存。快速清除正在监听的浏览器缓存

11) textwizard 编码解码工具，例如md5加密，url编码解码

3.会话列表  

	1）session列，右键，可以选择隐藏、自定义等  
	2）#点击可以排序，按照抓包时间正序、倒叙排列  

4.命令行+状态栏  

	1）断点设置，设置完断点，配合go一起使用。点一次，请求前断点，点go，发出去；点两次，响应后断点，点go，响应收到；第三次点击，取消断点  
	2）capture 点掉之后不抓包了，取消了代理

5.statistics 性能分析
6.inspectors 检查器，以不同形式展示请求、响应报文  
1）raw是比较全面的显示请求、响应  
2）其他格式化分开显示

7.autoresponder 自动响应器  
拦截某请求，进行以下操作： 

1）重定向到本地的资源    
例如，请求后不需要到服务器端，而是以本地的资源来响应请求。例如响应的信息是本地一张图片，步骤如下：  

	1.保存一张图片  
	2.拖动并选中抓包的请求到右框，add rule-->讲要响应的图片地址，设置到”rule edit“  
	3.指定内置响应，例如404  
	也可以设置其他js文件等  

2）使用fiddler的内置响应  
3）自定义响应
拖动并选中抓包的请求到右框，右键选择”edit response“，弹出框raw自己设置响应体，save。重新发请求。

8.composer 设计器  
设计请求的报文，excute发送，步骤：  

	1）抓包到请求，拖动到composer  
	2）request body里面修改请求体的内容，excute

9.filter 过滤器  

	1)host   
	只展示广域网、只展示局域网  
	只展示的host、隐藏以下host  
	
	2)process 进程过滤  
	3)request head 过滤  
	只展示某些url、隐藏某些url  
	4）状态码过滤  
	5）其他  

 10.断点  
1）设置全局断点  
工具栏rule-->antomatic breakpoint-->设置请求前断点、响应后断点  

	1.选择抓包的session，设置请求前断点，点击发送，在inspector里可以修改要发送的数据，修改之后，点击go或者run to completion，发送  2.设置响应后断点，发送请求，在响应体--raw中可以修改响应信息，run to completion，发送  

断点也可以模仿测试”网络中断“的场景，设置断点使收不到响应  

2）局部断点  
命令行黑色框输入   
请求前：bpu +url路径名或者部分关键字，取消请求前断点：直接bpu命令  
响应后断点：bpuafter +url路径名或者部分关键字,取消断点：  bpafter命令  

11.弱网测试，模拟网络限速  
rule--performance--simulate modem speed ,勾选之后，请求网速会非常慢  
可以限定延迟多长时间：rule--customize rule  ,find ”simulate“，找到延迟模块simulate modem ，修改配置时间，修改之后要重启fiddler生效  


12.https抓包
点击tools--fiddler options--https，勾选decrypt https traffic（解密https流量）  
还不行，试试配置：点击tools--fiddler options--https，勾选decrypt https traffic，actions--reset all certificate，重置证书，先删除旧证书，一步步配置新证书  
看是否配置成功，actions--open windows 证书管理，操作--查找包含”fidler“  
配置好之后，重启fiddler，即可抓包https  

如果有的浏览器不能抓包https，要看这个浏览器是否配置了fiddler的证书，例如火狐，选项--高级--证书--查看证书，导入fiddler的证书；
怎样获取fiddler的证书？actions--export root certificate to desktop，导出根证书  


13.安卓设备  
手机和本机的网络要在同一个网络  

	fiddler设置：options--connection，勾选allow remote computer connect  
	查看fiddler本机的主机名：工具栏online可以看到  端口：工具栏options--connections  
	设置代理：设置--wlan--网络详情--代理--手动--主机名：   端口:
	如果还不能抓包，尝试以下步骤：  
	打开设备浏览器，访问http://ipv4:8888/  其中ip是主机名  
	点击底部fiddler root certificate下载证书  
	设置--更多设置--系统安全--加密与凭据--从存储设备安装  
	选择证书安装  

14.ios设备  
手机和本机的网络要在同一个网络  

	fiddler设置：options--connection，勾选allow remote computer connect  
	查看fiddler本机的主机名：工具栏online可以看到  端口：工具栏options--connections  
	设置代理：设置--wifi--打开wifi设置--配置代理--手动--服务器：   端口:  
	确保手机防火墙允许fiddler进程可以远程连接  
	ios设备连接wifi  
	确保ios设备可以访问到http://fiddlermachineip：8888，改地址会返回fiddler echo service页面，点击底部fiddler root   certificate下载证书  
	打开证书文件并安装，安装成功后，在通用--关于本机--证书信任设置，信任刚刚安装的证书  










