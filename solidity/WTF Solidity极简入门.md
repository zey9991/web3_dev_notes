# Reference

[1. Hello Web3 (三行代码) | WTF Academy](https://www.wtf.academy/docs/solidity-101/HelloWeb3/)

https://docs.soliditylang.org/zh/v0.8.19/index.html

# 1. Hello Web3 (三行代码)

`Solidity` 是一种用于编写以太坊虚拟机（`EVM`）智能合约的编程语言。我认为掌握 `Solidity` 是参与链上项目的必备技能：区块链项目大部分是开源的，如果你能读懂代码，就可以规避很多亏钱项目。

## 开发工具：Remix

本教程中，我们将使用 `Remix` 运行 `Solidity` 合约。`Remix` 是以太坊官方推荐的智能合约集成开发环境（IDE），适合新手，可以在浏览器中快速开发和部署合约，无需在本地安装任何程序。

网址：[https://remix.ethereum.org](https://remix.ethereum.org/)

在 `Remix` 中，左侧菜单有三个按钮，分别对应文件（编写代码）、编译（运行代码）和部署（将合约部署到链上）。点击“创建新文件”（`Create New File`）按钮，即可创建一个空白的 `Solidity` 合约。

![img](http://www.kdocs.cn/api/v3/office//RmRKNHpyazc1MXMvUkdGQjhEd3JPSWlKVlBJNFB1R0dwaGRla01UQzhoUjAzZThzcUtBQXliYm8vZ3c5b3g5ODRBWnFpT094OGZIak9QNERRbjFhQjZidmdqVXFtMXU5MkFwV3BkUVdFaG5JWFQwTHI5eElqL0E2Tlh6amlOZTlDMTVoTzV3Zi83SGprUU1CZlI1dHpQcW0wVVJxdC82YUxLYVpaVWtQKzlUSm1QUmlzSmU2TjV5Q2dMZzdTNVZxZ0FHZGU2NTRNN3ZLbzYrUlZmOFpoZ1RubGZSY3dTNXU4YTVwQ3RKd25oS1dwNzhmNGZuYmk5L3BlK1Q2SUkrNFIxNnAvNG53eHBVPQ==/attach/object/ZXTZPBY3ABAEY?)

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

![img](http://www.kdocs.cn/api/v3/office//RmRKNHpyazc1MXMvUkdGQjhEd3JPSWlKVlBJNFB1R0dwaGRla01UQzhoUjAzZThzcUtBQXliYm8vZ3c5b3g5ODRBWnFpT094OGZIak9QNERRbjFhQjZidmdqVXFtMXU5MkFwV3BkUVdFaG5JWFQwTHI5eElqL0E2Tlh6amlOZTlDMTVoTzV3Zi83SGprUU1CZlI1dHpQcW0wVVJxdC82YUxLYVpaVWtQKzlUSm1QUmlzSmU2TjV5Q2dMZzdTNVZxZ0FHZGU2NTRNN3ZLbzYrUlZmOFpoZ1RubGZSY3dTNXU4YTVwQ3RKd25oS1dwNzhmNGZuYmk5L3BlK1Q2SUkrNFIxNnAvNG53eHBVPQ==/attach/object/QU7JVBY3AAQAK?)

默认情况下，`Remix` 会使用 `Remix` 虚拟机（以前称为 JavaScript 虚拟机）来模拟以太坊链，运行智能合约，类似在浏览器里运行一条测试链。`Remix` 还会为你分配一些测试账户，每个账户里有 100 ETH（测试代币），随意使用。点击 `Deploy`（黄色按钮），即可部署我们编写的合约。

![img](http://www.kdocs.cn/api/v3/office//RmRKNHpyazc1MXMvUkdGQjhEd3JPSWlKVlBJNFB1R0dwaGRla01UQzhoUjAzZThzcUtBQXliYm8vZ3c5b3g5ODRBWnFpT094OGZIak9QNERRbjFhQjZidmdqVXFtMXU5MkFwV3BkUVdFaG5JWFQwTHI5eElqL0E2Tlh6amlOZTlDMTVoTzV3Zi83SGprUU1CZlI1dHpQcW0wVVJxdC82YUxLYVpaVWtQKzlUSm1QUmlzSmU2TjV5Q2dMZzdTNVZxZ0FHZGU2NTRNN3ZLbzYrUlZmOFpoZ1RubGZSY3dTNXU4YTVwQ3RKd25oS1dwNzhmNGZuYmk5L3BlK1Q2SUkrNFIxNnAvNG53eHBVPQ==/attach/object/ONZJVBY3AAAG2?)

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

常用的整型运算符包括：

- 比较运算符（返回布尔值）： `<=`， `<`，`==`， `!=`， `>=`， `>`
- 算数运算符： `+`， `-`， `*`， `/`， `%`（取余），`**`（幂）

```solidity
// 整数运算
uint256 public _number1 = _number + 1; // +，-，*，/
uint256 public _number2 = 2**2; // 指数
uint256 public _number3 = 7 % 2; // 取余数
bool public _numberbool = _number2 > _number3; // 比大小
```

### 3. 地址类型

地址类型(address)有两类：

- 普通地址（address）: 存储一个 20 字节的值（以太坊地址的大小）。
- payable address: 比普通地址多了 `transfer` 和 `send` 两个成员方法，用于接收转账。

我们会在之后的章节更加详细地介绍 payable address。

```solidity
// 地址
address public _address = 0x7A58c0Be72BE218B41C608b7Fe7C5bB630736C71;
address payable public _address1 = payable(_address); // payable address，可以转账、查余额
// 地址类型的成员
uint256 public balance = _address1.balance; // balance of address
```



### 4. 定长字节数组[](https://www.wtf.academy/docs/solidity-101/ValueTypes/#4-定长字节数组)

字节数组分为定长和不定长两种：

- 定长字节数组: 属于值类型，数组长度在声明之后不能改变。根据字节数组的长度分为 `bytes1`, `bytes8`, `bytes32` 等类型。定长字节数组最多存储 32 bytes 数据，即`bytes32`。
- 不定长字节数组: 属于引用类型（之后的章节介绍），数组长度在声明之后可以改变，包括 `bytes` 等。

```solidity
// 固定长度的字节数组
bytes32 public _byte32 = "MiniSolidity"; 
bytes1 public _byte = _byte32[0]; 
```



在上述代码中，`MiniSolidity` 变量以字节的方式存储进变量 `_byte32`。如果把它转换成 `16 进制`，就是：`0x4d696e69536f6c69646974790000000000000000000000000000000000000000`

`_byte` 变量的值为 `_byte32` 的第一个字节，即 `0x4d`。

`_byte32` 的第一个字节是 `0x4d`，因为字符串 `"MiniSolidity"` 的第一个字符是 'M'。在 ASCII 编码中，'M' 对应的十六进制值是 `0x4d`。因此，当字符串被存储为字节数组时，第一位就是这个值。

### 5. 枚举 enum[](https://www.wtf.academy/docs/solidity-101/ValueTypes/#5-枚举-enum)

枚举（`enum`）是 Solidity 中用户定义的数据类型。它主要用于为 `uint` 分配名称，使程序易于阅读和维护。它与 `C 语言` 中的 `enum` 类似，使用名称来代替从 `0` 开始的 `uint`：

```solidity
// 用enum将uint 0， 1， 2表示为Buy, Hold, Sell
enum ActionSet { Buy, Hold, Sell }
// 创建enum变量 action
ActionSet action = ActionSet.Buy;
```



枚举可以显式地和 `uint` 相互转换，并会检查转换的正整数是否在枚举的长度内，否则会报错：

```solidity
// enum可以和uint显式的转换
function enumToUint() external view returns(uint){
    return uint(action);
}
```



`enum` 是一个比较冷门的变量，几乎没什么人用。

## 在 Remix 上运行[](https://www.wtf.academy/docs/solidity-101/ValueTypes/#在-remix-上运行)

- 部署合约后可以查看每个类型的变量的数值：



![2-1.png](https://www.wtf.academy/assets/images/2-1-90414d7e21f49e75101a07a8a55e602c.png)



- `enum` 和 `uint` 转换的示例：



![2-2.png](https://www.wtf.academy/assets/images/2-2-6c364618b30e6c498127e2d129f9e7e8.png)

![2-3.png](https://www.wtf.academy/assets/images/2-3-d2742673ffbd4df5c230d48a02a2921c.png)



## 总结[](https://www.wtf.academy/docs/solidity-101/ValueTypes/#总结)

在这一讲，我们介绍了 Solidity 中值类型，包括布尔型、整型、地址、定长字节数组和枚举。在后续章节，我们将继续介绍 Solidity 的其他变量类型，包括引用类型和映射类型。

# 3. 函数

Solidity语言的函数非常灵活，可以进行各种复杂操作。在本教程中，我们将会概述函数的基础概念，并通过一些示例演示如何使用函数。

我们先看一下 Solidity 中函数的形式:

```solidity
function <function name>(<parameter types>) {internal|external|public|private} [pure|view|payable] [returns (<return types>)]
```



看着有一些复杂，让我们从前往后逐个解释(方括号中的是可写可不 写的关键字)：

1. `function`：声明函数时的固定用法。要编写函数，就需要以 `function` 关键字开头。

2. `<function name>`：函数名。

3. `(<parameter types>)`：圆括号内写入函数的参数，即输入到函数的变量类型和名称。

4. `{internal|external|public|private}`：函数可见性说明符，共有4种。

   - `public`：内部和外部均可见。
   - `private`：只能从本合约内部访问，继承的合约也不能使用。
   - `external`：只能从合约外部访问（但内部可以通过 `this.f()` 来调用，`f`是函数名）。
   - `internal`: 只能从合约内部访问，继承的合约可以用。

   **注意 1**：合约中定义的函数需要明确指定可见性，它们没有默认值。

   **注意 2**：`public|private|internal` 也可用于修饰状态变量。`public`变量会自动生成同名的`getter`函数，用于查询数值。未标明可见性类型的状态变量，默认为`internal`。

5. `[pure|view|payable]`：决定函数权限/功能的关键字。`payable`（可支付的）很好理解，带着它的函数，运行的时候可以给合约转入 ETH。`pure` 和 `view` 的介绍见下一节。

6. `[returns ()]`：函数返回的变量类型和名称。

## [到底什么是 `Pure` 和`View`？](https://www.wtf.academy/docs/solidity-101/Function/#到底什么是-pure-和view)

刚开始学习 `solidity` 时，`pure` 和 `view` 关键字可能令人费解，因为其他编程语言中没有类似的关键字。`solidity` 引入这两个关键字主要是因为 以太坊交易需要支付气费（gas fee）。合约的状态变量存储在链上，gas fee 很贵，如果计算不改变链上状态，就可以不用付 `gas`。包含 `pure` 和 `view` 关键字的函数是不改写链上状态的，因此用户直接调用它们是不需要付 gas 的（注意，合约中非 `pure`/`view` 函数调用 `pure`/`view` 函数时需要付gas）。

在以太坊中，以下语句被视为修改链上状态：

1. 写入状态变量。
2. 释放事件。
3. 创建其他合约。
4. 使用 `selfdestruct`.
5. 通过调用发送以太币。
6. 调用任何未标记 `view` 或 `pure` 的函数。
7. 使用低级调用（low-level calls）。
8. 使用包含某些操作码的内联汇编。

为了帮助大家理解，我画了一个马里奥插图。在这幅插图中，我将合约中的状态变量（存储在链上）比作碧琪公主，三种不同的角色代表不同的关键字。



![WTF is pure and view in solidity?](https://images.mirror-media.xyz/publication-images/1B9kHsTYnDY_QURSWMmPb.png?height=1028&width=1758)



- `pure`，中文意思是“纯”，这里可以理解为”纯打酱油的”。`pure` 函数既不能读取也不能写入链上的状态变量。就像小怪一样，看不到也摸不到碧琪公主。
- `view`，“看”，这里可以理解为“看客”。`view`函数能读取但也不能写入状态变量。类似马里奥，能看到碧琪公主，但终究是看客，不能入洞房。
- 非 `pure` 或 `view` 的函数既可以读取也可以写入状态变量。类似马里奥里的 `boss`，可以对碧琪公主为所欲为🐶。

## [代码](https://www.wtf.academy/docs/solidity-101/Function/#代码)

### 1. [pure 和 view](https://www.wtf.academy/docs/solidity-101/Function/#1-pure-和-view)

我们在合约里定义一个状态变量 `number`，初始化为 5。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.21;
contract FunctionTypes{
    uint256 public number = 5;
}
```



定义一个 `add()` 函数，每次调用会让 `number` 增加 1。

```solidity
// 默认function
function add() external{
    number = number + 1;
}
```



如果 `add()` 函数被标记为 `pure`，比如 `function add() external pure`，就会报错。因为 `pure` 是不配读取合约里的状态变量的，更不配改写。那 `pure` 函数能做些什么？举个例子，你可以给函数传递一个参数 `_number`，然后让他返回 `_number + 1`，这个操作不会读取或写入状态变量。

```solidity
// pure: 纯纯牛马
function addPure(uint256 _number) external pure returns(uint256 new_number){
    new_number = _number + 1;
}
```





![3-3.png](https://www.wtf.academy/assets/images/3-3-5b5c10d460fd4d9721009d3a94a44ebb.png)



如果 `add()` 函数被标记为 `view`，比如 `function add() external view`，也会报错。因为 `view` 能读取，但不能够改写状态变量。我们可以稍微改写下函数，读取但是不改写 `number`，返回一个新的变量。

```solidity
// view: 看客
function addView() external view returns(uint256 new_number) {
    new_number = number + 1;
}
```





![3-4.png](https://www.wtf.academy/assets/images/3-4-049b8caacda74a086158981824991cb3.png)



### 2. [internal v.s. external](https://www.wtf.academy/docs/solidity-101/Function/#2-internal-vs-external)

```solidity
// internal: 内部函数
function minus() internal {
    number = number - 1;
}

// 合约内的函数可以调用内部函数
function minusCall() external {
    minus();
}
```



我们定义一个 `internal` 的 `minus()` 函数，每次调用使得 `number` 变量减少 1。由于 `internal` 函数只能由合约内部调用，我们必须再定义一个 `external` 的 `minusCall()` 函数，通过它间接调用内部的 `minus()` 函数。



![3-1.png](https://www.wtf.academy/assets/images/3-1-7ddf1b1c7336bbdd36e3a1fc105b7422.png)



### 3. [payable](https://www.wtf.academy/docs/solidity-101/Function/#3-payable)

```solidity
// payable: 递钱，能给合约支付eth的函数
function minusPayable() external payable returns(uint256 balance) {
    minus();    
    balance = address(this).balance;
}
```



我们定义一个 `external payable` 的 `minusPayable()` 函数，间接的调用 `minus()`，并且返回合约里的 ETH 余额（`this` 关键字可以让我们引用合约地址）。我们可以在调用 `minusPayable()` 时往合约里转入1个 ETH。



![mirror-image-1](https://images.mirror-media.xyz/publication-images/ETDPN8myq7jFfAL8CUAFt.png?height=148&width=588)



我们可以在返回的信息中看到，合约的余额变为 1 ETH。



![mirror-image-2](https://images.mirror-media.xyz/publication-images/nGZ2pz0MvzgXuKrENJPYf.png?height=128&width=1130)





![3-2.png](https://www.wtf.academy/assets/images/3-2-e1be980c21311dc80f6233dac763fd89.png)



## 总结

在这一讲，我们介绍了 `Solidity` 中的函数。`pure` 和 `view` 关键字比较难理解，在其他语言中没出现过：`view` 函数可以读取状态变量，但不能改写；`pure` 函数既不能读取也不能改写状态变量。

# 4. 函数输出

这一讲，我们将介绍 Solidity 函数输出，包括：返回多种变量，命名式返回，以及利用解构式赋值读取全部或部分返回值。

## 返回值：return 和 returns

Solidity 中与函数输出相关的有两个关键字：`return`和`returns`。它们的区别在于：

- `returns`：跟在函数名后面，用于声明返回的变量类型及变量名。
- `return`：用于函数主体中，返回指定的变量。

```solidity
// 返回多个变量
function returnMultiple() public pure returns(uint256, bool, uint256[3] memory){
    return(1, true, [uint256(1),2,5]);
}
```



在上述代码中，我们利用 `returns` 关键字声明了有多个返回值的 `returnMultiple()` 函数，然后我们在函数主体中使用 `return(1, true, [uint256(1),2,5])` 确定了返回值。

这里`uint256[3]`声明了一个长度为`3`且类型为`uint256`的数组作为返回值。因为`[1,2,3]`会默认为`uint8(3)`，因此`[uint256(1),2,5]`中首个元素必须强转`uint256`来声明该数组内的元素皆为此类型。数组类型返回值默认必须用memory修饰，在下一个章节会细说[变量的存储和作用域](https://www.wtf.academy/docs/solidity-101/DataStorage/)。

## 命名式返回

我们可以在 `returns` 中标明返回变量的名称。Solidity 会初始化这些变量，并且自动返回这些函数的值，无需使用 `return`。

```solidity
// 命名式返回
function returnNamed() public pure returns(uint256 _number, bool _bool, uint256[3] memory _array){
    _number = 2;
    _bool = false;
    _array = [uint256(3),2,1];
}
```



在上述代码中，我们用 `returns(uint256 _number, bool _bool, uint256[3] memory _array)` 声明了返回变量类型以及变量名。这样，在主体中只需为变量 `_number`、`_bool`和`_array` 赋值，即可自动返回。

当然，你也可以在命名式返回中用 `return` 来返回变量：

```solidity
// 命名式返回，依然支持return
function returnNamed2() public pure returns(uint256 _number, bool _bool, uint256[3] memory _array){
    return(1, true, [uint256(1),2,5]);
}
```



## 解构式赋值

Solidity 支持使用解构式赋值规则来**读取函数的全部或部分返回值**。

- 读取所有返回值：声明变量，然后将要赋值的变量用`,`隔开，按顺序排列。

  ```solidity
  uint256 _number;
  bool _bool;
  uint256[3] memory _array;
  (_number, _bool, _array) = returnNamed();
  ```

  

- 读取部分返回值：声明要读取的返回值对应的变量，不读取的留空。在下面的代码中，我们只读取`_bool`，而不读取返回的`_number`和`_array`：

  ```solidity
  (, _bool2, ) = returnNamed();
  ```

  

## 在 Remix 上运行

- 部署合约后查看三种返回方式的结果

  

  ![4-1.png](https://www.wtf.academy/assets/images/4-1-3c115fdc5afcb11e3f9eb51b8e2abbd8.png)

  

## 总结

这一讲，我们介绍 Solidity 函数返回值，包括：返回多种变量，命名式返回，以及利用解构式赋值读取全部或部分返回值。这些知识点有助于我们在编写智能合约时，更灵活地处理函数返回值。

# 5. 变量数据存储和作用域 storage/memory/calldata

## Solidity中的引用类型

**引用类型(Reference Type)**：包括数组（`array`）和结构体（`struct`），由于这类变量比较复杂，占用存储空间大，我们在使用时必须要声明数据存储的位置。

## 数据位置

Solidity数据存储位置有三类：`storage`，`memory`和`calldata`。不同存储位置的`gas`成本不同。`storage`类型的数据存在链上，类似计算机的硬盘，消耗`gas`多；`memory`和`calldata`类型的临时存在内存里，消耗`gas`少。大致用法：

1. `storage`：合约里的状态变量默认都是`storage`，存储在链上。
2. `memory`：函数里的参数和临时变量一般用`memory`，存储在内存中，不上链。尤其是如果返回数据类型是变长的情况下，必须加memory修饰，例如：string, bytes, array和自定义结构。
3. `calldata`：和`memory`类似，存储在内存中，不上链。与`memory`的不同点在于`calldata`变量不能修改（`immutable`），一般用于函数的参数。例子：

```solidity
function fCalldata(uint[] calldata _x) public pure returns(uint[] calldata){
    //参数为calldata数组，不能被修改
    // _x[0] = 0 //这样修改会报错
    return(_x);
}
```



**Example:**



![5-1.png](https://www.wtf.academy/assets/images/5-1-9d00a21842c77b3911aaf419f67ad691.png)



### 数据位置和赋值规则

在不同存储类型相互赋值时候，有时会产生独立的副本（修改新变量不会影响原变量），有时会产生引用（修改新变量会影响原变量）。规则如下：

- 赋值本质上是创建**引用**指向本体，因此修改本体或者是引用，变化可以被同步：

  - `storage`（合约的状态变量）赋值给本地`storage`（函数里的）时候，会创建引用，改变新变量会影响原变量。例子：

    ```solidity
    uint[] x = [1,2,3]; // 状态变量：数组 x
    
    function fStorage() public{
        //声明一个storage的变量 xStorage，指向x。修改xStorage也会影响x
        uint[] storage xStorage = x;
        xStorage[0] = 100;
    }
    ```

    

    **Example:**

    

    ![5-2.png](https://www.wtf.academy/assets/images/5-2-91bae5b0b86b0e55210cac541a6edee5.png)

    

  - `memory`赋值给`memory`，会创建引用，改变新变量会影响原变量。

- 其他情况下，赋值创建的是本体的副本，即对二者之一的修改，并不会同步到另一方

## 变量的作用域[](https://www.wtf.academy/docs/solidity-101/DataStorage/#变量的作用域)

`Solidity`中变量按作用域划分有三种，分别是状态变量（state variable），局部变量（local variable）和全局变量(global variable)

### 1. 状态变量[](https://www.wtf.academy/docs/solidity-101/DataStorage/#1-状态变量)

状态变量是数据存储在链上的变量，所有合约内函数都可以访问，`gas`消耗高。状态变量在合约内、函数外声明：

```solidity
contract Variables {
    uint public x = 1;
    uint public y;
    string public z;
}
```



我们可以在函数里更改状态变量的值：

```solidity
function foo() external{
    // 可以在函数里更改状态变量的值
    x = 5;
    y = 2;
    z = "0xAA";
}
```



### 2. 局部变量[](https://www.wtf.academy/docs/solidity-101/DataStorage/#2-局部变量)

局部变量是仅在函数执行过程中有效的变量，函数退出后，变量无效。局部变量的数据存储在内存里，不上链，`gas`低。局部变量在函数内声明：

```solidity
function bar() external pure returns(uint){
    uint xx = 1;
    uint yy = 3;
    uint zz = xx + yy;
    return(zz);
}
```



### 3. 全局变量[](https://www.wtf.academy/docs/solidity-101/DataStorage/#3-全局变量)

全局变量是全局范围工作的变量，都是`solidity`预留关键字。他们可以在函数内不声明直接使用：

```solidity
function global() external view returns(address, uint, bytes memory){
    address sender = msg.sender;
    uint blockNum = block.number;
    bytes memory data = msg.data;
    return(sender, blockNum, data);
}
```



在上面例子里，我们使用了3个常用的全局变量：`msg.sender`，`block.number`和`msg.data`，他们分别代表请求发起地址，当前区块高度，和请求数据。下面是一些常用的全局变量，更完整的列表请看这个[链接](https://learnblockchain.cn/docs/solidity/units-and-global-variables.html#special-variables-and-functions)：

- `blockhash(uint blockNumber)`: (`bytes32`) 给定区块的哈希值 – 只适用于256最近区块, 不包含当前区块。
- `block.coinbase`: (`address payable`) 当前区块矿工的地址
- `block.gaslimit`: (`uint`) 当前区块的gaslimit
- `block.number`: (`uint`) 当前区块的number
- `block.timestamp`: (`uint`) 当前区块的时间戳，为unix纪元以来的秒
- `gasleft()`: (`uint256`) 剩余 gas
- `msg.data`: (`bytes calldata`) 完整call data
- `msg.sender`: (`address payable`) 消息发送者 (当前 caller)
- `msg.sig`: (`bytes4`) calldata的前四个字节 (function identifier)
- `msg.value`: (`uint`) 当前交易发送的 `wei` 值
- `block.blobbasefee`: (`uint`) 当前区块的blob基础费用。这是Cancun升级新增的全局变量。
- `blobhash(uint index)`: (`bytes32`) 返回跟当前交易关联的第 `index` 个blob的版本化哈希（第一个字节为版本号，当前为`0x01`，后面接KZG承诺的SHA256哈希的最后31个字节）。若当前交易不包含blob，则返回空字节。这是Cancun升级新增的全局变量。

**Example:**



![5-4.png](https://www.wtf.academy/assets/images/5-4-5ee425310e1666a20575f2a8330c55cb.png)



### 4. 全局变量-以太单位与时间单位[](https://www.wtf.academy/docs/solidity-101/DataStorage/#4-全局变量-以太单位与时间单位)

#### 以太单位[](https://www.wtf.academy/docs/solidity-101/DataStorage/#以太单位)

`Solidity`中不存在小数点，以`0`代替为小数点，来确保交易的精确度，并且防止精度的损失，利用以太单位可以避免误算的问题，方便程序员在合约中处理货币交易。

- `wei`: 1
- `gwei`: 1e9 = 1000000000
- `ether`: 1e18 = 1000000000000000000

```solidity
function weiUnit() external pure returns(uint) {
    assert(1 wei == 1e0);
    assert(1 wei == 1);
    return 1 wei;
}

function gweiUnit() external pure returns(uint) {
    assert(1 gwei == 1e9);
    assert(1 gwei == 1000000000);
    return 1 gwei;
}

function etherUnit() external pure returns(uint) {
    assert(1 ether == 1e18);
    assert(1 ether == 1000000000000000000);
    return 1 ether;
}
```



**Example:**



![5-5.png](https://www.wtf.academy/assets/images/5-5-767daeb69da57fbfafec524599f721aa.png)



#### 时间单位[](https://www.wtf.academy/docs/solidity-101/DataStorage/#时间单位)

可以在合约中规定一个操作必须在一周内完成，或者某个事件在一个月后发生。这样就能让合约的执行可以更加精确，不会因为技术上的误差而影响合约的结果。因此，时间单位在`Solidity`中是一个重要的概念，有助于提高合约的可读性和可维护性。

- `seconds`: 1
- `minutes`: 60 seconds = 60
- `hours`: 60 minutes = 3600
- `days`: 24 hours = 86400
- `weeks`: 7 days = 604800

```solidity
function secondsUnit() external pure returns(uint) {
    assert(1 seconds == 1);
    return 1 seconds;
}

function minutesUnit() external pure returns(uint) {
    assert(1 minutes == 60);
    assert(1 minutes == 60 seconds);
    return 1 minutes;
}

function hoursUnit() external pure returns(uint) {
    assert(1 hours == 3600);
    assert(1 hours == 60 minutes);
    return 1 hours;
}

function daysUnit() external pure returns(uint) {
    assert(1 days == 86400);
    assert(1 days == 24 hours);
    return 1 days;
}

function weeksUnit() external pure returns(uint) {
    assert(1 weeks == 604800);
    assert(1 weeks == 7 days);
    return 1 weeks;
}
```



**Example:**



![5-6.png](https://www.wtf.academy/assets/images/5-6-3cbbbc11bfb461d7ad6544975736b0d1.png)



## 总结[](https://www.wtf.academy/docs/solidity-101/DataStorage/#总结)

在这一讲，我们介绍了`Solidity`中的引用类型，数据位置和变量的作用域。重点是`storage`, `memory`和`calldata`三个关键字的用法。他们出现的原因是为了节省链上有限的存储空间和降低`gas`。下一讲我们会介绍引用类型中的数组。

# 6. 引用类型, array, struct

这一讲，我们将介绍`Solidity`中的两个重要变量类型：数组（`array`）和结构体（`struct`）。

## 数组 array[](https://www.wtf.academy/docs/solidity-101/ArrayAndStruct/#数组-array)

数组（`Array`）是`Solidity`常用的一种变量类型，用来存储一组数据（整数，字节，地址等等）。数组分为固定长度数组和可变长度数组两种：

- 固定长度数组：在声明时指定数组的长度。用`T[k]`的格式声明，其中`T`是元素的类型，`k`是长度，例如：

  ```solidity
  // 固定长度 Array
  uint[8] array1;
  bytes1[5] array2;
  address[100] array3;
  ```

  

- 可变长度数组（动态数组）：在声明时不指定数组的长度。用`T[]`的格式声明，其中`T`是元素的类型，例如：

  ```solidity
  // 可变长度 Array
  uint[] array4;
  bytes1[] array5;
  address[] array6;
  bytes array7;
  ```

  

  **注意**：`bytes`比较特殊，是数组，但是不用加`[]`。另外，不能用`byte[]`声明单字节数组，可以使用`bytes`或`bytes1[]`。`bytes` 比 `bytes1[]` 省gas。

### 创建数组的规则[](https://www.wtf.academy/docs/solidity-101/ArrayAndStruct/#创建数组的规则)

在Solidity里，创建数组有一些规则：

- 对于`memory`修饰的`动态数组`，可以用`new`操作符来创建，但是必须声明长度，并且声明后长度不能改变。例子：

  ```solidity
  // memory动态数组
  uint[] memory array8 = new uint[](5);
  bytes memory array9 = new bytes(9);
  ```

  

- 数组字面常数(Array Literals)是写作表达式形式的数组，用方括号包着来初始化array的一种方式，并且里面每一个元素的type是以第一个元素为准的，例如`[1,2,3]`里面所有的元素都是`uint8`类型，因为在Solidity中，如果一个值没有指定type的话，会根据上下文推断出元素的类型，默认就是最小单位的type，这里默认最小单位类型是`uint8`。而`[uint(1),2,3]`里面的元素都是`uint`类型，因为第一个元素指定了是`uint`类型了，里面每一个元素的type都以第一个元素为准。

  下面的例子中，如果没有对传入 `g()` 函数的数组进行 `uint` 转换，是会报错的。

  ```solidity
  // SPDX-License-Identifier: GPL-3.0
  pragma solidity >=0.4.16 <0.9.0;
  
  contract C {
      function f() public pure {
          g([uint(1), 2, 3]);
      }
      function g(uint[3] memory _data) public pure {
          // ...
      }
  }
  ```

  

- 如果创建的是动态数组，你需要一个一个元素的赋值。

  ```solidity
  uint[] memory x = new uint[](3);
  x[0] = 1;
  x[1] = 3;
  x[2] = 4;
  ```

  

### 数组成员[](https://www.wtf.academy/docs/solidity-101/ArrayAndStruct/#数组成员)

- `length`: 数组有一个包含元素数量的`length`成员，`memory`数组的长度在创建后是固定的。
- `push()`: `动态数组`拥有`push()`成员，可以在数组最后添加一个`0`元素，并返回该元素的引用。
- `push(x)`: `动态数组`拥有`push(x)`成员，可以在数组最后添加一个`x`元素。
- `pop()`: `动态数组`拥有`pop()`成员，可以移除数组最后一个元素。

**Example:**



![6-1.png](https://www.wtf.academy/assets/images/6-1-ff58f00a7e037fcd318401ca2bc350b6.png)



## 结构体 struct[](https://www.wtf.academy/docs/solidity-101/ArrayAndStruct/#结构体-struct)

`Solidity`支持通过构造结构体的形式定义新的类型。结构体中的元素可以是原始类型，也可以是引用类型；结构体可以作为数组或映射的元素。创建结构体的方法：

```solidity
// 结构体
struct Student{
    uint256 id;
    uint256 score; 
}

Student student; // 初始一个student结构体
```



给结构体赋值的四种方法：

```solidity
//  给结构体赋值
// 方法1:在函数中创建一个storage的struct引用
function initStudent1() external{
    Student storage _student = student; // assign a  of student
    _student.id = 11;
    _student.score = 100;
}
```



**Example:**



![6-2.png](https://www.wtf.academy/assets/images/6-2-991e08767256fcc39717f429da21f05d.png)



```solidity
// 方法2:直接引用状态变量的struct
function initStudent2() external{
    student.id = 1;
    student.score = 80;
}
```



**Example:**



![6-3.png](https://www.wtf.academy/assets/images/6-3-7ccb3cbebd7eff492292a171a8de1852.png)



```solidity
// 方法3:构造函数式
function initStudent3() external {
    student = Student(3, 90);
}
```



**Example:**



![6-4.png](https://www.wtf.academy/assets/images/6-4-c434d897c58d9cdea3701404500b4e1d.png)



```solidity
// 方法4:key value
function initStudent4() external {
    student = Student({id: 4, score: 60});
}
```



**Example:**



![6-5.png](https://www.wtf.academy/assets/images/6-5-494c8879cfe08ac79d073573fad455f3.png)



## 总结[](https://www.wtf.academy/docs/solidity-101/ArrayAndStruct/#总结)

这一讲，我们介绍了Solidity中数组（`array`）和结构体（`struct`）的基本用法。下一讲我们将介绍Solidity中的哈希表——映射（`mapping`）。

# 7. 映射类型 mapping

这一讲，我们将介绍映射（`Mapping`）类型，Solidity中存储键值对的数据结构，可以理解为哈希表。

## 映射Mapping[](https://www.wtf.academy/docs/solidity-101/Mapping/#映射mapping)

在映射中，人们可以通过键（`Key`）来查询对应的值（`Value`），比如：通过一个人的`id`来查询他的钱包地址。

声明映射的格式为`mapping(_KeyType => _ValueType)`，其中`_KeyType`和`_ValueType`分别是`Key`和`Value`的变量类型。例子：

```solidity
mapping(uint => address) public idToAddress; // id映射到地址
mapping(address => address) public swapPair; // 币对的映射，地址到地址
```



## 映射的规则[](https://www.wtf.academy/docs/solidity-101/Mapping/#映射的规则)

- **规则1**：映射的`_KeyType`只能选择Solidity内置的值类型，比如`uint`，`address`等，不能用自定义的结构体。而`_ValueType`可以使用自定义的类型。下面这个例子会报错，因为`_KeyType`使用了我们自定义的结构体：

  ```solidity
  // 我们定义一个结构体 Struct
  struct Student{
      uint256 id;
      uint256 score; 
  }
  mapping(Student => uint) public testVar;
  ```

  

- **规则2**：映射的存储位置必须是`storage`，因此可以用于合约的状态变量，函数中的`storage`变量和library函数的参数（见[例子](https://github.com/ethereum/solidity/issues/4635)）。不能用于`public`函数的参数或返回结果中，因为`mapping`记录的是一种关系 (key - value pair)。

- **规则3**：如果映射声明为`public`，那么Solidity会自动给你创建一个`getter`函数，可以通过`Key`来查询对应的`Value`。

- **规则4**：给映射新增的键值对的语法为`_Var[_Key] = _Value`，其中`_Var`是映射变量名，`_Key`和`_Value`对应新增的键值对。例子：

  ```solidity
  function writeMap (uint _Key, address _Value) public{
      idToAddress[_Key] = _Value;
  }
  ```

  

## 映射的原理[](https://www.wtf.academy/docs/solidity-101/Mapping/#映射的原理)

- **原理1**: 映射不储存任何键（`Key`）的资讯，也没有length的资讯。
- **原理2**: 映射使用`keccak256(abi.encodePacked(key, slot))`当成offset存取value，其中`slot`是映射变量定义所在的插槽位置。
- **原理3**: 因为Ethereum会定义所有未使用的空间为0，所以未赋值（`Value`）的键（`Key`）初始值都是各个type的默认值，如uint的默认值是0。

## 在Remix上验证 (以 `Mapping.sol`为例)[](https://www.wtf.academy/docs/solidity-101/Mapping/#在remix上验证-以-mappingsol为例)

- 映射示例 1 部署

  

  ![7-1](https://www.wtf.academy/assets/images/7-1-2768f65eec9dbbc8771275b45c937e96.jpg)

  

- 映射示例 2 初始值

  

  ![7-2](https://www.wtf.academy/assets/images/7-2-886db6cf3743df280acac78c151971f3.jpg)

  

- 映射示例 3 key-value pair

  

  ![7-3](https://www.wtf.academy/assets/images/7-3-88745249067310f5e280dd60b2560adb.jpg)

  

## 总结[](https://www.wtf.academy/docs/solidity-101/Mapping/#总结)

这一讲，我们介绍了Solidity中哈希表——映射（`Mapping`）的用法。至此，我们已经学习了所有常用变量种类，之后我们会学习控制流`if-else`，`while`等。

# 8. 变量初始值

## 变量初始值[](https://www.wtf.academy/docs/solidity-101/InitialValue/#变量初始值)

在`Solidity`中，声明但没赋值的变量都有它的初始值或默认值。这一讲，我们将介绍常用变量的初始值。

### 值类型初始值[](https://www.wtf.academy/docs/solidity-101/InitialValue/#值类型初始值)

- `boolean`: `false`

- `string`: `""`

- `int`: `0`

- `uint`: `0`

- `enum`: 枚举中的第一个元素

- `address`: `0x0000000000000000000000000000000000000000` (或 `address(0)`)

- ```
  function
  ```

  - `internal`: 空白函数
  - `external`: 空白函数

可以用`public`变量的`getter`函数验证上面写的初始值是否正确：

```solidity
bool public _bool; // false
string public _string; // ""
int public _int; // 0
uint public _uint; // 0
address public _address; // 0x0000000000000000000000000000000000000000

enum ActionSet { Buy, Hold, Sell}
ActionSet public _enum; // 第1个内容Buy的索引0

function fi() internal{} // internal空白函数
function fe() external{} // external空白函数 
```



### 引用类型初始值[](https://www.wtf.academy/docs/solidity-101/InitialValue/#引用类型初始值)

- 映射`mapping`: 所有元素都为其默认值的`mapping`

- 结构体`struct`: 所有成员设为其默认值的结构体

- 数组

  ```
  array
  ```

  - 动态数组: `[]`
  - 静态数组（定长）: 所有成员设为其默认值的静态数组

可以用`public`变量的`getter`函数验证上面写的初始值是否正确：

```solidity
// Reference Types
uint[8] public _staticArray; // 所有成员设为其默认值的静态数组[0,0,0,0,0,0,0,0]
uint[] public _dynamicArray; // `[]`
mapping(uint => address) public _mapping; // 所有元素都为其默认值的mapping
// 所有成员设为其默认值的结构体 0, 0
struct Student{
    uint256 id;
    uint256 score; 
}
Student public student;
```



### `delete`操作符[](https://www.wtf.academy/docs/solidity-101/InitialValue/#delete操作符)

`delete a`会让变量`a`的值变为初始值。

```solidity
// delete操作符
bool public _bool2 = true; 
function d() external {
    delete _bool2; // delete 会让_bool2变为默认值，false
}
```



## 在remix上验证[](https://www.wtf.academy/docs/solidity-101/InitialValue/#在remix上验证)

- 部署合约查看值类型、引用类型的初始值

  

  ![8-1.png](https://www.wtf.academy/assets/images/8-1-bf8a5eafba9f2a6be29c8a116a5465bc.png)

  

- 值类型、引用类型`delete`操作后的默认值

  

  ![8-2.png](https://www.wtf.academy/assets/images/8-2-968b7c57cb793dc524a5665dfae26624.png)

  

## 总结[](https://www.wtf.academy/docs/solidity-101/InitialValue/#总结)

这一讲，我们介绍了`Solidity`中变量的初始值。变量被声明但没有赋值的时候，它的值默认为初始值。不同类型的变量初始值不同，`delete`操作符可以删除一个变量的值并代替为初始值。

# 9. 常数 constant和immutable

这一讲，我们介绍Solidity中和常量相关的两个关键字，`constant`（常量）和`immutable`（不变量）。状态变量声明这两个关键字之后，不能在初始化后更改数值。这样做的好处是提升合约的安全性并节省`gas`。

另外，只有数值变量可以声明`constant`和`immutable`；`string`和`bytes`可以声明为`constant`，但不能为`immutable`。

## constant和immutable[](https://www.wtf.academy/docs/solidity-101/Constant/#constant和immutable)

### constant[](https://www.wtf.academy/docs/solidity-101/Constant/#constant)

`constant`变量必须在声明的时候初始化，之后再也不能改变。尝试改变的话，编译不通过。

```solidity
// constant变量必须在声明的时候初始化，之后不能改变
uint256 constant CONSTANT_NUM = 10;
string constant CONSTANT_STRING = "0xAA";
bytes constant CONSTANT_BYTES = "WTF";
address constant CONSTANT_ADDRESS = 0x0000000000000000000000000000000000000000;
```



### immutable[](https://www.wtf.academy/docs/solidity-101/Constant/#immutable)

`immutable`变量可以在声明时或构造函数中初始化，因此更加灵活。在`Solidity v8.0.21`以后，`immutable`变量不需要显式初始化。反之，则需要显式初始化。 若`immutable`变量既在声明时初始化，又在constructor中初始化，会使用constructor初始化的值。

```solidity
// immutable变量可以在constructor里初始化，之后不能改变
uint256 public immutable IMMUTABLE_NUM = 9999999999;
address public immutable IMMUTABLE_ADDRESS;
uint256 public immutable IMMUTABLE_BLOCK;
uint256 public immutable IMMUTABLE_TEST;
```



你可以使用全局变量例如`address(this)`，`block.number` 或者自定义的函数给`immutable`变量初始化。在下面这个例子，我们利用了`test()`函数给`IMMUTABLE_TEST`初始化为`9`：

```solidity
// 利用constructor初始化immutable变量，因此可以利用
constructor(){
    IMMUTABLE_ADDRESS = address(this);
    IMMUTABLE_NUM = 1118;
    IMMUTABLE_TEST = test();
}

function test() public pure returns(uint256){
    uint256 what = 9;
    return(what);
}
```



## 在remix上验证[](https://www.wtf.academy/docs/solidity-101/Constant/#在remix上验证)

1. 部署好合约之后，通过remix上的`getter`函数，能获取到`constant`和`immutable`变量初始化好的值。

   

   ![9-1.png](https://www.wtf.academy/assets/images/9-1-4dd7d40c9799d42c60e4793394a4eb5e.png)

   

2. `constant`变量初始化之后，尝试改变它的值，会编译不通过并抛出`TypeError: Cannot assign to a constant variable.`的错误。

   

   ![9-2.png](https://www.wtf.academy/assets/images/9-2-5b85f9969dff8fbeb78cac9f8d4089ce.png)

   

3. `immutable`变量初始化之后，尝试改变它的值，会编译不通过并抛出`TypeError: Immutable state variable already initialized.`的错误。

   

   ![9-3.png](data:image/png;base64,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)

   

## 总结[](https://www.wtf.academy/docs/solidity-101/Constant/#总结)

这一讲，我们介绍了Solidity中两个关键字，`constant`（常量）和`immutable`（不变量），让不应该变的变量保持不变。这样的做法能在节省`gas`的同时提升合约的安全性。

# 10. 控制流，用Solidity实现插入排序

这一讲，我们将介绍`Solidity`中的控制流，然后讲如何用`Solidity`实现插入排序（`InsertionSort`），一个看起来简单，但实际上很容易写出`bug`的程序。

## 控制流[](https://www.wtf.academy/docs/solidity-101/InsertionSort/#控制流)

`Solidity`的控制流与其他语言类似，主要包含以下几种：

1. `if-else`

   ```solidity
   function ifElseTest(uint256 _number) public pure returns(bool){
       if(_number == 0){
           return(true);
       }else{
           return(false);
       }
   }
   ```

   

2. `for循环`

   ```solidity
   function forLoopTest() public pure returns(uint256){
       uint sum = 0;
       for(uint i = 0; i < 10; i++){
           sum += i;
       }
       return(sum);
   }
   ```

   

3. `while循环`

   ```solidity
   function whileTest() public pure returns(uint256){
       uint sum = 0;
       uint i = 0;
       while(i < 10){
           sum += i;
           i++;
       }
       return(sum);
   }
   ```

   

4. `do-while循环`

   ```solidity
   function doWhileTest() public pure returns(uint256){
       uint sum = 0;
       uint i = 0;
       do{
           sum += i;
           i++;
       }while(i < 10);
       return(sum);
   }
   ```

   

5. `三元运算符`

   三元运算符是`Solidity`中唯一一个接受三个操作数的运算符，规则`条件? 条件为真的表达式:条件为假的表达式`。此运算符经常用作`if`语句的快捷方式。

   ```solidity
   // 三元运算符 ternary/conditional operator
   function ternaryTest(uint256 x, uint256 y) public pure returns(uint256){
       // return the max of x and y
       return x >= y ? x: y; 
   }
   ```

   

另外还有`continue`（立即进入下一个循环）和`break`（跳出当前循环）关键字可以使用。

## 用`Solidity`实现插入排序[](https://www.wtf.academy/docs/solidity-101/InsertionSort/#用solidity实现插入排序)

**写在前面：90%以上的人用`Solidity`写插入算法都会出错。**

### 插入排序[](https://www.wtf.academy/docs/solidity-101/InsertionSort/#插入排序)

排序算法解决的问题是将无序的一组数字，例如`[2, 5, 3, 1]`，从小到大依次排列好。插入排序（`InsertionSort`）是最简单的一种排序算法，也是很多人学习的第一个算法。它的思路很简单，从前往后，依次将每一个数和排在他前面的数字比大小，如果比前面的数字小，就互换位置。示意图：



![插入排序](https://i.pinimg.com/originals/92/b0/34/92b034385c440e08bc8551c97df0a2e3.gif)



### `python`代码[](https://www.wtf.academy/docs/solidity-101/InsertionSort/#python代码)

我们可以先看一下插入排序的python代码：

```python
# Python program for implementation of Insertion Sort
def insertionSort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i-1
        while j >=0 and key < arr[j] :
            arr[j+1] = arr[j]
            j -= 1
        arr[j+1] = key
    return arr
```



### 改写成`Solidity`后有`BUG`[](https://www.wtf.academy/docs/solidity-101/InsertionSort/#改写成solidity后有bug)

一共8行`python`代码就可以完成插入排序，非常简单。那么我们将它改写成`Solidity`代码，将函数，变量，循环等等都做了相应的转换，只需要9行代码：

```solidity
    // 插入排序 错误版
function insertionSortWrong(uint[] memory a) public pure returns(uint[] memory) {    
    for (uint i = 1;i < a.length;i++){
        uint temp = a[i];
        uint j=i-1;
        while( (j >= 0) && (temp < a[j])){
            a[j+1] = a[j];
            j--;
        }
        a[j+1] = temp;
    }
    return(a);
}
```



那我们把改好的放到`remix`上去跑，输入`[2, 5, 3, 1]`。BOOM！有`bug`！改了半天，没找到`bug`在哪。我又去`google`搜”solidity insertion sort”，然后发现网上用`solidity`写的插入算法教程都是错的，比如：[Sorting in Solidity without Comparison](https://medium.com/coinmonks/sorting-in-solidity-without-comparison-4eb47e04ff0d)

Remix decoded output 出现错误内容



![10-1](https://www.wtf.academy/assets/images/10-1-e9590da7aad6c176501b7fc5abe3372f.jpg)



### 正确的Solidity插入排序[](https://www.wtf.academy/docs/solidity-101/InsertionSort/#正确的solidity插入排序)

花了几个小时，在`Dapp-Learning`社群一个朋友的帮助下，终于找到了`bug`所在。`Solidity`中最常用的变量类型是`uint`，也就是正整数，取到负值的话，会报`underflow`错误。而在插入算法中，变量`j`有可能会取到`-1`，引起报错。

这里，我们需要把`j`加1，让它无法取到负值。正确代码：

```solidity
// 插入排序 正确版
function insertionSort(uint[] memory a) public pure returns(uint[] memory) {
    // note that uint can not take negative value
    for (uint i = 1;i < a.length;i++){
        uint temp = a[i];
        uint j=i;
        while( (j >= 1) && (temp < a[j-1])){
            a[j] = a[j-1];
            j--;
        }
        a[j] = temp;
    }
    return(a);
}
```



运行后的结果：



!["输入[2,5,3,1] 输出[1,2,3,5] "](https://images.mirror-media.xyz/publication-images/S-i6rwCMeXoi8eNJ0fRdB.png?height=300&width=554)



## 总结[](https://www.wtf.academy/docs/solidity-101/InsertionSort/#总结)

这一讲，我们介绍了`Solidity`中控制流，并且用`Solidity`写了插入排序。看起来很简单，但实际很难。这就是`Solidity`，坑很多，每个月都有项目因为这些小`bug`损失几千万甚至上亿美元。掌握好基础，不断练习，才能写出更好的`Solidity`代码。

# 11. 构造函数和修饰器

这一讲，我们将用合约权限控制（`Ownable`）的例子介绍`Solidity`语言中构造函数（`constructor`）和独有的修饰器（`modifier`）。

## 构造函数[](https://www.wtf.academy/docs/solidity-101/Modifier/#构造函数)

构造函数（`constructor`）是一种特殊的函数，每个合约可以定义一个，并在部署合约的时候自动运行一次。它可以用来初始化合约的一些参数，例如初始化合约的`owner`地址：

```solidity
address owner; // 定义owner变量

// 构造函数
constructor(address initialOwner) {
    owner = initialOwner; // 在部署合约的时候，将owner设置为传入的initialOwner地址
}
```



**注意**：构造函数在不同的Solidity版本中的语法并不一致，在Solidity 0.4.22之前，构造函数不使用 `constructor` 而是使用与合约名同名的函数作为构造函数而使用，由于这种旧写法容易使开发者在书写时发生疏漏（例如合约名叫 `Parents`，构造函数名写成 `parents`），使得构造函数变成普通函数，引发漏洞，所以0.4.22版本及之后，采用了全新的 `constructor` 写法。

构造函数的旧写法代码示例：

```solidity
pragma solidity =0.4.21;
contract Parents {
    // 与合约名Parents同名的函数就是构造函数
    function Parents () public {
    }
}
```



## 修饰器[](https://www.wtf.academy/docs/solidity-101/Modifier/#修饰器)

修饰器（`modifier`）是`Solidity`特有的语法，类似于面向对象编程中的装饰器（`decorator`），声明函数拥有的特性，并减少代码冗余。它就像钢铁侠的智能盔甲，穿上它的函数会带有某些特定的行为。`modifier`的主要使用场景是运行函数前的检查，例如地址，变量，余额等。



![钢铁侠的modifier](https://images.mirror-media.xyz/publication-images/nVwXsOVmrYu8rqvKKPMpg.jpg?height=630&width=1200)



我们来定义一个叫做onlyOwner的modifier：

```solidity
// 定义modifier
modifier onlyOwner {
   require(msg.sender == owner); // 检查调用者是否为owner地址
   _; // 如果是的话，继续运行函数主体；否则报错并revert交易
}
```



带有`onlyOwner`修饰符的函数只能被`owner`地址调用，比如下面这个例子：

```solidity
function changeOwner(address _newOwner) external onlyOwner{
   owner = _newOwner; // 只有owner地址运行这个函数，并改变owner
}
```



我们定义了一个`changeOwner`函数，运行它可以改变合约的`owner`，但是由于`onlyOwner`修饰符的存在，只有原先的`owner`可以调用，别人调用就会报错。这也是最常用的控制智能合约权限的方法。

### OpenZeppelin的Ownable标准实现[](https://www.wtf.academy/docs/solidity-101/Modifier/#openzeppelin的ownable标准实现)

`OpenZeppelin`是一个维护`Solidity`标准化代码库的组织，他的`Ownable`标准实现如下： https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable.sol

## Remix 演示示例[](https://www.wtf.academy/docs/solidity-101/Modifier/#remix-演示示例)

以 `Owner.sol` 为例。

1. 在 Remix 上编译并部署代码,在合约部署时传入 initialOwner 变量。

   

   ![11-1](https://www.wtf.academy/assets/images/11-1-64d6caedfc3572b91c7a9aaffa87a465.jpg)

   

2. 点击 `owner` 按钮查看当前 owner 变量。

   

   ![11-2](https://www.wtf.academy/assets/images/11-2-3c24cb56c6581a46cf5fdfd1c47a4b37.jpg)

   

3. 以 owner 地址的用户身份，调用 `changeOwner` 函数，交易成功。

   

   ![11-3](https://www.wtf.academy/assets/images/11-3-fe43138393f83103cac7459c315a83ef.jpg)

   

4. 以非 owner 地址的用户身份，调用 `changeOwner` 函数，交易失败，因为modifier onlyOwner 的检查语句不满足。

   

   ![11-4](https://www.wtf.academy/assets/images/11-4-955abaae5352e5430e7bfbdaa9cf98f3.jpg)

   

## 总结[](https://www.wtf.academy/docs/solidity-101/Modifier/#总结)

这一讲，我们介绍了`Solidity`中的构造函数和修饰符，并写了一个控制合约权限的`Ownable`合约。

# 12. 事件

这一讲，我们用转账ERC20代币为例来介绍`Solidity`中的事件（`event`）。

## 事件[](https://www.wtf.academy/docs/solidity-101/Event/#事件)

`Solidity`中的事件（`event`）是`EVM`上日志的抽象，它具有两个特点：

- 响应：应用程序（[`ethers.js`](https://learnblockchain.cn/docs/ethers.js/api-contract.html#id18)）可以通过`RPC`接口订阅和监听这些事件，并在前端做响应。
- 经济：事件是`EVM`上比较经济的存储数据的方式，每个大概消耗2,000 `gas`；相比之下，链上存储一个新变量至少需要20,000 `gas`。

### 声明事件[](https://www.wtf.academy/docs/solidity-101/Event/#声明事件)

事件的声明由`event`关键字开头，接着是事件名称，括号里面写好事件需要记录的变量类型和变量名。以`ERC20`代币合约的`Transfer`事件为例：

```solidity
event Transfer(address indexed from, address indexed to, uint256 value);
```



我们可以看到，`Transfer`事件共记录了3个变量`from`，`to`和`value`，分别对应代币的转账地址，接收地址和转账数量，其中`from`和`to`前面带有`indexed`关键字，他们会保存在以太坊虚拟机日志的`topics`中，方便之后检索。

### 释放事件[](https://www.wtf.academy/docs/solidity-101/Event/#释放事件)

我们可以在函数里释放事件。在下面的例子中，每次用`_transfer()`函数进行转账操作的时候，都会释放`Transfer`事件，并记录相应的变量。

```solidity
// 定义_transfer函数，执行转账逻辑
function _transfer(
    address from,
    address to,
    uint256 amount
) external {

    _balances[from] = 10000000; // 给转账地址一些初始代币

    _balances[from] -=  amount; // from地址减去转账数量
    _balances[to] += amount; // to地址加上转账数量

    // 释放事件
    emit Transfer(from, to, amount);
}
```



## EVM日志 `Log`[](https://www.wtf.academy/docs/solidity-101/Event/#evm日志-log)

以太坊虚拟机（EVM）用日志`Log`来存储`Solidity`事件，每条日志记录都包含主题`topics`和数据`data`两部分。



![12-3](https://www.wtf.academy/assets/images/12-3-06b5d454b3752b96000f8a9477fa31de.png)



### 主题 `topics`[](https://www.wtf.academy/docs/solidity-101/Event/#主题-topics)

日志的第一部分是主题数组，用于描述事件，长度不能超过`4`。它的第一个元素是事件的签名（哈希）。对于上面的`Transfer`事件，它的事件哈希就是：

```solidity
keccak256("Transfer(address,address,uint256)")

//0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef
```



除了事件哈希，主题还可以包含至多`3`个`indexed`参数，也就是`Transfer`事件中的`from`和`to`。

`indexed`标记的参数可以理解为检索事件的索引“键”，方便之后搜索。每个 `indexed` 参数的大小为固定的256比特，如果参数太大了（比如字符串），就会自动计算哈希存储在主题中。

### 数据 `data`[](https://www.wtf.academy/docs/solidity-101/Event/#数据-data)

事件中不带 `indexed`的参数会被存储在 `data` 部分中，可以理解为事件的“值”。`data` 部分的变量不能被直接检索，但可以存储任意大小的数据。因此一般 `data` 部分可以用来存储复杂的数据结构，例如数组和字符串等等，因为这些数据超过了256比特，即使存储在事件的 `topics` 部分中，也是以哈希的方式存储。另外，`data` 部分的变量在存储上消耗的gas相比于 `topics` 更少。

## `Remix`演示[](https://www.wtf.academy/docs/solidity-101/Event/#remix演示)

以 `Event.sol` 合约为例，编译部署。

然后调用 `_transfer` 函数。



![12-1](https://www.wtf.academy/assets/images/12-1-21d3090d03ff4dbb241e5810f2177fe8.jpg)



点击右侧的交易查看详情，可以看到日志的具体内容。



![12-2](https://www.wtf.academy/assets/images/12-2-4faa09c9994dc41555b86c1f023b4c38.jpg)



### 在Etherscan上查询事件[](https://www.wtf.academy/docs/solidity-101/Event/#在etherscan上查询事件)

我们尝试用`_transfer()`函数在`Sepolia`测试网络上转账100代币，可以在`Etherscan`上查询到相应的`tx`：[网址](https://sepolia.etherscan.io/tx/0xb07dcd9943662e2e8b17c7add370f046401962ce24d0690a61bb249a385dc8c9#eventlog)。

点击`Logs`按钮，就能看到事件明细：



![Event明细](https://www.wtf.academy/assets/images/12-4-3397b1066a143a21feb58ed7c697164d.png)



`Topics`里面有三个元素，`[0]`是这个事件的哈希，`[1]`和`[2]`是我们定义的两个`indexed`变量的信息，即转账的转出地址和接收地址。`Data`里面是剩下的不带`indexed`的变量，也就是转账数量。

## 总结[](https://www.wtf.academy/docs/solidity-101/Event/#总结)

这一讲，我们介绍了如何使用和查询`Solidity`中的事件。很多链上分析工具包括`Nansen`和`Dune Analysis`都是基于事件工作的。

# 13. 继承

这一讲，我们介绍`Solidity`中的继承（`inheritance`），包括简单继承，多重继承，以及修饰器（`Modifier`）和构造函数（`Constructor`）的继承。

## 继承[](https://www.wtf.academy/docs/solidity-101/Inheritance/#继承)

继承是面向对象编程很重要的组成部分，可以显著减少重复代码。如果把合约看作是对象的话，`Solidity`也是面向对象的编程，也支持继承。

### 规则[](https://www.wtf.academy/docs/solidity-101/Inheritance/#规则)

- `virtual`: 父合约中的函数，如果希望子合约重写，需要加上`virtual`关键字。
- `override`：子合约重写了父合约中的函数，需要加上`override`关键字。

**注意**：用`override`修饰`public`变量，会重写与变量同名的`getter`函数，例如：

```solidity
mapping(address => uint256) public override balanceOf;
```



### 简单继承[](https://www.wtf.academy/docs/solidity-101/Inheritance/#简单继承)

我们先写一个简单的爷爷合约`Yeye`，里面包含1个`Log`事件和3个`function`: `hip()`, `pop()`, `yeye()`，输出都是”Yeye”。

```solidity
contract Yeye {
    event Log(string msg);

    // 定义3个function: hip(), pop(), man()，Log值为Yeye。
    function hip() public virtual{
        emit Log("Yeye");
    }

    function pop() public virtual{
        emit Log("Yeye");
    }

    function yeye() public virtual {
        emit Log("Yeye");
    }
}
```



我们再定义一个爸爸合约`Baba`，让他继承`Yeye`合约，语法就是`contract Baba is Yeye`，非常直观。在`Baba`合约里，我们重写一下`hip()`和`pop()`这两个函数，加上`override`关键字，并将他们的输出改为`”Baba”`；并且加一个新的函数`baba`，输出也是`”Baba”`。

```solidity
contract Baba is Yeye{
    // 继承两个function: hip()和pop()，输出改为Baba。
    function hip() public virtual override{
        emit Log("Baba");
    }

    function pop() public virtual override{
        emit Log("Baba");
    }

    function baba() public virtual{
        emit Log("Baba");
    }
}
```



我们部署合约，可以看到`Baba`合约里有4个函数，其中`hip()`和`pop()`的输出被成功改写成`”Baba”`，而继承来的`yeye()`的输出仍然是`”Yeye”`。

### 多重继承[](https://www.wtf.academy/docs/solidity-101/Inheritance/#多重继承)

`Solidity`的合约可以继承多个合约。规则：

1. 继承时要按辈分最高到最低的顺序排。比如我们写一个`Erzi`合约，继承`Yeye`合约和`Baba`合约，那么就要写成`contract Erzi is Yeye, Baba`，而不能写成`contract Erzi is Baba, Yeye`，不然就会报错。
2. 如果某一个函数在多个继承的合约里都存在，比如例子中的`hip()`和`pop()`，在子合约里必须重写，不然会报错。
3. 重写在多个父合约中都重名的函数时，`override`关键字后面要加上所有父合约名字，例如`override(Yeye, Baba)`。

例子：

```solidity
contract Erzi is Yeye, Baba{
    // 继承两个function: hip()和pop()，输出值为Erzi。
    function hip() public virtual override(Yeye, Baba){
        emit Log("Erzi");
    }

    function pop() public virtual override(Yeye, Baba) {
        emit Log("Erzi");
    }
}
```



我们可以看到，`Erzi`合约里面重写了`hip()`和`pop()`两个函数，将输出改为`”Erzi”`，并且还分别从`Yeye`和`Baba`合约继承了`yeye()`和`baba()`两个函数。

### 修饰器的继承[](https://www.wtf.academy/docs/solidity-101/Inheritance/#修饰器的继承)

`Solidity`中的修饰器（`Modifier`）同样可以继承，用法与函数继承类似，在相应的地方加`virtual`和`override`关键字即可。

```solidity
contract Base1 {
    modifier exactDividedBy2And3(uint _a) virtual {
        require(_a % 2 == 0 && _a % 3 == 0);
        _;
    }
}

contract Identifier is Base1 {

    //计算一个数分别被2除和被3除的值，但是传入的参数必须是2和3的倍数
    function getExactDividedBy2And3(uint _dividend) public exactDividedBy2And3(_dividend) pure returns(uint, uint) {
        return getExactDividedBy2And3WithoutModifier(_dividend);
    }

    //计算一个数分别被2除和被3除的值
    function getExactDividedBy2And3WithoutModifier(uint _dividend) public pure returns(uint, uint){
        uint div2 = _dividend / 2;
        uint div3 = _dividend / 3;
        return (div2, div3);
    }
}
```



`Identifier`合约可以直接在代码中使用父合约中的`exactDividedBy2And3`修饰器，也可以利用`override`关键字重写修饰器：

```solidity
modifier exactDividedBy2And3(uint _a) override {
    _;
    require(_a % 2 == 0 && _a % 3 == 0);
}
```



### 构造函数的继承[](https://www.wtf.academy/docs/solidity-101/Inheritance/#构造函数的继承)

子合约有两种方法继承父合约的构造函数。举个简单的例子，父合约`A`里面有一个状态变量`a`，并由构造函数的参数来确定：

```solidity
// 构造函数的继承
abstract contract A {
    uint public a;

    constructor(uint _a) {
        a = _a;
    }
}
```



1. 在继承时声明父构造函数的参数，例如：`contract B is A(1)`

2. 在子合约的构造函数中声明构造函数的参数，例如：

   ```solidity
   contract C is A {
       constructor(uint _c) A(_c * _c) {}
   }
   ```

   

### 调用父合约的函数[](https://www.wtf.academy/docs/solidity-101/Inheritance/#调用父合约的函数)

子合约有两种方式调用父合约的函数，直接调用和利用`super`关键字。

1. 直接调用：子合约可以直接用`父合约名.函数名()`的方式来调用父合约函数，例如`Yeye.pop()`

   ```solidity
   function callParent() public{
       Yeye.pop();
   }
   ```

   

2. `super`关键字：子合约可以利用`super.函数名()`来调用最近的父合约函数。`Solidity`继承关系按声明时从右到左的顺序是：`contract Erzi is Yeye, Baba`，那么`Baba`是最近的父合约，`super.pop()`将调用`Baba.pop()`而不是`Yeye.pop()`：

   ```solidity
   function callParentSuper() public{
       // 将调用最近的父合约函数，Baba.pop()
       super.pop();
   }
   ```

   

### 钻石继承[](https://www.wtf.academy/docs/solidity-101/Inheritance/#钻石继承)

在面向对象编程中，钻石继承（菱形继承）指一个派生类同时有两个或两个以上的基类。

在多重+菱形继承链条上使用`super`关键字时，需要注意的是使用`super`会调用继承链条上的每一个合约的相关函数，而不是只调用最近的父合约。

我们先写一个合约`God`，再写`Adam`和`Eve`两个合约继承`God`合约，最后让创建合约`people`继承自`Adam`和`Eve`，每个合约都有`foo`和`bar`两个函数。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.13;

/* 继承树：
  God
 /  \
Adam Eve
 \  /
people
*/

contract God {
    event Log(string message);

    function foo() public virtual {
        emit Log("God.foo called");
    }

    function bar() public virtual {
        emit Log("God.bar called");
    }
}

contract Adam is God {
    function foo() public virtual override {
        emit Log("Adam.foo called");
        super.foo();
    }

    function bar() public virtual override {
        emit Log("Adam.bar called");
        super.bar();
    }
}

contract Eve is God {
    function foo() public virtual override {
        emit Log("Eve.foo called");
        super.foo();
    }

    function bar() public virtual override {
        emit Log("Eve.bar called");
        super.bar();
    }
}

contract people is Adam, Eve {
    function foo() public override(Adam, Eve) {
        super.foo();
    }

    function bar() public override(Adam, Eve) {
        super.bar();
    }
}
```



在这个例子中，调用合约`people`中的`super.bar()`会依次调用`Eve`、`Adam`，最后是`God`合约。

虽然`Eve`、`Adam`都是`God`的子合约，但整个过程中`God`合约只会被调用一次。原因是`Solidity`借鉴了Python的方式，强制一个由基类构成的DAG（有向无环图）使其保证一个特定的顺序。更多细节你可以查阅[Solidity的官方文档](https://solidity-cn.readthedocs.io/zh/develop/contracts.html?highlight=继承#index-16)。

## 在Remix上验证[](https://www.wtf.academy/docs/solidity-101/Inheritance/#在remix上验证)

- 合约简单继承示例, 可以观察到Baba合约多了Yeye的函数

  

  ![13-1](https://www.wtf.academy/assets/images/13-1-42f0a6c7cc188762c41239403eb84e8b.png)

  ![13-2](https://www.wtf.academy/assets/images/13-2-9c0be37c4fab16f90c39580cbbead5ed.png)

  

- 合约多重继承可以参考简单继承的操作步骤来增加部署Erzi合约，然后观察暴露的函数以及尝试调用来查看日志

- 修饰器继承示例

  

  ![13-3](https://www.wtf.academy/assets/images/13-3-7fb3ed386135bd918b84cd92949884a4.png)

  ![13-4](https://www.wtf.academy/assets/images/13-4-c578cff17c65f768d1505da77c3cac0c.png)

  ![13-5](https://www.wtf.academy/assets/images/13-5-58a3d5a358dbda0ffb40afb626801005.png)

  

- 构造函数继承示例

  

  ![13-6](https://www.wtf.academy/assets/images/13-6-099cd67439dcb0194684557cc1e29289.png)

  ![13-7](https://www.wtf.academy/assets/images/13-7-2c772dcd6711e67afd51118ae7ded35e.png)

  

- 调用父合约示例

  

  ![13-8](https://www.wtf.academy/assets/images/13-8-dcc83777980c789aec12ff8467b8d51f.png)

  ![13-9](https://www.wtf.academy/assets/images/13-9-49f35bff8cf0343cbbce2dd8fe9d3c59.png)

  

- 菱形继承示例

  

  ![13-10](https://www.wtf.academy/assets/images/13-10-3e690c6705a19b1e5b7d43a0570f5d0e.png)

  

## 总结[](https://www.wtf.academy/docs/solidity-101/Inheritance/#总结)

这一讲，我们介绍了`Solidity`继承的基本用法，包括简单继承，多重继承，修饰器和构造函数的继承、调用父合约中的函数，以及多重继承中的菱形继承问题。

# 14. 抽象合约和接口

这一讲，我们用`ERC721`的接口合约为例介绍`Solidity`中的抽象合约（`abstract`）和接口（`interface`），帮助大家更好的理解`ERC721`标准。

## 抽象合约[](https://www.wtf.academy/docs/solidity-101/Interface/#抽象合约)

如果一个智能合约里至少有一个未实现的函数，即某个函数缺少主体`{}`中的内容，则必须将该合约标为`abstract`，不然编译会报错；另外，未实现的函数需要加`virtual`，以便子合约重写。拿我们之前的[插入排序合约](https://github.com/AmazingAng/WTF-Solidity/tree/main/10_InsertionSort)为例，如果我们还没想好具体怎么实现插入排序函数，那么可以把合约标为`abstract`，之后让别人补写上。

```solidity
abstract contract InsertionSort{
    function insertionSort(uint[] memory a) public pure virtual returns(uint[] memory);
}
```



## 接口[](https://www.wtf.academy/docs/solidity-101/Interface/#接口)

接口类似于抽象合约，但它不实现任何功能。接口的规则：

1. 不能包含状态变量
2. 不能包含构造函数
3. 不能继承除接口外的其他合约
4. 所有函数都必须是external且不能有函数体
5. 继承接口的非抽象合约必须实现接口定义的所有功能

虽然接口不实现任何功能，但它非常重要。接口是智能合约的骨架，定义了合约的功能以及如何触发它们：如果智能合约实现了某种接口（比如`ERC20`或`ERC721`），其他Dapps和智能合约就知道如何与它交互。因为接口提供了两个重要的信息：

1. 合约里每个函数的`bytes4`选择器，以及函数签名`函数名(每个参数类型）`。
2. 接口id（更多信息见[EIP165](https://eips.ethereum.org/EIPS/eip-165)）

另外，接口与合约`ABI`（Application Binary Interface）等价，可以相互转换：编译接口可以得到合约的`ABI`，利用[abi-to-sol工具](https://gnidan.github.io/abi-to-sol/)，也可以将`ABI json`文件转换为`接口sol`文件。

我们以`ERC721`接口合约`IERC721`为例，它定义了3个`event`和9个`function`，所有`ERC721`标准的NFT都实现了这些函数。我们可以看到，接口和常规合约的区别在于每个函数都以`;`代替函数体`{ }`结尾。

```solidity
interface IERC721 is IERC165 {
    event Transfer(address indexed from, address indexed to, uint256 indexed tokenId);
    event Approval(address indexed owner, address indexed approved, uint256 indexed tokenId);
    event ApprovalForAll(address indexed owner, address indexed operator, bool approved);
    
    function balanceOf(address owner) external view returns (uint256 balance);

    function ownerOf(uint256 tokenId) external view returns (address owner);

    function safeTransferFrom(address from, address to, uint256 tokenId) external;

    function transferFrom(address from, address to, uint256 tokenId) external;

    function approve(address to, uint256 tokenId) external;

    function getApproved(uint256 tokenId) external view returns (address operator);

    function setApprovalForAll(address operator, bool _approved) external;

    function isApprovedForAll(address owner, address operator) external view returns (bool);

    function safeTransferFrom( address from, address to, uint256 tokenId, bytes calldata data) external;
}
```



### IERC721事件[](https://www.wtf.academy/docs/solidity-101/Interface/#ierc721事件)

`IERC721`包含3个事件，其中`Transfer`和`Approval`事件在`ERC20`中也有。

- `Transfer`事件：在转账时被释放，记录代币的发出地址`from`，接收地址`to`和`tokenId`。
- `Approval`事件：在授权时被释放，记录授权地址`owner`，被授权地址`approved`和`tokenId`。
- `ApprovalForAll`事件：在批量授权时被释放，记录批量授权的发出地址`owner`，被授权地址`operator`和授权与否的`approved`。

### IERC721函数[](https://www.wtf.academy/docs/solidity-101/Interface/#ierc721函数)

- `balanceOf`：返回某地址的NFT持有量`balance`。
- `ownerOf`：返回某`tokenId`的主人`owner`。
- `transferFrom`：普通转账，参数为转出地址`from`，接收地址`to`和`tokenId`。
- `safeTransferFrom`：安全转账（如果接收方是合约地址，会要求实现`ERC721Receiver`接口）。参数为转出地址`from`，接收地址`to`和`tokenId`。
- `approve`：授权另一个地址使用你的NFT。参数为被授权地址`approve`和`tokenId`。
- `getApproved`：查询`tokenId`被批准给了哪个地址。
- `setApprovalForAll`：将自己持有的该系列NFT批量授权给某个地址`operator`。
- `isApprovedForAll`：查询某地址的NFT是否批量授权给了另一个`operator`地址。
- `safeTransferFrom`：安全转账的重载函数，参数里面包含了`data`。

### 什么时候使用接口？[](https://www.wtf.academy/docs/solidity-101/Interface/#什么时候使用接口)

如果我们知道一个合约实现了`IERC721`接口，我们不需要知道它具体代码实现，就可以与它交互。

无聊猿`BAYC`属于`ERC721`代币，实现了`IERC721`接口的功能。我们不需要知道它的源代码，只需知道它的合约地址，用`IERC721`接口就可以与它交互，比如用`balanceOf()`来查询某个地址的`BAYC`余额，用`safeTransferFrom()`来转账`BAYC`。

```solidity
contract interactBAYC {
    // 利用BAYC地址创建接口合约变量（ETH主网）
    IERC721 BAYC = IERC721(0xBC4CA0EdA7647A8aB7C2061c2E118A18a936f13D);

    // 通过接口调用BAYC的balanceOf()查询持仓量
    function balanceOfBAYC(address owner) external view returns (uint256 balance){
        return BAYC.balanceOf(owner);
    }

    // 通过接口调用BAYC的safeTransferFrom()安全转账
    function safeTransferFromBAYC(address from, address to, uint256 tokenId) external{
        BAYC.safeTransferFrom(from, to, tokenId);
    }
}
```



## 在Remix上验证[](https://www.wtf.academy/docs/solidity-101/Interface/#在remix上验证)

- 抽象合约示例（简单的演示代码如图所示）

  

  ![14-1](https://www.wtf.academy/assets/images/14-1-044a8470458eea92577e72cdbdd8dd24.png)

  

- 接口示例（简单的演示代码如图所示）

  

  ![14-2](https://www.wtf.academy/assets/images/14-2-ab611255e74b10302e9bd7a41763de91.png)

  

## 总结[](https://www.wtf.academy/docs/solidity-101/Interface/#总结)

这一讲，我介绍了`Solidity`中的抽象合约（`abstract`）和接口（`interface`），他们都可以写模版并且减少代码冗余。我们还讲了`ERC721`接口合约`IERC721`，以及如何利用它与无聊猿`BAYC`合约进行交互。

# 15. 异常

这一讲，我们介绍`Solidity`三种抛出异常的方法：`error`，`require`和`assert`，并比较三种方法的`gas`消耗。

## 异常[](https://www.wtf.academy/docs/solidity-101/Errors/#异常)

写智能合约经常会出`bug`，`Solidity`中的异常命令帮助我们`debug`。

### Error[](https://www.wtf.academy/docs/solidity-101/Errors/#error)

`error`是`solidity 0.8.4版本`新加的内容，方便且高效（省`gas`）地向用户解释操作失败的原因，同时还可以在抛出异常的同时携带参数，帮助开发者更好地调试。人们可以在`contract`之外定义异常。下面，我们定义一个`TransferNotOwner`异常，当用户不是代币`owner`的时候尝试转账，会抛出错误：

```solidity
error TransferNotOwner(); // 自定义error
```



我们也可以定义一个携带参数的异常，来提示尝试转账的账户地址

```solidity
error TransferNotOwner(address sender); // 自定义的带参数的error
```



在执行当中，`error`必须搭配`revert`（回退）命令使用。

```solidity
function transferOwner1(uint256 tokenId, address newOwner) public {
    if(_owners[tokenId] != msg.sender){
        revert TransferNotOwner();
        // revert TransferNotOwner(msg.sender);
    }
    _owners[tokenId] = newOwner;
}
```



我们定义了一个`transferOwner1()`函数，它会检查代币的`owner`是不是发起人，如果不是，就会抛出`TransferNotOwner`异常；如果是的话，就会转账。

### Require[](https://www.wtf.academy/docs/solidity-101/Errors/#require)

`require`命令是`solidity 0.8版本`之前抛出异常的常用方法，目前很多主流合约仍然还在使用它。它很好用，唯一的缺点就是`gas`随着描述异常的字符串长度增加，比`error`命令要高。使用方法：`require(检查条件，"异常的描述")`，当检查条件不成立的时候，就会抛出异常。

我们用`require`命令重写一下上面的`transferOwner1`函数：

```solidity
function transferOwner2(uint256 tokenId, address newOwner) public {
    require(_owners[tokenId] == msg.sender, "Transfer Not Owner");
    _owners[tokenId] = newOwner;
}
```



### Assert[](https://www.wtf.academy/docs/solidity-101/Errors/#assert)

`assert`命令一般用于程序员写程序`debug`，因为它不能解释抛出异常的原因（比`require`少个字符串）。它的用法很简单，`assert(检查条件）`，当检查条件不成立的时候，就会抛出异常。

我们用`assert`命令重写一下上面的`transferOwner1`函数：

```solidity
function transferOwner3(uint256 tokenId, address newOwner) public {
    assert(_owners[tokenId] == msg.sender);
    _owners[tokenId] = newOwner;
}
```



## 在remix上验证[](https://www.wtf.academy/docs/solidity-101/Errors/#在remix上验证)

1. 输入任意`uint256`数字和非0地址，调用`transferOwner1`，也就是`error`方法，控制台抛出了异常并显示我们自定义的`TransferNotOwner`。

   

   ![15-1.png](https://www.wtf.academy/assets/images/15-1-108068d779547bb5f2bbe63c4e350fab.png)

   

2. 输入任意`uint256`数字和非0地址，调用`transferOwner2`，也就是`require`方法，控制台抛出了异常并打印出`require`中的字符串。

   

   ![15-2.png](https://www.wtf.academy/assets/images/15-2-5cd86c90ad4a466946c842c346a5ee18.png)

   

3. 输入任意`uint256`数字和非0地址，调用`transferOwner3`，也就是`assert`方法，控制台只抛出了异常。

   

   ![15-3.png](https://www.wtf.academy/assets/images/15-3-390b3562e3410dd9f6256b66e8d2610f.png)

   

## 三种方法的gas比较[](https://www.wtf.academy/docs/solidity-101/Errors/#三种方法的gas比较)

我们比较一下三种抛出异常的`gas`消耗，通过remix控制台的Debug按钮，能查到每次函数调用的`gas`消耗分别如下： （使用0.8.17版本编译）

1. **`error`方法`gas`消耗**：24457 (**加入参数后`gas`消耗**：24660)
2. **`require`方法`gas`消耗**：24755
3. **`assert`方法`gas`消耗**：24473

我们可以看到，`error`方法`gas`最少，其次是`assert`，`require`方法消耗`gas`最多！因此，`error`既可以告知用户抛出异常的原因，又能省`gas`，大家要多用！（注意，由于部署测试时间的不同，每个函数的`gas`消耗会有所不同，但是比较结果会是一致的。）

**备注:** Solidity 0.8.0之前的版本，`assert`抛出的是一个 `panic exception`，会把剩余的 `gas` 全部消耗，不会返还。更多细节见[官方文档](https://docs.soliditylang.org/en/v0.8.17/control-structures.html)。

## 总结[](https://www.wtf.academy/docs/solidity-101/Errors/#总结)

这一讲，我们介绍`Solidity`三种抛出异常的方法：`error`，`require`和`assert`，并比较了三种方法的`gas`消耗。结论：`error`既可以告知用户抛出异常的原因，又能省`gas`。