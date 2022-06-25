## Python SMTP发送邮件

SMTP（Simple Mail Transfer Protocol）即简单邮件传输协议,它是一组用于由源地址到目的地址传送邮件的规则，由它来控制信件的中转方式。

python的smtplib提供了一种很方便的途径发送电子邮件。它对smtp协议进行了简单的封装。

## Python3 多线程
多线程类似于同时执行多个不同程序，多线程运行有如下优点：
- 使用线程可以把占据长时间的程序中的任务放到后台去处理。
- 用户界面可以更加吸引人，比如用户点击了一个按钮去触发某些事件的处理，可以弹出一个进度条来显示处理的进度。
- 程序的运行速度可能加快。
- 在一些等待的任务实现上如用户输入、文件读写和网络收发数据等，线程就比较有用了。在这种情况下我们可以释放一些珍贵的资源如内存占用等等。

### 开始学习Python线程
Python中使用线程有两种方式：函数或者用类来包装线程对象。

函数式：调用 _thread 模块中的start_new_thread()函数来产生新线程。语法如下:
> _thread.start_new_thread ( function, args[, kwargs] )
参数说明:
- function - 线程函数。
- args - 传递给线程函数的参数,他必须是个tuple类型。
- kwargs - 可选参数。

```python
#!/usr/bin/python3

import _thread
import time

# 为线程定义一个函数
def print_time( threadName, delay):
   count = 0
   while count < 5:
      time.sleep(delay)
      count += 1
      print ("%s: %s" % ( threadName, time.ctime(time.time()) ))

# 创建两个线程
try:
   _thread.start_new_thread( print_time, ("Thread-1", 2, ) )
   _thread.start_new_thread( print_time, ("Thread-2", 4, ) )
except:
   print ("Error: 无法启动线程")

while 1:
   pass
```
执行以上程序输出结果如下：
```
Thread-1: Wed Jan  5 17:38:08 2022
Thread-2: Wed Jan  5 17:38:10 2022
Thread-1: Wed Jan  5 17:38:10 2022
Thread-1: Wed Jan  5 17:38:12 2022
Thread-2: Wed Jan  5 17:38:14 2022
Thread-1: Wed Jan  5 17:38:14 2022
Thread-1: Wed Jan  5 17:38:16 2022
Thread-2: Wed Jan  5 17:38:18 2022
Thread-2: Wed Jan  5 17:38:22 2022
Thread-2: Wed Jan  5 17:38:26 2022
```

### 线程模块
Python3 通过两个标准库 _thread 和 threading 提供对线程的支持。

_thread 提供了低级别的、原始的线程以及一个简单的锁，它相比于 threading 模块的功能还是比较有限的。

threading 模块除了包含 _thread 模块中的所有方法外，还提供的其他方法：

- threading.currentThread(): 返回当前的线程变量。
- threading.enumerate(): 返回一个包含正在运行的线程的list。正在运行指线程启动后、结束前，不包括启动前和终止后的线程。
- threading.activeCount(): 返回正在运行的线程数量，与len(threading.enumerate())有相同的结果。
除了使用方法外，线程模块同样提供了Thread类来处理线程，Thread类提供了以下方法:
- run(): 用以表示线程活动的方法。
- start():启动线程活动。
- join([time]): 等待至线程中止。这阻塞调用线程直至线程的join() 方法被调用中止-正常退出或者抛出未处理的异常-或者是可选的超时发生。
- isAlive(): 返回线程是否活动的。
- getName(): 返回线程名。
- setName(): 设置线程名。

### 使用 threading 模块创建线程
我们可以通过直接从 threading.Thread 继承创建一个新的子类，并实例化后调用 start() 方法启动新线程，即它调用了线程的 run() 方法：

