---
title: 02-python流程控制
toc: true
date: 2020-09-22 17:32:26
tags:
categories:
- python
- python基础
---


# 一.条件控制_if

```
"""
流程控制：
python解释器：从上往下依次顺序解释执行
    顺序结构
    条件判断语句
    循环语句
"""

print("坐车去上班")
print("认真工作")
weather = 1 #0:天气不好 1：天气好
if weather == 0:
    #缩进语句
    print("去打篮球")   #只有在天气好的时候才打篮球
print("回家")

```

# 二.条件控制_if_else

```
"""
语法格式：
if 条件1：
    语句1
else:
    语句2

"""
#需求： 订单金额 >= 128 EMS包邮 否则 韵达包邮
amount = int(input("请输入您的订单金额："))
if amount >= 128:
    print("金额超过128元")
    print("EMS包邮")
else:
    print("韵达包邮")
```

# 三.流程控制_if_elif_else

```
"""
如果需要有超过2个结果需要处理，我们需要使用多个条件表达式进行判断
格式：
if 表达式1：
    语句1
elif 表达式2：
    语句2
else:
    语句3

需要：订单金额 >= 128 EMS包邮
      订单金额 》 68  韵达保留
      否则：邮费自理
"""

amount = int(input("请输入您的订单金额："))
print("---------start-------------")
if amount >= 128:
    print("EMS包邮")
elif amount > 68:
    print("韵达包邮")
else:
    print("运费自理")
print("---------end-------------")

```

# 四.条件判断_嵌套

```
"""
需求：
    你女朋友需要买一个lv, 需要向你借钱N(未知)元
    如果你的卡余额超过8000，
        输入密码转账操作
        如果输入的密码正确：123456
            转账成功
        否则：
            转账失败，密码错误
    否则：
        余额不足

"""

amount = int(input("宝贝,你需要多少钱啊："))
print("-----start------")
if amount <= 8000:
    password = input("请输入密码:")
    if password == "123456":
        print("转账成功")
        print("宝贝，钱收到了没有")
    else:
        print("密码错误")
else:
    print("钱不够")
print("------end------")

```

# 五.流程控制_练习

```
"""
需求：
    输入用户名，密码
    后台的用户名admin, 密码123456
    如果用户名密码都正确，登录成功
    如果只有用户名错误，提示用户名错误
    如果只有密码错误，提示密码错误
    否则： 用户名和密码都错误
"""

username = input("请输入用户名：")
password = input("请输入密码：")

if username == "admin" and password == "123456":
    print("登录成功")
elif username == "admin":
    print("密码错误")
elif password == "123456":
    print("用户名错误")
else:
    print("用户名和密码都错误")

```

# 六.while循环

```
"""
循环结构： 一些代码需要不断重复的去执行

while 条件：
    语句1
    语句2

"""

#需求：说100遍我爱你

start = 0
print("----start------")
while start < 100:
    print("我爱你%d"%start)
    start += 1
print("-----end-----")

```

# 七.while循环2

```
"""
计算1-100之间的和
"""

start = 1
sum = 0

while start <= 100:
    sum += start
    start += 1

print(sum)

```

# 八.while循环_矩形

```
"""
要求：打印 三行，每行5个*号
*****
*****
*****
"""

start = 1
while start <= 3:
    count = 1
    #每行打印5个*号
    while count <= 5:
        print("*",end="")  #end="" 打印结尾默认end="\n"
        count += 1
    #换行
    print()
    start += 1

```

# 九.while循环_三角形

```
"""
打印：三角形*号
*
**
***
"""

print("-----start------")
line = 1
while line <= 3:
    count = 1
    while count <= line:
        print("*",end="")
        count += 1
    print()
    line += 1
print("-----end------")

```

# 十.while循环_九九乘法表

```
"""

"""

x = 1
y = 1

while y <= 9:
    x = 1
    while x <= y:
        print("%d*%d=%d"%(x,y,(x*y)),end="\t")
        x += 1
    print()
    y += 1

```

# 十一.for循环

```
"""
打印字符串 wolfcode 中的每一个字符
"""

#while循环
text = "wolfcode"

print("while循环:")
length = len(text)
start = 0
while start < length:
    print(text[start])
    start += 1

print("for循环:")
for item in text:
    print(item)

```


## 参考资料
> - []()
> - []()
