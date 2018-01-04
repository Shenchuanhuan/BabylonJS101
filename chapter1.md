# 原文链接 [http://doc.babylonjs.com/babylon101/first](http://doc.babylonjs.com/babylon101/first)

目录：

1. 第一步
   1. the Playground
   2. 你自己的HTML
      1. HTML模板
   3. 笔记
2. 第二步
3. 扩展阅读
4. 有用的扩展链接

### 第一步

Babylon.JS是一个用来创建web 3D环境的非常棒的库，它使用的是HTML5的canvas元素。

#### 场景The Playground）

有一种超级快捷方便的方式来创建你自己的场景。创建一个3D场景非常简单，相机、灯光和3D状物体，就完成了。

The Playground 就是网页，它包含所有你构建3D场景所而创造的所有元素或者是已经存在的元素。下面是一个在场景内创建情景模板：

```javascript
var createScene = function() {
    // 创建情景空间
    var scene = new BABYLON.Scene(engine);
    
    //为情景内添加相机并装到canvas上
    var camera = new BABYLON.ArcRotateCamera("Camera", Math.PI/2, MATH.PI/2, 2, BABYLON.Vector3.Zero(), scene);
    camera.attachControl(canvas, true);
    
    //为情景添加灯光
    var light1 = new BABYLON.HemisphericLight("light1", new BABYLON.Vector3(1, 1, 0), scene);
    var light2 = new BABYLON.PointLight("light2", new BABYLON.Vector3(0, 1, -1), scene);
    
    //这是你创建并操作网眼的地方
    var sphere = BABYLON.MeshBuilder.CreateSphere("sphere", {}, scene);
    
    return scene;
    
};
```