```python
#!/usr/bin/python3

import threading
import time

exitFlag = 0

class myThread (threading.Thread):
    def __init__(self, threadID, name, delay):
        threading.Thread.__init__(self)
        self.threadID = threadID
        self.name = name
        self.delay = delay
    def run(self):
        print ("开始线程：" + self.name)
        print_time(self.name, self.delay, 5)
        print ("退出线程：" + self.name)

def print_time(threadName, delay, counter):
    while counter:
        if exitFlag:
            threadName.exit()
        time.sleep(delay)
        print ("%s: %s" % (threadName, time.ctime(time.time())))
        counter -= 1

# 创建新线程
thread1 = myThread(1, "Thread-1", 1)
thread2 = myThread(2, "Thread-2", 2)

# 开启新线程
thread1.start()
thread2.start()
thread1.join()
thread2.join()
print ("退出主线程")
```
以上程序执行结果如下；
```
开始线程：Thread-1
开始线程：Thread-2
Thread-1: Wed Jan  5 17:34:54 2022
Thread-2: Wed Jan  5 17:34:55 2022
Thread-1: Wed Jan  5 17:34:55 2022
Thread-1: Wed Jan  5 17:34:56 2022
Thread-2: Wed Jan  5 17:34:57 2022
Thread-1: Wed Jan  5 17:34:57 2022
Thread-1: Wed Jan  5 17:34:58 2022
退出线程：Thread-1
Thread-2: Wed Jan  5 17:34:59 2022
Thread-2: Wed Jan  5 17:35:01 2022
Thread-2: Wed Jan  5 17:35:03 2022
退出线程：Thread-2
退出主线程
```

### 线程同步
如果多个线程共同对某个数据修改，则可能出现不可预料的结果，为了保证数据的正确性，需要对多个线程进行同步。

使用 Thread 对象的 Lock 和 Rlock 可以实现简单的线程同步，这两个对象都有 acquire 方法和 release 方法，对于那些需要每次只允许一个线程操作的数据，可以将其操作放到 acquire 和 release 方法之间。如下：

多线程的优势在于可以同时运行多个任务（至少感觉起来是这样）。但是当线程需要共享数据时，可能存在数据不同步的问题。

考虑这样一种情况：一个列表里所有元素都是0，线程"set"从后向前把所有元素改成1，而线程"print"负责从前往后读取列表并打印。

那么，可能线程"set"开始改的时候，线程"print"便来打印列表了，输出就成了一半0一半1，这就是数据的不同步。为了避免这种情况，引入了锁的概念。

锁有两种状态——锁定和未锁定。每当一个线程比如"set"要访问共享数据时，必须先获得锁定；如果已经有别的线程比如"print"获得锁定了，那么就让线程"set"暂停，也就是同步阻塞；等到线程"print"访问完毕，释放锁以后，再让线程"set"继续。

经过这样的处理，打印列表时要么全部输出0，要么全部输出1，不会再出现一半0一半1的尴尬场面。
```python
#!/usr/bin/python3

import threading
import time

class myThread (threading.Thread):
    def __init__(self, threadID, name, delay):
        threading.Thread.__init__(self)
        self.threadID = threadID
        self.name = name
        self.delay = delay
    def run(self):
        print ("开启线程： " + self.name)
        # 获取锁，用于线程同步
        threadLock.acquire()
        print_time(self.name, self.delay, 3)
        # 释放锁，开启下一个线程
        threadLock.release()

def print_time(threadName, delay, counter):
    while counter:
        time.sleep(delay)
        print ("%s: %s" % (threadName, time.ctime(time.time())))
        counter -= 1

threadLock = threading.Lock()
threads = []

# 创建新线程
thread1 = myThread(1, "Thread-1", 1)
thread2 = myThread(2, "Thread-2", 2)

# 开启新线程
thread1.start()
thread2.start()

# 添加线程到线程列表
threads.append(thread1)
threads.append(thread2)

# 等待所有线程完成
for t in threads:
    t.join()
print ("退出主线程")
```
执行以上程序，输出结果为：
```
开启线程： Thread-1
开启线程： Thread-2
Thread-1: Wed Jan  5 17:36:50 2022
Thread-1: Wed Jan  5 17:36:51 2022
Thread-1: Wed Jan  5 17:36:52 2022
Thread-2: Wed Jan  5 17:36:54 2022
Thread-2: Wed Jan  5 17:36:56 2022
Thread-2: Wed Jan  5 17:36:58 2022
退出主线程
```

