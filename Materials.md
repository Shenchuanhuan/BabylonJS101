### [原文链接](http://doc.babylonjs.com/babylon101/materials)

目录

1.  材料
    1. 
    2. 颜色
        1. 
    3. 纹理
    
    6. 下一部分
    
2.  扩展阅读

### 材料 
你可以用颜色材料和纹理材料来包裹你的物体，并且需要灯光来展示。无论多少风格，一种材料都可以覆盖。

### 光感
无论材料是颜色或者是纹理，它都能对灯光做出不同的反应。
    1. Diffuse - 正常灯光视觉
    2. Specular - 高光下视觉
    3. Emissive - 放射灯光视觉
    4. Ambient - 阴影色贴图视觉
`Diffuse`和`Specular`需要构建一个光源。
阴影色贴图需要设置场景贴图，给一个背影灯光。

```javascript
    scene.ambientColor = new BABYLON.Color3(1, 1, 1);
```

1. 透明 - 材质的透明度可以被设定，并且图片的透明部分也可以应用，因此相应部分的材质会不可见。这样做需要设置`alpha`属性。

### 颜色
创建一种材料使用：
```javascript
    var myMaterial = new BABYLON.StandarMaterial("myMaterial", scene);
```
设置材料的颜色的时候可以只用一种或多种或者所有_diffuseColor_, _specularColor_, _emissiveColor_和_ambientColor_。记住，_ambientColor_只有当设置了`ambient color`的时候才会生效。

```javascript
    var myMaterial = new BABYLON.StandardMaterial("myMaterial", scene);

    myMaterial.diffuseColor = new BABYLON.Color3(1, 0, 1);
    myMaterial.specularColor = new BABYLON.Color3(0.5, 0.6, 0.87);
    myMaterial.emissiveColor = new BABYLON.Color3(1, 1, 1);
    myMaterial.ambientColor = new BABYLON.Color3(0.23, 0.98, 0.53);

    mesh.material = myMaterial;
```
### Diffuse Color例子
[例子](http://www.babylonjs-playground.com/#20OAV9#10)


|      |      |
| :--- | :--- |
| 黄色材料 | 紫色材料 |
| 蓝绿色材料 | 白色材料 |

反应白色、红色、绿色和蓝色的漫反射光线。注意视角下的光线。

### Ambient Color例子
[例子](http://www.babylonjs-playground.com/#20OAV9#14)

所有的球体都被同样的`hemisphereic light`照射，用_diffuse_红色和_groundColor_绿色。第一个球体没有使用`ambient color`，中间用了红色的`ambient color`作材料，右边的材料用的绿色的`ambient color`。场景的`ambient color`必须设置，且为白色。 