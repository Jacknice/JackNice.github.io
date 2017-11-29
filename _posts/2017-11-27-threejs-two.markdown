---
layout: post
title:  "three.js-第二篇（矩阵变换）"
date:   2017-02-11 
categories: threejs
tags: threejs
excerpt: Three.js 利用矩阵编码描述3D转换--转换(位置),旋转和缩放.对于每一个基于Object3D的矩阵(matrix)实例对象都会存储一个位置，旋转和缩放.这篇文档主要描述如何更新一个对象的变换.
author: YuKang
---

* content
{:toc}

Three.js 利用矩阵编码描述3D转换--转换(位置),旋转和缩放.对于每一个基于Object3D的矩阵(matrix)实例对象都会存储一个位置，旋转和缩放.这篇文档主要描述如何更新一个对象的变换.

### 便利性和矩阵的自动更新(matrixAutoUpdate)
#### 这里有两种方式更新对象的转换：

修改对象的位置,四元素,和缩放属性,然后让Three.js根据这些新的数据重新计算矩阵:
```
object.position.copy(start_position);
object.quaternion.copy(quaternion);
```
默认情况下,matrixAutoUpdate属性是设置为true的，然后矩阵就会自动进行重新计算.如果是静态对象，或者当重新计算的时候你希望手动进行操作,通过设置matrixAutoUpdate为false可以获得更好的性能：
```
object.matrixAutoUpdate = false;
```
并在更改任何属性后，手动更新矩阵:
```
object.updateMatrix();
```
直接修改对象的矩阵.Matrix4这个类有多种方法来进行修改矩阵：
```
object.matrix.setRotationFromQuaternion(quaternion);
object.matrix.setPosition(start_position);
object.matrixAutoUpdate = false;
```
在这里请注意，matrixAutoUpdate必须设置为false，并确保不要调用updateMatrix方法.调用updateMatrix将会影响到矩阵的手动更改，以及影响基于位置、缩放等的矩阵重新计算.
### 对象和世界矩阵
对象的矩阵(matrix)存储对象相对于对象的父对象(parent)的转换；在世界坐标系到对象的转换，您必须访问对象的Object3D.matrixWorld
当父或子对象的转换改变,你可以调用updateMatrixWorld()对子对象的matrixWorld进行更新.

### 旋转和四元
Three.js 提供两种方式来进行3D旋转：欧拉角(Euler angles)和四元素(Quaternions),以及两者之间的相互转换方法.欧拉角又叫做“万向节锁，“在某些配置情况下回失去一个自由度（如防止物体被绕一个轴）。因此，旋转对象总是存储在对象可能所处的四元数中.
以前的版本库包含一个useQuaternion属性,当设置为false的时候，会导致物体的矩阵是由欧拉角计算.这种做法已经是不被采用了的，相反，你应该在将更新的四元上使用setRotationFromEuler方法。
