# InputEventPackage


## 概述

Input事件数据包结构。

**相关模块:**

[Input](_input.md)


## 汇总


### Public 属性

  | 名称 | 描述 | 
| -------- | -------- |
| [type](#type) | uint32_t<br/>输入事件的属性&nbsp; | 
| [code](#code) | uint32_t<br/>输入事件的特定编码项&nbsp; | 
| [value](#value) | int32_t<br/>输入事件编码项对应的值&nbsp; | 
| [timestamp](#timestamp) | uint64_t<br/>输入事件对应的时间戳&nbsp; | 


## 类成员变量说明


### code

  
```
uint32_t InputEventPackage::code
```
**描述:**
输入事件的特定编码项


### timestamp

  
```
uint64_t InputEventPackage::timestamp
```
**描述:**
输入事件对应的时间戳


### type

  
```
uint32_t InputEventPackage::type
```
**描述:**
输入事件的属性


### value

  
```
int32_t InputEventPackage::value
```
**描述:**
输入事件编码项对应的值
