---
title: docker搭建consul多节点
date: 2022-03-05 15:47:40
tags: 微服务
---

# consul学习笔记

## windows下docker搭建consul多节点
>  在docker网站上有列出详细命令
```shell 
docker run -d --name=dev-consul -p 8500:8500-e CONSUL_BIND_INTERFACE=eth0 consul
```
>这里新增一个-p参数，这样就可以在本机用浏览器访问consul开放的8500的ui界面

### 增加第二个第三个节点
```shell 
docker run -d -e CONSUL_BIND_INTERFACE=eth0 consul agent -dev -join=172.17.0.3
docker run -d -e CONSUL_BIND_INTERFACE=eth0 consul agent -dev -join=172.17.0.3
consul members
//配置客户端
docker run -d -e CONSUL_BIND_INTERFACE='eth0' --name=consul_server_5 consul agent -client -node=5 -join='172.17.0.2' -client='0.0.0.0'
```
#### 这样就搭建了3个节点,再利用consul members 查看 已经有3个server client端ok了
---
