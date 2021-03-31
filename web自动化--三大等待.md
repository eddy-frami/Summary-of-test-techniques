等待作用  
当请求网址没有返回数据时，直接执行命令会报错，为了确保执行的正确率、有效性，在特定的时间要设置等待，让机器可以更好地执行自动化测试代码命令。  

1.强制等待 time.sleep(5)   
加5的强制等待，无论情况如何，运行到sleep（）就会一直等待，让等多少就等多少  
需要导入库包from time import sleep

2.隐式等待. webdriver.implicity_wait(10)  
设置隐形的等待，传入参数time_to_wait,最大等待时间，如果在时间内加载完成，则进行下一步，否则等待到最大时间。是一个全局等待，放在代码最开始位，所有需要等待的步骤都执行这个等待时间，设置一次就行了。

缺点：必须等待页面全部加载完成，才进行下一步；全局等待，不能对指定的元素进行等待

3.显式等待。  
webdriverwait(driver01,最大等待时间11，刷新的频率0.5秒刷一次).until(lamda el:driver.find_element_by_id("kw"))  
每0.5秒去页面刷一次看是否可以结束等待，根据后面的元素是否存在。设置等待的条件，比较灵活。一次性的，节约测试时间。  
from selenium.webdriver.support.wait import webdriverwait


