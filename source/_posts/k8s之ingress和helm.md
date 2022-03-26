---
title: k8s之ingress和helm
date: 2022-03-26 17:02:25
tags: k8s
---
## ingress
简单说就是nginx将域名解析到具体的服务,也就是说在服务的上层
### ingress controller
1. 指定所有的解析规则
2. 管理指向
3. 集群的入口点

安装ingress controller

` minikube addons enable ingress`

会自动开启k8s的nginx版本的ingress controller

ingress默认后端 如:default-http-backend:80
可以用来自定义一些错误页面

# Helm
## helm的作用
1. k8s的包管理器，helm charts 就是yaml文件 helm管理的包
2. 模板引擎，即将一些公共的变量如版本号，镜像版本号，使用helm登记，这样只需修改helm中的变量可以将yaml文件中所有登记的变量修改
3. 将同一程序部署在不同开发环境的集群