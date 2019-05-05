#### 小Tips

##### iter()：用来生成迭代器。 

```
语法：iter(object[, sentinel])
```

- object -- 支持迭代的集合对象。
- sentinel -- 如果传递了第二个参数，则参数 object 必须是一个可调用的对象（如，函数），此时，iter 创建了一个迭代器对象，每次调用这个迭代器对象的__next__()方法时，都会调用 object。

返回值：迭代器对象。

```
lst = [1, 2, 3]
for i in iter(lst):
	print(i)
```

打印前面 带序号的？？

##### 生成器的两种写法：

m = (i for i in range(10))

def foo():

	……

	yield 1

关于yield的理解：https://www.ibm.com/developerworks/cn/opensource/os-cn-python-yield/

##### enumerate函数

enumerate参数为可遍历的变量，如 字符串，元组，列表等； 返回值为enumerate类。 

enumerate函数用于遍历序列中的元素以及它们的下标 .

```
i = 0
seq = ['one', 'two', 'three']
for element in seq:
    print(i, seq[i])
    i += 1
#0 one
#1 two
#2 three
```

```
i = 0
seq = ['one', 'two', 'three']
for element in seq:
    print(i, seq[i])

#0 one
#0 one
#0 one
```

```
list1 = ['one', 'two', 'three']
for i, data in enumerate(list1):
    print(i, list1[i])
#0 one
#1 two
#2 three
```

```
for i,j in enumerate(list1):
    print (i,j)
#0 one
#1 two
#2 three
```

```
#元组
seq = (('one', 'two', 'three'),(1,2,3),(2,3,4))
for i,j in enumerate(seq):
    print (i,j)
>0 ('one', 'two', 'three')
>1 (1, 2, 3)
>2 (2, 3, 4)
```

```
#字典
for i,j in enumerate({'a':1,'b':2}):
    print(i,j)
#0 a
#1 b
```