### 线程优先级队列（ Queue）
Python 的 Queue 模块中提供了同步的、线程安全的队列类，包括FIFO（先入先出)队列Queue，LIFO（后入先出）队列LifoQueue，和优先级队列 PriorityQueue。

这些队列都实现了锁原语，能够在多线程中直接使用，可以使用队列来实现线程间的同步。

Queue 模块中的常用方法:
- Queue.qsize() 返回队列的大小
- Queue.empty() 如果队列为空，返回True,反之False
- Queue.full() 如果队列满了，返回True,反之False
- Queue.full 与 maxsize 大小对应
- Queue.get([block[, timeout]])获取队列，timeout等待时间
- Queue.get_nowait() 相当Queue.get(False)
- Queue.put(item) 写入队列，timeout等待时间
- Queue.put_nowait(item) 相当Queue.put(item, False)
- Queue.task_done() 在完成一项工作之后，Queue.task_done()函数向任务已经完成的队列发送一个信号
- Queue.join() 实际上意味着等到队列为空，再执行别的操作

```python
#!/usr/bin/python3

import queue
import threading
import time

exitFlag = 0

class myThread (threading.Thread):
    def __init__(self, threadID, name, q):
        threading.Thread.__init__(self)
        self.threadID = threadID
        self.name = name
        self.q = q
    def run(self):
        print ("开启线程：" + self.name)
        process_data(self.name, self.q)
        print ("退出线程：" + self.name)

def process_data(threadName, q):
    while not exitFlag:
        queueLock.acquire()
        if not workQueue.empty():
            data = q.get()
            queueLock.release()
            print ("%s processing %s" % (threadName, data))
        else:
            queueLock.release()
        time.sleep(1)

threadList = ["Thread-1", "Thread-2", "Thread-3"]
nameList = ["One", "Two", "Three", "Four", "Five"]
queueLock = threading.Lock()
workQueue = queue.Queue(10)
threads = []
threadID = 1

# 创建新线程
for tName in threadList:
    thread = myThread(threadID, tName, workQueue)
    thread.start()
    threads.append(thread)
    threadID += 1

# 填充队列
queueLock.acquire()
for word in nameList:
    workQueue.put(word)
queueLock.release()

# 等待队列清空
while not workQueue.empty():
    pass

# 通知线程是时候退出
exitFlag = 1

# 等待所有线程完成
for t in threads:
    t.join()
print ("退出主线程")
```

以上程序执行结果：
```
开启线程：Thread-1
开启线程：Thread-2
开启线程：Thread-3
Thread-3 processing One
Thread-1 processing Two
Thread-2 processing Three
Thread-3 processing Four
Thread-1 processing Five
退出线程：Thread-3
退出线程：Thread-2
退出线程：Thread-1
退出主线程
```
## Python JSON 数据解析
JSON (JavaScript Object Notation) 是一种轻量级的数据交换格式。

Python3 中可以使用 json 模块来对 JSON 数据进行编解码，它包含了两个函数：
- json.dumps(): 对数据进行编码。
- json.loads(): 对数据进行解码。

在 json 的编解码过程中，Python 的原始类型与 json 类型会相互转换，具体的转化对照如下：

### Python 编码为 JSON 类型转换对应表：

  
| Python | JSON |
| --- | --- |
| dict | object |
| list, tuple | array |
| str | string |
| int, float, int- & float-derived Enums | number |
| True | true |
| False | false |
| None | null |

### JSON 解码为 Python 类型转换对应表：

  
| JSON | Python |
| --- | --- |
| object | dict |
| array | list |
| string | str |
| number (int) | int |
| number (real) | float |
| true | True |
| false | False |
| null | None |

