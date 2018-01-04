# 

\[原文链接在这里\]\([http://doc.babylonjs.com/babylon101/discover\_basic\_elements](http://doc.babylonjs.com/babylon101/discover_basic_elements)\)

目录：

1. 设置形状101
   1. MeshBuilder 方法
      1. 盒状
      2. 球状
      3. 飞机
      4. 场地
   2. 你自己的HTML
   3. 笔记
   4. 要
   5. s
   6. 
2. 下一部分
3. 扩展阅读

### 设置形状 101

一些常用的形状都有命名，比如说盒状，球体，一个柱状体，圆锥体，常规多边形，飞机， 一个特殊的水平面被称为场地。但也有少数不太常用的未命名的，比如环状，环形节，不规则多边体。下一章会涉及如何创建这些由数据和参数来形成的不常用的形状。它们被称作参数形状。

在101课程中，你仅学习有限的形状，比如说这页开始提到的盒子，球体，飞机和场地。另外你也仅会用到新的方法_MeshBuilder_而不会用到旧方法。如何创建所有形状，两种方法的优缺点等可以通过扩展阅读来获取答案。

### MeshBuilder方法

创建形状的通用形式是：

var _shape_ = BABYLON.MeshBuilder.create_Shape\(name, options, scene\);_

options参数允许你设置形状的大小，设置形状是否可以更新。下面是一些特定例子：

#### Box

```javascript
var box = BABYLON.MeshBuilder.CreateBox('box', {}, scene);

var myBox = BABYLON.MeshBuilder.CreateBox('myBox', {height: 5, width: 2, depth: 0.5}, scene);
```

| **option** | value | default value |
| :--- | :--- | :--- |
| size | \(_number_\)size of each box side | 1 |
| height | \(_number_\)height size, overwrites size property | size |
| width | \(_number_\)width size, overwrites size property | size |
| depth | \(_number_\)depth size, overwrites size property | size |
| faceColors | \(_Color4\[\]_\)array of 6 Color4, one per box face | Color4\(1,1,1,1\)for each size |
| faceUV | \(_Vector4\[\]_\)array of 6 Vector4, one per box face | UVs\(0,0,1,1\) for each side |
| updatable | \(_boolean_\)true if the mesh is updatable | false |
| sideOrientation | \(_number_\)side orientation | DEFAULTSIDE |

立方体例子

[https://www.babylonjs-playground.com/\#3QW4J1\#1](https://www.babylonjs-playground.com/#3QW4J1#1)

