##### 一.使用python第三方库unittest，来做自动化测试

单元测试最集中的四个概念：test case（测试用例）、test suite（测试套件）、test runner（执行测试套件里面的测试用例）、test fixture（测试环境数据准备和数据清理或者测试脚手架）

1).test case：一个测试文件中，定义的测试函数，可以作为一个用例

2).test suite：多个测试用例，集成在一个套件里面

3).test runner：运行 集成好的测试用例，做到多个用例自动化测试

4).test fixture：测试用例环境的搭建和销毁

######  1.首先，需要生成一个集合，作用是把需要执行的用例、文件都放进这个集合里面

1).创建用例。创建一个测试类，继承unittest.TestCase

在文件a中创建类a1，在类a1中定义函数a01.

class a1(unittest.TestCase):

  def a01()

在文件b中创建类b1，在b1中定义函数b01.

class b1(unittest.TestCase):

  def b01()

2).在文件中导入第三方库unittest;导入其他文件的用例

import  unittest

import  a from a1

import  b from b1

3).使用unittest的TestSuite在要执行的总测试文件中，定义的类里面，生成一个集合（测试套件），集合名字自定义

suite= unittest.TestSuite()

4).用TestSuite的addTest将用例都集成在主文件的集合中

suite.addTest(a1('a01'))  #a1为文件a中定义的一个类，a01为类中的方法函数，作为用例被集成在suite中。

suite.addTest(b1('b01'))  #同a1

##### 2.使用unittest的TextTestRunner，执行suite里面的用例。这样就可以自动执行一组用例集合

unittest.TestTestRunner().run(suite)



































