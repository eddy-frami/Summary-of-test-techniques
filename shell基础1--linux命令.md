
1.Linux学习规范  

	例如创建文件、创建文件夹、保存文件、安装程序、运行程序。  
	命令、参数有几千个，不需要强制记忆。现学现查  
	文件都是区分大小写的，加上-i 表示不区分大小写  


2.创建、移动、删除文件/文件夹  

	  创建文件  touch a.txt
	  创建隐藏文件  touch .a1.txt  
	  创建文件夹 mkdir filename 
	  例如创建一个文件为“learnlinux”  mkdir learnlinux
	  删除文件 rm(remove)  rm a.txt
	  删除文件夹 rm -d filename  d表示directory文件；或者rm -r filename
  
  
3.查看当前位置  
  pwd  
4.ll   

	   ls(list)
	   ll  等于 ls -l   显示所有未隐藏文件的详细信息
	   ls -a  显示所有文件，包括隐藏文件
	   ls -a -l 显示所有文件的详细信息，又等于ls -al
	   ls filename  显示文件夹下面的所有文件
   
   
5.cd learnlinux 


    cd .. 回到上层
    cd ~ 回到根目录,直接cd 也是回到根目录
    混合使用：例如目前有目录   a/a1/a2/a3/a4, a/a1/a2/b1/b2  当前在a3下面，要去b1:  cd ../b1  
    自动补全快捷键tab键： cd le（匹配字）+tab键
    一个点表示当前路径，例如当前在a2，去a4，cd ./a3/a4
    相对路径与绝对路径。例如当前在a2，去a4，相对路径为cd a3/a4;绝对路径为cd /a/a1/a2/a3/a4,以斜杠开头。
    中杠，cd - ,表示和上个目录来回切换，反复横跳

6.关于隐藏文件  
  有些以点开头的文件，平时不会显示、编辑，因为大部分是软件下载、安装、运行的配置文件。

7.通配符  

	星号*  cd *.txt    *代表0个或者多个任意字符，可加在任意位置
	问号？ 代表一个任意字符   
	中括号[]  代表取中括号中的任一字符  [1234][abcd][1234].txt;
	                [1-4].txt  一到四中的一个
	                [a-z][1-9]bc.txt
	                [abju]bc.txt

8.移动文件  

	剪切 mv a.text  /a/a1/a2
	移动同时可改名  mv a.text ./aa.text
	复制文件 cp a.text /a/a1/a2/a3
	复制文件夹 cp -r /a/a1/a2/a3 -   杠表示复制到当前目录
	复制同时可改名  cp a.text ./aa.text  或者 cp a.text aa.text  

9.which查看命令所在位置  

    每个命令执行的时候，都会执行一个程序，包括当执行命令时要做那些事情、步骤
    which mv: 执行结果：/bin/mv  表示在执行bin目录下mv，bin下都是二进制文件，执行mv，命令所在位置在bin目录下
     了解：  
    /bin 二进制文件，普通命令
    /sbin 系统二进制文件，需要有系统权限
    /user/bin 用户安装的应用程序
    /user/sbin 超管安装的应用程序

10.find 文件搜索，范围、条件  

	   ➜  ~ find /Users/suyun/learnlinux -name text01.txt  find+地址 + -name表示找的是文件名 +文件名
	   ➜  ~ find / -name text01.txt   /表示在根目录中搜索
	  使用通配符模糊搜索，需要加上引号
	  ➜  ~ find /Users/suyun/learnlinux -name '*01.txt'
	  文件都是区分大小写的，加上-i 表示不区分大小写，在这里和-name一起使用，固定为-iname

11.按照文件大小搜索  

	➜  ~ find /Users/suyun/learnlinux -size -1  
	结果：/Users/suyun/learnlinux/text01.txt 
	“+1”代表查找大小大于一个数据块的文件。一个数据块=0.5k
	“-1”代表查找小于一个数据块的文件。也可以“+2”、“+9”等

