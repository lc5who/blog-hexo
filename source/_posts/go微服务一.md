---
title: go微服务一
date: 2022-03-04 23:54:10
tags: [微服务,go]
type: 微服务
---
# Go使用Protobuf

---

## 第一步
### 安装protobuf编译器
## 第二步
### 配置环境变量或将编译器拷贝置环境变量中某个文件夹
## 第三步
### 安装Go的protobuf的包
> 这一步记得把下载下来的proto-gen-go.exe目录也就是gopath添加到环境变量否则会生成失败
---
> 生成命令
```Shell  
 protoc --go_out=. test.proto
``` 
--- 
## 基本用法:
- protobuf 文件格式为 **.proto** 后缀
- 消息的定义:
    - required:必须包含
    - optional:可选
    - repeated: 可重复，可为0次
```protobuf
syntax="proto2";
option go_package = "./order/;order";

message Order{
  required int32 orderId = 1;//1代表字段顺序
  required int32 num = 2;
  required string ts = 3;
  }
``` 
### 序列化与反序列化
```go
    msg_order := &order.Order{
		OrderId: proto.Int32(1),
		Num:     proto.Int32(2),
		Ts:      proto.String("111"),
	}
	msgData,err := proto.Marshal(msg_order)
	if err != nil {
		panic(err)
		return
	}
	fmt.Println(msgData)
	msg :=order.Order{}
	err = proto.Unmarshal(msgData,&msg)
	if err != nil {
		panic(err)
		os.Exit(0)
	}
	fmt.Println(msg.GetOrderId())
	fmt.Println(msg.GetNum())
	fmt.Println(msg.GetTs())
``` 



    



