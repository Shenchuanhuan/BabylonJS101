### [原文链接](http://doc.babylonjs.com/babylon101/position)

目录

1.  位置、旋转和缩放
    1. 参考坐标系
    2. 向量
    3. 
    4. 位置
    5. 旋转
        1. 约定一：局部坐标系
        2. 约定二：全局坐标系
        3. 小结
    6. 有序旋转
    7. 缩放
    8. 下一部分
2.  扩展阅读

### 位置、旋转和缩放
101教程仅讨论物体的定位、旋转和缩放。[进一步阅读](http://doc.babylonjs.com/babylon101/position#further-reading)里会向你展示一系列给出的移动和旋转的方法。
无论使用什么方法，都需要一种参考坐标系，物体的定位、旋转和缩放都是根据这个坐标系来进行的。这种抽象可以用下面的*Pilot*（一种非对称形状）来帮助理解。
<br/>
![the Pilot](https://i.loli.net/2018/01/15/5a5c2be4d947a.jpg)

参考坐标系
在BABYLON里有两种参考坐标系，全局坐标系(*world axes*)和局部坐标系(*local axes*)。全局坐标系的源点不会改变。

在所有的图表和playgrounds(网站)里，X轴是红色，Y轴是绿色，Z轴是蓝色。

当物体被创建的时候他们的中心点就是全局坐标系的中心点，他们的位置移动也是相对于全局坐标系的。

*局部坐标系*是跟随物体移动而移动的。*局部坐标系*的中心点总是在物体中心点，不论物体的位置移动到哪。通常物体的中心旋转和放大是围绕*局部坐标系*的中心点进行的，但可以通过使用`TransformNode`或者`matrix`来设置[轴中心点](http://doc.babylonjs.com/how_to/pivots)来改变它们。

### 向量
位置、角度和大小是通过一个三维向量用`new BABYLON.Vector3(x,y,z)`来设置，并且可以分开单独设置。

### The Pilot
随着它的创建，pilot的位置处于全局坐标系的中心位置，所有轴的旋转角度都是0，缩放值为1。同时，全局坐标系与局部坐标系在这个时候是重叠的（即相同的）。


<br/>
![pilot.jpg](https://i.loli.net/2018/01/15/5a5c47fcdfa85.jpg)。

### 位置(Position)
*位置*参照全局坐标系，用`vector(x,y,z)`来设置pilot的位置。*局部坐标系*跟着pilot移动。
```javascript
    pilot.position = new BABLYON.Vector3(2, 3, 4);
```
或者 分开设置：

```javascript
    pilot.position.x = 2;
    pilot.position.y = 3;
    pilot.position.z = 4;
```
局部坐标和全局坐标仍然保持相同的角度。
<br/>
![pilot.jpg](https://i.loli.net/2018/01/15/5a5c4ea3bea44.jpg)
[上例链接](https://www.babylonjs-playground.com/#UBWFJT#2)

### 旋转(Rotation)
*注意* 在3D空间里，旋转总是棘手的。旋转会改变物体的方向并且你需要知道用的是哪个参考坐标系。在3D模型里有很多不同的约定来进行旋转。关于这些BABYLON里的约定的更多细节，详见[Applying Rotatings Convention BJS](http://doc.babylonjs.com/How_To/rotation_conventions)not found!

在BABLYONJS里，通过下面的方法设置旋转角度：

```javascript
    pilot.rotation = new BABYLON.Vector3(alpha, beta, gamma);
```

或者

```javascript
    pilot.rotation.x = alpha;  // rotation around x axis
    pilot.rotation.y = beta;   // rotation around y axis
    pilot.rotation.z = gamma;  // rotation around z axis
```
这里`alpha`，`beta`和`gamma`角度用的是弧度。

*停一来想一想:* 三个轴分别被给予三个不同的角度，你先要弄清楚： ’它们是按什么顺序？参考哪个坐标系？在哪个方向？‘
下面的两种约定都有在BABYLON里应用，无论是用哪一种，得到的结果都一样。

*约定1 - 局部坐标系*
局部坐标系使用`rotation`时，是按照y, x, z的顺序，参考局部坐标系进行旋转的。直视相对坐标轴的时候，所有的旋转都是逆时针方向的。

下面几幅图按顺序分别是初始化、y轴旋转π/2、x轴旋转π/2、z轴旋转π/2：
<br/>
![初始化](https://i.loli.net/2018/01/15/5a5c571b7655f.jpg)
![y轴旋转Math.PI/2](https://i.loli.net/2018/01/15/5a5c571b7fb2a.jpg)
![x轴旋转Math.PI/2](https://i.loli.net/2018/01/15/5a5c571b81413.jpg)
![z轴旋转Math.PI/2](https://i.loli.net/2018/01/15/5a5c571b89dd3.jpg)
图中小的坐标轴是全局坐标轴。
<br/>

*约定2 - 全局坐标系*
相对于约定1来说，旋转的中心并没有变化，但轴的旋转发生了变化。
全局坐标系使用`rotation`来旋转物体时，物体是围绕局部坐标系中心点与旋转中心的重合点按Z、X、Y的顺序要旋转。所有的旋转都是逆时针方向的。
下面几幅图按顺序分别是初始化、z轴旋转π/2、x轴旋转π/2、y轴旋转π/2：
<br/>
[![pilot1.jpg](https://i.loli.net/2018/01/15/5a5c63dc70382.jpg)](https://i.loli.net/2018/01/15/5a5c63dc70382.jpg)
[![pilot2.jpg](https://i.loli.net/2018/01/15/5a5c63dc7a9e6.jpg)](https://i.loli.net/2018/01/15/5a5c63dc7a9e6.jpg)
[![pilot3.jpg](https://i.loli.net/2018/01/15/5a5c63dc7c2a3.jpg)](https://i.loli.net/2018/01/15/5a5c63dc7c2a3.jpg)
[![pilot4.jpg](https://i.loli.net/2018/01/15/5a5c63dc85f58.jpg)](https://i.loli.net/2018/01/15/5a5c63dc85f58.jpg)
<br/>

[上例在playground](http://www.babylonjs-playground.com/#1ZMJQV#2)

### 小结
无论你想用哪种方式来旋转，结果都是一样的，下面的输出都是相同的：

```javascript
    pilot.rotation = new BABYLON.Vector3(alpha, beta, gamma);

    pilot.rotation.x = alpha;
    pilot.rotation.y = beta;
    pilot.rotation.z = gamma;

    pilot.rotation.z = gamma;
    pilot.rotation.x = alpha;
    pilot.rotation.y = beta;

    pilot.rotation.y = beta;
    pilot.rotation.z = gamma;
    pilot.rotation.x = alpha;
```
[例子：关于位移、缩放和旋转的盒子](http://www.babylonjs-playground.com/?3)

### 有序旋转
现在的问题是，如果你想按照x、y、z的顺序进行旋转，该怎么办呢？
如果在全局坐标系里你使用[旋转方法](http://doc.babylonjs.com/features/position,_rotation,_scaling),有`rotate`和`addRotation`两个方法可用。
你可以链式顺序调用`addRotation`方法来完成。这个方法提供了一种从头到尾在一个轴上的旋转，例如：
```javascript
    mesh.addRotation(Math.PI/2, 0, 0).addRotation(0, Math.PI/2, 0).addRotation(0, 0, Math.PI/2);
```
下面的图按序展示了上面的结果：
<br/>
[![pilot1.jpg](https://i.loli.net/2018/01/15/5a5c6c89786ef.jpg)](https://i.loli.net/2018/01/15/5a5c6c89786ef.jpg)
[![pilot2.jpg](https://i.loli.net/2018/01/15/5a5c6c8983124.jpg)](https://i.loli.net/2018/01/15/5a5c6c8983124.jpg)
[![pilot3.jpg](https://i.loli.net/2018/01/15/5a5c6c8984bee.jpg)](https://i.loli.net/2018/01/15/5a5c6c8984bee.jpg)
[![pilot4.jpg](https://i.loli.net/2018/01/15/5a5c6c898644a.jpg)](https://i.loli.net/2018/01/15/5a5c6c898644a.jpg)
小的坐标轴是全局坐标系。

<!-- 大体来说`mesh.addRotation(alpha, beta, gamma)`需要至少两个`alpha, beta, gamma`清零。 -->

### 缩放
在局部坐标系里的缩放用的是：
```javascript
    mesh.scaling = new BABYLON.Vector3(scale_x, scale_y, scale_z);
```
或者 单独设置：

```javascript
    mesh.scaling.y = 5;
```
下面的图像显示了一个长方体关于z轴旋转并且在y轴方向的缩放。
<br/>
![scaling1.jpg](https://i.loli.net/2018/01/15/5a5c6e4399dfe.jpg)

### 下一步
现在你知道怎么在场景里创建和移动物体，但你所有的网格都是相同的'皮肤'。下面，学习关于[材料的内容](http://doc.babylonjs.com/babylon101/materials)
### 扩展阅读
[旋转和移动概略](http://doc.babylonjs.com/features/position,_rotation,_scaling)