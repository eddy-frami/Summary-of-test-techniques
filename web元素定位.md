元素本质：html标签  
基本格式：<标签名 属性1=  属性2= ></>  
标签类型：  
a   
input  
img  
button  
根据属性定位标签。  
属性value ，例如一个按钮“百度一下”是value值；text  

close/quit 区别  
close关闭当前标签页  
quit关闭浏览器、释放进程

1.id，根据id的值进行定位。类似于身份证号，不会重复
driver.find_element_by_id("kw")

2.name,类似于名字，可能重复。
driver.find_element_by_name("name值")

3.link text,主要用于超链接进行定位，<a href="链接地址">连衣裙</a>，
driver.find_element_by_link_text("连衣裙").click()

4.partial link text:link text的模糊查询版本，类似于数据库的like。
driver.find_element_by_partial_link_text("连衣").click()

匹配到多个符合条件的元素，则匹配第一个。
如何定位到某个元素？driver.find_elements_by_partial_link_text("连衣")[2].click(),定位到第3个元素。
element加s，elements，是获取到了一个list

5.classname，元素样式，非常容易重复.值有空格会报错。
find _element_by_class_name("").send_keys("hello")

6.tagname，标签名，重复度最高，只有在定位后，二次筛选时会用
7.cssselector

8.xpath，基于页面结构定位。标签的路径，一层层查找。步骤：右键检查--找到要定位的元素--右键选择copy--copy xpath
driver.find_element_by_xpath('元素xpath路径')
绝对路径：从根路径一层层往下找
相对路径：基于匹配制度，依照xpath语法结构来找。

例如：//*[@id="kw"]  //表示从根路径开始查找元素，*任意元素，[]表示查找函数，@表示基于属性查找。
//input[@name="jj"]  表示查找input标签
//a[text()='连衣裙'] 根据链接名字，根据属性要前加@，根据文本不用加@

确认xpath路径正确：
1.开发者工具，元素页面，ctrl+f输入路径确认
2.console输入￥x()校验

函数定位元素：
//input[contains(@id,'kw')],contains函数表示进一步查找，匹配模糊查找
//input[contains(test(),'连衣裙')],text不需要加@，匹配模糊查找







