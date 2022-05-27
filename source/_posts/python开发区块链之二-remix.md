---
title: python开发区块链之二-remix
date: 2022-05-26 10:27:15
tags: ethereum
---

# Lesson 2: Welcome to Remix! Simple Storage

1. Type

    - int/uint
    - Address
    - bytes 

2. function 权限限定词
    - public 公共
    - internal 合约内部的方法可以调用类似protected 默认设为internal
    - external 外部合约才可以调用
    - private  

3. view

    - 返回读取合约的某属性
    - public字段默认也有view function 

4. pure 

    pure function 就是做一些纯计算型的function

5. struct
```solidity
struct People{
    uint256 favoriteNumber;
    string name;
}
People public person = People({favoriteNumber:2,name:"leo"});

```

6. memory & storage
    - memory: 数据只会在方法执行的期间存储
    - storage: 数据会在方法执行之后仍然存在
    > string 是bytes的array。所以是个object,需要考虑使用哪种存储模式
7. mapping
 
    mapping(string=>uint256) public nameToFavoriteNumber 

8. 合约导入另一合约，并调用并一合约方法
```solidity
import "./SimpleStorage.sol";
SimpleStorage[] public ssarray;
function create() public{
    SimpleStorage ss=new SimpleStorage();
    ssarray.push(ss);
}

function sstore(uint256 index,uint256 number) public{
    SimpleStorage ss=SimpleStorage(address(ssarray[index]));
    ss.store(number);
}
```

9. contract Simple is SimpleStorage{}  is=继承