### json.dumps 与 json.loads 实例

以下实例演示了 Python 数据结构转换为JSON：

```python
#!/usr/bin/python3
 
import json
 
# Python 字典类型转换为 JSON 对象
data = {
    'no' : 1,
    'name' : 'Runoob',
    'url' : 'http://www.runoob.com'
}
 
json_str = json.dumps(data)
print ("Python 原始数据：", repr(data))
print ("JSON 对象：", json_str)
```

执行以上代码输出结果为：

```
Python 原始数据： {'url': 'http://www.runoob.com', 'no': 1, 'name': 'Runoob'}
JSON 对象： {"url": "http://www.runoob.com", "no": 1, "name": "Runoob"}
```
通过输出的结果可以看出，简单类型通过编码后跟其原始的repr()输出结果非常相似。

接着以上实例，我们可以将一个JSON编码的字符串转换回一个Python数据结构：

```python
#!/usr/bin/python3
 
import json
 
# Python 字典类型转换为 JSON 对象
data1 = {
    'no' : 1,
    'name' : 'Runoob',
    'url' : 'http://www.runoob.com'
}
 
json_str = json.dumps(data1)
print ("Python 原始数据：", repr(data1))
print ("JSON 对象：", json_str)
 
# 将 JSON 对象转换为 Python 字典
data2 = json.loads(json_str)
print ("data2['name']: ", data2['name'])
print ("data2['url']: ", data2['url'])
```

执行以上代码输出结果为：

```
Python 原始数据： {'name': 'Runoob', 'no': 1, 'url': 'http://www.runoob.com'}
JSON 对象： {"name": "Runoob", "no": 1, "url": "http://www.runoob.com"}
data2['name']:  Runoob
data2['url']:  http://www.runoob.com
```

如果你要处理的是文件而不是字符串，你可以使用 **json.dump()** 和 **json.load()** 来编码和解码JSON数据。例如：
```python
# 写入 JSON 数据
with open('data.json', 'w') as f:
    json.dump(data, f)
 
# 读取数据
with open('data.json', 'r') as f:
    data = json.load(f)
```
## Python 日期和时间

Python 程序能用很多方式处理日期和时间，转换日期格式是一个常见的功能。

Python 提供了一个 time 和 calendar 模块可以用于格式化日期和时间。

时间间隔是以秒为单位的浮点小数。

每个时间戳都以自从 1970 年 1 月 1 日午夜（历元）经过了多长时间来表示。

Python 的 time 模块下有很多函数可以转换常见日期格式。如函数 time.time() 用于获取当前时间戳, 如下实例:
```python
#!/usr/bin/python3

import time  # 引入time模块

ticks = time.time()
print ("当前时间戳为:", ticks)
```
以上实例输出结果：
```
当前时间戳为: 1459996086.7115328
```
时间戳单位最适于做日期运算。但是1970年之前的日期就无法以此表示了。太遥远的日期也不行，UNIX和Windows只支持到2038年。

### 什么是时间元组？

很多Python函数用一个元组装起来的9组数字处理时间:

| 序号 | 字段 | 值 |
| --- | --- | --- |
| 0 | 4位数年 | 2008 |
| 1 | 月 | 1 到 12 |
| 2 | 日 | 1到31 |
| 3 | 小时 | 0到23 |
| 4 | 分钟 | 0到59 |
| 5 | 秒 | 0到61 (60或61 是闰秒) |
| 6 | 一周的第几日 | 0到6 (0是周一) |
| 7 | 一年的第几日 | 1到366 (儒略历) |
| 8 | 夏令时 | \-1, 0, 1, -1是决定是否为夏令时的标识 |

上述也就是 struct\_time 元组。这种结构具有如下属性：

