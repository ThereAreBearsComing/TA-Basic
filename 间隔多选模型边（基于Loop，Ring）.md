# 间隔多选模型边





## 脚本编辑器中的Trigger
```Python
import importlib
import selectEdgeN
importlib.reload(selectEdgeN)
selectEdgeN.main()
```

## 脚本
* 脚本文件名：selectEdgeN.py
```Python
from asyncore import loop
from cProfile import label
from distutils import core
from multiprocessing.sharedctypes import Value
from tkinter import Label
import pymel.core as pm

import maya.mel as mel

radioCol = None
intF = None

def main():
    global radioCol,intF
    UI = pm.window(
        title= "SelectN",
        toolbox = True 
        )

    formL = pm.formLayout()
    btn = pm.button(label = "Select Edge",h=30,command=btnCMD)

    colLay = pm.columnLayout(adj = True)
    # 当只能多选一时只能使用radioBotton,而非checkBox,radioCollection为必加固有解构。
    radioCol = pm.radioCollection() # 声明在这里则非全局变量，之后的函数无法访问。
    ckBtn1 = pm.radioButton(label ="Loop",w=70)
    ckBtn2 = pm.radioButton(label ="Ring",w=70)
    # 设置全局变量的初始值
    pm.radioCollection(radioCol,e=True,sl=ckBtn1)

    pm.setParent("..")
    intF = pm.intField (value=2,h=30)

    pm.formLayout(
        formL, e=True,
        af=[
            (colLay,"top",5),(colLay,"left",5),
            (btn,"left",5),(btn,"bottom",5),(btn,"right",5),
            (intF,"top",5),(intF,"right",5)
        ],
        ac={
            (intF,"left",3,colLay),
            (btn,"top",3, colLay)
        }
    )

    pm.showWindow(UI)

def btnCMD(*args): #Maya中定义函数必须给参数，默认加"*args"
    radioBtn = pm.radioCollection(radioCol, q=True, sl = True)
    mode = pm.radioButton(radioBtn, q = True, label = True)

    N = pm.intField(intF, q=True, value = True)
     
    mel.eval(
        "polySelectEdgesEveryN \"edge{}\" {};".format(mode, N)
        )
```
