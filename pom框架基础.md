自动化测试体系中，框架设计包含两类：  

1. 关键字驱动  
2. pom  

pageObject model，基于系统页面实现的架构设计。
传统的功能测试，只关注功能是否正确。输入账号，点击登录，进入首页。
pom是基于不同的页面来实现的。
所有的测试都会关注覆盖率，在自动化领域，一般测试执行覆盖率50%就是不错的自动化测试。pom的覆盖率在70%以上，是对单个系统覆盖率上最好的设计模式。
				
如何实现pom的测试框架设计：  

一：结构设计  
代码与数据分离  
逻辑代码与测试代码分离  

1.基类：底层逻辑类。主要实现常用的自动化测试操作。供页面对象调用  
2.页面对象：pom的核心代码，将自动化测试操作流程中关联的页面，全部提取，一个页面就是一个页面对象
          1）页面基本信息。元素、url等固定内容
          2）业务流程。各个流程的操作行为  
3.测试用例。所有的操作行为，都在用例中体现，测试代码  
4.测试数据。用例中关联的数据



二：源码实现  
1.首先创建4个包：基类base、页面对象page_object、测试用例case、数据data  
2.对基类：  
        创建一个py文件base_page.py  
        
        from selenium import webdriver

        class basePage:    
              driver = webdriver.chrome()

              #构造函数，调用类操作
               def __init__(self,driver):
                     self.driver = driver

               #访问url
               def open(self):
                     self.driver.get(self.url)

               #元素定位
               def locator(self, loc):
                      return self.driver.find_element(*loc)

               #输入
               def input(self, loc, text):
                     self.locator(loc).send_keys(text)

               #点击
               def click(self, loc):
                      self.locator(loc).click()

               #等待
              def wait(self, time_):
                    sleep(time_)


3.页面对象：  
每个页面就是一个页面对象  
1）创建一个登陆页面login_page.py  
要用到base_page里面的类及方法，用继承,常用的操作行为就都继承了

	  from base.base_page import basePage
	
	  class loginPage(basePage):
	
	    #url 页面对象，url标志是哪个页面
	     url= "http://www."
	
	    #元素
	    username = (By.NAME, 'user')
	    password = (By.NAME, 'pwd')
	    button = (By.XPATH, '/html/body/divjjkk')
	
	    #操作流程
	    def login(self, user, pwd):
	
	       #访问登陆页
	            self.open()
	
	       #输入账号
	            self.input(self.username, user)
	
	       #输入密码
	            self.input(self.password, pwd)
	
	       #点击登录按钮
	           self.click(self.button)
	
	if __name__ = '__main__'
	driver = webdriver.chrome()
	user = ‘user_1770001’
	pwd = '123456'
	lp = loginPage(driver)
	lp.login(user, pwd)


3.测试用例
在case包下，创建case_damo.py文件   

	import unittest
	class caseDemo(unnittest.testcase):
	    #前置对象
	
	    #用例1
	    def test_01_login(self):
	         driver = webdriver.chrome()
	         user = ‘user_1770001’
	         pwd = '123456'
	         lp = loginPage(driver)
	         lp.login(user, pwd)
	         lp.wait(5)
	 
	  if __name__ ==‘__main__’
	       unittest.main()