| 序号 | 属性 | 值 |
| --- | --- | --- |
| 0 | tm\_year | 2008 |
| 1 | tm\_mon | 1 到 12 |
| 2 | tm\_mday | 1 到 31 |
| 3 | tm\_hour | 0 到 23 |
| 4 | tm\_min | 0 到 59 |
| 5 | tm\_sec | 0 到 61 (60或61 是闰秒) |
| 6 | tm\_wday | 0 到 6 (0是周一) |
| 7 | tm\_yday | 一年中的第几天，1 到 366 |
| 8 | tm\_isdst | 是否为夏令时，值有：1(夏令时)、0(不是夏令时)、-1(未知)，默认 -1 |

### 获取格式化的时间

你可以根据需求选取各种格式，但是最简单的获取可读的时间模式的函数是asctime():

```python
#!/usr/bin/python3

import time

localtime = time.asctime( time.localtime(time.time()) )
print ("本地时间为 :", localtime)
```

以上实例输出结果：

```python
本地时间为 : Thu Apr  7 10:29:13 2016
```

### 格式化日期

我们可以使用 time 模块的 strftime 方法来格式化日期：

```python
time.strftime(format[, t])
```

### 实例

```python
#!/usr/bin/python3

import time

\# 格式化成2016-03-20 11:45:39形式  
print (time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()))

\# 格式化成Sat Mar 28 22:24:24 2016形式  
print (time.strftime("%a %b %d %H:%M:%S %Y", time.localtime()))

  \# 将格式字符串转换为时间戳  
a \= "Sat Mar 28 22:24:24 2016"  
print (time.mktime(time.strptime(a,"%a %b %d %H:%M:%S %Y")))
```

以上实例输出结果：

```python
2016-04-07 10:29:46
Thu Apr 07 10:29:46 2016
1459175064.0
```

python中时间日期格式化符号：

*   %y 两位数的年份表示（00-99）
*   %Y 四位数的年份表示（000-9999）
*   %m 月份（01-12）
*   %d 月内中的一天（0-31）
*   %H 24小时制小时数（0-23）
*   %I 12小时制小时数（01-12）
*   %M 分钟数（00=59）
*   %S 秒（00-59）
*   %a 本地简化星期名称
*   %A 本地完整星期名称
*   %b 本地简化的月份名称
*   %B 本地完整的月份名称
*   %c 本地相应的日期表示和时间表示
*   %j 年内的一天（001-366）
*   %p 本地A.M.或P.M.的等价符
*   %U 一年中的星期数（00-53）星期天为星期的开始
*   %w 星期（0-6），星期天为星期的开始
*   %W 一年中的星期数（00-53）星期一为星期的开始
*   %x 本地相应的日期表示
*   %X 本地相应的时间表示
*   %Z 当前时区的名称
*   %% %号本身

### 获取某月日历

Calendar 模块有很广泛的方法用来处理年历和月历，例如打印某月的月历：

**实例**

```python
#!/usr/bin/python3

import calendar

cal \= calendar.month(2016, 1)  
print ("以下输出2016年1月份的日历:")  
print (cal)
```

以上实例输出结果：

```python
以下输出2016年1月份的日历:
    January 2016
Mo Tu We Th Fr Sa Su
             1  2  3
 4  5  6  7  8  9 10
11 12 13 14 15 16 17
18 19 20 21 22 23 24
25 26 27 28 29 30 31
```

### Time 模块

Time 模块包含了以下内置函数，既有时间处理的，也有转换时间格式的：

| 序号 | 函数及描述 | 实例 |
| --- | --- | --- |
| 1 | time.altzone  
返回格林威治西部的夏令时地区的偏移秒数。如果该地区在格林威治东部会返回负值（如西欧，包括英国）。对夏令时启用地区才能使用。 | 
以下实例展示了 altzone()函数的使用方法：

```python
>>> import time
>>> print ("time.altzone %d " % time.altzone)
time.altzone -28800 
```
| 2 | time.asctime(\[tupletime\])  
接受时间元组并返回一个可读的形式为"Tue Dec 11 18:07:14 2008"（2008年12月11日 周二18时07分14秒）的24个字符的字符串。 | 

