---
title: k8s之minikube
date: 2022-03-25 16:16:04
tags: k8s
---

## minikube
一个node运行了一个master 和 一个worker在一个节点上方便本地测试
## kubectl
command line tool 与 k8s中的api server 联系,简单说管理工具。不仅只在minikube中使用,也可以在其它k8s集群中使用.

## minikube在mac中安装使用

```shell
brew install hyperkit //先安装hyperkit
brew install minikube //安装完成后
minikube start --vm-driver=hyperkit //启动
//创建deployment
kubectl create deployment nginx-depi --image=nginx
kubectl get pod
kubectl get replicaset
kubectl logs [podname]
kubectl describe pod [pod name]
//进入容器
kubectl exec -it mongo-depl-85ddc6d66-xn24j -- bin/bash
//删除deployment
kubectl delete deployment mongo-depl
kubectl apply -f filename
```
> 抽象关系：deployment > replicaset > all replicas . pod > container
