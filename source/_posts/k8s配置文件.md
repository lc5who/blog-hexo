---
title: k8s配置文件
date: 2022-03-26 11:17:32
tags: k8s
---

## k8s之配置文件
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.16
        resources:
          limits:
            memory: "128Mi"
            cpu: "500m"
        ports:
        - containerPort: 80
```
1. metadata
2. specification
3. status(由k8s管理，从etcd中获取）

> kubectl get pod -o wide 查看service是否与deployment匹配
