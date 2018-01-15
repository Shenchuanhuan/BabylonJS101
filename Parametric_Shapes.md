### [原文链接](http://doc.babylonjs.com/babylon101/parametric_shapes)

目录

1.  参数形状101
    1. 折线
        1. 更新选项
        2. 实例选项
2.  下一部分
3.  扩展阅读

### 参数形状101
   
这些形状或网格由参数或者数据来决定。包括线条，一系列线条，丝带，管状....等。在这个课程里，只接触线条，用MeshBuilder的方法来创建。如何创建所有的形状，详见扩展[阅读](http://doc.babylonjs.com/babylon101/parametric_shapes#further_reading)。

### Lines
3D里的线条是由线条片段首尾相连组成的。在3D空间里，线条也被称为一系列的点。
这三个点(0, 0, 0),(0, 1, 1), (0, 1, 0)会形成两条线片段。
这些具有方向矢量的点在Babylon.js里构成了Vector3对象，然后放入一个数组中被传递给_CreateLines_方法。

```javascript
var myPoints = [];

var point1 = new BABYLON.Vector3(0, 0, 0);
myPoints.push(point1);
var point2 = new BABYLON.Vector3(0, 1, 1);
myPoints.push(point2);
var point3 = new BABYLON.Vector3(0, 1, 0);
myPoints.push(point3);

//or possible the alternative

var myPoints = [
    new BABYLON.Vector3(0, 0, 0),
    new BABYLON.Vector3(0, 1, 1),
    new BABYLON.Vector3(0, 1, 0)
];
```
然后含有points的数组以对象的形式({})传给_CreateLines_方法。

```javascript
var lines = BABYLON.MeshBuilder.CreateLines('lines', { points: myPoints }, scene);
```
[例子](https://www.babylonjs-playground.com/#165IV6#60)

[螺旋状线条例子](https://www.babylonjs-playground.com/#165IV6#61)

你可以用虚线来创建，还可以通过参数来添加数字。
[例子](https://www.babylonjs-playground.com/#165IV6#62)


_CreateLines_的option配置


| **option** | value | default value |
| :--- | :--- | :--- |
| points | \(_Vector3\[\]_\)array of Vector3, the path of the line REQUIRED |  |
| updatable | \(_boolean_\)true if the mesh is updatable | false |
| instance | \(_LineMesh_\)an instance of a line mesh to be updated | null |
| colors | \(_Color4\[\]_\)array of Color4, each point color | null |
| useVertexColor | \(_boolean_\)true if the alpha value of the former array must de used | false |

_CreateDashedLines_的option配置

| **option** | value | default value |
| :--- | :--- | :--- |
| points | \(_Vector3\[\]_\)array of Vector3, the path of the line REQUIRED |  |
| dashSize | \(_Color4\[\]_\)size of the dashes | 3 |
| gapSize | \(_Color4\[\]_\)size of the gaps | 1 |
| dashBn | \(_Color4\[\]_\)intended number of dashes | 200 |
| updatable | \(_boolean_\)true if the mesh is updatable | false |
| instance | \(_LineMesh_\)an instance of a line mesh to be updated | null |

### 更新选项
线状和虚线都有更新选项。当这个选项为true时，顶点会时实响应数据来改变线条路径。更多详见[这里](http://doc.babylonjs.com/how_to/updating_vertices)

### 实例选项
线条还有一个可选选项。这个参数允许你传入一组新的坐标点来有选择性的更新线段路径。但如果要使用这个参数，在创建线段的时候一定要设置`updatable`选项为`true`，并且将已创建的线段作为实例参数传入。如下例：
```javascript
//create lines
var lines = BABYLON.MeshBuilder.CreateLines("lines", { points: myArray, updatable: true }, scene);

// updates the existing instance of lines: no need for the parameter scene here
lines = BABYLON.MeshBuilder.CreateLines("lines", {points: myNewArray, instance: lines});
```
[螺旋状线条例子](https://www.babylonjs-playground.com/#165IV6#63)

大多数参数形状都有_instance_这个参数，但一些没有的形状也可以用这种方式来更新mesh。

### 下一步
在之前的部分，关于设置形状，你可以看到当它们被创建的时候总是在中心点。同样的，参数形状也是如此。那么现在开始移动这些物体到它们需要的位置并且旋转和缩放。
准备好了吗?好了就请看这[位置，角度和缩放](http://doc.babylonjs.com/babylon101/position)

### 扩展阅读
[如何用MeshBuilder方法创建不规则形状](http://doc.babylonjs.com/how_to/parametric_shapes)
[如何用Legacy方法创建不规则形状](http://doc.babylonjs.com/how_to/legacy_param)
[新旧方法的优缺点](http://doc.babylonjs.com/features/shapes#ways-of-creating-a-predefined-mesh)