### [原文链接](http://doc.babylonjs.com/babylon101/first)

目录：

1. 第一步
   1. 场景（the Playground）
   2. 你自己的HTML
      1. HTML模板
   3. 笔记
2. 下一部分
3. 扩展阅读
4. 有用的扩展链接

### 第一步

Babylon.JS是一个用来创建web 3D环境的非常棒的库，它使用的是HTML5的canvas元素。

#### 场景（The Playground）

有一种超级快捷方便的方式来构建属于你的场景。创建一个3D场景非常简单，准备好相机、灯光和3D物体，就完成了。

你可以在[The Playground](http://www.babylonjs-playground.com/)这个网址上构建你自己的场景，你也可以在这个网站上查看别人构建好的例子。下面是一个在场景内创建情景模板：

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

你需要关心的一切仅仅是场景内的东西。

[以上代码的场景例子](http://www.babylonjs-playground.com/#WG9OY#1)

#### 你自己的HTML

当你写html的时候，需要用script标签把创建场景的方法嵌入HTML页面结构。你需要先加载Babylon.js的javascrpt代码。如果是在平板电脑或者移动端上使用，BabylyJS会使用点触事件代替鼠标事件，因此，PEP同样需要先加载。

之后，在body内添加一个canvas元素用来构建3D场景。在这之前需要先创建BabylonJS引擎。

最后，就是写3D情景的相关代码，让引擎循环渲染情景，并且当浏览器窗口大小发生变化时调整情景大小。

##### HTML模板

```javascript
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">

   <head>
      <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
      <title>Babylon Template</title>

      <style>
        html, body {
            overflow: hidden;
            width: 100%;
            height: 100%;
            margin: 0;
            padding: 0;
        }

        #renderCanvas {
            width: 100%;
            height: 100%;
            touch-action: none;
        }
    </style>

    <script src="https://cdn.babylonjs.com/babylon.js"></script>
    <script src="https://code.jquery.com/pep/0.4.1/pep.js"></script>

   </head>

   <body>

    <canvas id="renderCanvas" touch-action="none"></canvas> //touch-action="none" for best results from PEP

    <script>

            var canvas = document.getElementById("renderCanvas"); // 获取canvas元素

            var engine = new BABYLON.Engine(canvas, true); // 生成BABYLON 3D引擎

            /******* 添加情景创建方法 ******/
            var createScene = function () {

                        // Create the scene space
                        var scene = new BABYLON.Scene(engine);

                        // Add a camera to the scene and attach it to the canvas
                        var camera = new BABYLON.ArcRotateCamera("Camera", Math.PI / 2, Math.PI / 2, 2, BABYLON.Vector3.Zero(), scene);
                        camera.attachControl(canvas, true);

                        // Add lights to the scene
                        var light1 = new BABYLON.HemisphericLight("light1", new BABYLON.Vector3(1, 1, 0), scene);
                        var light2 = new BABYLON.PointLight("light2", new BABYLON.Vector3(0, 1, -1), scene);


                        // Add and manipulate meshes in the scene
                        var sphere = BABYLON.MeshBuilder.CreateSphere("sphere", {diameter:2}, scene);

                        return scene;
                };

                /******* End of the create scene function ******/    

                var scene = createScene(); //调用创建情景方法

            engine.runRenderLoop(function () { // 注册一个渲染循环来重复渲染情景
                scene.render();
            });


            window.addEventListener("resize", function () { // 监听 浏览器窗口和canvas元素的resize事件
                engine.resize();
            });
    </script>

   </body>

</html>
```

#### 注释

1. 以上的例子都用的较新的 `MeshBuilder` 方法来创建形状，。它接受一个可选的变量对象作为参数来设定形状，这比旧的方法 BABYLON.Mesh.Create...要好，旧方法是接收一个参数列表作参数。因为`MeshBuilder`方法是后面出来的新方法，The Playgrounds网站的大部分例子是用的旧方法。
2. 点触事件更推荐用PEP，之前是推荐使用handle.js。两个都能用，但现在已经弃用hand.js。你可能还会在文档里看到hand.js。

### 下一部分

现在你已经准备好进行更深入的学习如何来创建更多形状，比如球体、柱状体、盒状等。阅读[Set Shapes](http://doc.babylonjs.com/babylon101/discover_basic_elements)

### 扩展阅读

[BabylonJS Forum](http://www.html5gamedevs.com/forum/16-babylonjs/ "BabylonJS Forum")

[PEP and hand.js](http://www.html5gamedevs.com/topic/22474-how-does-babylonjs-get-pointer-events-working/#comment-127993)

### 有用的扩展链接

[BabylonJS Main Website](http://www.babylonjs.com/)

[BabylonJS Playground](http://www.babylonjs-playground.com/)

[PEP Github](https://github.com/jquery/PEP)

[hand.js Github](https://github.com/Deltakosh/handjs)

