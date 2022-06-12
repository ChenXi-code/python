## Python 简介

### python 是什么？
Python 是一种解释型、面向对象、动态数据类型的高级程序设计语言，它由 Guido van Rossum 在 1989 年发明。Python 官方宣布，2020 年 1 月 1 日， 停止 Python 2 的更新。Python 2.7 被确定为最后一个 Python 2.x 版本，目前建议 Python 用户使用3.X版本。

### Python 做什么？
Python 可以做的事情很多。
- Python 可以与软件一起使用来创建工作流。
- Python 可以连接到数据库系统。它还可以读取和修改文件。
- Python 可用于处理大数据并执行复杂的数学运算。
- Python 可用于快速原型设计，也可用于生产就绪的软件开发。

### 为何选择 Python？
Python 适用于不同的平台（Windows、Mac、Linux、Raspberry Pi 等）。
Python 有一种类似于英语的简单语法。
Python 的语法允许开发人员用比其他编程语言更少的代码行编写程序。
Python 在解释器系统上运行，这意味着代码可以在编写后立即执行。这也意味着原型设计可以非常快。
Python 可以以程序方式、面向对象的方式或功能方式来处理。

### Python 语法与其他编程语言比较
Python 是为可读性设计的，与英语有一些相似之处，并受到数学的影响。
Python 使用新行来完成命令，而不像通常使用分号或括号的其他编程语言。
Python 依赖缩进，使用空格来定义范围；例如循环、函数和类的范围。其他编程语言通常使用花括号来实现此目的。

### Python 特点
- 易于学习：Python有相对较少的关键字，结构简单，和一个明确定义的语法，学习起来更加简单。

- 易于阅读：Python代码定义的更清晰。

- 易于维护：Python的成功在于它的源代码是相当容易维护的。

- 一个广泛的标准库：Python的最大的优势之一是丰富的库，跨平台的，在UNIX，Windows和Macintosh兼容很好。

- 互动模式：互动模式的支持，您可以从终端输入执行代码并获得结果的语言，互动的测试和调试代码片断。

- 可移植：基于其开放源代码的特性，Python已经被移植（也就是使其工作）到许多平台。

- 可扩展：如果你需要一段运行很快的关键代码，或者是想要编写一些不愿开放的算法，你可以使用C或C++完成那部分程序，然后从你的Python程序中调用。

- 数据库：Python提供所有主要的商业数据库的接口。

- GUI编程：Python支持GUI可以创建和移植到许多系统调用。

- 可嵌入: 你可以将Python嵌入到C/C++程序，让你的程序的用户获得"脚本化"的能力。

## Python 环境搭建

### Python下载
Python最新源码，二进制文档，新闻资讯等可以在Python的官网查看到：

Python官网：https://www.python.org/

你可以在以下链接中下载 Python 的文档，你可以下载 HTML、PDF 和 PostScript 等格式的文档。

Python文档下载地址：https://www.python.org/doc/

### Python安装
Python已经被移植在许多平台上（经过改动使它能够工作在不同平台上）。

您需要下载适用于您使用平台的二进制代码，然后安装Python。

如果您平台的二进制代码是不可用的，你需要使用C编译器手动编译源代码。

编译的源代码，功能上有更多的选择性， 为python安装提供了更多的灵活性。

