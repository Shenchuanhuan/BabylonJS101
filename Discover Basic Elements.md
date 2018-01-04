

[原文链接](http://doc.babylonjs.com/babylon101/first)

目录：

1. 设置形状101
   1. MeshBuilder 方法
      1. 盒状
      2. 球状
      3. 平面
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


[立方体例子](https://www.babylonjs-playground.com/#3QW4J1#1)


#### Sphere

```javascript
var sphere = BABYLON.MeshBuilder.CreateSphere('sphere', {}, scene);

var mySphere = BABYLON.MeshBuilder.CreateSphere('mySphere', {diameter: 2, diameteX: 3}, scene);
```

| **option** | value | default value |
| :--- | :--- | :--- |
| segments | \(_number_\)number of horizontal segments | 32 |
| diameter | \(_number_\)diameter of the sphere | 1 |
| diameterX | \(_number_\)diameter on X axis, overwrites diameter property | diameter |
| diameterY | \(_number_\)diameter on Y axis, overwrites diameter property | diameter |
| diameterZ | \(_number_\)diameter on Z axis, overwrites diameter property | diameter |
| arc | \(_number_\)ratio of the circumference (latitude) between 0 and 1 | 1 |
| slice | \(_boolean_\)ratio of the height (longitude) between 0 and 1 | 1 |
| updatable | \(_number_\)true if the mesh is updatable | false |
| sideOrientation | \(_number_\)side orientation | DEFAULTSIDE |

[椭圆体例子](https://www.babylonjs-playground.com/#K6M44R)


#### Plane

```javascript
var plane = BABYLON.MeshBuilder.CreatePlane("plane", {}, scene);

var myPlane = BABYLON.MeshBuilder.CreatePlane("myPlane", {width: 5, height: 2}, scene);
```

| **option** | value | default value |
| :--- | :--- | :--- |
| size | \(_number_\)size of the plane | 1 |
| width | \(_number_\)size of the width | size |
| height | \(_number_\)size of the height | size |
| updatable | \(_boolean_\)true if the mesh is updatable | false |
| sideOrientation | \(_number_\)side orientation | DEFAULTSIDE |
| frontUVs | \(_Vector4\[\]_\)array of Vector4, **ONLY WHEN sideOrientation:BABYLON.Mesh.DOUBLESIDE set** | Vector4\(0,0,1,1\) |
| backUVs | \(_Vector4\[\]_\)array of Vector4, **ONLY WHEN sideOrientation:BABYLON.Mesh.DOUBLESIDE set** | Vector4\(1,1,1,1\) |
| sourcePlane | \(_plane_\)source plane (maths) the mesh will be transformed to | null |


[平面例子](https://www.babylonjs-playground.com/#K6M44R)

_sourcePlane_是平面里特殊的一种，它提供定位和定向方法。现在假设创建平面时定位使用的方向向量是(0,0,1)。现在你想重新定位到方向向量为(0,-1,1)的位置，那你可以用下面的方式创建一个原始平面：

```javascript
var sourcePlane = new BABYLON.Plane(0, -1, 1, 0);
sourcePlane.normalize();
```
这样就创建了一个以指定方向的精确定位的平面。第四个参数是距离原始点的距离。在这个例子里是0.

[源平面](https://www.babylonjs-playground.com/#LXZPJK#2)

[更多关于源平面的信息]()


### Groud

```javascript
var ground = BABYLON.MeshBuilder.CreateGround('ground', {}, scene);

var myGround = BABYLON.MeshBuilder.CreateGround('myGround', {width: 6, height: 4, subdivisions: 4}, scene);
```

| **option** | value | default value |
| :--- | :--- | :--- |
| width | \(_number_\)size of the width | 1 |
| height | \(_number_\)size of the height | 1 |
| updatable | \(_boolean_\)true if the mesh is updatable | false |
| subdivisions | \(_number_\)number of square subdivisions | 1 |

[场地例子](https://www.babylonjs-playground.com/#MJ6YSM)

[_CreateGroundFromHeightMap_](http://doc.babylonjs.com/babylon101/height_map)是 _CreateGround_方法的一种变异。该方法可以画出波浪起伏的面。

### Face Colors or UV
这个参数仅用于有不同面的形状，比如盒状（球状不能用）。它能给每个面单独着色或贴图。[详细资料看这里](http://doc.babylonjs.com/how_to/createbox_per_face_textures_and_colors)

### Updatable
当网格的updatable参数值为true时，那么这个网格的每个顶点数据实时响应，形状也随之响应变化。[更多详情请看这里](http://doc.babylonjs.com/how_to/updating_vertices)

### Side Orientation
该参数用于决定网格的每一边的视觉效果。

这个参数对应的值有以下四种：
-  BABYLON.Mesh.FRONTSIDE,
-  BABYLON.Mesh.BACKSIDE,
-  BABYLON.Mesh.DOUBLESIDE,
-  BABYLON.Mesh.DEFAULT(默认值，现在等价于FRONTSIDE).

通过左右移动屏幕上的鼠标（指针）可以旋转平面，在下面的例子里，你可以比较一下DEFAULT和DOUBLESIDE.
[DEFAULT](https://www.babylonjs-playground.com/#LXZPJK)

[DOUBLESIDE](https://www.babylonjs-playground.com/#LXZPJK#1)

### Front and Back UV
当一个网格有sideOrientation参数并且对应的值为DOUBLESIDE的时候，它的正面和反面可能展示不同的图像。更多信息详见[如何展示正反面图像](not found)

### Coming Soon
当你创建了一个网格的时候它总是在中心点，并且带着网络线。你会想要给它一个不同的位置和旋转度。[详见](http://doc.babylonjs.com/babylon101/position)

### 下一部分
现在你已经学会画一部分形状了，开始[不常用形状的创建](http://doc.babylonjs.com/babylon101/parametric_shapes)

### 扩展阅读
基础-L1
[如何用MeshBuilder创建形状](http://doc.babylonjs.com/how_to/set_shapes)
[如何用Legacy方法创建形状](http://doc.babylonjs.com/how_to/legacy_set)
[优缺点](http://doc.babylonjs.com/how_to/legacy_set)