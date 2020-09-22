---
title: 01-python基础
toc: true
date: 2020-09-22 17:14:52
categories:
- python
- python基础
tags:

---


# 一. 变量和常量

```
username = "jack"
print(username)

print(type(username))

username = 8
print(username)

print(username+5)

print(type(username))

```

# 二. 变量_对象和引用

```
"""
操作流程
1，创建一个数字对象100
2， 创建一个变量a
3, 将100赋值给变量a
"""

a = 100
print(a)

 # id(a),   变量a中所存放的内存地址
print(id(a))

a = 108
print(a)
print(id(a))
```

# 三. 垃圾回收_共享引用

```
"""
在程序运行的过程中，把创建的对象而且已经是没有用的对象自动回收，这个过程，称之为垃圾回收
"""

a = "python"
b = a

 #a, b两个变量共享引用数据 python
print(id(a))
print(id(b))

a = "wolfcode"
print(a)
print(id(a))
print(id(b))
```

# 四. 数字基本操作

```
"""
数值类型：整数(int) ,和 小数(float), 复数
1，数值是不可变类型的对象
2，数值的表达方式有： 十进制，十六进制，八进制， 二进制
3，数据之间的进制转换 
    hex()，转换成十六进制
    oct(), 转换成八进制
    bin(), 转换成二进制
    int(),  转换成十进制
"""
#十进制
num1 = 100
print(num1)

#十六进制
num2 = 0xff
print(num2)

#八进制
num3 = 0o75
print(num3)

#二进制
num4 = 0b101
print(num4)

#进制之间的转换
num5 = 6890
print(num5)
#bin(num)  使用二进制表示
print(bin(num5))

#hex(num)  使用十六进制表示
print(hex(num5))

#oct(num)  使用八进制表示
print(oct(num5))

#把八进制转换成十进制
print(int(0o77))

#把字符串转换成数字
print(int("1099"))
```

# 五. 数字的其他操作

```
"""
表达式操作
x//y  整除， 取x除以y的整除部分
x%y   取余数， x除以y的余数部分
x**Y   x的y次方

pow(x,y)  ==>   x**y 的次方
abs(x) ==> |x| 返回的是x的绝对值
"""

import  random

print(5/2)
print(-5/2)
print(5//2)
print(-5//2)
print(5%2)
print(5*2)
print(5**2)

print(pow(5,3))
print(abs(-3))

print("int转换=================")
print(int("100"))   #100，   转换成十进制数字
print(int("100",2))  # 100是二进制数字，转换成十进制数字=4
print(int("100",16))

print("随机数=======================")

#生成一个1-10之间的随机数字
print(random.randint(1,10))

#dir 显示模块有哪些方法可以使用
print(dir(random))

#help 查看方法的帮助文档
print(help(random.randint))
```

# 六. 布尔类型

```
"""
布尔类型： 只有两个值，True,和 False,
1, 可以和整数直接参数运算
2, 如果把True, False 转换为数字， True --> 1, False --> 0
3, 数字可以转换为布尔类型， 0-->False，非0 -->Ture   使用bool(num)函数
4, 在python中，所有的数据都可以表示为True,False, 
    在字符串中，空字符串表示为False, 非空字符串表示True,   bool(str) 函数
"""

flag = True

print(flag)

# 进行加法运算
print(flag+4)

# bool(num)  把一个数字转换为布尔类型
print(bool(0.0))
print(bool(100))

print(bool(""))
print(bool("\n"))

```

# 七. 字符串基本操作

```
"""
字符串：使用引号括起来的文字，通常情况表达的是文字的信息，有序的字符集合
1, 使用单引号
2，使用双引号
3, 使用三重引号，可以对字符串换行

字符串的特点：
1，有序的字符集合
2，对于字符串中的每一个字符串都有一个对应的索引，从左往右，从0开始， text[0]
    索引特点： 从左往右，从0开始， 从右往左，从-1开始
3，对于字符串是不可变对象，跟数字一样
4，对于字符串的长度，可以使用len()函数
5，str()函数，可以把其他对应转换为字符串
"""
text = "python"
print(text)
#type(text) 查看对象的类型
print(type(text))

text2 = "wolfcode"
print(text2)

text3 = """呵呵呵
 你好啊
"""
print(text3)
print(type(text3))

print("======================================")
#访问text的第一个字符
print(text[0])
#访问text的最后一个字符
print(text[-1])

#错误，不能修改字符串中的字符
#text[-1]="B"

#len(text) text的长度
print(len(text))

#去除最后一个元素
print(text[len(text) -1])

#str(123), 将数字123转换成字符串
print(str(123456))
print(type(str(123456)))

print("====加法和乘法====")
#字符串连接符号
print("python" + "java")
print("123" + str(456))
print(int(123) + 456)

#乘法操作, 显示50个 = 字符
print("="*50)
```

# 八. 转义字符_原始字符

```
"""
转义字符：
转义序列可以让我们在字符串中表示不容易通过键盘输入或者在输入过程中字符本身有一些特殊意义的，
我们需要使用转义字符来表示
\n 表示换行
转义字符： \+固定的字符
比如：
\'  单引号，普通的字符串，不在是字符串的边界标记
\"  双引号，普通的字符串，不在是字符串的边界标记
\n  换行符, 输入换行符
\t  制表符
\r  回车， 返回到当前行最开始的位置
"""

text = "abc\nmp"
print(text)
print(len(text))

text2 = 'abc\'\"mp'
print(text2)

text3 = "abc\tdef"
print(text3)

# \r返回当前行最开始的地方
print("abcdefghijk\r呵呵呵")

print("abc\\tdef")

#filename = "d:\\name\\text2.txt"
#在字符串的前面加上r, 代表原始字符串
filename = r"d:\name\text2.txt"
print(filename)

```

