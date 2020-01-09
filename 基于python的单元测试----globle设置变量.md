##### python定义全局变量，作用：在总文件中修改字段的值，使之生效，不需要每次都去各个用例中修改用例字段的值，集成在总文件中集中修改。

##### 1.新建一个全局文件globle，定义一个包含存数据、取数据函数的类



class globle1():

   merchlist={}  #在类里面，方法外面，生成一个空的字典。

   def init(self):

​        globle merchlist  #将定义的字典，用globle函数全局化



   def  set(self,merch,value):

​         self.merchlis['merch']=value   #set函数，填充并修改字典的值。传入一个值value，赋给merch这个字段



  def get(self,merch):

​       return self.merchlist['merch']   #get函数，取出字典里面某个字段的值



##### 2.定义好存值函数set和取值函数get，就可以在总测试用例里面，使用set函数定字典里面各个字段的值；在各个用例里面使用get函数取出来字段值，然后送去做接口测试



1).在总测试用例里面使用set函数，灵活定义字典里面字段的值

from globle import globle1  #总测试文件中，引入设置全局文件的类，以便使用类的对象

g1=globle1()  #定义一个对象

g1.set('merchid','000001')  #利用set函数，传入两个值，将000001赋给meichid这个字段



2).在各个接口用例中，使用get函数，取出在总用例集合中随机定义的字段值

from globle import globle1  #各个接口测试文件中，引入设置全局文件的类，以便使用类的对象

g2=globle1()   #定义一个对象

```
def addac0101(self):
   self.addata['body']['orderCode'] = g2.get('orderCode')
```









