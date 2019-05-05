### **序列化**

> 把**变量** **从内存**中变成可存储或者传输的过程称之为序列化。

在Python中叫picking,在其他语言中也被称为serialization,marshalling,flattening等等。

> 序列化之后，就可以把**序列化后**的内容**写入磁盘**，或是通过网络传输到别的机器上。反过来，把变量内容从序列化的对象重新读到内存里称之为反序列化，即unpickling。 

#### pickle

Python提供了`pickle`模块来实现序列化：

pickle是python中独有的序列化模块，所谓独有，就是指不能和其他编程语言的序列化进行交互,因为pickle**将数据对象转化为bytes**

pickle模块提供了四个功能：dumps、dump、loads、load。

​	dumps和dump都是进行序列化，而loads和load则是反序列化。

**dumps**

将所传入的变量的值序列化为一个**bytes**，然后，就可以将这个bytes写入磁盘或者进行传输。 

```
import pickle
d = [1,2,3,4]
r = pickle.dumps(d)
print(r)
》b'\x80\x03]q\x00(K\x01K\x02K\x03K\x04e.'
```

**dump**

> pickle.dump(object，file)
> file:打开以供写入的文件
> obj:需要写入的对象/需要序列化的变量
> 功能:可以将任意的对象obj序列化为bytes,写入到**文件**file中.

```
with open("lili.txt",'wb')as f:
    pickle.dump(d,f)
>>会出现一个新的lili.txt文件，里面是d的二进制字节
```

**loads**

当我们要把对象从磁盘读到内存时，可以先把内容读到一个**bytes**，然后用**loads**方法反序列化出**对象**。

**load**直接从一个文件反序列化出对象。 

```
R1 = pickle.loads(r)
print(R1)
>>[1, 2, 3, 4]
```

```
with open('lili.txt','rb')as f1:
    R2 = pickle.load(f1)
    print(R2)
>>[1, 2, 3, 4]
```

反序列化出来的这个变量和原来的变量是完全不相干的对象，它们只是内容相同而已。 

[https://www.cnblogs.com/cobbliu/archive/2012/09/04/2670178.html]: pickle

#### json

不同的编程语言之间需要通信的时候,我们必须将我们的对象
序列化为标准模式,**json实际上就是一个字符串**,所以使用它
来进行转递数据非常的方便读取,速度非常快. 

| JSON类型   | Python类型 |
| ---------- | ---------- |
| {}         | dict       |
| []         | list       |
| "string"   | str        |
| 1234.56    | int或float |
| true/false | True/False |
| null       | None       |

> json.dumps(): 将字典序列化为json字符串
>
> json.loads(): 将json字符串反序列化为字典
>
> json.dump(): 将字典序列化到一个文件，是文本文件，相当于将序列化后的json字符串写入到一个文件
>
> json.load(): 从文件中反序列化出字典

**总结**： 不带s的是序列化到文件或者从文件中反序列化，带s的是都在内存中操作不涉及到持久化

```
import json

if __name__ == '__main__':
    s = {"name": "xiaoxue","age": 18}
    # 序列化为字符串
    json_string = json.dumps(s)
    print(json_string)
》》{"name": "xiaoxue", "age": 18} string格式的
    # 从字符串中反序列化
    json_dict = json.loads(json_string)
    print(json_dict)
》》 {"name": "xiaoxue", "age": 18}  dict格式
    # 序列化到文件中
    with open('json1', 'w',encoding="utf-8") as json_file:
        json.dump(s, json_file)
》》创建一个json1的文件，以utf-8格式写入s
    # 从文件中反序列化
    with open('json1', 'r',encoding="utf-8") as json_file:
        json_dict = json.load(json_file)
        print(json_dict)
》》{'name': 'xiaoxue', 'age': 18} dict格式
```

但JSON只能处理基本数据类型。pickle能处理所有Python的数据类型。



**拓展：把任意class的实例变为dict：**
**print(json.dumps(s, default=lambda obj: obj.`__dict__`))**

default参数就是告知json如何进行序列化

通常class的实例都有一个`__dict__`属性，它就是一个dict，用来存储实例变量。也有少数例外，比如定义了`__slots__`的class，那这种情况下只能自定义编解码函数，具体如下

[https://www.cnblogs.com/tkqasn/p/6005025.html]: json详解

