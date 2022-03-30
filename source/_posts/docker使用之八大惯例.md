---
title: docker使用之八大惯例
date: 2022-03-30 22:37:01
tags: docker
---

# docker使用之八大惯例手法

## 1. 使用官方镜像作为基础镜像

## 2. 指定镜像版本 如: FROM node:17.0.1

## 3. 尽量使用体积较小的镜像如: FROM node:17.0.1-alpine

## 4. 优化缓存每一层命令生成的容器镜像
bad案例:
```
FROM node:17.0.1-alpine //from cache
WORKDIR /app    //from cache
COPY myapp /app   //每一次改动代码就会更新镜像不使用缓存
RUN npm install --production
CMD['node','src/index.js']
```
> 每当有一层的镜像改变，则接下来的layer都需要重新生成,即不走缓存

优化后:
```
FROM node:17.0.1-alpine //from cache
WORKDIR /app    //from cache
COPY package.json package-lock.json .   //每一次改动代码就会更新镜像不使用缓存
RUN npm install --production
COPY myapp /app
CMD['node','src/index.js']
```
如此只有在package.json发生改变时，才会不走缓存 代码发生改变时，只有2层layer不走缓存

> 总结: 将dockerfile的命令排序,使之顺序为从上往下为最不经常改变layer的命令到最经常改变layer的命令

## 5. 使用.dockerignore文件 忽略一些不必要添加进来的文件
.git 

.cache

## 6. 使用multi-stage 分割 构建镜像和运行镜像
例如:
```dockerfile
#build stage
FROM mave as build
WORKDIR /app
COPY myapp /app
RUN maven packge
#run stage
FROM tomcat
COPY --from=build /app/target/file.war /usr/local/tomcat/file.war
...
```
> 最以最后的FROM为基本镜像

## 7. 使用最小权限的用户
```dockerfile
RUN groupadd -r tom && useradd -g tom tom
RUN chmod -R tom:tom /app
USER tom
```
> 一些官方镜像有默认的用户

## 8. 使用docker scan 检查镜像
```shell
docker login
...
docker scan myapp:1.0
```