# 九. 字符串转换

```
"""
str()   把一个对象转换为字符串
ord()   返回字符的unicode编码
chr()   把unicode编码转换为字符
"""

#字符串拼接
print("123"+str(456))

#中 对应的unicode编码
print(ord("A"))

# 将unicode编码转换成字符
print(chr(65))

```

# 十. 字符串分片.py

```
"""
字符串是一个有序的字符的集合
通过字符串索引text[0] 是可以获取到一个字符
如果需要从字符串中获取多个字符的话，需要用到分片

str[start:end:step]
如果start省略，默认0
如果end省略， 默认len(str)
如果step省略， 默认1
start: 正整数，负整数
end:正整数，负整数
step: 正整数，正偏移， 负整数，负偏移
"""
text = "python"
text2 = "wolfcode"

text3 = text2[4:8]
print(text3)

#如果不写结束索引，默认为结尾，即字符串的长度len(text2)
print(text2[2:])

#如果不写开始索引，默认为0
print(text2[:4])

#拷贝出一个新的字符串
text4 = text2[:]
print(text4)

print("="*50)

#步长： 默认为1
#text2[start:end:step]
#需求： 索引值0 2 4 6 8 这样的字符
text5 = text2[::2]
print(text5)

#需求： 获取wolfcode的最后三个字符
print(text2[-3:])

#需求，将字符串wolfcode倒叙过来，组成edocflow这个字符串
print(text2[-1::-1])

```

# 十一. 字符串格式化

```
"""
方式一： %占位符来表示字符串中的变量
%s 字符串  %d整数 %f小数
"""

#方式一
name = "lucy"
age = 19
print("my name is %s"%name)
print("my name is %s, I am %d"%(name,age))

job = "IT"
print("my job is %s, your job is %s"%(job,job))

# %.2f 保留两位小数
print("this number is %.2f"%3.1415926)

print("="*50)

#使用位置占位符，如果不写，默认是从0开始
#text = "my name is {}, I am {}".format(name,age)
#text = "my name is {0}, I am {1}".format(name,age)

#使用名称占位符
text = "my name is {name}, I am {age}".format(name="jack", age=18)
print(text)
```

# 十二. 字符串的常用方法

```
"""
查找：x.find(y) 在字符串x中查找y,如果找到，返回第一次找到对应的索引值,
    如果没有找到，返回-1
    text = " good good study day day up"
    num = text.find("study1")
    print(num)

x.index(y): 在字符串x中查找y, 如果找到，返回第一次找到的索引，如果找不到，
    报错 ValueError
    text = " good good study day day up"
    num = text.index("study1")
    print(num)

替换：
x.replace(y,z), 把字符串x中的y替换为z, 替换完之后返回一个新的字符串，
    原来的字符串不变
    x = "I am good boy"
    text2 = x.replace("good","bad")
    print(text2)

字符串分割：x.split([y]), 把字符串x按照y进行分割
字符串合并: y.join(x),  用字符串y将x中的每个数据进行连接
去除空格： x.strip(), 把字符串x两边的空格去掉
编码： x.encode("utf-8")   把字符串x编码为字节数据，参数为编码规则，默认为utf-8
解码： x.decode("utf-8")   把字节数据x解码为字符串，参数为解码规则，同编码一致
"""

x = "你好,谢谢,对不起,请,再见"
text3 = x.split(",")
print(text3)

text4 = "%4%".join(text3)
print(text4)

x = "   wolf code,   code color   "
y = x.strip()
print(x)
print(y)

print("="*50)
x = "hello,你好"
y = x.encode("utf-8")   #b开头
print(x)
print(y)
print(type(x))
print(type(y))
text5 = y.decode()
print(text5)
```

# 十三. 运算符操作

```
"""
1，复合运算符 + - * / +=
x+=y  ==> x = x+y

2，关系运算符 > < >= <=  == 返回结果是布尔值，True,False

3, 逻辑运算符, 对于所有的对象数据都可以转换为布尔类型
    逻辑与： and
    逻辑或： or
    逻辑非:  not
x and y:  如果x为False，那么返回x, 否则返回y, 返回第一个为False的值， 或者是最后一个值
x or y: 如果x为True, 那么返回x, 否则就返回y, 返回第一个为True的值，或者是最后一个值
not x: x如果为True的话，返回False, 否则返回True
"""

print(0 and 100)
print(1 and 100)
print("wolf" and 80)

print("="*50)
print("wolf" or 1)
print("" or 10)
print(0 or 10)
print(1 or 0)

print("="*50)
print(not "wolf")
print(not "")
print(not 0)
print(not 10)

```

# 十四. 运算符_实体关系

```
"""
成员关系： 体现的是对象(序列对象，字符串，元组，列表，集合)之间的包含关系
x in y:   如果在y中包含x, 返回True, 否则返回False
x not in y: 如果在y中不包含x, 返回True, 否则返回False

实体对象测试：判断两个变量是否存的是同一个对象（共享引用），id(x) == id(y)
x is y: 表示x和y是同一个对象 即id(x)=id(y), 内存地址是同一个
x is not y: 表示x和y不是同一个对象,即内存地址不一样
"""

text1 = "wolfcode"
text2 = "code"
print(text2 in text1)  #True
print(text2 not in text1) #False
print("00xx" not in text1) #True

text3 = text1

print(id(text1))
print(id(text3))
print(text1 is text3)  #这儿比较的是内存地址
print(text1 == text3)  #这儿比较的是值

```