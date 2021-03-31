核心：  
1.testcase：测试用例，unittest.testcase类，所有的用例都是基于testcase类来继承  
2.test_fixtures：setup前置条件、testdown后置条件  
3：test_suite：测试套件，管理测试用例集  
4：test_runner：运行器  

编码规范：  
1.用例命名要以test开头，否则系统不会以为函数是一个测试用例，而觉得是一个被其他调用的函数  
2.要运行必须经过unittest——main（）函数  
3.测试套件和运行器，需要和unittest类分开 


	#导入unittest框架
	import unittest
	
	#定义一个继承于unittest类的类
	class demo(unittest.testcase):
	    #测试用例1
	    def test_1(self):
	           print("hello1")
	
	  #测试用例2
	    def test_1(self):
	           print("hello2")
	
	  #测试用例3
	    def test_1(self):
	           print("hello3")
	
	    #前置函数
	    def setup(self) -> none:
	           print("setup")
	 #后置函数
	     def teardown(self) -> none:
	          print("teardown")
	
	  #unittest运行函数
	if __name__=='__main__':
	  unittest.main()

执行结果：
setup
hello1
teardown

setup
hello2
teardown

setup
hello3
teardown

unittest有很多自带的断言
在函数里面调用asset，例如在函数里面self.assertEqual("su",self.driver.title,msg="不一样")
当su的值和self.driver.title值对比，不相等时报msg“不一样”


2.如何一条用例执行多个数据，不用for循环？   

	#ddt功能有很多  
	from ddt import ddt,date,unpack
	@date(('http://www.baidu.com','犬夜叉'),
	             ('http://www.baidu.com','滑头鬼'),
	             ('http://www.baidu.com','小玲')
	)    
	#unpack解析上面date里面元组的值，传到测试用例里面调用
	@unpack
	def test_1(self,url,text):
	    self.driver.get(url)
	    self.driver.find_element_by_id('kw').send(text)
	    self.driver.find_element_by_id('su').click

这样会依次获取数据，运行三次用例

3.通过文件的形式传数据，首先需要一个文件

	#定解析文件filename的数据，并保存到list里面
	def readfile():
	    params = []
	    file = open('filename','r',encoding = 'gbk')
	    for line in file.realines():
	         params.append(line.strip('\n').split(','))
	    return params
	
	#调用解析文件函数
	@data(*readfile)
	@unpack
	def test_2(self, url, text)
	    self.driver.get(url)
	    self.driver.find_element_by_id('kw').send(text)
	    self.driver.find_element_by_id('su').click

4.如何手动生成一个list，给测试用例调用
