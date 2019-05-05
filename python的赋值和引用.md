python的赋值和引用

```python
from copy import copy, deepcopy
from pickle import dumps, loads


# 变量对对象的实体也是一种引用
x = [2, 3, 4]
y = x
z = y
print(x is y is z)  # True
del x
print(y, z)  # 说明列表还存在
del y, z
# print(x, y, z)  # name is not defined


a = ['x', 'y', 'z']
b = [a] * 3
c = copy(b)
d = deepcopy(b)
e = loads(dumps(b, 4))  # 0-4，4是最快的一种算法

b[1].append(999)
print(b)
print(b[0] is b[1] is b[2])  # True
print(b[0] is b[1] is b[2] is a)  # True

c[1].append(999)
print(b)
# [['x', 'y', 'z', 999, 999], ['x', 'y', 'z', 999, 999], ['x', 'y', 'z', 999, 999]]
print(c)
# [['x', 'y', 'z', 999, 999], ['x', 'y', 'z', 999, 999], ['x', 'y', 'z', 999, 999]]
print(a)  # ['x', 'y', 'z', 999, 999]

print(d)  # [['x', 'y', 'z'], ['x', 'y', 'z'], ['x', 'y', 'z']]
d[1].append(999)
print(d)
# deepcopy在内存中重新创建所有子元素，所以有三个指向
# [['x', 'y', 'z', 999], ['x', 'y', 'z', 999], ['x', 'y', 'z', 999]]

print(e)  # [['x', 'y', 'z'], ['x', 'y', 'z'], ['x', 'y', 'z']]
print(e is b)  # False
e[1].append(999)
e.append(111)
# 非常类似于深拷贝，重新创建了子列表
# 区别在与：元组在深拷贝时不会重新开辟新的内存，认为它是不可变的。
# 但在pickle中处理，元组也会被重新创建一份出来。

my_deepcopy = lambda item: loads(dumps(item, 4))
# ipython 里有timeit的方法
# timeit -r 3 -n 100000 deepcopy(b)  对deepcopy(b)执行十万次测试它执行的时间
# 测试结果显示，我们自定义的深拷贝速度更快

```

