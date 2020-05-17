---
layout: post
title: "The Google File System"
date: 2020-05-17
categories: wiki
tags: [paper]
---

`GHEMAWAT, Sanjay; GOBIOFF, Howard; LEUNG, Shun-Tak. The Google file system. In: Proceedings of the nineteenth ACM symposium on Operating systems principles. 2003. p. 29-43.`

## Introduction

### Difference points in design space

  1. Component failure는 예외적인 상황이 아니라 항상 있는 일이다.  
    파일 시스템은 수백 ~ 수천 개의 storage machine으로 이루어져 있고, 비슷한 수의 client와 상호작용한다. 이 정도 규모에서는, 어느 순간에든 다양한 이유로 제대로 동작하지 않는 component가 항상 있다.  
    그러므로 constant monitoring, error detection, fault tolerence, automatic recovery가 반드시 시스템에 포함되어야 한다.

  2. 파일의 크기가 매우 크다.  
    급속도로 커지는 TB 단위의 데이터셋을 관리하는 시스템을 KB-단위로 관리하기는 너무 크다. 그래서 design assumptions, parameters (예를 들어 I/O operation이나 block 크기 등) 를 제고해야 했다.

  3. 대부분의 데이터 변경은 append로만 일어난다. Random write는 거의 발생하지 않는다.  
    한 번 쓰여진 후에 파일들은 거의 읽히기만 하며, 그것도 앞에서부터 순차적으로 일어난다.  
    그래서 performance optimization, atomicity guarantee를 할 때는 appending에 초점을 맞췄다.

  4. File system API와 applications를 같이 설계함으로서 유연성을 증가시켰다.  
    Atomic appending operation을 도입하여 여러 client들이, 따로 동기화할 필요 없이 같은 파일에 동시에 append할 수 있도록 하였다.  
    (자세한 얘기는 이후에 설명)
