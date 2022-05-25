---
title: python开发区块链之一
date: 2022-05-25 13:49:17
tags: ethereum
---

# Lesson 1. Welcome To Blockchain

1. smart contract && hybrid contract
   - hybrid contract 比之smart contract 多了一些离线运算
2. Blockchain的优点
- Decentralized 去中心化
- Transparency & Flexibility 透明且灵活
- Speed & Efficiency 快速且高效
- Security & Immutability 安全且不可更改
- Removal of counterparty risk 消除交易风险
- Trust Minimized Agreement 无需信任的合同。合同自动完成
3. Block explorer 
   
   > 区块链浏览器可以让我们查看发生在区快链上的交易

4. gas
- 油费,一种测量计算量的单位，当你发起交易的计算量越大，油费越多，链上每一笔交易都要花油费
- gas是 计算 计算量的所需要用到的邮费
- gasprice 是 每一单位的gas的价格
- gas limit 是最大能使用的油费,超出则交易取消
  gas price设置的越大交易完成的时间越快
  具体数值可查看 ethgasstation.info
5. Hahs
   
   一个唯一，固定长度的字符串，用来验证一块数据。是用 hash function将可视数据生成的。
   
   [Blockchain Demo](https://andersbrownworth.com/blockchain/hash)

6. Nonce
   
   ![](C:\Users\leo\AppData\Roaming\marktext\images\2022-05-25-16-05-12-image.png)
   
   点击挖矿时会 计算出一个nonce，并生成以0000开头的hash

7. 区块链为什么难以更改
   
   - 链上的每一个区块都有一个自身hash，跟指向前一个区块的哈希。哈希由 block号，nonce,data,prev 计算而成. 当其中的一个区块数据发生了变化，之后的区块不得不重新计算nonce。
   
   ![](C:\Users\leo\AppData\Roaming\marktext\images\2022-05-25-16-18-23-image.png)
   
   - 去中心化区块链
     
     首先拥有节点中最后一个区块的hash值就可以得到链上所有的区块hash(每个区块都有一个指向前一个区块hash的字段) 当节点a中的数据发生改变，那么最后一个区块的hash值必然变化。就会发生3个节点的hash不一致.那么此时，区块链就会比对，将发生错误的节点剔除出链，将链上数据一致数量较多的节点组合成区块链 
     
8. proof of work && proof of stake
   - proof of work
      在比特币区块链上，每隔 10 - 15 分钟就会把这期间的所有交易讯息打包成一个区块并加到最长的区块链上，帮助成功验证新区块链的节点会被区块链上的奖励机制给予帮助新区块生成的营运奖励金，这整串打包区块纪录帐本与获得奖励的过程即俗称挖矿 mining，而所有参与写入帐本竞争的节点则称为矿工 miner。

      比特币区块链上的节点，需付出工作量证明来获得记帐权。意味在比特币区块链上的所有节点，只要提出工作量证明都可以参与写帐本打包新区块的竞争。优先胜出的节点会将新区块的帐本讯息广播至比特币全网路上，其馀的节点验证后即从竞争改为接受新的区块并同步新区块的帐本讯息，大家全部完成后再一同参与新的交易讯息区块打包.
   - proof of stake