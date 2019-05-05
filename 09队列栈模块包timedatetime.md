#### 栈

> 特点：先进后出【手枪弹夹】

```
'''在python中我们是通过列表来模仿栈'''
# 初始化栈
mystack = []

#向栈中压入数据
mystack.append(1)
mystack.append(2)
mystack.append(3)
mystack.append(4)

#从栈中向外取数据
'''
mystack.pop()
删除元素【默认从最后一个删除的】，并且返回被删除的元素，
'''
print(mystack.pop())
print(mystack.pop())
print(mystack.pop())
print(mystack.pop())
```

#### 队列

> 先进先出【水管】

```
import collections

'''collections是Python内建的一个集合模块，提供了许多有用的集合类。
使用list存储数据时，按索引访问元素很快，但是插入和删除元素就很慢了，因为list是线性存储，数据量大的时候，插入和删除效率很低。
deque是为了高效实现插入和删除操作的双向列表，适合用于队列和栈：'''
queue = collections.deque()
print(queue)  # deque([])

#进队
queue.append(1)
queue.append(2)
queue.append(3)
queue.append(4)
#出队
'''
queue.popleft()
本质：删除元素【从左边删除】，并且返回被删除的元素
'''
print(queue.popleft())
print(queue.popleft())
print(queue.popleft())
print(queue.popleft())
```

#### 模块

```
'''
模块：在python中一个.py文件就是一个模块
注意:一般情况下，我们会将具有类似功能函数放在一个文件中，
那么此文件就为一个功能模块。

优点：
1.提高代码的复用性
2.提高代码的可维护性
3.引用其他模块（包括内置模块，第三方模块，自定义模块）
4.避免函数名与变量名的冲突。
注意：定义变量或者模块的时候，尽量不要与第三方或者是内置模块的
模块名或者变量名冲突。
'''
```

#### name属性

```
'''
每一个模块都有一个__name__属性，当__name__的结果为__main__
的时候，则表示在自身模块中执行，当他的结果为模块名，则表示它被
导入到了其他模块中。

注意：以后写代码的时候最好添加上这么一行代码,类似于当前程序的入口
if __name__ == "__main__":
    pass
'''
```

#### 包

```
思考:上述已经知道模块的用法以及好处,但是如果不同的人编写的模块名相同怎么办?
解决:为了避免模块名冲突,python又引入按目录来组织模块的方法,称为包.

特点:引入包以后,只要顶层的包不与其他人发生冲突,那么模块都不会与别人的发生冲突

注意:每个包目录下都会有一个init.py文件,这个文件必须存在,否则python就把这个目录当成普通目录,而不是一个包。__init__.py可以是空文件,也可以有python代码,因为__init__.py本身就是一个模块.

```

### 时间模块

```
表示时间的两种方式：
1. 时间戳(相对于1970.1.1 00:00:00以秒计算的偏移量),时间戳是惟一的
2. 时间元组 即(struct_time),共有九个元素，分别表示，同一个时间戳的struct_time会因为时区不同而不同
```

#### time

```python
import  time

# 睡眠 参数number 单位s
# 线程推迟指定的时间运行适合放在脚本里
time.sleep(2)

# 以浮点数计算的秒数返回当前的CPU时间。用来衡量不同程序的耗时
time.clock()
'''
1.在第一次调用的时候，返回的是程序运行的实际时间；
而第二次之后的调用是自第一次调用以后到现在的运行时间。

2.在win32系统下，这个函数返回的是真实时间（wall time），而在Unix/Linux下返回的是CPU时间。（WIN32实际上是以WIN32上QueryPerformanceCounter()为基础，它比毫秒表示更为精确）
'''
time1 = time.clock()
......something.....
time2 = time.clock()
time_result = time2 - time1 # 计算响应时间

# 获取当前时间的时间戳,浮点数形式,不需要参数
time1 = time.time()
print(time1)

# 年-月-日，时：分：秒
# 将时间戳转为格林尼治时间[把时间戳转为元组]
gm = time.gmtime(time1)
print(gm)
>>>time.struct_time(tm_year=2018, tm_mon=3, tm_mday=27, tm_hour=14, tm_min=3, tm_sec=26, tm_wday=1, tm_yday=86, tm_isdst=0)

# 将时间戳转为当前时区的struct_time
# time.localtime([secs])如果seconds参数未输入，则以当前时间为转换标准
lm = time.localtime(time1)
print(lm)

# 将时间元组转为指定格式的字符串time.strftime(format[, t])
# t未指定，传入time.localtime()作为默认参数：
strf = time.strftime("%Y-%m-%d %X")
print(strf)
>>>2019-03-13 11:44:47
# 指定t为time.localtime(1407945600.0)时：
strf = time.strftime("%Y-%m-%d %H:%M:%S",time.localtime(1407945600.0))
print(strf)
>>>2014-08-14 00:00:00

# 将时间元组转为字符串        
asctime = time.asctime(lm)
print(asctime)   
>>>Wed Mar 13 11:55:50 2019
        
# 将时间戳直接转为本地时间的字符串格式
ctime = time.ctime(time1)
print(ctime) 
>>>Wed Mar 13 12:01:04 2019
        
# 将一个时间元组转换为时间戳
time2 = time.mktime(lm)
print(time2)
>>>1552449809.0

# 将指定时间格式的字符串,转为时间元组
# strptime(string, format)
srtptime = time.strptime("2018-07-30 11:26:03","%Y-%m-%d %X")
print(srtptime)
```

##### CPUtime/wall time

