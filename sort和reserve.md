**描述**

**sorted()**： 函数对**所有可迭代的对象**进行排序操作。**保留原列表**，返回一个新的排序好的list。

**sort()**:对**列表**（只能是列表）内容进行升序，排序后的新列表会**覆盖**在原列表上（id位置不变）。

```
g=[1,4,6,8,9,3,5]
print(sorted((g))		#默认为升序
》[1, 3, 4, 5, 6, 8, 9]
a=sorted({1: 'D', 2: 'B', 3: 'B', 4: 'E', 5: 'A'})
print(a)				#返回的总是列表，若是字典则返回键的列表。
》[1, 2, 3, 4, 5]		
print(g.sort())			#返回值为None
》None
b=g.sort
print(b)				#想得到sort后的值直接打印原列表
》[1, 3, 4, 5, 6, 8, 9]
```

**语法：**

> sorted(iterable, key=None, reverse=False) 
>
> 参数说明：
>
> - iterable -- 可迭代对象。
> - key -- 参数的值为一个函数，此函数只有一个参数且返回一个值用来进行比较，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。
> - reverse -- 排序规则，reverse = True 降序 ， reverse = False 升序（默认）。

```
print(sorted("This is a test string from Andrew".split(), key=str.lower))
》['a', 'Andrew', 'from', 'is', 'string', 'test', 'This']

x = [1,5,2,3,4]
print(sorted((x),reverse = True))
>>> [5, 4, 3, 2, 1]
```

**reverse()**：把原列表中的元素顺序从左至右的重新存放，而不会对列表中的参数进行排序整理。 

reversed():同上

> reverse()与sort的使用方式一样，而reversed()与sorted()的使用方式相同 

```
x = [1,5,2,3,4] 
print(x) 		 	#>>> [1, 5, 2, 3, 4]
print(x.reverse()) 	 #>>> None	
print(x)		    #>>> [4, 3, 2, 5, 1]
print(sorted(x))	#>>> [1, 2, 3, 4, 5]
print(reversed(x))	#>>> <list_reverseiterator object at 0x0000000001DF4FD0>
for i in reversed(x):
	print(i)		#4 3 2 5 1
```