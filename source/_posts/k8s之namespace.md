---
title: k8s之namespace
date: 2022-03-26 15:45:02
tags: k8s
---
# Namespace
默认有4个namespace
1. kube-system 不能动kube内部的namespace
2. kube-publice 存储configmap之类数据的namespace
3. kube-node-release 节点信息namespace
4. default 默认namespace

### 为什么使用namespace
1. 将资源分组
2. 将不同项目组分离
3. 复用公共资源
4. 多版本服务

> 每个namespace 必须拥有自己的configmap,secretmap

> volume和node 组件不能放在namespace下
### 创建namespace
`kubectl create namespace my-space`

`kubectl apply -f mysql.yamel --namespace=myns`

切换默认命名空间

```shell
brew install kubectx
kubens
kubens my-ns
```