> 总CPU时间（用户时间+系统时间）
>
> user-cpu time用户CPU时间是运行程序代码（或库中的代码）的处理器所花费的时间; 
>
> system-cpu time系统CPU时间是代表程序在操作系统内核中运行代码所花费的时间。
>
> **wall-clock time**指墙上的时钟（或手表中的秒表）在过程开始和“现在”之间经过的时间。不是进程在CPU上花费的秒数; 它是经过的时间，包括等待CPU开启所花费的时间（其他进程运行时）。
>
> 如果挂钟时间<CPU时间，则表示您正在并行执行程序。如果挂钟时间> CPU时间，则表示您正在等待磁盘，网络或其他设备。
>
> UNIX中的wall-clock-time，user-cpu-time和system-cpu-time具体是什么？:https://stackoverflow.com/questions/7335920/what-specifically-are-wall-clock-time-user-cpu-time-and-system-cpu-time-in-uni

##### struct_time元组元素结构

```
属性                            值
tm_year（年）                  比如2011 
tm_mon（月）                   1 - 12
tm_mday（日）                  1 - 31
tm_hour（时）                  0 - 23
tm_min（分）                   0 - 59
tm_sec（秒）                   0 - 61
tm_wday（weekday）             0 - 6（0表示周日）
tm_yday（一年中的第几天）        1 - 366
tm_isdst（是否是夏令时）        默认为-1
```

##### format time结构化表示

```
格式	含义	备注
%a	本地（locale）简化星期名称	
%A	本地完整星期名称	
%b	本地简化月份名称	
%B	本地完整月份名称	
%c	本地相应的日期和时间表示	
%d	一个月中的第几天（01 - 31）	
%H	一天中的第几个小时（24小时制，00 - 23）	
%I	第几个小时（12小时制，01 - 12）	
%j	一年中的第几天（001 - 366）	
%m	月份（01 - 12）	
%M	分钟数（00 - 59）	
%p	本地am或者pm的相应符	一
%S	秒（01 - 61）	二
%U	一年中的星期数。（00 - 53星期天是一个星期的开始。）第一个星期天之前的所有天数都放在第0周。	三
%w	一个星期中的第几天（0 - 6，0是星期天）	三
%W	和%U基本相同，不同的是%W以星期一为一个星期的开始。	
%x	本地相应日期	
%X	本地相应时间	
%y	去掉世纪的年份（00 - 99）	
%Y	完整的年份	
%Z	时区的名字（如果不存在为空字符）	
%%	‘%'字符

常见结构化时间组合：
time2 = time.strftime("%Y-%m-%d %X")
# 2019-03-13 12:19:16
```

#### datetime

参考链接https://www.jianshu.com/p/97a76e78b3e0

```
datetime模块常用的主要有下面这四个类：
1. datetime.date: 是指年月日构成的日期(相当于日历)
2. datetime.time: 是指时分秒微秒构成的一天24小时中的具体时间(相当于手表)
3. datetime.datetime: 上面两个合在一起，既包含时间又包含日期
4. datetime.timedelta: 时间间隔对象(timedelta)。一个时间点(datetime)加上一个时间间隔(timedelta)可以得到一个新的时间点(datetime)。比如今天的上午3点加上5个小时得到今天的上午8点。同理，两个时间点相减也会得到一个时间间隔。
```

##### datetime.datetime

```
1.获取系统当前时间[<class 'datetime.datetime'>]
time1 = datetime.datetime.today()
print(time1)

2.datetime.datetime.now([tz]) 当不指定时区时，和datetime.datetime.today()是一样的结果
time2 = datetime.datetime.now()
print(time2)

# *获取指定时间【鸡肋】
time3 = datetime.datetime(2018, 3, 28, 21, 59, 7, 95015)
print(time3)
>>>2018-03-28 21:59:07.095015

3.将时间格式化输出为字符串
time4 = time1.strftime("%Y-%m-%d %X")
print(time4)
>>>2019-03-13 15:28:49

4.
print(time1.timestamp())  # 转为时间戳
print(time1.timetuple())  # 转为struct_time
print(time1.ctime())  # 显示英文格式
print(time1.isocalendar())  # 显示日历 (年, 该年中的第几周, 周几)
print(type(time1.isocalendar())) # 元组
```

##### datetime.timedelta

```
# 两个datatime对象相减得到是一个时间间隔的对象
time5 = datetime.datetime(2018, 3, 28, 21, 59, 7, 95015)
time6 = time5 -time1
print(time6)
print(type(time6))  # <class 'datetime.timedelta'>

# 时间间隔对象获取间隔天数
print(time6.days)

# 除间隔天数之外的秒数
print(time6.seconds)
```

#### calendar

```
import  calendar

# 返回指定年的日历【字符串类型】
ca = calendar.calendar(2018)
print(ca)
print(type(ca)) 

# 打印指定月份的日历
print(calendar.month(2018,7))

# 判断某一年是否为闰年，若是则返回True，否则返回False
print(calendar.isleap(200))

# 返回【year1，year2)之间闰年的个数
print(calendar.leapdays(2000,2020))

#返回指定月的第一天为周几【日期码周一~周日【0，6】】，
# 以及这个月总共的天数
print(calendar.monthrange(2018,7))

#返回指定日期的日期码，周几
print(calendar.weekday(2018,7,30))

# 返回一个二维列表，列表中的每个元素以每一周为元素序列。
# 注意：跨月的日期为0
print(calendar.monthcalendar(2018,7))

# 将日历转化为html 格式, 可以设置 年月日, 星期等
cal = calendar.HTMLCalendar(calendar.MONDAY)
print(cal)  # <calendar.HTMLCalendar object>
# print(cal.formatyear(2017))
```