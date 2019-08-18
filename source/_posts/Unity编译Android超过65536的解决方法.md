---
title: Unity编译Android超过65536的解决方法
date: 2019-07-10 14:23:44
tags:
- Unity 
- Android
categories: U3D
halftitle: unity-android65536
---
Android开发中有对APK的方法数量做限制，不能超过65536.如果超过了该数目，会遇到如下异常：
`Conversion to Dalvikformat failed:Unable toexecute dex: method ID not in [0, 0xffff]: 65536`
#### 解决方案如下：
1、在Android工程的build.gradle中启用MultiDex并包含MultiDex支持
``` java
defaultConfig 
{
    multiDexEnabled true
}

dependencies 
{ 
    compile 'com.android.support:multidex:1.0.1' 
}
```
重新Build一下工程或者MakeModule一下模块，目的是让配置生效
2、在Android工程的application中重写一下attachBaseContext
<!--more-->
``` java
@Overrideprotected   
void attachBaseContext(Context base) 
{                  
    super.attachBaseContext(base);                  
    MultiDex.install(this); 
}
```
3、在Unity的Android打包设置(File->Build Settings->Player Settings)中勾选`Custom Gradle Template`这时候会在Plugins/Android文件夹下出现mainTemplate.gradle在下面这些地方添加代码
``` java
defaultConfig 
{
    multiDexEnabled true
    target SdkVersion 
    **TARGETSDKVERSION**
}

dependencies
{ 
    compile 'com.android.support:multidex:1.0.1'
}
```
**在构建流程中出现这种问题，根据提示我们大概明白这是方法数过大导致的，而这些方法是存在于编译后的.class文件中的，而.class最后要存在于dex文件中，单个dex的方法或者字段数量不能超过65536所以会报错。完成以上配置重新打包生成的jar包就不会放在一个.class文件里面了，而是分成很多个.class文件根据生成的清单进行引用。**

