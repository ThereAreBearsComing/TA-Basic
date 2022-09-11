# TA_Basic_Rendering
Technical Artist Skills
# Pymel

```python
import pymel.core as pm
import maya.cmds as cmds

lst1 = pm.ls(selection=True)
lst2 = cmds.ls(selection=True)
#lst2[0] = "pCube"
trans1 = lst1[0].getTranslation()
trans2 = cmds.getAttr(lst2[0]+".translate")
# trans2 = [(0.0, 0.0, 0.0)]
print(trans1)
# result [0.0, 0.0, 0.0]
print(trans2)
# result [(0.0, 0.0, 0.0)]
```
## 常用Maya帮助文档
# Pymel类于层级
```Python
import pymel.core as pm

# node types
selList = pm.ls(sl =True)
firstSel = selList[0]
# 子集,Children,mesh = firstSel.getChildren(), result [nt.Mesh('pCubeShape1')] 
mesh = firstSel.getShape()
pos = firstSel.getTranslation()

e = mesh.edges[0]
pm.select(e)
# mesh打成软边，Shift+鼠标右键>>Soft/Hard Egdes(右下角)>>Toggle Soft Edge Display（正下方）
print(e.isSmooth) #判断软硬边

print(mesh,pos)
#result pCubeShape1 [0.0, 0.0, 0.0]
# 检测类型type()
```

# 合并工具
将打组 (Ctrl + G)后的几个物体合并，且改名为最后一个框选的物体。
* 写的工具添加工具栏：选择全部代码，按住鼠标中键，拖动至右上角空位置，右键选择编辑。

```Pyhon
import pymel.core as pm
# 获取所有选择物体
selList = pm.ls(sl =True)
# 拿到最后一个选择物体
lastSel = selList[-1]
# 那到所选物父集
p = lastSel.getParent()
# combine 合并
a = pm.polyUnite(selList)[0]  
# 把它设置成之前保存的父集，即
a.setParent(p)
# 清楚历史记录
pm.delete(a, ch = True)
# 改名
a.rename(lastSel)

```


