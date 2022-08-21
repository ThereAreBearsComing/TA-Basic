# TA_Basic_Rendering
Technical Artist Skills

# Python for maya

## 列表
```python
#列表添加

a.append()

a.insert(0, “xx”)

#删除

del a[1]

a = a.pop(1) #弹出索引值，会存在a中

a.remove(“删除内容值”)

#排序由小到大

a.sort()

#得列表长度

len(a)

#切片

b = a[0:2] #切0到2位也可写 [ :2]

l = a[: -1] #只切到最后一位

l = a[: : 2] #隔一个存一个,3的话隔两个。


polyCube = ["cube1", [0.0, 10.0, 5.0], 8 , 12, 6, "lambert"]

name = polyCube[0]

pos = polyCube[1]

print("The name of cube" + name)
#需要统一属性
print("and the position" + + str(pos))
```
## 字典, 键key: 值value

```python
polyCubeDict = {

"name":"cube1"

"position": [0.0, 10.0, 5.0],

"points":8,

"edges":12,

"face": 6,

"material": "lambert1"

}

get = polyCubeDict["key"]

#改 
polyCubeDict["key"] = newvalue

#添加 
polyCubeDict["newkey"] = newTrue

#删除 
del polyCubeDict["key"] 

#返回所有keys or values

polyCubeDict.keys()

polyCubeDict.values()

polyCubeDict.items()

```
# For 循环,遍历
```Python
myList[0,1,2,3,4]
myString = "Hello World!"

for letter in myString:
    print("The letter is:") ##遍历
print("the end!") ##遍历完，退出执行

for i in myList:
    print(i)
    
for i range(2,4):
    print(i) #打印2~4位

for i in range(len(myList)):
    print(i)
    print(myList[i])
##打印出 位+值

##遍历字典
for k,v in polyCubeDict.items():
    print("key":{}, "value": {}, format(k, polyCubeDict[k]))
    print(k)
    print(ployCuibeDict[k])

for k,v in polyCubeDict.items():
    print("key":{}, "value": {}, format(k, v))

```
# 判断

```python
# 布尔值 bool
condition = true
if condition:
    print()
elif condition_2:
    print()
else:
    print()
##condition 有 and, or
##判断中一定是 ==

#if 8 in polyCube ,判断在不在表内

```
# 函数&类
```python
class Human():
    def __init__(self, name, age=0, hight=0.0, weight=0.0, sex="boy"): #构造函数，初始化函数
        self.name = name #成员变量，属性
        self.age = age
        self.height = height
        self.weight = weight
        self.sex = sex
        
    def info(self):
    print("My name is {}, {} years old and I'm a {}". format(self.name, self.name, self.sex))
    
XiaoHong = Human("xiao hong", 18, 160, 90, "girl") #实力化
## 执行
XiaoHong.weight = 80 # 属性
XiaoHong.info()      # 方法
```
# 模块和标准库
```python
# 导入
import class02  as c2# 文件名儿

HM1 = class02.Human("LaoWang")
class02.sayHello() #模块名(模块别名).函数名
print(HM1.name)

#从模块导入
from class02 import sayHello

sayHello #这个方法不用前缀模块名

#常用标准库
import math
import os, sys ,json

cwd = os.getcwd()
print(cwd)
os.startfile(r"C:\Sc........") #路径名

```
