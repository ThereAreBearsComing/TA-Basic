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