以下实例展示了 asctime()函数的使用方法：

```python
>>> import time
>>> t = time.localtime()
>>> print ("time.asctime(t): %s " % time.asctime(t))
time.asctime(t): Thu Apr  7 10:36:20 2016 
```
用以浮点数计算的秒数返回当前的CPU时间。用来衡量不同程序的耗时，比time.time()更有用。 

由于该方法依赖操作系统，在 Python 3.3 以后不被推荐，而在 3.8 版本中被移除，需使用下列两个函数替代。

```python
time.perf_counter()  # 返回系统运行时间
time.process_time()  # 返回进程运行时间
```
以下实例展示了 ctime()函数的使用方法：

```python
>>> import time
>>> print ("time.ctime() : %s" % time.ctime())
time.ctime() : Thu Apr  7 10:51:58 2016
```

以下实例展示了 gmtime()函数的使用方法：

```python
>>> import time
>>> print ("gmtime :", time.gmtime(1455508609.34375))
gmtime : time.struct_time(tm_year=2016, tm_mon=2, tm_mday=15, tm_hour=3, tm_min=56, tm_sec=49, tm_wday=0, tm_yday=46, tm_isdst=0)
```

以下实例展示了 localtime()函数的使用方法：

```python
>>> import time
>>> print ("localtime(): ", time.localtime(1455508609.34375))
localtime():  time.struct_time(tm_year=2016, tm_mon=2, tm_mday=15, tm_hour=11, tm_min=56, tm_sec=49, tm_wday=0, tm_yday=46, tm_isdst=0)
```

以下实例展示了 sleep()函数的使用方法：

```python
#!/usr/bin/python3
import time

print ("Start : %s" % time.ctime())
time.sleep( 5 )
print ("End : %s" % time.ctime())
```

以下实例展示了 strftime()函数的使用方法：

```python
>>> import time
>>> print (time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()))
2016-04-07 11:18:05
```

以下实例展示了 strptime()函数的使用方法：

```python
>>> import time
>>> struct_time = time.strptime("30 Nov 00", "%d %b %y")
>>> print ("返回元组: ", struct_time)
```

以下实例展示了 time()函数的使用方法：

```python
>>> import time
>>> print(time.time())
1459999336.1963577
```

Time模块包含了以下2个非常重要的属性：

| 序号 | 属性及描述 |
| --- | --- |
| 1 | **time.timezone**  
属性time.timezone是当地时区（未启动夏令时）距离格林威治的偏移秒数（>0，美洲;<=0大部分欧洲，亚洲，非洲）。 |
| 2 | **time.tzname**  
属性time.tzname包含一对根据情况的不同而不同的字符串，分别是带夏令时的本地时区名称，和不带的。 |


### 日历（Calendar）模块

此模块的函数都是日历相关的，例如打印某月的字符月历。

星期一是默认的每周第一天，星期天是默认的最后一天。更改设置需调用calendar.setfirstweekday()函数。模块包含了以下内置函数：

| 序号 | 函数及描述 |
| --- | --- |
| 1 | **calendar.calendar(year,w=2,l=1,c=6)**  
返回一个多行字符串格式的 year 年年历，3 个月一行，间隔距离为 c。 每日宽度间隔为w字符。每行长度为 21\* W+18+2\* C。**l** 是每星期行数。 |
| 2 | **calendar.firstweekday( )**  
返回当前每周起始日期的设置。默认情况下，首次载入 calendar 模块时返回 0，即星期一。 |
| 3 | **calendar.isleap(year)**
是闰年返回 True，否则为 False。

```python
>>> import calendar
>>> print(calendar.isleap(2000))
True
>>> print(calendar.isleap(1900))
False
```

返回两个整数。第一个是该月的星期几，第二个是该月有几天。星期几是从0（星期一）到 6（星期日）。

```python
>>> import calendar
>>> calendar.monthrange(2014, 11)
(5, 30)
```












