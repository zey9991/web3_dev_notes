# Reference

[1. Hello Web3 (三行代码) | WTF Academy](https://www.wtf.academy/docs/solidity-101/HelloWeb3/)

https://docs.soliditylang.org/zh/v0.8.19/index.html

# 1. Hello Web3 (三行代码)

`Solidity` 是一种用于编写以太坊虚拟机（`EVM`）智能合约的编程语言。我认为掌握 `Solidity` 是参与链上项目的必备技能：区块链项目大部分是开源的，如果你能读懂代码，就可以规避很多亏钱项目。

## 开发工具：Remix

本教程中，我们将使用 `Remix` 运行 `Solidity` 合约。`Remix` 是以太坊官方推荐的智能合约集成开发环境（IDE），适合新手，可以在浏览器中快速开发和部署合约，无需在本地安装任何程序。

网址：[https://remix.ethereum.org](https://remix.ethereum.org/)

在 `Remix` 中，左侧菜单有三个按钮，分别对应文件（编写代码）、编译（运行代码）和部署（将合约部署到链上）。点击“创建新文件”（`Create New File`）按钮，即可创建一个空白的 `Solidity` 合约。

![img](http://www.kdocs.cn/api/v3/office/copy/RmRKNHpyazc1MXMvUkdGQjhEd3JPSWlKVlBJNFB1R0dwaGRla01UQzhoUjAzZThzcUtBQXliYm8vZ3c5b3g5ODRBWnFpT094OGZIak9QNERRbjFhQjZidmdqVXFtMXU5MkFwV3BkUVdFaG5JWFQwTHI5eElqL0E2Tlh6amlOZTlDMTVoTzV3Zi83SGprUU1CZlI1dHpQcW0wVVJxdC82YUxLYVpaVWtQKzlUSm1QUmlzSmU2TjV5Q2dMZzdTNVZxZ0FHZGU2NTRNN3ZLbzYrUlZmOFpoZ1RubGZSY3dTNXU4YTVwQ3RKd25oS1dwNzhmNGZuYmk5L3BlK1Q2SUkrNFIxNnAvNG53eHBVPQ==/attach/object/ZXTZPBY3ABAEY?)

## 第一个 Solidity 程序

这个简单的程序只有 1 行注释和 3 行代码：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.21;
contract HelloWeb3{
    string public _string = "Hello Web3!";
}
```

第 1 行是注释，说明代码所使用的软件许可（license），这里使用的是 MIT 许可。如果不写许可，编译时会出现警告（warning），但程序仍可运行。Solidity 注释以“//”开头，后面跟注释内容，注释不会被程序执行。

第 2 行声明源文件所使用的 Solidity 版本，因为不同版本的语法有差异。这行代码表示源文件将不允许小于 0.8.21 版本或大于等于 0.9.0 的编译器编译（第二个条件由 `^` 提供）。Solidity 语句以分号（;）结尾。

第 3-4 行是合约部分。第 3 行创建合约（contract），并声明合约名为 `HelloWeb3`。第 4 行是合约内容，声明了一个 string（字符串）变量 `_string`，并赋值为 "Hello Web3!"。

## 编译并部署代码

在 Remix 编辑代码的页面，按 Ctrl + S 即可编译代码，非常方便。

编译完成后，点击左侧菜单的“部署”按钮，进入部署页面。

![img](http://www.kdocs.cn/api/v3/office/copy/RmRKNHpyazc1MXMvUkdGQjhEd3JPSWlKVlBJNFB1R0dwaGRla01UQzhoUjAzZThzcUtBQXliYm8vZ3c5b3g5ODRBWnFpT094OGZIak9QNERRbjFhQjZidmdqVXFtMXU5MkFwV3BkUVdFaG5JWFQwTHI5eElqL0E2Tlh6amlOZTlDMTVoTzV3Zi83SGprUU1CZlI1dHpQcW0wVVJxdC82YUxLYVpaVWtQKzlUSm1QUmlzSmU2TjV5Q2dMZzdTNVZxZ0FHZGU2NTRNN3ZLbzYrUlZmOFpoZ1RubGZSY3dTNXU4YTVwQ3RKd25oS1dwNzhmNGZuYmk5L3BlK1Q2SUkrNFIxNnAvNG53eHBVPQ==/attach/object/QU7JVBY3AAQAK?)

默认情况下，`Remix` 会使用 `Remix` 虚拟机（以前称为 JavaScript 虚拟机）来模拟以太坊链，运行智能合约，类似在浏览器里运行一条测试链。`Remix` 还会为你分配一些测试账户，每个账户里有 100 ETH（测试代币），随意使用。点击 `Deploy`（黄色按钮），即可部署我们编写的合约。

![img](http://www.kdocs.cn/api/v3/office/copy/RmRKNHpyazc1MXMvUkdGQjhEd3JPSWlKVlBJNFB1R0dwaGRla01UQzhoUjAzZThzcUtBQXliYm8vZ3c5b3g5ODRBWnFpT094OGZIak9QNERRbjFhQjZidmdqVXFtMXU5MkFwV3BkUVdFaG5JWFQwTHI5eElqL0E2Tlh6amlOZTlDMTVoTzV3Zi83SGprUU1CZlI1dHpQcW0wVVJxdC82YUxLYVpaVWtQKzlUSm1QUmlzSmU2TjV5Q2dMZzdTNVZxZ0FHZGU2NTRNN3ZLbzYrUlZmOFpoZ1RubGZSY3dTNXU4YTVwQ3RKd25oS1dwNzhmNGZuYmk5L3BlK1Q2SUkrNFIxNnAvNG53eHBVPQ==/attach/object/ONZJVBY3AAAG2?)

部署成功后，在下方会看到名为 `HelloWeb3` 的合约。点击 `_string`，即可看到 "Hello Web3!"。

## 总结

本节课程中，我们简要介绍了 `Solidity` 和 `Remix` 工具，并完成了第一个 `Solidity` 程序 —— `HelloWeb3`。接下来，我们将继续深入学习 `Solidity`！

# 2. 值类型

## Solidity中的变量类型

1. 值类型(Value Type)：包括布尔型，整数型等等，这类变量赋值时候直接传递数值。
2. 引用类型(Reference Type)：包括数组和结构体，这类变量占空间大，赋值时候直接传递地址（类似指针）。
3. 映射类型(Mapping Type): Solidity中存储键值对的数据结构，可以理解为哈希表

我们将仅介绍常用类型，不常用的类型不会涉及，本篇将介绍值类型。

## 值类型

### 1. 布尔型

布尔型是二值变量，取值为 `true` 或 `false`。

```
// 布尔值
bool public _bool = true;
```

布尔值的运算符包括：

- `!` （逻辑非）
- `&&` （逻辑与，"and"）
- `||` （逻辑或，"or"）
- `==` （等于）
- `!=` （不等于）

```
// 布尔运算
bool public _bool1 = !_bool; // 取非
bool public _bool2 = _bool && _bool1; // 与
bool public _bool3 = _bool || _bool1; // 或
bool public _bool4 = _bool == _bool1; // 相等
bool public _bool5 = _bool != _bool1; // 不相等
```

在上述代码中：变量 `_bool` 的取值是 `true`；`_bool1` 是 `_bool` 的非，为 `false`；`_bool && _bool1` 为 `false`；`_bool || _bool1` 为 `true`；`_bool == _bool1` 为 `false`；`_bool != _bool1` 为 `true`。

值得注意的是：`&&` 和 `||` 运算符遵循短路规则，这意味着，假如存在 `f(x) || g(y)` 的表达式，如果 `f(x)` 是 `true`，`g(y)` 不会被计算，即使它和 `f(x)` 的结果是相反的。假如存在`f(x) && g(y)` 的表达式，如果 `f(x)` 是 `false`，`g(y)` 不会被计算。 所谓“短路规则”，一般出现在逻辑与（&&）和逻辑或（||）中。 当逻辑与（&&）的第一个条件为false时，就不会再去判断第二个条件； 当逻辑或（||）的第一个条件为true时，就不会再去判断第二个条件，这就是短路规则。

### 2. 整型

整型是 Solidity 中的整数，最常用的包括：

```
// 整型
int public _int = -1; // 整数，包括负数
uint public _uint = 1; // 正整数
uint256 public _number = 20220330; // 256位正整数
```