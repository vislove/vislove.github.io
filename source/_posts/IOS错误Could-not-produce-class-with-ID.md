---
title: Unity发布IOS错误Could not produce class with ID
date: 2019-08-10 19:06:11
tags:
- Unity
categories: 
- U3D
halftitle: 
- Unity-IOS-Could-not-produce-class-with-ID
---
## 问题
**有时候Unity发布在IOS上会出现：`Could not produce class with ID XXX.This could be caused by a class being stripped from the build even though it is needed. Try disabling 'Strip Engine Code' inPlayer Settings.:<LoadWWWIEnumerator>c__Iterator99:MoveNext()`的错误。**
## 原因及解决办法
**原因是勾选了`Strip Engine Code`，所以我们要做的就是在`Player Setting – Other Setting`，去掉勾选 `Strip Engine`**
## 如果要Strip Engine
**如果要Strip Engine，那就需要把不想被strip的添加进来。**<br>
1、新建link.xml放在Assets目录下，里面添加不想被strip的dll的名字<br>
ID查询： https://docs.unity3d.com/Manual/ClassIDReference.html <br>
下面是导入高通Vuforia之后，SDK中默认的link.xml的内容
<!--more-->
``` xml
<linker>
    <!-- The following assemblies contain namespaces that should be fully preserved
         even when assembly stripping is used. Not excluding the assemblies below from
         stripping can result in crashes or various exceptions. -->
    <assembly fullname="Vuforia.UnityExtensions">
        <namespace fullname="Vuforia" preserve="all"/>
    </assembly>
    <assembly fullname="System">
        <namespace fullname="System.Runtime.InteropServices" preserve="all"/>
        <namespace fullname="System.Collections.Generic;" preserve="all"/>
        <namespace fullname="System.Linq;" preserve="all"/>
        <namespace fullname="System.Text.RegularExpressions;" preserve="all"/>
        <namespace fullname="System.IO;" preserve="all"/>
        <namespace fullname="System;" preserve="all"/>
    </assembly>
</linker>
```
如果提示的ID的是Editor的，比如 AnimatorController(ID 91)属于Editor包里的，不能用link.xm加回来，可以在Resource下建一个空的prefab,在上面挂一个AnimatorController，打包时留下这个prefab就可以确保这个类不被strip掉了。
参考：https://forum.unity3d.com/threads/could-not-produce-class-with-id-91-ios.267548/
## Unity的默认值
以Unity5.3.5为例ios平台，默认勾选了 Strip Engine Code，且Script Background为I2CPP<br>
android平台，默认disabled Strip Engine Code，且Script Background为Mono2x

