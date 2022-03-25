---
title: k8s基本概念
date: 2022-03-25 15:10:49
tags: k8s
---
## k8s基本概念
- ### node
    一台工作节点,一台server
- ### pod
    k8s最小运行单位,包含一个或多个相关的容器
- ### configMap
    配置文件
- ### secret
    存储密码的配置文件
- ### volumes
    k8s组件,硬盘,可持续化存储,可附加在node本地硬盘也可附加在远程存储上,k8s本身不管理数据存储
- ### services
    * 静态ip,访问地址不变
    * 负载均衡 讲请求分发到空闲机器
- ### deployments
    pod容器的创建计划,pod是container的父级,则deployment是pod的父级,可以指定需要创建多少个Pod副本，以及设置配置文件.数据库pod不适用副本,因为数据库pod拥有data,副本会造成数据不一致.
- ### statefulsets
    适用于数据库pod的deployment,但是比较难用，一般将db置于k8s之外
##  k8s集群架构
- ### worker machine
    * 每个node拥有多个pods
    * 每个node都运行了3个处理程序
        * container runtime - 容器运行环境如:docker
        * kubelet - 管理contanier的程序，分配容器内存，cpu之类的工作
        * kybe proxy - 类似调度器
    * worker node做了实际的工作
- ### master node
    * 每个master node都跑了4个程序
    1. api server - cluster gateway 管理接口
    2. scheduler - 调度，从apiServer收集到请求，通过调度器决定何时创建
    3. controller manager - 检测pod的状态，并通知scheduler
    4. etcd - k-v数据存储,存储k8s的数据，app的数据除外
