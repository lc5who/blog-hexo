---
title: python开发区块链之三-基础概念
date: 2022-05-26 16:09:35
tags: ethereum
---

# Lesson 3: Fund Me

## Interface
### inteface是用来告诉合约哪些方法能被另外的合约调用。其编译后就是abi
```sol
interfaceType x = interfanceType(合约地址)
```

## uint256
### uint256(sum)
    当数值超过最大值，solidity会将其转为最小值
    safeMath用法:
        using safeMath for uint256

## require
    The require function either creates an error without any data or an error of type Error(string). It should be used to ensure valid conditions that cannot be detected until execution time. This includes conditions on inputs or return values from calls to external contracts.
    
    ex:require(msg.value % 2 == 0, "Even value required.");

## withdraw
    msg.sender.transfer(address(this).balance)
    this = 所在的合约本身
    需要一个owner才能提现
    require(msg.sender==owner)
    那么如何设置owner？ answer: Constructor
```solidity
address public owner;
constructor() public {
    owner = msg.sender;
}
```

## modifier
    modifier是一种方法的修饰符，以声明的形式
    modifier onlyOwner{
        require(msg.sender == owner);
        _;
    }
    ex:
    function withdraw() payable onlyOwner public{

    }