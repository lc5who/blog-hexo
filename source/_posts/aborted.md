---
title: git解决 ssl_read ,ssl的问题
date: 2022-03-04 17:27:57
tags: git
---

## 解决办法

记录一下
之前尝试过各种 unset http.proxy 等一系列，最后发现还是这个管用

```git config http.postBuffer 524288000```

```git config http.sslVerify "false"```