12.按照所属人 -user +用户  

	➜  find /Users/suyun/learnlinux -user suyun
	结果：/Users/suyun/learnlinux/text01.txt 

13.按照文件更改时间  

	➜  find /Users/suyun/learnlinux -mmin -5
	-5更改时间小于5分钟，+6大于6分钟

14.按照文件类型、id、搜索条件链接  

	➜   find /Users/suyun/learnlinux -type f/d/l
	f文件，d文件夹，l链接

15.变量  

1）read 交互式定义变量

	目的：用户自己给变量赋值
	语法：read 选项 变量名
	常见选项：
	-p 定义提示用户的信息
	-n 字符数，限制变量的长度
	-s 不显示用户输入的内容
	-t 定义变量的超时时间

例子1 ：用户自己定义变量值  

	sh-3.2$ read -p "your name:" name
	your name:baba
	sh-3.2$ echo $name
	baba
	例子2：变量值来自文件
	sh-3.2$ vim text02.txt  ----文件中有值：mama
	sh-3.2$ read -p "我的名字:" myname < text02.txt  ----变量myname的值来自于text02.txt文件
	sh-3.2$ echo $myname
	mama

2）declear 定义有类型的变量  

	目的：给变量做一些限制，例如整形、只读
	语法：declear 选项 变量名=变量值
	常见选项：
	-i 整数  declear -i A=123
	-r只读 declear -r B=hello
	-x 环境变量  declear -x AA=heima

变量名规则：  

	1.区分大小写
	2.特殊字符
	3.不能以数字开头
	4.等号两边不能有空格
	5.见名知意
	6.变量值有空格，用引号  A=“hello world”
	7.调用变量 echo $A 或 echo ${A:2:3}
	8.双引号、单引号区别 双引号可以引用变量，单引号不可以

16：取消变量   
  unset 变量名  

17.编辑脚本：  

	vim 脚本文件名
	-i 编辑状态
	按esc键退出编辑
	:wq 保存并退出
	执行脚本：sh 脚本名字  或者 1.给脚本赋权限 chmod -x 脚本名字   2.脚本路径，例如./a1/text.txt


18.变量类型  

	1）本地变量，只在当前进程有效，例如A=111，只在当前窗口有效
	2）环境变量，当前进程有效，并且能被子进程调用
	    env 查看所有环境变量
	    set 查看环境变量、本地变量
	       例如：
	             sh-3.2$ set|grep name
	             myname=mama
	             name=baba
   本地变量如何更改为环境变量：  
   
    1）定义本地变量   BB=hello
    2）export BB
   或者直接 export DD=nihao

19.四则运算  

整数运算： 

	1）$(())   echo $((1+2));echo $((10-4))
	2) $[]     echo $[10*2];echo $[10/8] 商结果为1；取余数% echo $[10%8],结果为2
	3) expr  加减符号与数字之间要有空格，乘法*之前要有转义字符\,即\*
	加：sh-3.2$ expr 10 + 1 结果：11
	减：sh-3.2$ expr 10 - 1 结果：9
	乘：sh-3.2$ expr 2 \* 10 结果：20
	除：sh-3.2$ expr 10 / 6 结果：1
	
	4) n=1;let n+=1 等价于 let n=n+1;同理 n-=3;n*=2;n/=3; 
	    求n的3次方：let n=n**3
	   
	bc支持小数运算：
	5）echo $[1+1.5]报错，可以echo 1+1.5|bc
	  或者直接bc命令，进入后随意加减，退出用quit命令;在bc模式下，取次方不能用**，例如直接2的3次方，2**3会报错，要2^3,结果为8

20.i++  和++i  

	i=1;j=1;
	let x=i++；（先赋值再运算）let y=++j;(先运算再赋值)
	echo $x,$y
	1,2


 

   

    





 

   


   


  

    
    