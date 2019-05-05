print函数默认换行，是end='\n'在起作用，

print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)

```
>>> for i in range(10):
print(i)

0
1
2
3
4
5
6
7
8
9
```

**如果不想换行可以用 print(xxx,end='')**

```
>>> for i in range(10):

print(i,end='')

0123456789

```

如果想打印制表符用print(xxx,end='\t') 

```
>>> for i in range(10):
print(i,end='\t')  # 不换行，数字之间打印制表符

0 　　1 　　2　　 3 　　4 　　5 　　6 　　7　　 8　　 9
```

```
>>> for i in range(10):
print(i,end='**')           #不换行，结尾后追加**

0**1**2**3**4**5**6**7**8**9**
```

