# MAYA UI结构
Maya参数搜索:https://help.autodesk.com/cloudhelp/2018/JPN/Maya-Tech-Docs/PyMel/modules.html
## UI结构

```Python
import pymel.core as pm

gLE = pm.window("MayaWindow", q = True, le = True ) #q = True来访问问，窗口，按钮等
UI = pm.window(
    title = "hello",
     height = 300, #可缩写h,w
     width = 500,
     le = gLE+300  # 打开在主窗口最左侧+300像素得位置
    )
pm.columnLayout(bgc=(1,0,0))    //bgc: Backgroud color
pm.button()
pm.button()
pm.button()
pm.checkBox()

pm.rowLayout(nc = 3,bgc=(0,1,0)) //nc: number of children
pm.button()
pm.button()
pm.button()

pm.showWindow(UI)
```
![image](https://user-images.githubusercontent.com/74708198/189692986-f1e3a7e9-1ae7-4c2a-bba8-a170f18c82ac.png)

## UI布局——行与列
在MayaHelp中搜，rowLayout 和 columnLayout获得相应参数。
```Python
import pymel.core as pm

UI = pm.window(
    title = "hello",
    # sizeable = False #无法调整大小
    )
pm.columnLayout(
    columnAttach=('both', 5),
    columnWidth=300,
    rowSpacing=5,
    adj = True #自适应大小
    )    
pm.button()
pm.button()
pm.button()
pm.checkBox()

pm.rowLayout( nc = 3,
    columnWidth3=(50, 50, 100),
    columnAttach=[(1, 'both', 0), (2, 'both', 5), (3, 'both', 0)],
    adj = 2 #第二个按钮自适应
    )    
pm.button()
pm.button()
pm.button()

pm.showWindow(UI)

# 大小布局可以通过自行计算得到
```

## UI布局——层级关系

```Python
import pymel.core as pm
#    Maya主窗口，访问（query），左边框（left edge）
gLE = pm.window("MayaWindow", q = True, le = True ) #q = True来访问问，窗口，按钮等 
UI = pm.window(
    title = "hello",
    le = gLE+300,
    # sizeable = False, #无法调整大小
    toolbox = True #简洁形界面
    )
    
formL = pm.formLayout()
   
btA=pm.button(label="A")
btB=pm.button(label="B")
btC=pm.button(label="C")
#    我们之前声明得布局，edit编辑
pm.formLayout(formL, e = True,
    # 以窗口为参考位置来设置
    attachForm =[
        (btA, 'top', 5), (btA, 'left', 5), (btA, 'right', 5), 
        (btB, 'left', 5), (btB, 'bottom', 5),
        (btC, 'bottom', 5),(btC, 'right', 5)
        ],
    # 以按钮为参考位置来设置   
    attachControl =[
        (btB, 'top', 5, btA),
        (btC, 'top', 5, btA),(btC, 'left', 5, btB)
    ]
)
    
pm.showWindow(UI)

```
![image](https://user-images.githubusercontent.com/74708198/189903715-1a6d64ef-0049-4ff2-93d2-20f3e33d7afa.png)

## UI布局——窗体布局
* 在布局中套布局
<br>Tips:VScode中双击变量，Ctrl + F2 批量选择可以统一修改。
```Python
import pymel.core as pm
#    Maya主窗口，访问（query），左边框（left edge）
gLE = pm.window("MayaWindow", q = True, le = True ) #q = True来访问问，窗口，按钮等 
UI = pm.window(
    title = "hello",
    le = gLE+300,
    # sizeable = False, #无法调整大小
    toolbox = True #简洁形界面
    )
    
formL = pm.formLayout()
   
btA = pm.button(label="A", h = 60)
btB = pm.button(label="B", w = 50)
colLay = pm.columnLayout(bgc = (1.0, 0.5 , 0.5), adj = True, rs = 5)
pm.button(label="1")
pm.button(label="2")
pm.button(label="3")
pm.setParent("..") #返回上一级，ie.跳出columnLayout。
btC = pm.button(label="C", h = 50)

#    我们之前声明得布局，edit编辑
pm.formLayout(formL, e = True,
    # 以窗口为参考位置来设置
    attachForm =[
        (btA, 'top', 5), (btA, 'left', 5), (btA, 'right', 5), 
        (btB, 'left', 5), (btB, 'bottom', 5),
        (colLay, 'right', 5),
        (btC,'bottom', 5), (btC,'right', 5),
        ],
    # 以按钮为参考位置来设置   
    attachControl =[
        (btB, 'top', 5, btA),
        (colLay, 'top', 5, btA),(colLay, 'left', 5, btB),
        (btC, 'top', 5, colLay),(btC, 'left', 5, btB)
    ]
)

pm.showWindow(UI)
```
![image](https://user-images.githubusercontent.com/74708198/189908817-397c5671-f880-498a-ac97-f3697736fb26.png)
* 理清挡关系！
* eg：当代码formLayout中的attachForm同时存在两个bottm设置时，会出现遮挡问题。
![image](https://user-images.githubusercontent.com/74708198/189909065-e6d4bb79-9bfc-4e55-8c65-439e0dc92810.png)
```Python
  (colLay, 'bottom', 5),(colLay, 'right', 5),
  (btC,'bottom', 5), (btC,'right', 5),
```
![image](https://user-images.githubusercontent.com/74708198/189909626-77393699-5f1b-4977-95bd-4d19d4cb363c.png)
* 左为错误（被遮挡）， 右则正确。


