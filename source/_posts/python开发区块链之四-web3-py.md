---
title: python开发区块链之四-web3.py
date: 2022-05-27 14:52:10
tags: ethereum
---

# Lesson 4: Web3.py Simple Storage

## 1. complie contract
    //安装编译库
    pip install py-solc-x
python 代码：
```python
print("Installing...")
install_solc("0.6.0")

# Solidity source code
compiled_sol = compile_standard(
    {
        "language": "Solidity",
        "sources": {"SimpleStorage.sol": {"content": simple_storage_file}},
        "settings": {
            "outputSelection": {
                "*": {
                    "*": ["abi", "metadata", "evm.bytecode", "evm.bytecode.sourceMap"]
                }
            }
        },
    },
    solc_version="0.6.0",
)
```