---
layout: post
title:  "Oculus Unity Step Two"
date:   2022-11-25
categories: VR, Unity, Oculus Quest2
comments: true
---

# Oculus Unity
```
上一次开发中，使用的是OVRCameraRig，但是缺少一些Touch的控制，这一次，需要做出使用控制抓住物体的功能：Hand Grab
```


## OVRPlayerController
----
### Setup
- 添加*OVRPlayerController* prefab到Scene中
- 修改*OVRPlayerController*下的*OVRCameraRig*的*Tracking Origin*属性为`Floor Level`
- 修改*OVRPlayerController*的Character Controller属性的*Radius*为`0.25`

<img src="/files/20221125105803.png"/>


## OVRControllerPrefab
---

### Setup
- 添加*OVRControllerPrefab*到*LeftControllerAnchor*和*RightControllerAnchor*下
- <img src="/files/20221125110104.png"/>
- 点击*OVRControllerPrefab*，到`inspector`窗口修改*OVR Controller Helper*脚本的`Controller`属性，左控制器和右控制器分别修改为`L Touch`和`R Touch`


## OVRGrabber
---
```
重头戏来了，抓取物体完全靠他和他兄弟: OVRGrabbable
```

### Setup
- 添加*OVRGrabber*组件到左右控制器的*OVRController*里，选中*Parent Held Object*
- 添加*Rigidbody*组件到左右控制器的*OVRController*里，并修改它的属性：取消`Use Gravity`，选中`Kinematic`
- 把*Grip Transform*设置为`OVRPlayerController`游戏对象
- 把*Grip Volumes*添加一个Element，也设置为`OVRPlayerController`游戏对象
- 并修改*OVRController*的*Sphere Collider*的Radius属性值为: 0.075, 并勾选`Is Trigger`
- <img src="/files/20221125110740.png"/>

## OVRGrabbable

### Setup
- 在Scene里添加一个Sphere, 这是我们需要抓取的物体
- 给他添加上*OVRGrabbable*和*Rigidbody*组件
- <img src="/files/20221125111709.png"/>

## Build And Run


## 引用
- [Oculus SDK Unity Setup](https://gist.github.com/neogeek/f463d1f4d6d4fb85ad497c128fca1ca7)