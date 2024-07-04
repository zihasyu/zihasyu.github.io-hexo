---
title: Chunking summary
date: 2024-07-04 19:48:04
tags:
  - Chunking
  - Compression
  - Storage system
  - Operating system
  - Computer science
categories:
  - Compression algorithms
---

 **Content-Defined Chunking**
#### Idea
最初的，基于内容分块，可变长，能解决边界偏移的问题。
#### The work of this method：
##### fp的计算方式：
新块（E,1字节）进入窗口时加上他的哈希值，且减去最高有效位（A,1字节）的哈希值
![[Pasted image 20240604101310.png]]
##### 断点的确定方式
	fp&mask == 0
#### Readme
mask可以随便取，但尽量在高32位，1的位数决定预计块的大小，例如13个1代表8KB。因为fp为滑窗内所有块哈希值的加和，所以fp的每一位都是有效位。