以下是各个平台安装包的下载地址：
![](https://user-images.githubusercontent.com/36021452/173181004-ac10d046-0b4f-4ca0-b102-46a931cee7b0.png#pic_center)

### 集成开发环境: PyCharm
PyCharm 是由 JetBrains 打造的一款 Python IDE，支持 macOS、 Windows、 Linux 系统。

PyCharm 功能 : 调试、语法高亮、Project管理、代码跳转、智能提示、自动完成、单元测试、版本控制……

PyCharm 下载地址 : https://www.jetbrains.com/pycharm/download/

PyCharm 安装地址：http://www.runoob.com/w3cnote/pycharm-windows-install.html

### pip 使用方法

说到 pip ，大家都不会陌生。但我相信不少人，只是熟悉几个常用的用法，而对于其他几个低频且实用的用法，却知之甚少，这两天，我把这些用法整理了一下，应该是网络上比较全的介绍

#### 查询软件包

查询当前环境安装的所有软件包

```bash
$ pip list
```

查询 pypi 上含有某名字的包

```bash
$ pip search pkg
```

查询当前环境中可升级的包

```bash
$ pip list --outdated
```

查询一个包的详细内容

```bash
$ pip show pkg
```

#### 下载软件包

在不安装软件包的情况下下载软件包到本地

```bash
$ pip download --destination-directory /local/wheels -r requirements.txt
```

下载完，总归是要安装的，可以指定这个目录中安装软件包，而不从 pypi 上安装。

```bash
$ pip install --no-index --find-links=/local/wheels -r requirements.txt
```

当然你也从你下载的包中，自己构建生成 wheel 文件

```bash
$ pip install wheel
$ pip wheel --wheel-dir=/local/wheels -r requirements.txt
```

#### 安装软件包

使用 `pip install <pkg>` 可以很方便地从 pypi 上搜索下载并安装 python 包。

如下所示

```bash
$ pip install requests
```

这是安装包的基本格式，我们也可以为其添加更多参数来实现不同的效果。

**1 只从本地安装，而不从 pypi 安装**

```bash
# 前提你得保证你已经下载 pkg 包到 /local/wheels 目录下
$ pip install --no-index --find-links=/local/wheels pkg
```

**2 限定版本进行软件包安装**

以下三种，对单个 python 包的版本进行了约束

```bash
# 所安装的包的版本为 2.1.2
$ pip install pkg==2.1.2

# 所安装的包必须大于等于 2.1.2
$ pip install pkg>=2.1.2

# 所安装的包必须小于等于 2.1.2
$ pip install pkg<=2.1.2
```

以下命令用于管理/控制整个 python 环境的包版本

```bash
# 导出依赖包列表
pip freeze >requirements.txt

# 从依赖包列表中安装
pip install -r requirements.txt

# 确保当前环境软件包的版本(并不确保安装)
pip install -c constraints.txt
```

**3 限制不使用二进制包安装**

由于默认情况下，wheel 包的平台是运行 pip download 命令 的平台，所以可能出现平台不适配的情况。

比如在 MacOS 系统下得到的 pymongo-2.8-cp27-none-macosx\_10\_10\_intel.whl 就不能在 linux\_x86\_64 安装。

使用下面这条命令下载的是 tar.gz 的包，可以直接使用 pip install 安装。

比 wheel 包，这种包在安装时会进行编译，所以花费的时间会长一些。

```bash
# 下载非二进制的包
$ pip download --no-binary=:all: pkg

#　安装非二进制的包
$ pip install pkg --no-binary
```

**4 指定代理服务器安装**

当你身处在一个内网环境中时，无法直接连接公网。这时候你使用`pip install` 安装包，就会失败。

面对这种情况，可以有两种方法：

1.  下载离线包拷贝到内网机器中安装
    
2.  使用代理服务器转发请求
    

第一种方法，虽说可行，但有相当多的弊端

*   步骤繁杂，耗时耗力
    
*   无法处理包的依赖问题
    

这里重点来介绍，第二种方法：

```bash
$ pip install --proxy [user:passwd@]http_server_ip:port pkg
```

每次安装包就发输入长长的参数，未免有些麻烦，为此你可以将其写入配置文件中：`$HOME/.config/pip/pip.conf`

对于这个路径，说明几点

*   不同的操作系统，路径各不相同
    

```bash
# Linux/Unix:
/etc/pip.conf
~/.pip/pip.conf
~/.config/pip/pip.conf

# Mac OSX:
~/Library/Application Support/pip/pip.conf
~/.pip/pip.conf
/Library/Application Support/pip/pip.conf

# Windows:
%APPDATA%\pip\pip.ini
%HOME%\pip\pip.ini
C:\Documents and Settings\All Users\Application Data\PyPA\pip\pip.conf (Windows XP)
C:\ProgramData\PyPA\pip\pip.conf (Windows 7及以后) 
```

* 若在你的机子上没有此文件，则自行创建即可
    

如何配置，这边给个样例：

```bash
[global]
index-url = http://mirrors.aliyun.com/pypi/simple/ 

# 替换出自己的代理地址，格式为[user:passwd@]proxy.server:port
proxy=http://xxx.xxx.xxx.xxx:8080 

[install]
# 信任阿里云的镜像源，否则会有警告
trusted-host=mirrors.aliyun.com 
```

**5 安装用户私有软件包**

很多人可能还不清楚，python 的安装包是可以用户隔离的。

如果你拥有管理员权限，你可以将包安装在全局环境中。在全局环境中的这个包可被该机器上的所有拥有管理员权限的用户使用。

如果一台机器上的使用者不只一样，自私地将在全局环境中安装或者升级某个包，是不负责任且危险的做法。

面对这种情况，我们就想能否安装单独为我所用的包呢？

庆幸的是，还真有。

我能想到的有两种方法：

1.使用虚拟环境
    
2.将包安装在用户的环境中
    

虚拟环境，之前写过几篇文章，这里不再展开讲。

今天的重点是第二种方法，教你如何安装用户私有的包？

命令也很简单，只要加上 `--user` 参数，pip 就会将其安装在当前用户的 `~/.local/lib/python3.x/site-packages` 下，而其他用户的 python 则不会受影响。

```bash
pip install --user pkg
```

来举个例子

```bash
# 在全局环境中未安装 requests
[root@localhost ~]# pip list | grep requests   
[root@localhost ~]# su - wangbm
[root@localhost ~]# 

# 由于用户环境继承自全局环境，这里也未安装
[wangbm@localhost ~]# pip list | grep requests 
[wangbm@localhost ~]# pip install --user requests  
[wangbm@localhost ~]# pip list | grep requests 
requests (2.22.0)
[wangbm@localhost ~]# 

# 从 Location 属性可发现 requests 只安装在当前用户环境中
[wangbm@ws_compute01 ~]$ pip show requests
---
Metadata-Version: 2.1
Name: requests
Version: 2.22.0
Summary: Python HTTP for Humans.
Home-page: http://python-requests.org
Author: Kenneth Reitz
Author-email: me@kennethreitz.org
Installer: pip
License: Apache 2.0
Location: /home/wangbm/.local/lib/python2.7/site-packages
[wangbm@localhost ~]$ exit
logout

# 退出 wangbm 用户，在 root 用户环境中发现 requests 未安装
[root@localhost ~]$ pip list | grep requests
[root@localhost ~]$ 
```

当你身处个人用户环境中，python 导包时会先检索当前用户环境中是否已安装这个包，已安装则优先使用，未安装则使用全局环境中的包。

验证如下：

```bash
>>> import sys
>>> from pprint import pprint 
>>> pprint(sys.path)
['',
 '/usr/lib64/python27.zip',
 '/usr/lib64/python2.7',
 '/usr/lib64/python2.7/plat-linux2',
 '/usr/lib64/python2.7/lib-tk',
 '/usr/lib64/python2.7/lib-old',
 '/usr/lib64/python2.7/lib-dynload',
 '/home/wangbm/.local/lib/python2.7/site-packages',
 '/usr/lib64/python2.7/site-packages',
 '/usr/lib64/python2.7/site-packages/gtk-2.0',
 '/usr/lib/python2.7/site-packages',
 '/usr/lib/python2.7/site-packages/pip-18.1-py2.7.egg',
 '/usr/lib/python2.7/site-packages/lockfile-0.12.2-py2.7.egg']
>>> 
```

**6 延长超时时间**

若网络情况不是很好，在安装某些包时经常会因为 ReadTimeout 而失败。

对于这种情况，一般重试几次就好了。

但是这样难免有些麻烦，有没有更好的解决方法呢？

有的，可以通过延长超时时间。

```bash
$ pip install --default-timeout=100 <packages>
```

4.卸载软件包

就一条命令，不再赘述

```bash
$ pip uninstall pkg
```

#### 升级软件包
---------

想要对现有的 python 进行升级，其本质上也是先从 pypi 上下载最新版本的包，再对其进行安装。所以升级也是使用 `pip install`，只不过要加一个参数 `--upgrade`。

```bash
$ pip install --upgrade pkg
```

在升级的时候，其实还有一个不怎么用到的选项 `--upgrade-strategy`，它是用来指定升级策略。

它的可选项只有两个：

*   `eager` ：升级全部依赖包
    
*   `only-if-need`：只有当旧版本不能适配新的父依赖包时，才会升级。
    

在 pip 10.0 版本之后，这个选项的默认值是 `only-if-need`，因此如下两种写法是一互致的。

```bash
pip install --upgrade pkg1 
pip install --upgrade pkg1 --upgrade-strategy only-if-need
```

#### 配置文件

由于在使用 pip 安装一些包时，默认会使用 pip 的官方源，所以经常会报网络超时失败。

常用的解决办法是，在安装包时，使用 `-i` 参数指定一个国内的镜像源。但是每次指定就很麻烦呀，还要打超长的一串字母。

这时候，其实可以将这个源写进 pip 的配置文件里。以后安装的时候，就默认从你配置的这个 源里安装了。

那怎么配置呢？文件文件在哪？

使用`win+r` 输入 `%APPDATA%` 进入用户资料文件夹，查看有没有一个 pip 的文件夹，若没有则创建之。

然后进入这个 文件夹，新建一个 `pip.ini` 的文件，内容如下

```bash
[global]
time-out=60
index-url=https://pypi.tuna.tsinghua.edu.cn/simple/
[install]
trusted-host=tsinghua.edu.cn
```
以上几乎包含了 pip 的所有使用场景，也许有不少用法你还没有用过，不过没关系，你只要收藏本文，等到要用的时候再来查阅即可。


## Python 基础语法
默认情况下，Python 3 源码文件以 UTF-8 编码，所有字符串都是 unicode 字符串。 当然你也可以为源码文件指定不同的编码：
### 标识符
- 第一个字符必须是字母表中字母或下划线 _ 。
- 标识符的其他的部分由字母、数字和下划线组成。
- 标识符对大小写敏感。
在 Python 3 中，可以用中文作为变量名，非 ASCII 标识符也是允许的了。
### python保留字
保留字即关键字，我们不能把它们用作任何标识符名称。Python 的标准库提供了一个 keyword 模块，可以输出当前版本的所有关键字：

```bash
>>> import keyword
>>> keyword.kwlist
['False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```
### 注释
Python中单行注释以 # 开头，实例如下：
```python
#!/usr/bin/python3
 
# 第一个注释
print ("Hello, Python!") # 第二个注释
```
多行注释可以用多个 # 号，还有 ''' 和 """：
```python
#!/usr/bin/python3
 
# 第一个注释
# 第二个注释
 
'''
第三注释
第四注释
'''
 
"""
第五注释
第六注释
"""
print ("Hello, Python!")
```
### 数字(Number)类型
python中数字有四种类型：整数、布尔型、浮点数和复数。
- int (整数), 如 1, 只有一种整数类型 int，表示为长整型，没有 python2 中的 Long。
- bool (布尔), 如 True。
- float (浮点数), 如 1.23、3E-2
- complex (复数), 如 1 + 2j、 1.1 + 2.2j

### 字符串(String)
- Python 中单引号 ' 和双引号 " 使用完全相同。
- 使用三引号(''' 或 """)可以指定一个多行字符串。
- 转义符 \。
- 反斜杠可以用来转义，使用 r 可以让反斜杠不发生转义。 如 r"this is a line with \n" 则 \n 会显示，并不是换行。
- 按字面意义级联字符串，如 "this " "is " "string" 会被自动转换为 this is string。
- 字符串可以用 + 运算符连接在一起，用 * 运算符重复。
- Python 中的字符串有两种索引方式，从左往右以 0 开始，从右往左以 -1 开始。
- Python 中的字符串不能改变。
- Python 没有单独的字符类型，一个字符就是长度为 1 的字符串。
- 字符串的截取的语法格式如下：变量[头下标:尾下标:步长]

```python
word = '字符串'
sentence = "这是一个句子。"
paragraph = """这是一个段落，
可以由多行组成"""
```
实例
```python
#!/usr/bin/python3
str='123456789'
print(str)                 # 输出字符串
print(str[0:-1])           # 输出第一个到倒数第二个的所有字符
print(str[0])              # 输出字符串第一个字符
print(str[2:5])            # 输出从第三个开始到第五个的字符
print(str[2:])             # 输出从第三个开始后的所有字符
print(str[1:5:2])          # 输出从第二个开始到第五个且每隔一个的字符（步长为2）
print(str * 2)             # 输出字符串两次
print(str + '你好')         # 连接字符串
print('------------------------------')
print('hello\nrunoob')      # 使用反斜杠(\)+n转义特殊字符
print(r'hello\nrunoob')     # 在字符串前面添加一个 r，表示原始字符串，不会发生转义
```

### import 与 from...import
在 python 用 import 或者 from...import 来导入相应的模块。

- 将整个模块(somemodule)导入，格式为： import somemodule
- 从某个模块中导入某个函数,格式为： from somemodule import somefunction
- 从某个模块中导入多个函数,格式为： from somemodule import firstfunc, secondfunc, thirdfunc
- 将某个模块中的全部函数导入，格式为： from somemodule import *

### 命令行参数
很多程序可以执行一些操作来查看一些基本信息，Python可以使用-h参数查看各参数帮助信息：
```python
$ python -h
usage: python [option] ... [-c cmd | -m mod | file | -] [arg] ...
Options and arguments (and corresponding environment variables):
-c cmd : program passed in as string (terminates option list)
-d     : debug output from parser (also PYTHONDEBUG=x)
-E     : ignore environment variables (such as PYTHONPATH)
-h     : print this help message and exit
```

## Python3 基本数据类型
Python 中的变量不需要声明。每个变量在使用前都必须赋值，变量赋值以后该变量才会被创建。

在 Python 中，变量就是变量，它没有类型，我们所说的"类型"是变量所指的内存中对象的类型。等号（=）用来给变量赋值。等号（=）运算符左边是一个变量名,等号（=）运算符右边是存储在变量中的值。例如：
```python
#!/usr/bin/python3

counter = 100          # 整型变量
miles   = 1000.0       # 浮点型变量
name    = "runoob"     # 字符串

print (counter)
print (miles)
print (name)
```
执行以上程序会输出如下结果：
```python
100
1000.0
runoob
```
### 多个变量赋值
Python允许你同时为多个变量赋值。例如：
```python
a = b = c = 1
```
您也可以为多个对象指定多个变量。例如：
```python
a, b, c = 1, 2, "runoob"
```
### 标准数据类型
Python3 中有六个标准的数据类型：

- Number（数字）
- String（字符串）
- List（列表）
- Tuple（元组）
- Set（集合）
- Dictionary（字典）

Python3 的六个标准数据类型中：
不可变数据（3 个）：Number（数字）、String（字符串）、Tuple（元组）；
可变数据（3 个）：List（列表）、Dictionary（字典）、Set（集合）。

#### Number（数字）
Python3 支持 int、float、bool、complex（复数）。

在Python 3里，只有一种整数类型 int，表示为长整型，没有 python2 中的 Long。

像大多数语言一样，数值类型的赋值和计算都是很直观的。

内置的 type() 函数可以用来查询变量所指的对象类型。
```python
>>> a, b, c, d = 20, 5.5, True, 4+3j
>>> print(type(a), type(b), type(c), type(d))
<class 'int'> <class 'float'> <class 'bool'> <class 'complex'>
```
#### String（字符串）
Python中的字符串用单引号 ' 或双引号 " 括起来，同时使用反斜杠 \ 转义特殊字符。

字符串的截取的语法格式如下：
> 变量[头下标:尾下标]
索引值以 0 为开始值，-1 为从末尾的开始位置。

![](https://wx3.sinaimg.cn/mw690/008cwYRrgy1h35713cqg6j30f105l0sw.jpg#pic_center)

实例如下：
```python
#!/usr/bin/python3
str = 'Runoob'
print (str)          # 输出字符串
print (str[0:-1])    # 输出第一个到倒数第二个的所有字符
print (str[0])       # 输出字符串第一个字符
print (str[2:5])     # 输出从第三个开始到第五个的字符
print (str[2:])      # 输出从第三个开始的后的所有字符
print (str * 2)      # 输出字符串两次，也可以写成 print (2 * str)
print (str + "TEST") # 连接字符串
```
![](https://i0.hdslb.com/bfs/article/bfba9969f54e103468ce761cc71d65f6c00ea7d0.jpg@878w_progressive.webp#pic_center)

![](https://img-blog.csdnimg.cn/20210716081201655.png#pic_center)















