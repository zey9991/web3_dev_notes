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



### 4. 定长字节数组

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

### 5. 枚举 enum

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

## 在 Remix 上运行

- 部署合约后可以查看每个类型的变量的数值：



![2-1.png](https://www.wtf.academy/assets/images/2-1-90414d7e21f49e75101a07a8a55e602c.png)



- `enum` 和 `uint` 转换的示例：



![2-2.png](https://www.wtf.academy/assets/images/2-2-6c364618b30e6c498127e2d129f9e7e8.png)

![2-3.png](https://www.wtf.academy/assets/images/2-3-d2742673ffbd4df5c230d48a02a2921c.png)



## 总结

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

### storage

合约里的状态变量默认都是`storage`，存储在链上。

### memory

函数里的参数和临时变量一般用`memory`，存储在内存中，不上链。尤其是如果返回数据类型是变长的情况下，必须加memory修饰，例如：string, bytes, array和自定义结构。

### calldata

和`memory`类似，存储在内存中，不上链。与`memory`的不同点在于`calldata`变量不能修改（`immutable`），一般用于函数的参数。例子：

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

## 变量的作用域

`Solidity`中变量按作用域划分有三种，分别是状态变量（state variable），局部变量（local variable）和全局变量(global variable)

### 1. 状态变量

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



### 2. 局部变量

局部变量是仅在函数执行过程中有效的变量，函数退出后，变量无效。局部变量的数据存储在内存里，不上链，`gas`低。局部变量在函数内声明：

```solidity
function bar() external pure returns(uint){
    uint xx = 1;
    uint yy = 3;
    uint zz = xx + yy;
    return(zz);
}
```



### 3. 全局变量（预留关键字）

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



### 4. 全局变量-以太单位与时间单位

#### 以太单位

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

`assert` 是 Solidity 中的一个内置函数，常用于进行 **程序内部的调试检查**，确保某些条件在执行期间始终成立。如果 `assert` 语句中的条件为 **false**，则会触发 **异常**，并停止执行合约代码。

`assert` 通常用于检查**永远不应该失败的条件**，比如数学运算中的除零、数组越界、对不可变变量的错误修改等。

一般来说，`assert` 用来捕捉程序中的**不可恢复的错误**，如果断言失败，就说明程序有严重错误。

**Example:**



![5-5.png](https://www.wtf.academy/assets/images/5-5-767daeb69da57fbfafec524599f721aa.png)



#### 时间单位

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



## 总结

在这一讲，我们介绍了`Solidity`中的引用类型，数据位置和变量的作用域。重点是`storage`, `memory`和`calldata`三个关键字的用法。他们出现的原因是为了节省链上有限的存储空间和降低`gas`。下一讲我们会介绍引用类型中的数组。

# 6. 引用类型, array, struct

这一讲，我们将介绍`Solidity`中的两个重要变量类型：数组（`array`）和结构体（`struct`）。

## 数组 array

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

### 创建数组的规则

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

  

### 数组成员

- `length`: 数组有一个包含元素数量的`length`成员，`memory`数组的长度在创建后是固定的。
- `push()`: `动态数组`拥有`push()`成员，可以在数组最后添加一个`0`元素，并返回该元素的引用。
- `push(x)`: `动态数组`拥有`push(x)`成员，可以在数组最后添加一个`x`元素。
- `pop()`: `动态数组`拥有`pop()`成员，可以移除数组最后一个元素。

**Example:**



![6-1.png](https://www.wtf.academy/assets/images/6-1-ff58f00a7e037fcd318401ca2bc350b6.png)



## 结构体 struct

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



## 总结

这一讲，我们介绍了Solidity中数组（`array`）和结构体（`struct`）的基本用法。下一讲我们将介绍Solidity中的哈希表——映射（`mapping`）。

# 7. 映射类型 mapping

这一讲，我们将介绍映射（`Mapping`）类型，Solidity中存储键值对的数据结构，可以理解为哈希表。

## 映射Mapping

在映射中，人们可以通过键（`Key`）来查询对应的值（`Value`），比如：通过一个人的`id`来查询他的钱包地址。

声明映射的格式为`mapping(_KeyType => _ValueType)`，其中`_KeyType`和`_ValueType`分别是`Key`和`Value`的变量类型。例子：

```solidity
mapping(uint => address) public idToAddress; // id映射到地址
mapping(address => address) public swapPair; // 币对的映射，地址到地址
```



## 映射的规则

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

  

## 映射的原理

- **原理1**: 映射不储存任何键（`Key`）的资讯，也没有length的资讯。
  - 这意味着你无法遍历一个映射，也无法获取映射的所有键，除非你使用外部手段来追踪这些键。

- **原理2**: 映射使用`keccak256(abi.encodePacked(key, slot))`当成offset存取value，其中`slot`是映射变量定义所在的插槽位置。
  - **Solidity 中的映射数据通过 `keccak256` 哈希函数来定位**。存储时，键值对中的键和映射变量的插槽位置会被编码后通过 `keccak256` 生成一个哈希值，哈希值作为存储位置的偏移量。由于是通过哈希计算位置，所以映射不会暴露所有键。
  - **`slot` 是映射在存储布局中的位置**，每个映射变量都有一个固定的插槽（`slot`），并根据键值进行哈希计算来确定具体数据的存储位置。

- **原理3**: 因为Ethereum会定义所有未使用的空间为0，所以未赋值（`Value`）的键（`Key`）初始值都是各个type的默认值，如uint的默认值是0。

## [在Remix上验证 (以 `Mapping.sol`为例)](https://www.wtf.academy/docs/solidity-101/Mapping/#在remix上验证-以-mappingsol为例)

- 映射示例 1 部署

  

  ![7-1](https://www.wtf.academy/assets/images/7-1-2768f65eec9dbbc8771275b45c937e96.jpg)

  这个图展示了一个映射合约部署到 Remix IDE 中，并成功编译和部署。这个过程证明了映射在 Solidity 中的基本工作原理。

- 映射示例 2 初始值

  

  ![7-2](https://www.wtf.academy/assets/images/7-2-886db6cf3743df280acac78c151971f3.jpg)

  这个图展示了一个映射中尚未赋值的键的默认值。在例子中，查询未赋值的键，返回了 `uint` 类型的默认值 `0`。这印证了原理3：所有未赋值的键在查询时都会返回该类型的默认值。

- 映射示例 3 key-value pair

  

  ![7-3](https://www.wtf.academy/assets/images/7-3-88745249067310f5e280dd60b2560adb.jpg)

  这个图展示了将一个键值对存入映射后，可以通过键查询到相应的值。该图表明了映射如何存储和检索键值对数据。

## 总结

这一讲，我们介绍了Solidity中哈希表——映射（`Mapping`）的用法。至此，我们已经学习了所有常用变量种类，之后我们会学习控制流`if-else`，`while`等。

# 8. 变量初始值

## 变量初始值

在`Solidity`中，声明但没赋值的变量都有它的初始值或默认值。这一讲，我们将介绍常用变量的初始值。

### 值类型初始值

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



### 引用类型初始值

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



### `delete`操作符

`delete a`会让变量`a`的值变为初始值。

```solidity
// delete操作符
bool public _bool2 = true; 
function d() external {
    delete _bool2; // delete 会让_bool2变为默认值，false
}
```



## 在remix上验证

- 部署合约查看值类型、引用类型的初始值

  

  ![8-1.png](https://www.wtf.academy/assets/images/8-1-bf8a5eafba9f2a6be29c8a116a5465bc.png)

  

- 值类型、引用类型`delete`操作后的默认值

  

  ![8-2.png](https://www.wtf.academy/assets/images/8-2-968b7c57cb793dc524a5665dfae26624.png)

  

## 总结

这一讲，我们介绍了`Solidity`中变量的初始值。变量被声明但没有赋值的时候，它的值默认为初始值。不同类型的变量初始值不同，`delete`操作符可以删除一个变量的值并代替为初始值。

# 9. 常数 constant和immutable

这一讲，我们介绍Solidity中和常量相关的两个关键字，`constant`（常量）和`immutable`（不变量）。状态变量声明这两个关键字之后，不能在初始化后更改数值。这样做的好处是提升合约的安全性并节省`gas`。

另外，只有数值变量可以声明`constant`和`immutable`；`string`和`bytes`可以声明为`constant`，但不能为`immutable`。

### constant

`constant`变量必须在声明的时候初始化，之后再也不能改变。尝试改变的话，编译不通过。

```solidity
// constant变量必须在声明的时候初始化，之后不能改变
uint256 constant CONSTANT_NUM = 10;
string constant CONSTANT_STRING = "0xAA";
bytes constant CONSTANT_BYTES = "WTF";
address constant CONSTANT_ADDRESS = 0x0000000000000000000000000000000000000000;
```



### immutable

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



## 在remix上验证

1. 部署好合约之后，通过remix上的`getter`函数，能获取到`constant`和`immutable`变量初始化好的值。

   

   ![9-1.png](https://www.wtf.academy/assets/images/9-1-4dd7d40c9799d42c60e4793394a4eb5e.png)

   

2. `constant`变量初始化之后，尝试改变它的值，会编译不通过并抛出`TypeError: Cannot assign to a constant variable.`的错误。

   

   ![9-2.png](https://www.wtf.academy/assets/images/9-2-5b85f9969dff8fbeb78cac9f8d4089ce.png)

   

3. `immutable`变量初始化之后，尝试改变它的值，会编译不通过并抛出`TypeError: Immutable state variable already initialized.`的错误。

   

   ![9-3.png](data:image/png;base64,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)

   

## 总结

这一讲，我们介绍了Solidity中两个关键字，`constant`（常量）和`immutable`（不变量），让不应该变的变量保持不变。这样的做法能在节省`gas`的同时提升合约的安全性。

# 10. 控制流，用Solidity实现插入排序

这一讲，我们将介绍`Solidity`中的控制流，然后讲如何用`Solidity`实现插入排序（`InsertionSort`），一个看起来简单，但实际上很容易写出`bug`的程序。

## 控制流

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

## 用`Solidity`实现插入排序

**写在前面：90%以上的人用`Solidity`写插入算法都会出错。**

### 插入排序

排序算法解决的问题是将无序的一组数字，例如`[2, 5, 3, 1]`，从小到大依次排列好。插入排序（`InsertionSort`）是最简单的一种排序算法，也是很多人学习的第一个算法。它的思路很简单，从前往后，依次将每一个数和排在他前面的数字比大小，如果比前面的数字小，就互换位置。示意图：



![插入排序](https://i.pinimg.com/originals/92/b0/34/92b034385c440e08bc8551c97df0a2e3.gif)



### `python`代码

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



### 改写成`Solidity`后有`BUG、

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



### 正确的Solidity插入排序

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



## 总结

这一讲，我们介绍了`Solidity`中控制流，并且用`Solidity`写了插入排序。看起来很简单，但实际很难。这就是`Solidity`，坑很多，每个月都有项目因为这些小`bug`损失几千万甚至上亿美元。掌握好基础，不断练习，才能写出更好的`Solidity`代码。

# 11. 构造函数和修饰器

这一讲，我们将用合约权限控制（`Ownable`）的例子介绍`Solidity`语言中构造函数（`constructor`）和独有的修饰器（`modifier`）。

## 构造函数constructor

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



## 修饰器modifier

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

### OpenZeppelin的Ownable标准实现

`OpenZeppelin`是一个维护`Solidity`标准化代码库的组织，他的`Ownable`标准实现如下： https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable.sol

## Remix 演示示例

以 `Owner.sol` 为例。

1. 在 Remix 上编译并部署代码,在合约部署时传入 initialOwner 变量。

   

   ![11-1](https://www.wtf.academy/assets/images/11-1-64d6caedfc3572b91c7a9aaffa87a465.jpg)

   

2. 点击 `owner` 按钮查看当前 owner 变量。

   

   ![11-2](https://www.wtf.academy/assets/images/11-2-3c24cb56c6581a46cf5fdfd1c47a4b37.jpg)

   

3. 以 owner 地址的用户身份，调用 `changeOwner` 函数，交易成功。

   

   ![11-3](https://www.wtf.academy/assets/images/11-3-fe43138393f83103cac7459c315a83ef.jpg)

   

4. 以非 owner 地址的用户身份，调用 `changeOwner` 函数，交易失败，因为modifier onlyOwner 的检查语句不满足。

   

   ![11-4](https://www.wtf.academy/assets/images/11-4-955abaae5352e5430e7bfbdaa9cf98f3.jpg)

   

## 总结

这一讲，我们介绍了`Solidity`中的构造函数和修饰符，并写了一个控制合约权限的`Ownable`合约。

# 12. 事件

这一讲，我们用转账ERC20代币为例来介绍`Solidity`中的事件（`event`）。

## 事件

`Solidity`中的事件（`event`）是`EVM`上日志的抽象，它具有两个特点：

- 响应：应用程序（[`ethers.js`](https://learnblockchain.cn/docs/ethers.js/api-contract.html#id18)）可以通过`RPC`接口订阅和监听这些事件，并在前端做响应。
- 经济：事件是`EVM`上比较经济的存储数据的方式，每个大概消耗2,000 `gas`；相比之下，链上存储一个新变量至少需要20,000 `gas`。

### 声明事件

事件的声明由`event`关键字开头，接着是事件名称，括号里面写好事件需要记录的变量类型和变量名。以`ERC20`代币合约的`Transfer`事件为例：

```solidity
event Transfer(address indexed from, address indexed to, uint256 value);
```



我们可以看到，`Transfer`事件共记录了3个变量`from`，`to`和`value`，分别对应代币的转账地址，接收地址和转账数量，其中`from`和`to`前面带有`indexed`关键字，他们会保存在以太坊虚拟机日志的`topics`中，方便之后检索。

### 释放事件

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



## EVM日志 `Log`

以太坊虚拟机（EVM）用日志`Log`来存储`Solidity`事件，每条日志记录都包含主题`topics`和数据`data`两部分。



![12-3](https://www.wtf.academy/assets/images/12-3-06b5d454b3752b96000f8a9477fa31de.png)



### 主题 `topics`

日志的第一部分是主题数组，用于描述事件，长度不能超过`4`。它的第一个元素是事件的签名（哈希）。对于上面的`Transfer`事件，它的事件哈希就是：

```solidity
keccak256("Transfer(address,address,uint256)")

//0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef
```



除了事件哈希，主题还可以包含至多`3`个`indexed`参数，也就是`Transfer`事件中的`from`和`to`。

`indexed`标记的参数可以理解为检索事件的索引“键”，方便之后搜索。每个 `indexed` 参数的大小为固定的256比特，如果参数太大了（比如字符串），就会自动计算哈希存储在主题中。

在 Solidity 中，事件可以有多个参数，但最多只有 **三个** 带有 `indexed` 的参数。

`indexed` 关键字可以修饰多种基本类型，但不支持动态数组、结构体和映射类型。因此，使用时需要遵循这些规则。

### 数据 `data`

事件中不带 `indexed`的参数会被存储在 `data` 部分中，可以理解为事件的“值”。`data` 部分的变量不能被直接检索，但可以存储任意大小的数据。因此一般 `data` 部分可以用来存储复杂的数据结构，例如数组和字符串等等，因为这些数据超过了256比特，即使存储在事件的 `topics` 部分中，也是以哈希的方式存储。另外，`data` 部分的变量在存储上消耗的gas相比于 `topics` 更少。

## `Remix`演示

以 `Event.sol` 合约为例，编译部署。

然后调用 `_transfer` 函数。



![12-1](https://www.wtf.academy/assets/images/12-1-21d3090d03ff4dbb241e5810f2177fe8.jpg)



点击右侧的交易查看详情，可以看到日志的具体内容。



![12-2](https://www.wtf.academy/assets/images/12-2-4faa09c9994dc41555b86c1f023b4c38.jpg)



### 在Etherscan上查询事件

我们尝试用`_transfer()`函数在`Sepolia`测试网络上转账100代币，可以在`Etherscan`上查询到相应的`tx`：[网址](https://sepolia.etherscan.io/tx/0xb07dcd9943662e2e8b17c7add370f046401962ce24d0690a61bb249a385dc8c9#eventlog)。

点击`Logs`按钮，就能看到事件明细：



![Event明细](https://www.wtf.academy/assets/images/12-4-3397b1066a143a21feb58ed7c697164d.png)



`Topics`里面有三个元素，`[0]`是这个事件的哈希，`[1]`和`[2]`是我们定义的两个`indexed`变量的信息，即转账的转出地址和接收地址。`Data`里面是剩下的不带`indexed`的变量，也就是转账数量。

## 总结

这一讲，我们介绍了如何使用和查询`Solidity`中的事件。很多链上分析工具包括`Nansen`和`Dune Analysis`都是基于事件工作的。

# 13. 继承

这一讲，我们介绍`Solidity`中的继承（`inheritance`），包括简单继承，多重继承，以及修饰器（`Modifier`）和构造函数（`Constructor`）的继承。

## 继承

继承是面向对象编程很重要的组成部分，可以显著减少重复代码。如果把合约看作是对象的话，`Solidity`也是面向对象的编程，也支持继承。

### 规则

- `virtual`: 父合约中的函数，如果希望子合约重写，需要加上`virtual`关键字。
- `override`：子合约重写了父合约中的函数，需要加上`override`关键字。

**注意**：用`override`修饰`public`变量，会重写与变量同名的`getter`函数，例如：

```solidity
mapping(address => uint256) public override balanceOf;
```

```solidity
// 父合约
contract Parent {
    // 声明一个可重写的函数
    function greet() public virtual returns (string memory) {
        return "Hello from Parent";
    }
}

// 子合约
contract Child is Parent {
    // 重写父合约中的 greet 函数
    function greet() public override returns (string memory) {
        return "Hello from Child";
    }
}

```



### 简单继承

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

### 多重继承

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

### 修饰器的继承

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



### 构造函数的继承

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



1. 在继承时声明父构造函数的参数，例如：`contract B is A(1)`// B 合约自动调用 A(1) 构造函数，a = 1

2. 在子合约的构造函数中声明构造函数的参数，例如：

   ```solidity
   contract C is A {
       constructor(uint _c) A(_c * _c) {}
   }
   ```

   合约 `C` 继承了父合约 `A`，但它在自己的构造函数中调用父合约的构造函数，并将参数 `_c * _c` 传递给父合约的构造函数。例如，如果 `_c` 的值为 `3`，则父合约 `A` 的构造函数将接收到 `9`，并将状态变量 `a` 初始化为 `9`。

3. **方式1**：在继承声明时直接指定父构造函数参数，简化了子合约的部署，但参数是固定的。

   **方式2**：在子合约构造函数中调用父构造函数，允许子合约在部署时传递动态参数。

### 调用父合约的函数

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

   

### 钻石继承

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

## 在Remix上验证

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

  

## 总结

这一讲，我们介绍了`Solidity`继承的基本用法，包括简单继承，多重继承，修饰器和构造函数的继承、调用父合约中的函数，以及多重继承中的菱形继承问题。

# 14. 抽象合约和接口

这一讲，我们用`ERC721`的接口合约为例介绍`Solidity`中的抽象合约（`abstract`）和接口（`interface`），帮助大家更好的理解`ERC721`标准。

## 抽象合约

如果一个智能合约里至少有一个未实现的函数，即某个函数缺少主体`{}`中的内容，则必须将该合约标为`abstract`，不然编译会报错；另外，未实现的函数需要加`virtual`，以便子合约重写。拿我们之前的[插入排序合约](https://github.com/AmazingAng/WTF-Solidity/tree/main/10_InsertionSort)为例，如果我们还没想好具体怎么实现插入排序函数，那么可以把合约标为`abstract`，之后让别人补写上。

```solidity
abstract contract InsertionSort{
    function insertionSort(uint[] memory a) public pure virtual returns(uint[] memory);
}
```



## 接口

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



### IERC721事件

`IERC721`包含3个事件，其中`Transfer`和`Approval`事件在`ERC20`中也有。

- `Transfer`事件：在转账时被释放，记录代币的发出地址`from`，接收地址`to`和`tokenId`。
- `Approval`事件：在授权时被释放，记录授权地址`owner`，被授权地址`approved`和`tokenId`。
- `ApprovalForAll`事件：在批量授权时被释放，记录批量授权的发出地址`owner`，被授权地址`operator`和授权与否的`approved`。

### IERC721函数

- `balanceOf`：返回某地址的NFT持有量`balance`。
- `ownerOf`：返回某`tokenId`的主人`owner`。
- `transferFrom`：普通转账，参数为转出地址`from`，接收地址`to`和`tokenId`。
- `safeTransferFrom`：安全转账（如果接收方是合约地址，会要求实现`ERC721Receiver`接口）。参数为转出地址`from`，接收地址`to`和`tokenId`。
- `approve`：授权另一个地址使用你的NFT。参数为被授权地址`approve`和`tokenId`。
- `getApproved`：查询`tokenId`被批准给了哪个地址。
- `setApprovalForAll`：将自己持有的该系列NFT批量授权给某个地址`operator`。
- `isApprovedForAll`：查询某地址的NFT是否批量授权给了另一个`operator`地址。
- `safeTransferFrom`：安全转账的重载函数，参数里面包含了`data`。

### 什么时候使用接口？

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



## 在Remix上验证

- 抽象合约示例（简单的演示代码如图所示）

  

  ![14-1](https://www.wtf.academy/assets/images/14-1-044a8470458eea92577e72cdbdd8dd24.png)

  

- 接口示例（简单的演示代码如图所示）

  

  ![14-2](https://www.wtf.academy/assets/images/14-2-ab611255e74b10302e9bd7a41763de91.png)

  

## 总结

这一讲，我介绍了`Solidity`中的抽象合约（`abstract`）和接口（`interface`），他们都可以写模版并且减少代码冗余。我们还讲了`ERC721`接口合约`IERC721`，以及如何利用它与无聊猿`BAYC`合约进行交互。

# 15. 异常

这一讲，我们介绍`Solidity`三种抛出异常的方法：`error`，`require`和`assert`，并比较三种方法的`gas`消耗。

## 异常

写智能合约经常会出`bug`，`Solidity`中的异常命令帮助我们`debug`。

### Error

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

### Require

`require`命令是`solidity 0.8版本`之前抛出异常的常用方法，目前很多主流合约仍然还在使用它。它很好用，唯一的缺点就是`gas`随着描述异常的字符串长度增加，比`error`命令要高。使用方法：`require(检查条件，"异常的描述")`，当检查条件不成立的时候，就会抛出异常。

我们用`require`命令重写一下上面的`transferOwner1`函数：

```solidity
function transferOwner2(uint256 tokenId, address newOwner) public {
    require(_owners[tokenId] == msg.sender, "Transfer Not Owner");
    _owners[tokenId] = newOwner;
}
```



### Assert

`assert`命令一般用于程序员写程序`debug`，因为它不能解释抛出异常的原因（比`require`少个字符串）。它的用法很简单，`assert(检查条件）`，当检查条件不成立的时候，就会抛出异常。

我们用`assert`命令重写一下上面的`transferOwner1`函数：

```solidity
function transferOwner3(uint256 tokenId, address newOwner) public {
    assert(_owners[tokenId] == msg.sender);
    _owners[tokenId] = newOwner;
}
```



## 在remix上验证

1. 输入任意`uint256`数字和非0地址，调用`transferOwner1`，也就是`error`方法，控制台抛出了异常并显示我们自定义的`TransferNotOwner`。

   

   ![15-1.png](https://www.wtf.academy/assets/images/15-1-108068d779547bb5f2bbe63c4e350fab.png)

   

2. 输入任意`uint256`数字和非0地址，调用`transferOwner2`，也就是`require`方法，控制台抛出了异常并打印出`require`中的字符串。

   

   ![15-2.png](https://www.wtf.academy/assets/images/15-2-5cd86c90ad4a466946c842c346a5ee18.png)

   

3. 输入任意`uint256`数字和非0地址，调用`transferOwner3`，也就是`assert`方法，控制台只抛出了异常。

   

   ![15-3.png](https://www.wtf.academy/assets/images/15-3-390b3562e3410dd9f6256b66e8d2610f.png)

   

## 三种方法的gas比较

我们比较一下三种抛出异常的`gas`消耗，通过remix控制台的Debug按钮，能查到每次函数调用的`gas`消耗分别如下： （使用0.8.17版本编译）

1. **`error`方法`gas`消耗**：24457 (**加入参数后`gas`消耗**：24660)
2. **`require`方法`gas`消耗**：24755
3. **`assert`方法`gas`消耗**：24473

我们可以看到，`error`方法`gas`最少，其次是`assert`，`require`方法消耗`gas`最多！因此，`error`既可以告知用户抛出异常的原因，又能省`gas`，大家要多用！（注意，由于部署测试时间的不同，每个函数的`gas`消耗会有所不同，但是比较结果会是一致的。）

**备注:** Solidity 0.8.0之前的版本，`assert`抛出的是一个 `panic exception`，会把剩余的 `gas` 全部消耗，不会返还。更多细节见[官方文档](https://docs.soliditylang.org/en/v0.8.17/control-structures.html)。

## 总结

这一讲，我们介绍`Solidity`三种抛出异常的方法：`error`，`require`和`assert`，并比较了三种方法的`gas`消耗。结论：`error`既可以告知用户抛出异常的原因，又能省`gas`。

# 16. 函数重载

## 重载

`Solidity`中允许函数进行重载（`overloading`），即名字相同但输入参数类型不同的函数可以同时存在，他们被视为不同的函数。==注意，`Solidity`不允许修饰器（`modifier`）重载。==

### 函数重载

举个例子，我们可以定义两个都叫`saySomething()`的函数，一个没有任何参数，输出`"Nothing"`；另一个接收一个`string`参数，输出这个`string`。

```solidity
function saySomething() public pure returns(string memory){
    return("Nothing");
}

function saySomething(string memory something) public pure returns(string memory){
    return(something);
}
```



最终重载函数在经过编译器编译后，由于不同的参数类型，都变成了不同的函数选择器（selector）。关于函数选择器的具体内容可参考[WTF Solidity极简入门: 29. 函数选择器Selector](https://github.com/AmazingAng/WTF-Solidity/tree/main/29_Selector)。

以 `Overloading.sol` 合约为例，在 Remix 上编译部署后，分别调用重载函数 `saySomething()` 和 `saySomething(string memory something)`，可以看到他们返回了不同的结果，被区分为不同的函数。



![16-1.jpg](https://www.wtf.academy/assets/images/16-1-02e5e7643e93251800ec337e341a58a4.jpg)



### 实参匹配（Argument Matching）

在调用重载函数时，会把输入的实际参数和函数参数的变量类型做匹配。 如果出现多个匹配的重载函数，则会报错。下面这个例子有两个叫`f()`的函数，一个参数为`uint8`，另一个为`uint256`：

```solidity
function f(uint8 _in) public pure returns (uint8 out) {
    out = _in;
}

function f(uint256 _in) public pure returns (uint256 out) {
    out = _in;
}
```



我们调用`f(50)`，因为`50`既可以被转换为`uint8`，也可以被转换为`uint256`，因此会报错。

## 总结

这一讲，我们介绍了`Solidity`中函数重载的基本用法：名字相同但输入参数类型不同的函数可以同时存在，他们被视为不同的函数。

# 17. 库合约 站在巨人的肩膀上

这一讲，我们用`ERC721`的引用的库合约`Strings`为例介绍`Solidity`中的库合约（`Library`），并总结了常用的库合约。

## 库合约

库合约是一种特殊的合约，为了提升`Solidity`代码的复用性和减少`gas`而存在。库合约是一系列的函数合集，由大神或者项目方创作，咱们站在巨人的肩膀上，会用就行了。



![库合约：站在巨人的肩膀上](https://images.mirror-media.xyz/publication-images/HJC0UjkALdrL8a2BmAE2J.jpeg?height=300&width=388)



他和普通合约主要有以下几点不同：

1. 不能存在状态变量
2. 不能够继承或被继承
3. 不能接收以太币
4. 不可以被销毁

需要注意的是，库合约重的函数可见性如果被设置为`public`或者`external`，则在调用函数时会触发一次`delegatecall`。而如果被设置为`internal`，则不会引起。对于设置为`private`可见性的函数来说，其仅能在库合约中可见，在其他合约中不可用。

## Strings库合约

`Strings库合约`是将`uint256`类型转换为相应的`string`类型的代码库，样例代码如下：

```solidity
library Strings {
    bytes16 private constant _HEX_SYMBOLS = "0123456789abcdef";

    /**
     * @dev Converts a `uint256` to its ASCII `string` decimal representation.
     */
    function toString(uint256 value) public pure returns (string memory) {
        // Inspired by OraclizeAPI's implementation - MIT licence
        // https://github.com/oraclize/ethereum-api/blob/b42146b063c7d6ee1358846c198246239e9360e8/oraclizeAPI_0.4.25.sol

        if (value == 0) {
            return "0";
        }
        uint256 temp = value;
        uint256 digits;
        while (temp != 0) {
            digits++;
            temp /= 10;
        }
        bytes memory buffer = new bytes(digits);
        while (value != 0) {
            digits -= 1;
            buffer[digits] = bytes1(uint8(48 + uint256(value % 10)));
            value /= 10;
        }
        return string(buffer);
    }

    /**
     * @dev Converts a `uint256` to its ASCII `string` hexadecimal representation.
     */
    function toHexString(uint256 value) public pure returns (string memory) {
        if (value == 0) {
            return "0x00";
        }
        uint256 temp = value;
        uint256 length = 0;
        while (temp != 0) {
            length++;
            temp >>= 8;
        }
        return toHexString(value, length);
    }

    /**
     * @dev Converts a `uint256` to its ASCII `string` hexadecimal representation with fixed length.
     */
    function toHexString(uint256 value, uint256 length) public pure returns (string memory) {
        bytes memory buffer = new bytes(2 * length + 2);
        buffer[0] = "0";
        buffer[1] = "x";
        for (uint256 i = 2 * length + 1; i > 1; --i) {
            buffer[i] = _HEX_SYMBOLS[value & 0xf];
            value >>= 4;
        }
        require(value == 0, "Strings: hex length insufficient");
        return string(buffer);
    }
}
```



他主要包含两个函数，`toString()`将`uint256`转为`string`，`toHexString()`将`uint256`转换为`16进制`，在转换为`string`。

### 如何使用库合约

我们用`Strings`库合约的`toHexString()`来演示两种使用库合约中函数的办法。

#### 利用using for指令

指令`using A for B;`可用于附加库合约（从库 A）到任何类型（B）。添加完指令后，库`A`中的函数会自动添加为`B`类型变量的成员，可以直接调用。注意：在调用的时候，这个变量会被当作第一个参数传递给函数：

```solidity
// 利用using for指令
using Strings for uint256;
function getString1(uint256 _number) public pure returns(string memory){
    // 库合约中的函数会自动添加为uint256型变量的成员
    return _number.toHexString();
}
```



#### 通过库合约名称调用函数

```solidity
// 直接通过库合约名调用
function getString2(uint256 _number) public pure returns(string memory){
    return Strings.toHexString(_number);
}
```



我们部署合约并输入`170`测试一下，两种方法均能返回正确的`16进制string` “0xaa”。证明我们调用库合约成功！



![成功调用库合约](https://images.mirror-media.xyz/publication-images/bzB_JDC9f5VWHRjsjQyQa.png?height=750&width=580)



## 总结

这一讲，我们用`ERC721`的引用的库合约`Strings`为例介绍`Solidity`中的库合约（`Library`）。99%的开发者都不需要自己去写库合约，会用大神写的就可以了。我们只需要知道什么情况该用什么库合约。常用的有：

1. [Strings](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/4a9cc8b4918ef3736229a5cc5a310bdc17bf759f/contracts/utils/Strings.sol)：将`uint256`转换为`String`
2. [Address](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/4a9cc8b4918ef3736229a5cc5a310bdc17bf759f/contracts/utils/Address.sol)：判断某个地址是否为合约地址
3. [Create2](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/4a9cc8b4918ef3736229a5cc5a310bdc17bf759f/contracts/utils/Create2.sol)：更安全的使用`Create2 EVM opcode`
4. [Arrays](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/4a9cc8b4918ef3736229a5cc5a310bdc17bf759f/contracts/utils/Arrays.sol)：跟数组相关的库合约

# 18. Import

在Solidity中，`import`语句可以帮助我们在一个文件中引用另一个文件的内容（导入其他合约中的全局符号，这包括合约、库、接口的声明，允许在当前合约中使用它们的函数、变量等。不过，`import` 并不允许直接访问其他合约中的私有变量或内部变量），提高代码的可重用性和组织性。本教程将向你介绍如何在Solidity中使用`import`语句。

## `import`用法

- 通过源文件相对位置导入，例子：

  ```text
  文件结构
  ├── Import.sol
  └── Yeye.sol
  
  // 通过文件相对位置import
  import './Yeye.sol';
  ```

  

- 通过源文件网址导入网上的合约的全局符号，例子：

  ```text
  // 通过网址引用
  import 'https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/Address.sol';
  ```

  

- 通过`npm`的目录导入，例子：

  ```solidity
  import '@openzeppelin/contracts/access/Ownable.sol';
  ```

  

- 通过指定`全局符号`导入合约特定的全局符号，例子：

  ```solidity
  import {Yeye} from './Yeye.sol';
  ```

  

- 引用(`import`)在代码中的位置为：在声明版本号之后，在其余代码之前。



例题  以下import写法错误的是：

选择一个答案

A. `import from "./Yeye.sol";`

B. `import {Yeye} from "./Yeye.sol"; `

**正确**：这种写法用于导入特定的合约或库。

C. `import {Yeye as Wowo} from "./Yeye.sol";`

**正确**：这种写法用于导入特定的合约或库，并且可以重命名。

D. `import * as Wowo from "./Yeye.sol";`

**正确**：这种写法用于导入整个模块。

## 测试导入结果

我们可以用下面这段代码测试是否成功导入了外部源代码：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.21;

// 通过文件相对位置import
import './Yeye.sol';
// 通过`全局符号`导入特定的合约
import {Yeye} from './Yeye.sol';
// 通过网址引用
import 'https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/Address.sol';
// 引用OpenZeppelin合约
import '@openzeppelin/contracts/access/Ownable.sol';

contract Import {
    // 成功导入Address库
    using Address for address;
    // 声明yeye变量
    Yeye yeye = new Yeye();

    // 测试是否能调用yeye的函数
    function test() external{
        yeye.hip();
    }
}
```





![result](https://www.wtf.academy/assets/images/18-1-be3039b3dda4b85f9a3197fbe6102abb.png)



## 总结

这一讲，我们介绍了利用`import`关键字导入外部源代码的方法。通过`import`关键字，可以引用我们写的其他文件中的合约或者函数，也可以直接导入别人写好的代码，非常方便。

例题  被导入文件中的全局符号想要被其他合约单独导入，应该怎么编写？

选择一个答案

A. 将合约结构包含

B. 包含在合约结构中

C. 与合约并列在文件结构中

解析  当我们说“被导入文件中的全局符号想要被其他合约单独导入”，指的是：

- 如果某个文件（比如 `Library.sol`）中定义了多个合约、库、结构体等，而你只希望导入其中的某一个或几个全局符号，通常需要确保这些符号是在合约结构之外定义的。
- 例如，如果你在 `Library.sol` 中有多个结构体和合约，并且你只想导入某个特定的结构体，你需要把它放在合约的外部，而不是放在某个合约的内部





# 19. 接收ETH receive和fallback

`Solidity`支持两种特殊的回调函数，`receive()`和`fallback()`，他们主要在两种情况下被使用：

1. 接收ETH
2. 处理合约中不存在的函数调用（代理合约proxy contract）

注意⚠️：在Solidity 0.6.x版本之前，语法上只有 `fallback()` 函数，用来接收用户发送的ETH时调用以及在被调用函数签名没有匹配到时，来调用。 0.6版本之后，Solidity才将 `fallback()` 函数拆分成 `receive()` 和 `fallback()` 两个函数。

我们这一讲主要讲接收ETH的情况。

## 接收ETH函数 receive

`receive()`函数是在合约收到`ETH`转账时被调用的函数。一个合约最多有一个`receive()`函数，声明方式与一般函数不一样，不需要`function`关键字：`receive() external payable { ... }`。`receive()`函数不能有任何的参数，不能返回任何值，必须包含`external`和`payable`。

当合约接收ETH的时候，`receive()`会被触发。`receive()`最好不要执行太多的逻辑因为如果别人用`send`和`transfer`方法发送`ETH`的话，`gas`会限制在`2300`，`receive()`太复杂可能会触发`Out of Gas`报错；如果用`call`就可以自定义`gas`执行更复杂的逻辑（这三种发送ETH的方法我们之后会讲到）。

我们可以在`receive()`里发送一个`event`，例如：

```solidity
// 定义事件
event Received(address Sender, uint Value);
// 接收ETH时释放Received事件
receive() external payable {
    emit Received(msg.sender, msg.value);
}
```



有些恶意合约，会在`receive()` 函数（老版本的话，就是 `fallback()` 函数）嵌入恶意消耗`gas`的内容或者使得执行故意失败的代码，导致一些包含退款和转账逻辑的合约不能正常工作，因此写包含退款等逻辑的合约时候，一定要注意这种情况。

## 回退函数 fallback

`fallback()`函数会在调用合约不存在的函数时被触发。可用于接收ETH，也可以用于代理合约`proxy contract`。`fallback()`声明时不需要`function`关键字，必须由`external`修饰，一般也会用`payable`修饰，用于接收ETH:`fallback() external payable { ... }`。

我们定义一个`fallback()`函数，被触发时候会释放`fallbackCalled`事件，并输出`msg.sender`，`msg.value`和`msg.data`:

```solidity
event fallbackCalled(address Sender, uint Value, bytes Data);

// fallback
fallback() external payable{
    emit fallbackCalled(msg.sender, msg.value, msg.data);
}
```



## receive和fallback的区别

`receive`和`fallback`都能够用于接收`ETH`，他们触发的规则如下：

```text
触发fallback() 还是 receive()?
           接收ETH
              |
         msg.data是空？
            /  \
          是    否
          /      \
receive()存在?   fallback()
        / \
       是  否
      /     \
receive()   fallback()
```



简单来说，合约接收`ETH`时，`msg.data`为空且存在`receive()`时，会触发`receive()`；`msg.data`不为空或不存在`receive()`时，会触发`fallback()`，此时`fallback()`必须为`payable`。

`receive()`和`payable fallback()`均不存在的时候，向合约**直接**发送`ETH`将会报错（你仍可以通过带有`payable`的函数向合约发送`ETH`）。

## Remix 演示

1. 首先在 Remix 上部署合约 "Fallback.sol"。

2. "VALUE" 栏中填入要发送给合约的金额（单位是 Wei），然后点击 "Transact"。

   

   ![19-1.jpg](https://www.wtf.academy/assets/images/19-1-4ba34e6d9cbb74a98a3c8affd59bc583.jpg)

   

3. 可以看到交易成功，并且触发了 "receivedCalled" 事件。

   

   ![19-2.jpg](https://www.wtf.academy/assets/images/19-2-b933741438ce18210739446f85b8e3c4.jpg)

   

4. "VALUE" 栏中填入要发送给合约的金额（单位是 Wei），"CALLDATA" 栏中填入随意编写的`msg.data`，然后点击 "Transact"。

   

   ![19-3.jpg](https://www.wtf.academy/assets/images/19-3-83c411c3270d886d6ea0535c4cc9660d.jpg)

   

5. 可以看到交易成功，并且触发了 "fallbackCalled" 事件。

   

   ![19-4.jpg](https://www.wtf.academy/assets/images/19-4-a6bbcb103838f43fe8987b95606b8e27.jpg)

   

## 总结

这一讲，我介绍了`Solidity`中的两种特殊函数，`receive()`和`fallback()`，他们主要在两种情况下被使用，处理接收`ETH`和代理合约`proxy contract`。

# 20. 发送ETH

`Solidity`有三种方法向其他合约发送`ETH`，他们是：`transfer()`，`send()`和`call()`，其中`call()`是被鼓励的用法。

## 接收ETH合约

我们先部署一个接收`ETH`合约`ReceiveETH`。`ReceiveETH`合约里有一个事件`Log`，记录收到的`ETH`数量和`gas`剩余。还有两个函数，一个是`receive()`函数，收到`ETH`被触发，并发送`Log`事件；另一个是查询合约`ETH`余额的`getBalance()`函数。

```solidity
contract ReceiveETH {
    // 收到eth事件，记录amount和gas
    event Log(uint amount, uint gas);
    
    // receive方法，接收eth时被触发
    receive() external payable{
        emit Log(msg.value, gasleft());
    }
    
    // 返回合约ETH余额
    function getBalance() view public returns(uint) {
        return address(this).balance;
    }
}
```



部署`ReceiveETH`合约后，运行`getBalance()`函数，可以看到当前合约的`ETH`余额为`0`。



![20-1](https://www.wtf.academy/assets/images/20-1-b18baa5867c909e527eca6852945ad46.png)



## 发送ETH合约

我们将实现三种方法向`ReceiveETH`合约发送`ETH`。首先，先在发送ETH合约`SendETH`中实现`payable`的`构造函数`和`receive()`，让我们能够在部署时和部署后向合约转账。

```solidity
contract SendETH {
    // 构造函数，payable使得部署的时候可以转eth进去
    constructor() payable{}
    // receive方法，接收eth时被触发
    receive() external payable{}
}
```



### transfer

- 用法是`接收方地址.transfer(发送ETH数额)`。
- `transfer()`的`gas`限制是`2300`，足够用于转账，但对方合约的`fallback()`或`receive()`函数不能实现太复杂的逻辑。
- `transfer()`如果转账失败，会自动`revert`（回滚交易）。

代码样例，注意里面的`_to`填`ReceiveETH`合约的地址，`amount`是`ETH`转账金额：

```solidity
// 用transfer()发送ETH
function transferETH(address payable _to, uint256 amount) external payable{
    _to.transfer(amount);
}
```



部署`SendETH`合约后，对`ReceiveETH`合约发送ETH，此时`amount`为10，`value`为0，`amount`>`value`，转账失败，发生`revert`。



![20-2](https://www.wtf.academy/assets/images/20-2-572c8ac0dfa42d4ea7fc62de0ff1c5af.png)



此时`amount`为10，`value`为10，`amount`<=`value`，转账成功。



![20-3](https://www.wtf.academy/assets/images/20-3-c48a1c9f41ff2a53095bbf4d0b7767b7.png)



在`ReceiveETH`合约中，运行`getBalance()`函数，可以看到当前合约的`ETH`余额为`10`。



![20-4](data:image/png;base64,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)



### send

- 用法是`接收方地址.send(发送ETH数额)`。
- `send()`的`gas`限制是`2300`，足够用于转账，但对方合约的`fallback()`或`receive()`函数不能实现太复杂的逻辑。
- `send()`如果转账失败，不会`revert`。
- `send()`的返回值是`bool`，代表着转账成功或失败，需要额外代码处理一下。

代码样例：

```solidity
error SendFailed(); // 用send发送ETH失败error

// send()发送ETH
function sendETH(address payable _to, uint256 amount) external payable{
    // 处理下send的返回值，如果失败，revert交易并发送error
    bool success = _to.send(amount);
    if(!success){
        revert SendFailed();
    }
}
```



对`ReceiveETH`合约发送ETH，此时`amount`为10，`value`为0，`amount`>`value`，转账失败，因为经过处理，所以发生`revert`。



![20-5](https://www.wtf.academy/assets/images/20-5-cb457285c7185c438995bfcc95b6a01d.png)



此时`amount`为10，`value`为11，`amount`<=`value`，转账成功。



![20-6](https://www.wtf.academy/assets/images/20-6-1ae2f81d902c618059d813e5b16cbe4c.png)



### call

- 用法是`接收方地址.call{value: 发送ETH数额}("")`。
- `call()`没有`gas`限制，可以支持对方合约`fallback()`或`receive()`函数实现复杂逻辑。
- `call()`如果转账失败，不会`revert`。
- `call()`的==返回值是`(bool, bytes)`==，其中`bool`代表着转账成功或失败，需要额外代码处理一下。

代码样例：

```solidity
error CallFailed(); // 用call发送ETH失败error

// call()发送ETH
function callETH(address payable _to, uint256 amount) external payable{
    // 处理下call的返回值，如果失败，revert交易并发送error
    (bool success,) = _to.call{value: amount}("");
    if(!success){
        revert CallFailed();
    }
}
```



对`ReceiveETH`合约发送ETH，此时`amount`为10，`value`为0，`amount`>`value`，转账失败，因为经过处理，所以发生`revert`。



![20-7](https://www.wtf.academy/assets/images/20-7-bbfe1e7134676767c0a6c9612165ea9e.png)



此时`amount`为10，`value`为11，`amount`<=`value`，转账成功。



![20-8](https://www.wtf.academy/assets/images/20-8-5c25a6d4556ce624ff27752f24e85d4a.png)



运行三种方法，可以看到，他们都可以成功地向`ReceiveETH`合约发送`ETH`。

## 总结

这一讲，我们介绍`Solidity`三种发送`ETH`的方法：`transfer`，`send`和`call`。

- `call`没有`gas`限制，最为灵活，是最提倡的方法；
- `transfer`有`2300 gas`限制，但是发送失败会自动`revert`交易，是次优选择；
- `send`有`2300 gas`限制，而且发送失败不会自动`revert`交易，几乎没有人用它。

## 例题

假设存在如下两个合约(sendETH和ReceiveETH)，两个合约目前ETH余额皆为0，现在vitalik想通过SendETH合约的callETH函数往ReceiveETH合约转入1ETH，他将交易的value设置为2ETH，同时交易成功执行，那么此时sendETH合约和ReceiveETH的ETH余额分别为？

```solidity
error CallFailed(); // 用call发送ETH失败error
error SendFailed();
// call()发送ETH
function callETH(address payable _to, uint256 amount) external payable{
    // 处理下call的返回值，如果失败，revert交易并发送error
    (bool success,) = _to.call{value: amount}("");
    if(!success){
        revert CallFailed();
    }
}
contract ReceiveETH {
    // 收到eth事件，记录amount和gas
    event Log(uint amount, uint gas);
    // receive方法，接收eth时被触发
    receive() external payable{
        emit Log(msg.value, gasleft());
    }  
}
```

A. 1ETH；1ETH

B. 0ETH；2ETH

C. 0ETH；1ETH

D. 2ETH；0ETH

正确答案是：

**C. 0ETH；1ETH**

解释：

1. `SendETH` 合约中的 `callETH` 函数通过 `call{value: amount}("")` 将 `amount`（即 1 ETH）发送给 `ReceiveETH` 合约。
2. `vitalik` 发起交易时设置了 `value = 2 ETH`，但 `callETH` 函数仅通过 `amount` 参数发送了 1 ETH 给 `ReceiveETH` 合约。
3. 剩下的 1 ETH（2 ETH - 1 ETH）将保留在 `SendETH` 合约中作为未使用的余额。

因此：

- `SendETH` 合约的余额为 **0 ETH**，因为所有发送的 ETH 都通过 `callETH` 被传递走了。
- `ReceiveETH` 合约接收了 1 ETH，余额为 **1 ETH**。



# 21. 调用其他合约

## 调用已部署合约

在`Solidity`中，一个合约可以调用另一个合约的函数，这在构建复杂的DApps时非常有用。本教程将会介绍如何在已知合约代码（或接口）和地址的情况下，调用已部署的合约。

## 目标合约

我们先写一个简单的合约`OtherContract`，用于被其他合约调用。

```solidity
contract OtherContract {
    uint256 private _x = 0; // 状态变量_x
    // 收到eth的事件，记录amount和gas
    event Log(uint amount, uint gas);
    
    // 返回合约ETH余额
    function getBalance() view public returns(uint) {
        return address(this).balance;
    }

    // 可以调整状态变量_x的函数，并且可以往合约转ETH (payable)
    function setX(uint256 x) external payable{
        _x = x;
        // 如果转入ETH，则释放Log事件
        if(msg.value > 0){
            emit Log(msg.value, gasleft());
        }
    }

    // 读取_x
    function getX() external view returns(uint x){
        x = _x;
    }
}
```



这个合约包含一个状态变量`_x`，一个事件`Log`在收到`ETH`时触发，三个函数：

- `getBalance()`: 返回合约`ETH`余额。
- `setX()`: `external payable`函数，可以设置`_x`的值，并向合约发送`ETH`。
- `getX()`: 读取`_x`的值。

## 调用`OtherContract`合约

我们可以利用合约的地址和合约代码（或接口）来创建合约的引用：`_Name(_Address)`，其中`_Name`是合约名，应与合约代码（或接口）中标注的合约名保持一致，`_Address`是合约地址。然后用合约的引用来调用它的函数：`_Name(_Address).f()`，其中`f()`是要调用的函数。

下面我们介绍4个调用合约的例子，在remix中编译合约后，分别部署`OtherContract`和`CallContract`：



![deploy contract0 in remix](https://www.wtf.academy/assets/images/21-1-9c522c370dfc53d1a0c273716f949c9e.png)





![deploy contract1 in remix](https://www.wtf.academy/assets/images/21-2-a3c672e6dca937bf09dc3dfe5a421534.png)





![deploy contract2 in remix](https://www.wtf.academy/assets/images/21-3-dd0cfc401d8462761c9b740ec21aa994.png)



### 1. 传入合约地址

我们可以在函数里传入目标合约地址，生成目标合约的引用，然后调用目标函数。以调用`OtherContract`合约的`setX`函数为例，我们在新合约中写一个`callSetX`函数，传入已部署好的`OtherContract`合约地址`_Address`和`setX`的参数`x`：

```solidity
function callSetX(address _Address, uint256 x) external{
    OtherContract(_Address).setX(x);
}
```



复制`OtherContract`合约的地址，填入`callSetX`函数的参数中，成功调用后，调用`OtherContract`合约中的`getX`验证`x`变为123



![call contract1 in remix](https://www.wtf.academy/assets/images/21-4-89e705ffc18c8f90063c922e7504b31e.png)





![call contract2 in remix](https://www.wtf.academy/assets/images/21-5-52866e87f467b4ebad52d6d00d4d2744.png)



### 2. 传入合约变量

我们可以直接在函数里传入合约的引用，只需要把上面参数的`address`类型改为目标合约名，比如`OtherContract`。下面例子实现了调用目标合约的`getX()`函数。

**注意**：该函数参数`OtherContract _Address`底层类型仍然是`address`，生成的`ABI`中、调用`callGetX`时传入的参数都是`address`类型

```solidity
function callGetX(OtherContract _Address) external view returns(uint x){
    x = _Address.getX();
}
```



复制`OtherContract`合约的地址，填入`callGetX`函数的参数中，调用后成功获取`x`的值



![call contract3 in remix](https://www.wtf.academy/assets/images/21-6-615b6ab5f73c18a1c4a7a7d0be5f7228.png)



### 3. 创建合约变量

我们可以创建合约变量，然后通过它来调用目标函数。下面例子，我们给变量`oc`存储了`OtherContract`合约的引用：

```solidity
function callGetX2(address _Address) external view returns(uint x){
    OtherContract oc = OtherContract(_Address);
    x = oc.getX();
}
```



复制`OtherContract`合约的地址，填入`callGetX2`函数的参数中，调用后成功获取`x`的值



![call contract4 in remix](https://www.wtf.academy/assets/images/21-7-ab9a5e3d84b27006392eb368b1e93d2d.png)



### 4. 调用合约并发送`ETH`

如果目标合约的函数是`payable`的，那么我们可以通过调用它来给合约转账：`_Name(_Address).f{value: _Value}()`，其中`_Name`是合约名，`_Address`是合约地址，`f`是目标函数名，`_Value`是要转的`ETH`数额（以`wei`为单位）。

`OtherContract`合约的`setX`函数是`payable`的，在下面这个例子中我们通过调用`setX`来往目标合约转账。

```solidity
function setXTransferETH(address otherContract, uint256 x) payable external{
    OtherContract(otherContract).setX{value: msg.value}(x);
}
```



复制`OtherContract`合约的地址，填入`setXTransferETH`函数的参数中，并转入10ETH



![call contract5 in remix](https://www.wtf.academy/assets/images/21-8-3566ee52a32b536dded77112c6599bdb.png)



转账后，我们可以通过`Log`事件和`getBalance()`函数观察目标合约`ETH`余额的变化。



![call contract6 in remix](https://www.wtf.academy/assets/images/21-9-d90c3bad37dd4d77acbd2ea8b695242e.png)



## 总结

这一讲，我们介绍了如何通过目标合约代码（或接口）和地址来创建合约的引用，从而调用目标合约的函数。

## 例题

### 假设我们部署了合约 OtherContract （合约内容见下）

其合约地址为 0xd9145CCE52D386f254917e481eB44e9943F39138。我们希望在另一个合约中调用该合约，考虑如下两种方式：

```solidity
//OtherContract 合约如下：
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.6;

interface IOtherContract {
    function getBalance() external returns(uint);
    function setX(uint256 x) external payable;
    function getX() external view returns(uint x);
}

contract OtherContract is IOtherContract{
    uint256 private _x = 0;
    event Log(uint amount, uint gas);
    
    function getBalance() external view override returns(uint) {
        return address(this).balance;
    }

    function setX(uint256 x) external override payable{
        _x = x;
        if(msg.value > 0){
            emit Log(msg.value, gasleft());
        }
    }

    function getX() external view override returns(uint x){
        x = _x;
    }
}
```

下列说法正确的是：

选择一个答案

A. (1)(2) 两种写法均会报错

B. 仅 (1) 是调用其他合约的正确写法，(2) 会报错

C. 仅 (2) 是调用其他合约的正确写法，(1) 会报错

D. (1)(2) 均是调用其他合约的正确写法

解释：

- **(1) 方式**：`OtherContract other = OtherContract(0xd9145CCE52D386f254917e481eB44e9943F39138);` 这里我们直接使用 `OtherContract` 类型来实例化合约。这是正确的做法，因为我们知道具体的合约 `OtherContract`，并可以调用合约中的所有公开和继承的函数。
- **(2) 方式**：`IOtherContract other = IOtherContract(0xd9145CCE52D386f254917e481eB44e9943F39138);` 这里我们使用的是接口 `IOtherContract` 来实例化合约。这同样是有效的，因为接口定义了合约的外部函数，我们可以通过接口调用合约的函数。接口实例化合约的方式通常用于调用其他合约的公开函数，尤其在我们只关心合约的接口时。

因此，这两种写法都可以成功调用 `OtherContract` 中的函数，所以选项 D 是正确的。

### 假设我们新写了一个合约

在合约中调用上述已部署的合约 0xd9145CCE52D386f254917e481eB44e9943F39138，如下：

```solidity
contract MyContract {
    OtherContract other = OtherContract(0xd9145CCE52D386f254917e481eB44e9943F39138);
    function call_getX() external view returns(uint x){
        x = other.getX();
    }
    function call_setX(uint256 x) external{
        other.setX(x);
    }
}
```

部署该合约，其地址为 0x9D7f74d0C41E726EC95884E0e97Fa6129e3b5E99。下列说法正确的是：

选择一个答案

A. MyContract 是 OtherContract 的子类

B. MyContract 是 IOtherContract 的一个实现

C. MyContract 需要 0xd9145CCE52D386f254917e481eB44e9943F39138 的某种许可，才可以调用其中的函数

D. MyContract 的函数 call_setX 可以实现，这意味着 OtherContract 中 setX 的权限没有门槛，存在安全隐患

# 22. Call

我们曾在[第20讲：发送ETH](https://github.com/AmazingAng/WTF-Solidity/tree/main/20_SendETH)那一讲介绍过利用`call`来发送`ETH`，这一讲我们将介绍如何利用它调用合约。

`call` 是`address`类型的低级成员函数，它用来与其他合约交互。它的返回值为`(bool, bytes memory)`，分别对应`call`是否成功以及目标函数的返回值。

- `call`是`Solidity`官方推荐的通过触发`fallback`或`receive`函数发送`ETH`的方法。
- 不推荐用`call`来调用另一个合约，因为当你调用不安全合约的函数时，你就把主动权交给了它。推荐的方法仍是声明合约变量后调用函数，见[第21讲：调用其他合约](https://github.com/AmazingAng/WTF-Solidity/tree/main/21_CallContract)
- 当我们不知道对方合约的源代码或`ABI`，就没法生成合约变量；这时，我们仍可以通过`call`调用对方合约的函数。

### `call`的使用规则

`call`的使用规则如下：

```text
目标合约地址.call(字节码);
```



其中`字节码`利用结构化编码函数`abi.encodeWithSignature`获得：

```text
abi.encodeWithSignature("函数签名", 逗号分隔的具体参数)
```



`函数签名`为`"函数名（逗号分隔的参数类型）"`。例如`abi.encodeWithSignature("f(uint256,address)", _x, _addr)`。

另外`call`在调用合约时可以指定交易发送的`ETH`数额和`gas`数额：

```text
目标合约地址.call{value:发送数额, gas:gas数额}(字节码);
```



看起来有点复杂，下面我们举个`call`应用的例子。

### 目标合约

我们先写一个简单的目标合约`OtherContract`并部署，代码与第21讲中基本相同，只是多了`fallback`函数。

```solidity
contract OtherContract {
    uint256 private _x = 0; // 状态变量x
    // 收到eth的事件，记录amount和gas
    event Log(uint amount, uint gas);
    
    fallback() external payable{}

    // 返回合约ETH余额
    function getBalance() view public returns(uint) {
        return address(this).balance;
    }

    // 可以调整状态变量_x的函数，并且可以往合约转ETH (payable)
    function setX(uint256 x) external payable{
        _x = x;
        // 如果转入ETH，则释放Log事件
        if(msg.value > 0){
            emit Log(msg.value, gasleft());
        }
    }

    // 读取x
    function getX() external view returns(uint x){
        x = _x;
    }
}
```



这个合约包含一个状态变量`x`，一个在收到`ETH`时触发的事件`Log`，三个函数：

- `getBalance()`: 返回合约`ETH`余额。
- `setX()`: `external payable`函数，可以设置`x`的值，并向合约发送`ETH`。
- `getX()`: 读取`x`的值。

### 利用`call`调用目标合约

#### 1. Response事件

我们写一个`Call`合约来调用目标合约函数。首先定义一个`Response`事件，输出`call`返回的`success`和`data`，方便我们观察返回值。

```solidity
// 定义Response事件，输出call返回的结果success和data
event Response(bool success, bytes data);
```



#### 2. 调用setX函数

我们定义`callSetX`函数来调用目标合约的`setX()`，转入`msg.value`数额的`ETH`，并释放`Response`事件输出`success`和`data`：

```solidity
function callSetX(address payable _addr, uint256 x) public payable {
    // call setX()，同时可以发送ETH
    (bool success, bytes memory data) = _addr.call{value: msg.value}(
        abi.encodeWithSignature("setX(uint256)", x)
    );

    emit Response(success, data); //释放事件
}
```



接下来我们调用`callSetX`把状态变量`_x`改为5，参数为`OtherContract`地址和`5`，由于目标函数`setX()`没有返回值，因此`Response`事件输出的`data`为`0x`，也就是空。



![22-1](https://www.wtf.academy/assets/images/22-1-c8df2a8eb61086564f7e7bd4346ae8a8.png)



#### 3. 调用getX函数

下面我们调用`getX()`函数，它将返回目标合约`_x`的值，类型为`uint256`。我们可以利用`abi.decode`来解码`call`的返回值`data`，并读出数值。

```solidity
function callGetX(address _addr) external returns(uint256){
    // call getX()
    (bool success, bytes memory data) = _addr.call(
        abi.encodeWithSignature("getX()")
    );

    emit Response(success, data); //释放事件
    return abi.decode(data, (uint256));
}
```



从`Response`事件的输出，我们可以看到`data`为`0x0000000000000000000000000000000000000000000000000000000000000005`。而经过`abi.decode`，最终返回值为`5`。



![22-2](https://www.wtf.academy/assets/images/22-2-008a7b4cdb2734426c2c284cfca79b41.png)



#### 4. 调用不存在的函数

如果我们给`call`输入的函数不存在于目标合约，那么目标合约的`fallback`函数会被触发。

```solidity
function callNonExist(address _addr) external{
    // call 不存在的函数
    (bool success, bytes memory data) = _addr.call(
        abi.encodeWithSignature("foo(uint256)")
    );

    emit Response(success, data); //释放事件
}
```



上面例子中，我们`call`了不存在的`foo`函数。`call`仍能执行成功，并返回`success`，但其实调用的目标合约`fallback`函数。



![22-3](https://www.wtf.academy/assets/images/22-3-b6b8e21fc3d39b5592c1a54f75fdad66.png)



## 总结

这一讲，我们介绍了如何用`call`这一低级函数来调用其他合约。`call`不是调用合约的推荐方法，因为不安全。但他能让我们在不知道源代码和`ABI`的情况下调用目标合约，很有用。

## 例题

### 下面哪种使用方式不正确？

选择一个答案

A. address(nameReg).call{gas: 1000000}(abi.encodeWithSignature("register(string)", "MyName"));

B. address(nameReg).call{value: 1 ether}(abi.encodeWithSignature("register(string)", "MyName"));

C. address.call{gas: 1000000, value: 1 ether}

D. address(nameReg).call{gas: 1000000, value: 1 ether}

**原因：**

- **A、B 和 D** 都正确使用了 `call` 函数，并且在调用中传递了 `abi.encodeWithSignature` 来编码需要调用的函数签名和参数。
- **C 选项**：`address.call{gas: 1000000, value: 1 ether}` 缺少函数签名和字节码，没有指定要调用的目标函数。这是错误的调用方式。

# 23. Delegatecall

## `Delegatecall`

`delegatecall`与`call`类似，是`Solidity`中地址类型的低级成员函数。`delegate`中是委托/代表的意思，那么`delegatecall`委托了什么？

当用户`A`通过合约`B`来`call`合约`C`的时候，执行的是合约`C`的函数，`上下文`(`Context`，可以理解为包含变量和状态的环境)也是合约`C`的：`msg.sender`是`B`的地址，并且如果函数改变一些状态变量，产生的效果会作用于合约`C`的变量上。



![call的上下文](https://images.mirror-media.xyz/publication-images/VgMR533pA8WYtE5Lr65mQ.png?height=698&width=1860)



而当用户`A`通过合约`B`来`delegatecall`合约`C`的时候，执行的是合约`C`的函数，但是`上下文`仍是合约`B`的：`msg.sender`是`A`的地址，并且如果函数改变一些状态变量，产生的效果会作用于合约`B`的变量上。



![delegatecall的上下文](https://images.mirror-media.xyz/publication-images/JucQiWVixdlmJl6zHjCSI.png?height=702&width=1862)



大家可以这样理解：一个投资者（用户`A`）把他的资产（`B`合约的`状态变量`）都交给一个风险投资代理（`C`合约）来打理。执行的是风险投资代理的函数，但是改变的是资产的状态。

`delegatecall`语法和`call`类似，也是：

```solidity
目标合约地址.delegatecall(二进制编码);
```



其中`二进制编码`利用结构化编码函数`abi.encodeWithSignature`获得：

```solidity
abi.encodeWithSignature("函数签名", 逗号分隔的具体参数)
```



`函数签名`为`"函数名（逗号分隔的参数类型）"`。例如`abi.encodeWithSignature("f(uint256,address)", _x, _addr)`。

和`call`不一样，`delegatecall`在调用合约时可以指定交易发送的`gas`，但==不能指定发送的`ETH`数额==

> **注意**：`delegatecall`有安全隐患，使用时要保证当前合约和目标合约的状态变量存储结构相同，并且目标合约安全，不然会造成资产损失。

## 什么情况下会用到`delegatecall`?

目前`delegatecall`主要有两个应用场景：

1. 代理合约（`Proxy Contract`）：将智能合约的存储合约和逻辑合约分开，代理合约（`Proxy Contract`）存储所有相关的变量，并且保存逻辑合约的地址；所有函数存在逻辑合约（`Logic Contract`）里，通过`delegatecall`执行。当升级时，只需要将代理合约指向新的逻辑合约即可。
2. EIP-2535 Diamonds（钻石）：钻石是一个支持构建可在生产中扩展的模块化智能合约系统的标准。钻石是具有多个实施合约的代理合约。 更多信息请查看：[钻石标准简介](https://eip2535diamonds.substack.com/p/introduction-to-the-diamond-standard)。

## `delegatecall`例子

调用结构：你（`A`）通过合约`B`调用目标合约`C`。

### 被调用的合约C

我们先写一个简单的目标合约`C`：有两个`public`变量：`num`和`sender`，分别是`uint256`和`address`类型；有一个函数，可以将`num`设定为传入的`_num`，并且将`sender`设为`msg.sender`。

```solidity
// 被调用的合约C
contract C {
    uint public num;
    address public sender;

    function setVars(uint _num) public payable {
        num = _num;
        sender = msg.sender;
    }
}
```



### 发起调用的合约B

首先，合约`B`必须和目标合约`C`的变量存储布局必须相同，两个变量，并且顺序为`num`和`sender`（==变量类型、声明顺序都必须相同，变量名可以不同==）

```solidity
contract B {
    uint public num;
    address public sender;
}
```



接下来，我们分别用`call`和`delegatecall`来调用合约`C`的`setVars`函数，更好的理解它们的区别。

`callSetVars`函数通过`call`来调用`setVars`。它有两个参数`_addr`和`_num`，分别对应合约`C`的地址和`setVars`的参数。

```solidity
// 通过call来调用C的setVars()函数，将改变合约C里的状态变量
function callSetVars(address _addr, uint _num) external payable{
    // call setVars()
    (bool success, bytes memory data) = _addr.call(
        abi.encodeWithSignature("setVars(uint256)", _num)
    );
}
```



而`delegatecallSetVars`函数通过`delegatecall`来调用`setVars`。与上面的`callSetVars`函数相同，有两个参数`_addr`和`_num`，分别对应合约`C`的地址和`setVars`的参数。

```solidity
// 通过delegatecall来调用C的setVars()函数，将改变合约B里的状态变量
function delegatecallSetVars(address _addr, uint _num) external payable{
    // delegatecall setVars()
    (bool success, bytes memory data) = _addr.delegatecall(
        abi.encodeWithSignature("setVars(uint256)", _num)
    );
}
```



### 在remix上验证

1. 首先，我们把合约`B`和`C`都部署好

   

   ![deploy.png](https://www.wtf.academy/assets/images/23-1-85c05f2d534e1a100a08f48bdea973b0.png)

   

2. 部署之后，查看`C`合约状态变量的初始值，`B`合约的状态变量也是一样。

   

   ![initialstate.png](https://www.wtf.academy/assets/images/23-2-0710e49786d637814b5998a6b2c33dc0.png)

   

3. 此时，调用合约`B`中的`callSetVars`，传入参数为合约`C`地址和`10`

   

   ![call.png](https://www.wtf.academy/assets/images/23-3-24a8e170ef4ffc2ee1964ecea2e3fa46.png)

   

4. 运行后，合约`C`中的状态变量将被修改：`num`被改为`10`，`sender`变为合约`B`的地址

   

   ![resultcall.png](https://www.wtf.academy/assets/images/23-4-dc4ef0d4cdcdd6fa306fc19dd4b3f931.png)

   

5. 接下来，我们调用合约`B`中的`delegatecallSetVars`，传入参数为合约`C`地址和`100`

   

   ![delegatecall.png](https://www.wtf.academy/assets/images/23-5-48ec2ddb52f11031a3d1fba839e74f26.png)

   

6. 由于是`delegatecall`，上下文为合约`B`。在运行后，合约`B`中的状态变量将被修改：`num`被改为`100`，`sender`变为你的钱包地址。合约`C`中的状态变量不会被修改。

   

   ![resultdelegatecall.png](https://www.wtf.academy/assets/images/23-6-563be58ca9837183438ce89b76b618fb.png)

   

## 总结

这一讲我们介绍了`Solidity`中的另一个低级函数`delegatecall`。与`call`类似，它可以用来调用其他合约；不同点在于运行的上下文，`B call C`，上下文为`C`；而`B delegatecall C`，上下文为`B`。目前`delegatecall`最大的应用是代理合约和`EIP-2535 Diamonds`（钻石）。

## 例题

### 假设存在如下函数：

```solidity
function delegatecallMint(address _addr, uint _num) external payable{
    ________________________________________
}
```

那么下面选项中可以填在横线上的是？

选择一个答案

A. `(bool success, bytes memory data) = _addr.delegatecall(abi.encodeWithSignature("mint(uint256)", _num));`

B. `(bool success, bytes memory data) = _addr.delegatecall(abi.encodeWithSignature("mint(uint)", num));`

C. `(bool success, bytes memory data) = _addr.delegatecall(abi.encodeWithSignature("mint(uint)", _num));`

D. `(bool success, bytes memory data) = _addr.delegatecall(abi.encodeWithSignature(mint(uint256), num));`

解析：选A

C选项中有一个问题：它使用的函数签名为 `abi.encodeWithSignature("mint(uint)", _num)`，而正确的签名应该是 `abi.encodeWithSignature("mint(uint256)", _num)`。在Solidity中，`uint` 默认指向 `uint256`，但是在函数签名的表示中，必须准确地反映参数的类型。

虽然 `uint` 和 `uint256` 在 Solidity 语法中是等价的，但在 ABI 函数签名中，必须使用完整的类型名称。因此，C选项因签名不完全而导致错误，故而不正确。选项A则使用了正确的类型和格式。

### 当用户A通过合约B来delegatecall合约C时

执行了\__的函数，语境是\__，msg.sender和msg.value来自\__， 并且如果函数改变一些状态变量，产生的效果会作用于__的变量上

选择一个答案

A. C;B;A;B

B. C;C;B;C

C. B;B;A;B

D. C;B;A;C

分析：选A



# 24. 在合约中创建新合约

在以太坊链上，用户（外部账户，`EOA`）可以创建智能合约，智能合约同样也可以创建新的智能合约。去中心化交易所`uniswap`就是利用工厂合约（`PairFactory`）创建了无数个币对合约（`Pair`）。这一讲，我会用简化版的`uniswap`讲如何通过合约创建合约。

## `create`

有两种方法可以在合约中创建新合约，`create`和`create2`，这里我们讲`create`，下一讲会介绍`create2`。

`create`的用法很简单，就是`new`一个合约，并传入新合约构造函数所需的参数：

```solidity
Contract x = new Contract{value: _value}(params)
```



其中`Contract`是要创建的合约名，`x`是合约对象（地址），如果构造函数是`payable`，可以创建时转入`_value`数量的`ETH`，`params`是==新合约构造函数==的参数。

## 极简Uniswap

`Uniswap V2`[核心合约](https://github.com/Uniswap/v2-core/tree/master/contracts)中包含两个合约：

1. UniswapV2Pair: 币对合约，用于管理币对地址、流动性、买卖。
2. UniswapV2Factory: 工厂合约，用于创建新的币对，并管理币对地址。

下面我们用`create`方法实现一个极简版的`Uniswap`：`Pair`币对合约负责管理币对地址，`PairFactory`工厂合约用于创建新的币对，并管理币对地址。

### `Pair`合约

```solidity
contract Pair{
    address public factory; // 工厂合约地址
    address public token0; // 代币1
    address public token1; // 代币2

    constructor() payable {
        factory = msg.sender;
    }

    // called once by the factory at time of deployment
    function initialize(address _token0, address _token1) external {
        require(msg.sender == factory, 'UniswapV2: FORBIDDEN'); // sufficient check
        token0 = _token0;
        token1 = _token1;
    }
}
```



`Pair`合约很简单，包含3个状态变量：`factory`，`token0`和`token1`。

构造函数`constructor`在部署时将`factory`赋值为工厂合约地址。`initialize`函数会由工厂合约在部署完成后手动调用以初始化代币地址，将`token0`和`token1`更新为币对中两种代币的地址。

> **提问**：为什么`uniswap`不在`constructor`中将`token0`和`token1`地址更新好？
>
> **答**：因为`uniswap`使用的是`create2`创建合约，生成的合约地址可以实现预测，更多详情请阅读[第25讲](https://github.com/AmazingAng/WTF-Solidity/blob/main/25_Create2/readme.md)。

### `PairFactory`

```solidity
contract PairFactory{
    mapping(address => mapping(address => address)) public getPair; // 通过两个代币地址查Pair地址
    address[] public allPairs; // 保存所有Pair地址

    function createPair(address tokenA, address tokenB) external returns (address pairAddr) {
        // 创建新合约
        Pair pair = new Pair(); 
        // 调用新合约的initialize方法
        pair.initialize(tokenA, tokenB);
        // 更新地址map
        pairAddr = address(pair);
        allPairs.push(pairAddr);
        getPair[tokenA][tokenB] = pairAddr;
        getPair[tokenB][tokenA] = pairAddr;
    }
}
```



工厂合约（`PairFactory`）有两个状态变量`getPair`是两个代币地址到币对地址的`map`，方便根据代币找到币对地址；`allPairs`是币对地址的数组，存储了所有代币地址。

> [!NOTE]
>
> **`getPair[tokenA][tokenB] = pairAddr;`**:
>
> - 这行代码将 `tokenA` 和 `tokenB` 作为键（key），并将对应的交易对地址 `pairAddr` 存储在 `getPair` 映射中。
> - 意思是：通过 `tokenA` 和 `tokenB` 可以找到交易对的地址 `pairAddr`。
>
> **`getPair[tokenB][tokenA] = pairAddr;`**:
>
> - 这行代码将 `tokenB` 和 `tokenA` 作为键，进行相同的映射。
> - 意思是：通过 `tokenB` 和 `tokenA` 也可以找到同样的交易对的地址 `pairAddr`。
> - 这样无论你以何种顺序传递代币地址，都可以方便地获取到相应的交易对地址。
>
> ### 例子
>
> 假设我们有两个代币地址：
>
> - `tokenA`: 0x1234... (假设是某个代币的地址)
> - `tokenB`: 0x5678... (另一个代币的地址)
>
> 当调用 `createPair(tokenA, tokenB)` 时，代码会执行如下操作：
>
> - `getPair[0x1234][0x5678] = pairAddr;`
> - `getPair[0x5678][0x1234] = pairAddr;`
>
> 通过上述两行代码，用户可以使用 `getPair` 映射以任意顺序查询代币对的交易对地址。例如：
>
> - 如果用户查询 `getPair[0x1234][0x5678]`，会返回 `pairAddr`。
> - 如果用户查询 `getPair[0x5678][0x1234]`，同样会返回 `pairAddr`。
>
> ### 总结
>
> 这种双向映射的设计提高了代码的灵活性，简化了查询过程，使得用户在查询时不需要关心代币地址的顺序，从而提升了使用体验。



`PairFactory`合约只有一个`createPair`函数，根据输入的两个代币地址`tokenA`和`tokenB`来创建新的`Pair`合约。其中

```solidity
Pair pair = new Pair(); 
```



就是创建合约的代码，非常简单。大家可以部署好`PairFactory`合约，然后用下面两个地址作为参数调用`createPair`，看看创建的币对地址是什么：

```text
WBNB地址: 0x2c44b726ADF1963cA47Af88B284C06f30380fC78
BSC链上的PEOPLE地址: 0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c
```



### 在remix上验证

1. 使用`WBNB`和`PEOPLE`的地址作为参数调用`createPair`,得到`Pair`合约地址：0xD3e2008b4Da2cD6DEAF73471590fF30C86778A48

   

   ![24-1](https://www.wtf.academy/assets/images/24-1-d4a6d130254e0486a4cb649b74cb40c4.png)

   

2. 查看`Pair`合约变量

   

   ![24-2](https://www.wtf.academy/assets/images/24-2-3521680cc697424ef856eae959ad61c0.png)

   

3. Debug查看`create`操作码

   

   ![24-3](https://www.wtf.academy/assets/images/24-3-f4526e2f8351ddfcabb223ec5ec6d20a.png)

   

## 总结

这一讲，我们用极简`Uniswap`的例子介绍了如何使用`create`方法再合约里创建合约，下一讲我们将介绍如何使用`create2`方法来实现极简`Uniswap`。

## 例题

### Solidity中创建新合约的关键字是：

选择一个答案

A. create

B. create1

C. create2

D. new

使用 `new` 关键字可以创建一个新的合约实例。例如，`Pair pair = new Pair();` 会创建一个新的 `Pair` 合约实例。其他选项如 `create`、`create1` 和 `create2` 并不是 Solidity 中用于创建新合约的关键字。

### Contract x = new Contract{value: _value}(params)，表达式中value代表什么？

选择一个答案

A. 当前合约发送给新创建合约的ETH

B. 当前合约发送给新创建合约的Token

C. 当前合约调用者发送给当前合约的ETH

D. 当前合约调用者发送给当前合约的Token

`value: _value` 指定了在创建新合约时，当前合约会向新合约发送 `_value` 数量的以太币（ETH）。



# 25. CREATE2

## CREATE2

`CREATE2` 操作码使我们在智能合约部署在以太坊网络之前就能预测合约的地址。`Uniswap`创建`Pair`合约用的就是`CREATE2`而不是`CREATE`。这一讲，我将介绍`CREATE2`的用法

### CREATE如何计算地址

智能合约可以由其他合约和普通账户利用`CREATE`操作码创建。 在这两种情况下，新合约的地址都以相同的方式计算：创建者的地址(通常为部署的钱包地址或者合约地址)和`nonce`(该地址发送交易的总数,对于合约账户是创建的合约总数,每创建一个合约nonce+1)的哈希。

```text
新地址 = hash(创建者地址, nonce)
```



创建者地址不会变，但`nonce`可能会随时间而改变，因此用`CREATE`创建的合约地址不好预测。

### CREATE2如何计算地址

`CREATE2`的目的是为了让合约地址独立于未来的事件。不管未来区块链上发生了什么，你都可以把合约部署在事先计算好的地址上。用`CREATE2`创建的合约地址由4个部分决定：

- `0xFF`：一个常数，避免和`CREATE`冲突
- `CreatorAddress`: 调用 CREATE2 的当前合约（创建合约）地址。
- `salt`（盐）：一个创建者指定的`bytes32`类型的值，它的主要目的是用来影响新创建的合约的地址。
- `initcode`: 新合约的初始字节码（合约的Creation Code和构造函数的参数）。

```text
新地址 = hash("0xFF",创建者地址, salt, initcode)
```



`CREATE2` 确保，如果创建者使用 `CREATE2` 和提供的 `salt` 部署给定的合约`initcode`，它将存储在 `新地址` 中。

## 如何使用`CREATE2`

`CREATE2`的用法和之前讲的`CREATE`类似，同样是`new`一个合约，并传入新合约构造函数所需的参数，只不过要多传一个`salt`参数：

```solidity
Contract x = new Contract{salt: _salt, value: _value}(params)
```



其中`Contract`是要创建的合约名，`x`是合约对象（地址），`_salt`是指定的盐；如果构造函数是`payable`，可以创建时转入`_value`数量的`ETH`，`params`是新合约构造函数的参数。

## 极简Uniswap2

跟[上一讲](https://mirror.xyz/wtfacademy.eth/kojopp2CgDK3ehHxXc_2fkZe87uM0O5OmsEU6y83eJs)类似，我们用`CREATE2`来实现极简`Uniswap`。

### `Pair`

```solidity
contract Pair{
    address public factory; // 工厂合约地址
    address public token0; // 代币1
    address public token1; // 代币2

    constructor() payable {
        factory = msg.sender;
    }

    // called once by the factory at time of deployment
    function initialize(address _token0, address _token1) external {
        require(msg.sender == factory, 'UniswapV2: FORBIDDEN'); // sufficient check
        token0 = _token0;
        token1 = _token1;
    }
}
```



`Pair`合约很简单，包含3个状态变量：`factory`，`token0`和`token1`。

构造函数`constructor`在部署时将`factory`赋值为工厂合约地址。`initialize`函数会在`Pair`合约创建的时候被工厂合约调用一次，将`token0`和`token1`更新为币对中两种代币的地址。

### `PairFactory2`

```solidity
contract PairFactory2{
    mapping(address => mapping(address => address)) public getPair; // 通过两个代币地址查Pair地址
    address[] public allPairs; // 保存所有Pair地址

    function createPair2(address tokenA, address tokenB) external returns (address pairAddr) {
        require(tokenA != tokenB, 'IDENTICAL_ADDRESSES'); //避免tokenA和tokenB相同产生的冲突
        // 用tokenA和tokenB地址计算salt
        (address token0, address token1) = tokenA < tokenB ? (tokenA, tokenB) : (tokenB, tokenA); //将tokenA和tokenB按大小排序
        bytes32 salt = keccak256(abi.encodePacked(token0, token1));
        // 用create2部署新合约
        Pair pair = new Pair{salt: salt}(); 
        // 调用新合约的initialize方法
        pair.initialize(tokenA, tokenB);
        // 更新地址map
        pairAddr = address(pair);
        allPairs.push(pairAddr);
        getPair[tokenA][tokenB] = pairAddr;
        getPair[tokenB][tokenA] = pairAddr;
    }
}
```



工厂合约（`PairFactory2`）有两个状态变量`getPair`是两个代币地址到币对地址的`map`，方便根据代币找到币对地址；`allPairs`是币对地址的数组，存储了所有币对地址。

`PairFactory2`合约只有一个`createPair2`函数，使用`CREATE2`根据输入的两个代币地址`tokenA`和`tokenB`来创建新的`Pair`合约。其中

```solidity
Pair pair = new Pair{salt: salt}(); 
```



就是利用`CREATE2`创建合约的代码，非常简单，而`salt`为`token1`和`token2`的`hash`：

```solidity
bytes32 salt = keccak256(abi.encodePacked(token0, token1));
```



### 事先计算`Pair`地址

```solidity
// 提前计算pair合约地址
function calculateAddr(address tokenA, address tokenB) public view returns(address predictedAddress){
    require(tokenA != tokenB, 'IDENTICAL_ADDRESSES'); //避免tokenA和tokenB相同产生的冲突
    // 计算用tokenA和tokenB地址计算salt
    (address token0, address token1) = tokenA < tokenB ? (tokenA, tokenB) : (tokenB, tokenA); //将tokenA和tokenB按大小排序
    bytes32 salt = keccak256(abi.encodePacked(token0, token1));
    // 计算合约地址方法 hash()
    predictedAddress = address(uint160(uint(keccak256(abi.encodePacked(
        bytes1(0xff),
        address(this),
        salt,
        keccak256(type(Pair).creationCode)
        )))));
}
```



我们写了一个`calculateAddr`函数来事先计算`tokenA`和`tokenB`将会生成的`Pair`地址。通过它，我们可以验证我们事先计算的地址和实际地址是否相同。

大家可以部署好`PairFactory2`合约，然后用下面两个地址作为参数调用`createPair2`，看看创建的币对地址是什么，是否与事先计算的地址一样：

```text
WBNB地址: 0x2c44b726ADF1963cA47Af88B284C06f30380fC78
BSC链上的PEOPLE地址: 0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c
```



#### 如果部署合约构造函数中存在参数

例如当create2合约时：

> Pair pair = new Pair{salt: salt}(address(this));

计算时，需要将参数和initcode一起进行打包：

> ~~keccak256(type(Pair).creationCode)~~ => keccak256(abi.encodePacked(type(Pair).creationCode, abi.encode(address(this))))

```solidity
predictedAddress = address(uint160(uint(keccak256(abi.encodePacked(
                bytes1(0xff),
                address(this),
                salt,
                keccak256(abi.encodePacked(type(Pair).creationCode, abi.encode(address(this))))
            )))));
```



### 在remix上验证

1. 首先用`WBNB`和`PEOPLE`的地址哈希作为`salt`来计算出`Pair`合约的地址

2. 调用`PairFactory2.createPair2`传入参数为`WBNB`和`PEOPLE`的地址，获取出创建的`pair`合约地址

3. 对比合约地址

   

   ![create2_remix_test.png](https://www.wtf.academy/assets/images/25-1-2d1f4ed217fe799a46e8b53a44cfdd3b.png)

   

## create2的实际应用场景

1. 交易所为新用户预留创建钱包合约地址。
2. 由 `CREATE2` 驱动的 `factory` 合约，在`Uniswap V2`中交易对的创建是在 `Factory`中调用`CREATE2`完成。这样做的好处是: 它可以得到一个确定的`pair`地址, 使得 `Router`中就可以通过 `(tokenA, tokenB)` 计算出`pair`地址, 不再需要执行一次 `Factory.getPair(tokenA, tokenB)` 的跨合约调用。

## 总结

这一讲，我们介绍了`CREATE2`操作码的原理，使用方法，并用它完成了极简版的`Uniswap`并提前计算币对合约地址。`CREATE2`让我们可以在部署合约前确定它的合约地址，这也是一些`layer2`项目的基础。

# 26. 删除合约

## `selfdestruct`

`selfdestruct`命令可以用来删除智能合约，并将该合约剩余`ETH`转到指定地址。`selfdestruct`是为了应对合约出错的极端情况而设计的。它最早被命名为`suicide`（自杀），但是这个词太敏感。为了保护抑郁的程序员，改名为`selfdestruct`；在 [v0.8.18](https://blog.soliditylang.org/2023/02/01/solidity-0.8.18-release-announcement/) 版本中，`selfdestruct` 关键字被标记为「不再建议使用」，在一些情况下它会导致预期之外的合约语义，但由于目前还没有代替方案，目前只是对开发者做了编译阶段的警告，相关内容可以查看 [EIP-6049](https://eips.ethereum.org/EIPS/eip-6049)。

然而，在以太坊坎昆（Cancun）升级中，[EIP-6780](https://eips.ethereum.org/EIPS/eip-6780)被纳入升级以实现对`Verkle Tree`更好的支持。EIP-6780减少了`SELFDESTRUCT`操作码的功能。根据提案描述，当前`SELFDESTRUCT`仅会被用来将合约中的ETH转移到指定地址，而原先的删除功能只有在`合约创建-自毁`这两个操作处在同一笔交易时才能生效。所以目前来说：

1. 已经部署的合约无法被`SELFDESTRUCT`了。
2. 如果要使用原先的`SELFDESTRUCT`功能，必须在同一笔交易中创建并`SELFDESTRUCT`。

### 如何使用`selfdestruct`

`selfdestruct`使用起来非常简单：

```solidity
selfdestruct(_addr)；
```



其中`_addr`是接收合约中剩余`ETH`的地址。`_addr` 地址不需要有`receive()`或`fallback()`也能接收`ETH`。

### Demo-转移ETH功能

以下合约在坎昆升级前可以完成合约的自毁，在坎昆升级后仅能实现内部ETH余额的转移。

```solidity
contract DeleteContract {

    uint public value = 10;

    constructor() payable {}

    receive() external payable {}

    function deleteContract() external {
        // 调用selfdestruct销毁合约，并把剩余的ETH转给msg.sender
        selfdestruct(payable(msg.sender));
    }

    function getBalance() external view returns(uint balance){
        balance = address(this).balance;
    }
}
```



在`DeleteContract`合约中，我们写了一个`public`状态变量`value`，两个函数：`getBalance()`用于获取合约`ETH`余额，`deleteContract()`用于自毁合约，并把`ETH`转入给发起人。

部署好合约后，我们向`DeleteContract`合约转入1 `ETH`。这时，`getBalance()`会返回1 `ETH`，`value`变量是10。

当我们调用`deleteContract()`函数，合约将触发`selfdestruct`操作。**在坎昆升级前，合约会被自毁。但是在升级后，合约依然存在，只是将合约包含的ETH转移到指定地址，而合约依然能够调用。**

#### 在remix上验证

##### 坎昆升级之前

1. 部署合约并且转入1ETH，查看合约状态

   

   ![deployContract.png](https://www.wtf.academy/assets/images/26-1-dac95a82f5f955f125b9ca9ffdd5ed53.png)

   

2. 销毁合约，查看合约状态

   

   ![deleteContract.png](https://www.wtf.academy/assets/images/26-2-41801f1808ac30c605fec490779e6724.png)

   

从测试中观察合约状态可以发现合约销毁后的ETH返回给了指定的地址，在合约销毁后再次调用合约函数进行交互则会失败。

##### 坎昆升级之后

1. 部署合约并且转入1ETH，查看合约状态

   

   ![deployContract2.png](https://www.wtf.academy/assets/images/26-3-b5a1d17f644c390ab75afed72fdb8953.png)

   

2. 销毁合约，查看合约状态

   

   ![deleteContract2.png](https://www.wtf.academy/assets/images/26-4-bf4621e9413dca9838aea86f35abc54f.png)

   

从测试中观察合约状态可以发现合约包含的ETH已经清零（返回给了指定的地址），再次调用合约函数进行交互依然可以成功。

注意：`value`在这里只是一个状态变量，不是`balance`，所以`value`仍然为10

### Demo-同笔交易内实现合约创建-自毁

根据提案，原先的删除功能只有在`合约创建-自毁`这两个操作处在同一笔交易时才能生效。所以我们需要通过另一个合约进行控制。

```solidity
contract DeployContract {

    struct DemoResult {
        address addr;
        uint balance;
        uint value;
    }

    constructor() payable {}

    function getBalance() external view returns(uint balance){
        balance = address(this).balance;
    }

    function demo() public payable returns (DemoResult memory){
        DeleteContract del = new DeleteContract{value:msg.value}();
        DemoResult memory res = DemoResult({
            addr: address(del),
            balance: del.getBalance(),
            value: del.value()
        });
        del.deleteContract();
        return res;
    }
//    function deleteContract() external {
        // 调用selfdestruct销毁合约，并把剩余的ETH转给msg.sender
//        selfdestruct(payable(msg.sender));
//    }
    
}
```



#### 在remix上验证

1. 部署`DeployContract`合约并且转入1ETH调用`demo`方法，查看合约状态，显示`DeleteContract`已被正确部署，且在`selfdestruct`后ETH已转移到`DeployContract`。

   

   ![deployContract3.png](https://www.wtf.academy/assets/images/26-5-c51212189776fee91b343bfdc02cea88.png)

   

2. 选择导入返回值中的地址为`DeleteContract`。显示该地址不存有ETH，且调用合约函数进行交互均失败。

   

   ![deleteContract3.png](https://www.wtf.academy/assets/images/26-6-3c5f783a4db1b6236aebe803f4291c9c.png)

   

### 注意事项

1. 对外提供合约销毁接口时，最好设置为只有合约所有者可以调用，可以使用函数修饰符`onlyOwner`进行函数声明。
2. 当合约中有`selfdestruct`功能时常常会带来安全问题和信任问题，合约中的selfdestruct功能会为攻击者打开攻击向量(例如使用`selfdestruct`向一个合约频繁转入token进行攻击，这将大大节省了GAS的费用，虽然很少人这么做)，此外，此功能还会降低用户对合约的信心。

## 总结

`selfdestruct`是智能合约的紧急按钮，销毁合约并将剩余`ETH`转移到指定账户。当著名的`The DAO`攻击发生时，以太坊的创始人们一定后悔过没有在合约里加入`selfdestruct`来停止黑客的攻击吧。在坎昆升级后，`selfdestruct`的作用也逐渐发生了改变，什么都不是一成不变的，还是要保持学习。

# 27. ABI编码解码

`ABI` (Application Binary Interface，应用二进制接口)是与以太坊智能合约交互的标准。数据基于他们的类型编码；并且由于编码后不包含类型信息，解码时需要注明它们的类型。

`Solidity`中，`ABI编码`有4个函数：`abi.encode`, `abi.encodePacked`, `abi.encodeWithSignature`, `abi.encodeWithSelector`。而`ABI解码`有1个函数：`abi.decode`，用于解码`abi.encode`的数据。这一讲，我们将学习如何使用这些函数。

## ABI编码

我们将编码4个变量，他们的类型分别是`uint256`（别名 uint）, `address`, `string`, `uint256[2]`：

```solidity
uint x = 10;
address addr = 0x7A58c0Be72BE218B41C608b7Fe7C5bB630736C71;
string name = "0xAA";
uint[2] array = [5, 6]; 
```



### `abi.encode`

将给定参数利用[ABI规则](https://learnblockchain.cn/docs/solidity/abi-spec.html)编码。`ABI`被设计出来跟智能合约交互，他将每个参数填充为32字节的数据，并拼接在一起。如果你要和合约交互，你要用的就是`abi.encode`。

```solidity
function encode() public view returns(bytes memory result) {
    result = abi.encode(x, addr, name, array);
}
```



编码的结果为`0x000000000000000000000000000000000000000000000000000000000000000a0000000000000000000000007a58c0be72be218b41c608b7fe7c5bb630736c7100000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000000005000000000000000000000000000000000000000000000000000000000000000600000000000000000000000000000000000000000000000000000000000000043078414100000000000000000000000000000000000000000000000000000000`，由于`abi.encode`将每个数据都填充为32字节，中间有很多`0`。

### `abi.encodePacked`

将给定参数根据其所需最低空间编码。它类似 `abi.encode`，但是会把其中填充的很多`0`省略。比如，只用1字节来编码`uint8`类型。当你想省空间，并且不与合约交互的时候，可以使用`abi.encodePacked`，例如算一些数据的`hash`时。

```solidity
function encodePacked() public view returns(bytes memory result) {
    result = abi.encodePacked(x, addr, name, array);
}
```



编码的结果为`0x000000000000000000000000000000000000000000000000000000000000000a7a58c0be72be218b41c608b7fe7c5bb630736c713078414100000000000000000000000000000000000000000000000000000000000000050000000000000000000000000000000000000000000000000000000000000006`，由于`abi.encodePacked`对编码进行了压缩，长度比`abi.encode`短很多。

### `abi.encodeWithSignature`

与`abi.encode`功能类似，只不过第一个参数为`函数签名`，比如`"foo(uint256,address,string,uint256[2])"`。当调用其他合约的时候可以使用。

```solidity
function encodeWithSignature() public view returns(bytes memory result) {
    result = abi.encodeWithSignature("foo(uint256,address,string,uint256[2])", x, addr, name, array);
}
```



编码的结果为`0xe87082f1000000000000000000000000000000000000000000000000000000000000000a0000000000000000000000007a58c0be72be218b41c608b7fe7c5bb630736c7100000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000000005000000000000000000000000000000000000000000000000000000000000000600000000000000000000000000000000000000000000000000000000000000043078414100000000000000000000000000000000000000000000000000000000`，等同于在`abi.encode`编码结果前加上了4字节的`函数选择器`[说明](https://www.wtf.academy/docs/solidity-102/ABIEncode/#fn-说明)。 [说明](https://www.wtf.academy/docs/solidity-102/ABIEncode/#fn-说明): 函数选择器就是通过函数名和参数进行签名处理(Keccak–Sha3)来标识函数，可以用于不同合约之间的函数调用

### `abi.encodeWithSelector`

与`abi.encodeWithSignature`功能类似，只不过第一个参数为`函数选择器`，为`函数签名`Keccak哈希的前4个字节。

```solidity
function encodeWithSelector() public view returns(bytes memory result) {
    result = abi.encodeWithSelector(bytes4(keccak256("foo(uint256,address,string,uint256[2])")), x, addr, name, array);
}
```



编码的结果为`0xe87082f1000000000000000000000000000000000000000000000000000000000000000a0000000000000000000000007a58c0be72be218b41c608b7fe7c5bb630736c7100000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000000005000000000000000000000000000000000000000000000000000000000000000600000000000000000000000000000000000000000000000000000000000000043078414100000000000000000000000000000000000000000000000000000000`，与`abi.encodeWithSignature`结果一样。

## ABI解码

### `abi.decode`

`abi.decode`用于解码`abi.encode`生成的二进制编码，将它还原成原本的参数。

```solidity
function decode(bytes memory data) public pure returns(uint dx, address daddr, string memory dname, uint[2] memory darray) {
    (dx, daddr, dname, darray) = abi.decode(data, (uint, address, string, uint[2]));
}
```



我们将`abi.encode`的二进制编码输入给`decode`，将解码出原来的参数：



![27-3](https://images.mirror-media.xyz/publication-images/jboRaaq0U57qVYjmsOgbv.png?height=408&width=624)



## 在remix上验证

- 部署合约查看abi.encode方法的编码结果

  

  ![27-1](https://www.wtf.academy/assets/images/27-1-5c958984759bdbbc1769eb68741619bb.png)

  

- 对比验证四种编码方法的异同点

  

  ![27-2](https://www.wtf.academy/assets/images/27-2-35f3b3d1e509829aaf8ee0f1a417124e.png)

  

- 查看abi.decode方法的解码结果

  

  ![27-3](https://www.wtf.academy/assets/images/27-3-55465b86340661b3e6fce60abc8b8c0a.png)

  

## ABI的使用场景

1. 在合约开发中，ABI常配合call来实现对合约的底层调用。

   ```solidity
   bytes4 selector = contract.getValue.selector;
   
   bytes memory data = abi.encodeWithSelector(selector, _x);
   (bool success, bytes memory returnedData) = address(contract).staticcall(data);
   require(success);
   
   return abi.decode(returnedData, (uint256));
   ```

   

2. ethers.js中常用ABI实现合约的导入和函数调用。

   ```solidity
   const wavePortalContract = new ethers.Contract(contractAddress, contractABI, signer);
   /*
       * Call the getAllWaves method from your Smart Contract
       */
   const waves = await wavePortalContract.getAllWaves();
   ```

   

3. 对不开源合约进行反编译后，某些函数无法查到函数签名，可通过ABI进行调用。

   - 0x533ba33a() 是一个反编译后显示的函数，只有函数编码后的结果，并且无法查到函数签名

     

     ![27-4](https://www.wtf.academy/assets/images/27-4-44125ad122d74749a18973a2d540a629.png)

     ![27-5](https://www.wtf.academy/assets/images/27-5-a3fde61a9c64764247c116c66921da9a.png)

     

   - 这种情况无法通过构造interface接口或contract来进行调用

     ![27-6](https://www.wtf.academy/assets/images/27-6-b572fe57168b496f61448b04f2e77e19.png)

     

     这种情况下，就可以通过ABI函数选择器来调用

     ```solidity
     bytes memory data = abi.encodeWithSelector(bytes4(0x533ba33a));
     
     (bool success, bytes memory returnedData) = address(contract).staticcall(data);
     require(success);
     
     return abi.decode(returnedData, (uint256));
     ```

     

## 总结

在以太坊中，数据必须编码成字节码才能和智能合约交互。这一讲，我们介绍了4种`abi编码`方法和1种`abi解码`方法。

## 例题

### 下列有关ABI编码的函数中，返回值不可能当作调用智能合约的数据的一项是：

选择一个答案

A. `abi.encode`

B. `abi.encodePacked`

C. `abi.encodeWithSignature`

D. `abi.encodeWithSelector`

选择答案：

**B. abi.encodePacked**

解释：

- `abi.encodePacked` 返回的编码数据是紧凑的，不保留类型信息，因此不适用于某些需要保持类型信息的场景，如合约调用。它通常用于哈希计算等。
- 其他选项（`abi.encode`、`abi.encodeWithSignature` 和 `abi.encodeWithSelector`）都可以生成适合用于智能合约调用的数据。

### 已知函数foo在智能合约中定义声明如下：

```solidity
function foo(uint256 a) public view
```

而字符串`"foo(uint256)"`的keccak256哈希值为：

```
0x2fbebd3821c4e005fbe0a9002cc1bd25dc266d788dba1dbcb39cc66a07e7b38b
```

那么，当我们希望调用函数foo()时，以下生成调用数据的写法中，正确且最节省gas的一项是：

选择一个答案

A. `abi.encodeWithSignature("foo(uint256)", a)`

B. `abi.encodeWithSelector("foo(uint256)", a)`

C. `abi.encodeWithSelector(bytes(keccak256("foo(uint256)")), a)`

D. `abi.encodeWithSelector(bytes4(0x2fbebd38), a)`

解释：

- **A.** `abi.encodeWithSignature("foo(uint256)", a)` 使用字符串形式生成选择器，较为直接，但相对较贵。
- **B.** `abi.encodeWithSelector("foo(uint256)", a)` 错误，因为 `abi.encodeWithSelector` 需要一个字节选择器，而不是字符串。
- **C.** `abi.encodeWithSelector(bytes(keccak256("foo(uint256)")), a)` 中调用 `keccak256` 生成选择器，尽管是正确的，但额外计算哈希值增加了开销。
- **D.** `abi.encodeWithSelector(bytes4(0x2fbebd38), a)` 是直接使用已知的函数选择器，最节省 gas，因为它避免了额外的字符串解析和哈希计算。

# 28. Hash

哈希函数（hash function）是一个密码学概念，它可以将任意长度的消息转换为一个固定长度的值，这个值也称作哈希（hash）。这一讲，我们简单介绍一下哈希函数及在`Solidity`的应用。

## Hash的性质

一个好的哈希函数应该具有以下几个特性：

- ==单向性==：从输入的消息到它的哈希的正向运算简单且唯一确定，而反过来非常难，只能靠暴力枚举。
- 灵敏性：输入的消息改变一点对它的哈希改变很大。
- ==高效性==：从输入的消息到哈希的运算高效。
- 均一性：每个哈希值被取到的概率应该基本相等。
- ==抗碰撞性==：
  - 弱抗碰撞性：给定一个消息`x`，找到另一个消息`x'`，使得`hash(x) = hash(x')`是困难的。
  - 强抗碰撞性：找到任意`x`和`x'`，使得`hash(x) = hash(x')`是困难的。

## Hash的应用

- 生成数据唯一标识
- 加密签名
- 安全加密

## Keccak256

`Keccak256`函数是`Solidity`中最常用的哈希函数，用法非常简单：

```solidity
哈希 = keccak256(数据);
```



### Keccak256和sha3

这是一个很有趣的事情：

1. sha3由keccak标准化而来，在很多场合下Keccak和SHA3是同义词，但在2015年8月SHA3最终完成标准化时，NIST调整了填充算法。**所以SHA3就和keccak计算的结果不一样**，这点在实际开发中要注意。
2. 以太坊在开发的时候sha3还在标准化中，所以采用了keccak，所以Ethereum和Solidity智能合约代码中的SHA3是指Keccak256，而不是标准的NIST-SHA3，为了避免混淆，直接在合约代码中写成Keccak256是最清晰的。

### 生成数据唯一标识

我们可以利用`keccak256`来生成一些数据的唯一标识。比如我们有几个不同类型的数据：`uint`，`string`，`address`，我们可以先用`abi.encodePacked`方法将他们打包编码，然后再用`keccak256`来生成唯一标识：

```solidity
function hash(
    uint _num,
    string memory _string,
    address _addr
    ) public pure returns (bytes32) {
    return keccak256(abi.encodePacked(_num, _string, _addr));
}
```



### 弱抗碰撞性

我们用`keccak256`演示一下之前讲到的弱抗碰撞性，即给定一个消息`x`，找到另一个消息`x'`，使得`hash(x) = hash(x')`是困难的。

我们给定一个消息`0xAA`，试图去找另一个消息，使得它们的哈希值相等：

```solidity
// 弱抗碰撞性
function weak(
    string memory string1
    )public view returns (bool){
    return keccak256(abi.encodePacked(string1)) == _msg;
}
```



大家可以试个10次，看看能不能幸运的碰撞上。

### 强抗碰撞性

我们用`keccak256`演示一下之前讲到的强抗碰撞性，即找到任意不同的`x`和`x'`，使得`hash(x) = hash(x')`是困难的。

我们构造一个函数`strong`，接收两个不同的`string`参数`string1`和`string2`，然后判断它们的哈希是否相同：

```solidity
// 强抗碰撞性
function strong(
        string memory string1,
        string memory string2
    )public pure returns (bool){
    return keccak256(abi.encodePacked(string1)) == keccak256(abi.encodePacked(string2));
}
```



大家可以试个10次，看看能不能幸运的碰撞上。

## 在remix上验证

- 部署合约查看唯一标识的生成结果

  

  ![28-1](https://www.wtf.academy/assets/images/28-1-a652cceccf35f1bd6233ad66dfb5636c.png)

  

- 验证哈希函数的灵敏性，以及强、弱抗碰撞性

  

  ![28-2](https://www.wtf.academy/assets/images/28-2-5a09094f947f2b6eb141497901cb5d74.png)

  

## 总结

这一讲，我们介绍了什么是哈希函数，以及如何使用`Solidity`最常用的哈希函数`keccak256`。

# 29. 函数选择器Selector

当我们调用智能合约时，本质上是向目标合约发送了一段`calldata`，在remix中发送一次交易后，可以在详细信息中看见`input`即为此次交易的`calldata`



![tx input in remix](https://www.wtf.academy/assets/images/29-1-0cdac97a91d23b8b328265d1df3a56b5.png)



发送的`calldata`中前4个字节是`selector`（函数选择器）。这一讲，我们将介绍`selector`是什么，以及如何使用。

### msg.data

`msg.data`是`Solidity`中的一个全局变量，值为完整的`calldata`（调用函数时传入的数据）。

在下面的代码中，我们可以通过`Log`事件来输出调用`mint`函数的`calldata`：

```solidity
// event 返回msg.data
event Log(bytes data);

function mint(address to) external{
    emit Log(msg.data);
}
```



当参数为`0x2c44b726ADF1963cA47Af88B284C06f30380fC78`时，输出的`calldata`为

```text
0x6a6278420000000000000000000000002c44b726adf1963ca47af88b284c06f30380fc78
```



这段很乱的字节码可以分成两部分：

```text
前4个字节为函数选择器selector：
0x6a627842

后面32个字节为输入的参数：
0x0000000000000000000000002c44b726adf1963ca47af88b284c06f30380fc78
```



其实`calldata`就是告诉智能合约，我要调用哪个函数，以及参数是什么。

### method id、selector和函数签名

`method id`定义为`函数签名`的`Keccak`哈希后的前4个字节，当`selector`与`method id`相匹配时，即表示调用该函数，那么`函数签名`是什么？

其实在第21讲中，我们简单介绍了函数签名，为`"函数名（逗号分隔的参数类型)"`。举个例子，上面代码中`mint`的函数签名为`"mint(address)"`。在同一个智能合约中，不同的函数有不同的函数签名，因此我们可以通过函数签名来确定要调用哪个函数。

**注意**，在函数签名中，`uint`和`int`要写为`uint256`和`int256`。

我们写一个函数，来验证`mint`函数的`method id`是否为`0x6a627842`。大家可以运行下面的函数，看看结果。

```solidity
function mintSelector() external pure returns(bytes4 mSelector){
    return bytes4(keccak256("mint(address)"));
}
```



结果正是`0x6a627842`：



![method id in remix](https://www.wtf.academy/assets/images/29-2-911dbb86f21d4631b1b82d5ed988a742.png)



由于计算`method id`时，需要通过函数名和函数的参数类型来计算。在`Solidity`中，函数的参数类型主要分为：基础类型参数，固定长度类型参数，可变长度类型参数和映射类型参数。

##### 基础类型参数

`solidity`中，基础类型的参数有：`uint256`(`uint8`, ... , `uint256`)、`bool`, `address`等。在计算`method id`时，只需要计算`bytes4(keccak256("函数名(参数类型1,参数类型2,...)"))`。例如，如下函数，函数名为`elementaryParamSelector`，参数类型分别为`uint256`和`bool`。所以，只需要计算`bytes4(keccak256("elementaryParamSelector(uint256,bool)"))`便可得到此函数的`method id`。

```solidity
    // elementary（基础）类型参数selector
    // 输入：param1: 1，param2: 0
    // elementaryParamSelector(uint256,bool) : 0x3ec37834
    function elementaryParamSelector(uint256 param1, bool param2) external returns(bytes4 selectorWithElementaryParam){
        emit SelectorEvent(this.elementaryParamSelector.selector);
        return bytes4(keccak256("elementaryParamSelector(uint256,bool)"));
    }
```



##### 固定长度类型参数

固定长度的参数类型通常为固定长度的数组，例如：`uint256[5]`等。例如，如下函数`fixedSizeParamSelector`的参数为`uint256[3]`。因此，在计算该函数的`method id`时，只需要通过`bytes4(keccak256("fixedSizeParamSelector(uint256[3])"))`即可。

```solidity
    // fixed size（固定长度）类型参数selector
    // 输入： param1: [1,2,3]
    // fixedSizeParamSelector(uint256[3]) : 0xead6b8bd
    function fixedSizeParamSelector(uint256[3] memory param1) external returns(bytes4 selectorWithFixedSizeParam){
        emit SelectorEvent(this.fixedSizeParamSelector.selector);
        return bytes4(keccak256("fixedSizeParamSelector(uint256[3])"));
    }
```



##### 可变长度类型参数

可变长度参数类型通常为可变长的数组，例如：`address[]`、`uint8[]`、`string`等。例如，如下函数`nonFixedSizeParamSelector`的参数为`uint256[]`和`string`。因此，在计算该函数的`method id`时，只需要通过`bytes4(keccak256("nonFixedSizeParamSelector(uint256[],string)"))`即可。

```solidity
    // non-fixed size（可变长度）类型参数selector
    // 输入： param1: [1,2,3]， param2: "abc"
    // nonFixedSizeParamSelector(uint256[],string) : 0xf0ca01de
    function nonFixedSizeParamSelector(uint256[] memory param1,string memory param2) external returns(bytes4 selectorWithNonFixedSizeParam){
        emit SelectorEvent(this.nonFixedSizeParamSelector.selector);
        return bytes4(keccak256("nonFixedSizeParamSelector(uint256[],string)"));
    }
```



##### 映射类型参数

映射类型参数通常有：`contract`、`enum`、`struct`等。在计算`method id`时，需要将该类型转化成为`ABI`类型。

例如，如下函数`mappingParamSelector`中`DemoContract`需要转化为`address`，结构体`User`需要转化为`tuple`类型`(uint256,bytes)`，枚举类型`School`需要转化为`uint8`。因此，计算该函数的`method id`的代码为`bytes4(keccak256("mappingParamSelector(address,(uint256,bytes),uint256[],uint8)"))`。

```solidity
contract DemoContract {
    // empty contract
}

contract Selector{
    // Struct User
    struct User {
        uint256 uid;
        bytes name;
    }
    // Enum School
    enum School { SCHOOL1, SCHOOL2, SCHOOL3 }
    ...
    // mapping（映射）类型参数selector
    // 输入：demo: 0x9D7f74d0C41E726EC95884E0e97Fa6129e3b5E99， user: [1, "0xa0b1"], count: [1,2,3], mySchool: 1
    // mappingParamSelector(address,(uint256,bytes),uint256[],uint8) : 0xe355b0ce
    function mappingParamSelector(DemoContract demo, User memory user, uint256[] memory count, School mySchool) external returns(bytes4 selectorWithMappingParam){
        emit SelectorEvent(this.mappingParamSelector.selector);
        return bytes4(keccak256("mappingParamSelector(address,(uint256,bytes),uint256[],uint8)"));
    }
    ...
}
```



### 使用selector

我们可以利用`selector`来调用目标函数。例如我想调用`elementaryParamSelector`函数，我只需要利用`abi.encodeWithSelector`将`elementaryParamSelector`函数的`method id`作为`selector`和参数打包编码，传给`call`函数：

```solidity
    // 使用selector来调用函数
    function callWithSignature() external{
    ...
        // 调用elementaryParamSelector函数
        (bool success1, bytes memory data1) = address(this).call(abi.encodeWithSelector(0x3ec37834, 1, 0));
    ...
    }
```



在日志中，我们可以看到`elementaryParamSelector`函数被成功调用，并输出`Log`事件。



![logs in remix](https://www.wtf.academy/assets/images/29-3-ebdc4d09bf2102f2016400a5def9b7ae.png)



## 总结

这一讲，我们介绍了什么是`函数选择器`（`selector`），它和`msg.data`、`函数签名`的关系，以及如何使用它调用目标函数。

# 30. Try Catch

`try-catch`是现代编程语言几乎都有的处理异常的一种标准方式，`Solidity`0.6版本也添加了它。这一讲，我们将介绍如何利用`try-catch`处理智能合约中的异常。

## `try-catch`

在`Solidity`中，`try-catch`只能被用于`external`函数或创建合约时`constructor`（被视为`external`函数）的调用。基本语法如下：

```solidity
try externalContract.f() {
    // call成功的情况下 运行一些代码
} catch {
    // call失败的情况下 运行一些代码
}
```



其中`externalContract.f()`是某个外部合约的函数调用，`try`模块在调用成功的情况下运行，而`catch`模块则在调用失败时运行。

同样可以使用`this.f()`来替代`externalContract.f()`，`this.f()`也被视作为外部调用，但不可在构造函数中使用，因为此时合约还未创建。

如果调用的函数有返回值，那么必须在`try`之后声明`returns(returnType val)`，并且在`try`模块中可以使用返回的变量；如果是创建合约，那么返回值是新创建的合约变量。

```solidity
try externalContract.f() returns(returnType val){
    // call成功的情况下 运行一些代码
} catch {
    // call失败的情况下 运行一些代码
}
```



另外，`catch`模块支持捕获特殊的异常原因：

```solidity
try externalContract.f() returns(returnType){
    // call成功的情况下 运行一些代码
} catch Error(string memory /*reason*/) {
    // 捕获revert("reasonString") 和 require(false, "reasonString")
} catch Panic(uint /*errorCode*/) {
    // 捕获Panic导致的错误 例如assert失败 溢出 除零 数组访问越界
} catch (bytes memory /*lowLevelData*/) {
    // 如果发生了revert且上面2个异常类型匹配都失败了 会进入该分支
    // 例如revert() require(false) revert自定义类型的error
}
```



## `try-catch`实战

### `OnlyEven`

我们创建一个外部合约`OnlyEven`，并使用`try-catch`来处理异常：

```solidity
contract OnlyEven{
    constructor(uint a){
        require(a != 0, "invalid number");
        assert(a != 1);
    }

    function onlyEven(uint256 b) external pure returns(bool success){
        // 输入奇数时revert
        require(b % 2 == 0, "Ups! Reverting");
        success = true;
    }
}
```



`OnlyEven`合约包含一个构造函数和一个`onlyEven`函数。

- 构造函数有一个参数`a`，当`a=0`时，`require`会抛出异常；当`a=1`时，`assert`会抛出异常；其他情况均正常。
- `onlyEven`函数有一个参数`b`，当`b`为奇数时，`require`会抛出异常。

### 处理外部函数调用异常

首先，在`TryCatch`合约中定义一些事件和状态变量：

```solidity
// 成功event
event SuccessEvent();

// 失败event
event CatchEvent(string message);
event CatchByte(bytes data);

// 声明OnlyEven合约变量
OnlyEven even;

constructor() {
    even = new OnlyEven(2);
}
```



`SuccessEvent`是调用成功会释放的事件，而`CatchEvent`和`CatchByte`是抛出异常时会释放的事件，分别对应`require/revert`和`assert`异常的情况。`even`是个`OnlyEven`合约类型的状态变量。

然后我们在`execute`函数中使用`try-catch`处理调用外部函数`onlyEven`中的异常：

```solidity
// 在external call中使用try-catch
function execute(uint amount) external returns (bool success) {
    try even.onlyEven(amount) returns(bool _success){
        // call成功的情况下
        emit SuccessEvent();
        return _success;
    } catch Error(string memory reason){
        // call不成功的情况下
        emit CatchEvent(reason);
    }
}
```



### 在remix上验证，处理外部函数调用异常

当运行`execute(0)`的时候，因为`0`为偶数，满足`require(b % 2 == 0, "Ups! Reverting");`，没有异常抛出，调用成功并释放`SuccessEvent`事件。



![30-1](https://www.wtf.academy/assets/images/30-1-bc1902da9a689fdaa28758811d80322d.png)



当运行`execute(1)`的时候，因为`1`为奇数，不满足`require(b % 2 == 0, "Ups! Reverting");`，异常抛出，调用失败并释放`CatchEvent`事件。



![30-2](https://www.wtf.academy/assets/images/30-2-c4e6e20e992cd70883e8f61fd677f436.png)



### 处理合约创建异常

这里，我们利用`try-catch`来处理合约创建时的异常。只需要把`try`模块改写为`OnlyEven`合约的创建就行：

```solidity
// 在创建新合约中使用try-catch （合约创建被视为external call）
// executeNew(0)会失败并释放`CatchEvent`
// executeNew(1)会失败并释放`CatchByte`
// executeNew(2)会成功并释放`SuccessEvent`
function executeNew(uint a) external returns (bool success) {
    try new OnlyEven(a) returns(OnlyEven _even){
        // call成功的情况下
        emit SuccessEvent();
        success = _even.onlyEven(a);
    } catch Error(string memory reason) {
        // catch失败的 revert() 和 require()
        emit CatchEvent(reason);
    } catch (bytes memory reason) {
        // catch失败的 assert()
        emit CatchByte(reason);
    }
}
```



### 在remix上验证，处理合约创建异常

当运行`executeNew(0)`时，因为`0`不满足`require(a != 0, "invalid number");`，会失败并释放`CatchEvent`事件。



![30-3](https://www.wtf.academy/assets/images/30-3-6e6311e36ea0b1d2899ec09f73873cec.png)



当运行`executeNew(1)`时，因为`1`不满足`assert(a != 1);`，会失败并释放`CatchByte`事件。



![30-4](https://www.wtf.academy/assets/images/30-4-3650d78ee025618d1a9dc7d557b7140a.png)



当运行`executeNew(2)`时，因为`2`满足`require(a != 0, "invalid number");`和`assert(a != 1);`，会成功并释放`SuccessEvent`事件。



![30-5](https://www.wtf.academy/assets/images/30-5-65efcbd5de616b04d9b151323ccc10c4.png)



## 总结

在这一讲，我们介绍了如何在`Solidity`使用`try-catch`来处理智能合约运行中的异常：

- 只能用于外部合约调用和合约创建。
- 如果`try`执行成功，返回变量必须声明，并且与返回的变量类型相同。

## 例题

### 以下异常返回值类型为bytes的是：

选择一个答案

A. revert()

B. require()

C. assert()

D. 以上都是

答案是 C（？）

# 31. ERC20

这一讲，我们将介绍以太坊上的`ERC20`代币标准，并发行自己的测试代币。

## ERC20

`ERC20`是以太坊上的代币标准，来自2015年11月V神参与的[`EIP20`](https://eips.ethereum.org/EIPS/eip-20)。它实现了代币转账的基本逻辑：

- 账户余额(balanceOf())
- 转账(transfer())
- 授权转账(transferFrom())
- 授权(approve())
- 代币总供给(totalSupply())
- 授权转账额度(allowance())
- 代币信息（可选）：名称(name())，代号(symbol())，小数位数(decimals())

## IERC20

`IERC20`是`ERC20`代币标准的接口合约，规定了`ERC20`代币需要实现的函数和事件。 之所以需要定义接口，是因为有了规范后，就存在所有的`ERC20`代币都通用的函数名称，输入参数，输出参数。 在接口函数中，只需要定义函数名称，输入参数，输出参数，并不关心函数内部如何实现。 由此，函数就分为内部和外部两个内容，一个重点是实现，另一个是对外接口，约定共同数据。 这就是为什么需要`ERC20.sol`和`IERC20.sol`两个文件实现一个合约。

### 事件

`IERC20`定义了`2`个事件：`Transfer`事件和`Approval`事件，分别在转账和授权时被释放

```solidity
/**
 * @dev 释放条件：当 `value` 单位的货币从账户 (`from`) 转账到另一账户 (`to`)时.
 */
event Transfer(address indexed from, address indexed to, uint256 value);

/**
 * @dev 释放条件：当 `value` 单位的货币从账户 (`owner`) 授权给另一账户 (`spender`)时.
 */
event Approval(address indexed owner, address indexed spender, uint256 value);
```



### 函数

`IERC20`定义了`6`个函数，提供了转移代币的基本功能，并允许代币获得批准，以便其他链上第三方使用。

- `totalSupply()`返回代币总供给

  ```solidity
  /**
   * @dev 返回代币总供给.
   */
  function totalSupply() external view returns (uint256);
  ```

  

- `balanceOf()`返回账户余额

  ```solidity
  /**
   * @dev 返回账户`account`所持有的代币数.
   */
  function balanceOf(address account) external view returns (uint256);
  ```

  

- `transfer()`转账

  ```solidity
  /**
   * @dev 转账 `amount` 单位代币，从调用者账户到另一账户 `to`.
   *
   * 如果成功，返回 `true`.
   *
   * 释放 {Transfer} 事件.
   */
  function transfer(address to, uint256 amount) external returns (bool);
  ```

  

- `allowance()`返回授权额度

  ```solidity
  /**
   * @dev 返回`owner`账户授权给`spender`账户的额度，默认为0。
   *
   * 当{approve} 或 {transferFrom} 被调用时，`allowance`会改变.
   */
  function allowance(address owner, address spender) external view returns (uint256);
  ```

  

- `approve()`授权

  ```solidity
  /**
   * @dev 调用者账户给`spender`账户授权 `amount`数量代币。
   *
   * 如果成功，返回 `true`.
   *
   * 释放 {Approval} 事件.
   */
  function approve(address spender, uint256 amount) external returns (bool);
  ```

  

- `transferFrom()`授权转账

  ```solidity
  /**
   * @dev 通过授权机制，从`from`账户向`to`账户转账`amount`数量代币。转账的部分会从调用者的`allowance`中扣除。
   *
   * 如果成功，返回 `true`.
   *
   * 释放 {Transfer} 事件.
   */
  function transferFrom(
      address from,
      address to,
      uint256 amount
  ) external returns (bool);
  ```

  

## 实现ERC20

现在我们写一个`ERC20`，将`IERC20`规定的函数简单实现。

### 状态变量

我们需要状态变量来记录账户余额，授权额度和代币信息。其中`balanceOf`, `allowance`和`totalSupply`为`public`类型，会自动生成一个同名`getter`函数，实现`IERC20`规定的`balanceOf()`, `allowance()`和`totalSupply()`。而`name`, `symbol`, `decimals`则对应代币的名称，代号和小数位数。

**注意**：用`override`修饰`public`变量，会重写继承自父合约的与变量同名的`getter`函数，比如`IERC20`中的`balanceOf()`函数。

```solidity
mapping(address => uint256) public override balanceOf;

mapping(address => mapping(address => uint256)) public override allowance;

uint256 public override totalSupply;   // 代币总供给

string public name;   // 名称
string public symbol;  // 代号

uint8 public decimals = 18; // 小数位数
```



### 函数

- 构造函数：初始化代币名称、代号。

  ```solidity
  constructor(string memory name_, string memory symbol_){
      name = name_;
      symbol = symbol_;
  }
  ```

  

- `transfer()`函数：实现`IERC20`中的`transfer`函数，代币转账逻辑。调用方扣除`amount`数量代币，接收方增加相应代币。土狗币会魔改这个函数，加入税收、分红、抽奖等逻辑。

  ```solidity
  function transfer(address recipient, uint amount) public override returns (bool) {
      balanceOf[msg.sender] -= amount;
      balanceOf[recipient] += amount;
      emit Transfer(msg.sender, recipient, amount);
      return true;
  }
  ```

  

- `approve()`函数：实现`IERC20`中的`approve`函数，代币授权逻辑。被授权方`spender`可以支配授权方的`amount`数量的代币。`spender`可以是EOA账户，也可以是合约账户：当你用`uniswap`交易代币时，你需要将代币授权给`uniswap`合约。

  ```solidity
  function approve(address spender, uint amount) public override returns (bool) {
      allowance[msg.sender][spender] = amount;
      emit Approval(msg.sender, spender, amount);
      return true;
  }
  ```

  

- `transferFrom()`函数：实现`IERC20`中的`transferFrom`函数，授权转账逻辑。被授权方将授权方`sender`的`amount`数量的代币转账给接收方`recipient`。

  ```solidity
  function transferFrom(
      address sender,
      address recipient,
      uint amount
  ) public override returns (bool) {
      allowance[sender][msg.sender] -= amount;
      balanceOf[sender] -= amount;
      balanceOf[recipient] += amount;
      emit Transfer(sender, recipient, amount);
      return true;
  }
  ```

  

- `mint()`函数：铸造代币函数，不在`IERC20`标准中。这里为了教程方便，任何人可以铸造任意数量的代币，实际应用中会加权限管理，只有`owner`可以铸造代币：

  ```solidity
  function mint(uint amount) external {
      balanceOf[msg.sender] += amount;
      totalSupply += amount;
      emit Transfer(address(0), msg.sender, amount);
  }
  ```

  

- `burn()`函数：销毁代币函数，不在`IERC20`标准中。

  ```solidity
  function burn(uint amount) external {
      balanceOf[msg.sender] -= amount;
      totalSupply -= amount;
      emit Transfer(msg.sender, address(0), amount);
  }
  ```

  

## 发行`ERC20`代币

有了`ERC20`标准后，在`ETH`链上发行代币变得非常简单。现在，我们发行属于我们的第一个代币。

在`Remix`上编译好`ERC20`合约，在部署栏输入构造函数的参数，`name_`和`symbol_`都设为`WTF`，然后点击`transact`键进行部署。



![部署合约](https://www.wtf.academy/assets/images/31-1-ec6f958e7cd464bc471465252548fa1e.png)



这样，我们就创建好了`WTF`代币。我们需要运行`mint()`函数来给自己铸造一些代币。点开`Deployed Contract`中的`ERC20`合约，在`mint`函数那一栏输入`100`并点击`mint`按钮，为自己铸造`100`个`WTF`代币。

可以点开右侧的Debug按钮，具体查看下面的logs。

里面包含四个关键信息：

- 事件`Transfer`
- 铸币地址`0x0000000000000000000000000000000000000000`
- 接收地址`0x5B38Da6a701c568545dCfcB03FcB875f56beddC4`
- 代币数额`100`



![铸造代币](https://www.wtf.academy/assets/images/31-2-e1e6bd01e9471e8f8042e5f036bac484.png)



我们利用`balanceOf()`函数来查询账户余额。输入我们当前的账户，可以看到余额变为`100`，铸造成功。

账户信息如图左侧，右侧标注为函数执行的具体信息。



![查询余额](https://www.wtf.academy/assets/images/31-3-c051bc9f25db49f67be465dfc56ecd8e.png)



## 总结

在这一讲，我们学习了以太坊上的`ERC20`标准及其实现，并且发行了我们的测试代币。2015年底提出的`ERC20`代币标准极大的降低了以太坊上发行代币的门槛，并开启了`ICO`大时代。在投资时，仔细阅读项目的代币合约，可以有效避开貔貅，增加投资成功率。

# 32. 代币水龙头

我们在第31讲学习了`ERC20`代币标准。这一讲，我们将学习`ERC20`水龙头的智能合约。在这个合约中，用户可以领到免费的`ERC20`代币。

## 代币水龙头

当人渴的时候，就要去水龙头接水；当人想要免费代币的时候，就要去代币水龙头领。代币水龙头就是让用户免费领代币的网站/应用。

最早的代币水龙头是比特币（BTC）水龙头：现在BTC一枚要$30,000，但是在2010年，BTC的价格只有不到$0.1，并且持有人很少。为了扩大影响力，比特币社区的Gavin Andresen开发了BTC水龙头，让别人可以免费领BTC。撸羊毛大家都喜欢，当时就有很多人去撸，一部分变为了BTC的信徒。BTC水龙头一共送出了超过19,700枚BTC，现在价值约6亿美元！

## ERC20水龙头合约

这里，我们实现一个简版的`ERC20`水龙头，逻辑非常简单：我们将一些`ERC20`代币转到水龙头合约里，用户可以通过合约的`requestToken()`函数来领取`100`单位的代币，每个地址只能领一次。

### 状态变量

我们在水龙头合约中定义3个状态变量

- `amountAllowed`设定每次能领取代币数量（默认为`100`，不是一百枚，因为代币有小数位数）。
- `tokenContract`记录发放的`ERC20`代币合约地址。
- `requestedAddress`记录领取过代币的地址。

```solidity
uint256 public amountAllowed = 100; // 每次领 100 单位代币
address public tokenContract;   // token合约地址
mapping(address => bool) public requestedAddress;   // 记录领取过代币的地址
```



### 事件

水龙头合约中定义了1个`SendToken`事件，记录了每次领取代币的地址和数量，在`requestTokens()`函数被调用时释放。

```solidity
// SendToken事件    
event SendToken(address indexed Receiver, uint256 indexed Amount); 
```



### 函数

合约中只有两个函数：

- 构造函数：初始化`tokenContract`状态变量，确定发放的`ERC20`代币地址。

  ```solidity
  // 部署时设定ERC20代币合约
  constructor(address _tokenContract) {
    tokenContract = _tokenContract; // set token contract
  }
  ```

  

- `requestTokens()`函数，用户调用它可以领取`ERC20`代币。

  ```solidity
  // 用户领取代币函数
  function requestTokens() external {
      require(!requestedAddress[msg.sender], "Can't Request Multiple Times!"); // 每个地址只能领一次
      IERC20 token = IERC20(tokenContract); // 创建IERC20合约对象
      require(token.balanceOf(address(this)) >= amountAllowed, "Faucet Empty!"); // 水龙头空了
  
      token.transfer(msg.sender, amountAllowed); // 发送token
      requestedAddress[msg.sender] = true; // 记录领取地址 
      
      emit SendToken(msg.sender, amountAllowed); // 释放SendToken事件
  }
  ```

  

## Remix演示

1. 首先，部署`ERC20`代币合约，名称和符号为`WTF`，并给自己`mint` 10000 单位代币。

   ![部署`ERC20`](https://www.wtf.academy/assets/images/32-1-5b232ca00c103a5fe8ead68e61650da2.png)

   

2. 部署`Faucet`水龙头合约，初始化的参数填上面`ERC20`代币的合约地址。

   ![部署`Faucet`水龙头合约](https://www.wtf.academy/assets/images/32-2-4acfc621d8d213f12abc95aed7a9fd8c.png)

   

3. 利用`ERC20`代币合约的`transfer()`函数，将 10000 单位代币转账到`Faucet`合约地址。

   ![给`Faucet`水龙头合约转账](https://www.wtf.academy/assets/images/32-3-4e5ea0dc6174f24155e920dce57a8b54.png)

   

4. 换一个新账户，调用`Faucet`合约`requestTokens()`函数，领取代币。可以在终端看到`SendToken`事件被释放。

   ![切换账户](https://www.wtf.academy/assets/images/32-4-56b470ee083c0412ca002c2b247bb03f.png)

   

   

   ![requestToken](https://www.wtf.academy/assets/images/32-5-acfddb18f641690d958c9494f77ff190.png)

   

5. 在`ERC20`代币合约上利用`balanceOf`查询领取水龙头的账户余额，可以看到余额变为`100`，领取成功！

   ![领取成功](https://www.wtf.academy/assets/images/32-6-c9e6591caa24482c1fa226e0a76dbc79.png)

   

## 总结

这一讲，我们介绍了代币水龙头的历史和`ERC20`水龙头合约。大家觉得下一个`BTC`水龙头会在哪里？

# 33. 空投合约

在币圈，最开心的一件事就是领空投，空手套白狼。这一讲，我们将学习如何使用智能合约发送`ERC20`代币空投。

## 空投 Airdrop

空投是币圈中一种营销策略，项目方将代币免费发放给特定用户群体。为了拿到空投资格，用户通常需要完成一些简单的任务，如测试产品、分享新闻、介绍朋友等。项目方通过空投可以获得种子用户，而用户可以获得一笔财富，两全其美。

因为每次接收空投的用户很多，项目方不可能一笔一笔的转账。利用智能合约批量发放`ERC20`代币，可以显著提高空投效率。

### 空投代币合约

`Airdrop`空投合约逻辑非常简单：利用循环，一笔交易将`ERC20`代币发送给多个地址。合约中包含两个函数

- `getSum()`函数：返回`uint`数组的和。

  ```solidity
  // 数组求和函数
  function getSum(uint256[] calldata _arr) public pure returns(uint sum){
      for(uint i = 0; i < _arr.length; i++)
          sum = sum + _arr[i];
  }
  ```

  

- `multiTransferToken()`函数：发送`ERC20`代币空投，包含`3`个参数：

  - `_token`：代币合约地址（`address`类型）
  - `_addresses`：接收空投的用户地址数组（`address[]`类型）
  - `_amounts`：空投数量数组，对应`_addresses`里每个地址的数量（`uint[]`类型）

  该函数有两个检查：第一个`require`检查了`_addresses`和`_amounts`两个数组长度是否相等；第二个`require`检查了空投合约的授权额度大于要空投的代币数量总和。

  ```solidity
  /// @notice 向多个地址转账ERC20代币，使用前需要先授权
  ///
  /// @param _token 转账的ERC20代币地址
  /// @param _addresses 空投地址数组
  /// @param _amounts 代币数量数组（每个地址的空投数量）
  function multiTransferToken(
      address _token,
      address[] calldata _addresses,
      uint256[] calldata _amounts
      ) external {
      // 检查：_addresses和_amounts数组的长度相等
      require(_addresses.length == _amounts.length, "Lengths of Addresses and Amounts NOT EQUAL");
      IERC20 token = IERC20(_token); // 声明IERC合约变量
      uint _amountSum = getSum(_amounts); // 计算空投代币总量
      // 检查：授权代币数量 >= 空投代币总量
      require(token.allowance(msg.sender, address(this)) >= _amountSum, "Need Approve ERC20 token");
  
      // for循环，利用transferFrom函数发送空投
      for (uint8 i; i < _addresses.length; i++) {
          token.transferFrom(msg.sender, _addresses[i], _amounts[i]);
      }
  }
  ```

  

- `multiTransferETH()`函数：发送`ETH`空投，包含`2`个参数：

  - `_addresses`：接收空投的用户地址数组（`address[]`类型）
  - `_amounts`：空投数量数组，对应`_addresses`里每个地址的数量（`uint[]`类型）

  ```solidity
  /// 向多个地址转账ETH
  function multiTransferETH(
      address payable[] calldata _addresses,
      uint256[] calldata _amounts
  ) public payable {
      // 检查：_addresses和_amounts数组的长度相等
      require(_addresses.length == _amounts.length, "Lengths of Addresses and Amounts NOT EQUAL");
      uint _amountSum = getSum(_amounts); // 计算空投ETH总量
      // 检查转入ETH等于空投总量
      require(msg.value == _amountSum, "Transfer amount error");
      // for循环，利用transfer函数发送ETH
      for (uint256 i = 0; i < _addresses.length; i++) {
          // 注释代码有Dos攻击风险, 并且transfer 也是不推荐写法
          // Dos攻击 具体参考 https://github.com/AmazingAng/WTF-Solidity/blob/main/S09_DoS/readme.md
          // _addresses[i].transfer(_amounts[i]);
          (bool success, ) = _addresses[i].call{value: _amounts[i]}("");
          if (!success) {
              failTransferList[_addresses[i]] = _amounts[i];
          }
      }
  }
  ```

  

### 空投实践

1. 部署`ERC20`代币合约，并给自己`mint`10000 单位代币。

   

   ![部署`ERC20`](https://www.wtf.academy/assets/images/33-1-5200c2a1063a08e3ee56ddb6021e1ecd.png)

   

   

   ![mint](https://www.wtf.academy/assets/images/33-2-3e29d5f04275dc5e79461140832f69e6.png)

   

2. 部署`Airdrop`空投合约。

   

   ![部署`Airdrop`合约](https://www.wtf.academy/assets/images/33-3-f4a5796f2433428a80c395ef80312554.png)

   

3. 利用`ERC20`代币合约中的`approve()`函数，给`Airdrop`空投合约授权 10000 单位代币。

   

   ![授权`Airdrop`合约](https://www.wtf.academy/assets/images/33-4-df0c6eef3fdff0033007ee8df1ad06f3.png)

   

4. 执行`Airdrop`合约的`multiTransferToken()`函数进行空投， `_token`填`ERC20`代币地址，`_addresses`和`_amounts`按照以下填写

   ```text
   // _addresses填写
   ["0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2", "0x5B38Da6a701c568545dCfcB03FcB875f56beddC4"]
   
   // _amounts填写
   [100, 200]
   ```

   

   

   ![空投](https://www.wtf.academy/assets/images/33-5-f547c3ad9fc5e8d6c1f5fd79f75be044.png)

   

5. 利用`ERC20`合约的`balanceOf()`函数查询上面用户地址的代币余额，成功变为`100`和`200`，空投成功！

   

   ![查询空投用户的代币余额](https://www.wtf.academy/assets/images/33-6-ef8550dd0b350ac57f2c8d1ffc1eaea1.png)

   

## 总结

这一讲，我们介绍了如何使用`Solidity`写`ERC20`代币空投合约，极大增加空投效率。我撸空投收获最大的一次是`ENS`空投，你们呢？

# 34. ERC721

`BTC`和`ETH`这类代币都属于同质化代币，矿工挖出的第`1`枚`BTC`与第`10000`枚`BTC`并没有不同，是等价的。但世界中很多物品是不同质的，其中包括房产、古董、虚拟艺术品等等，这类物品无法用同质化代币抽象。因此，[以太坊EIP721](https://eips.ethereum.org/EIPS/eip-721)提出了`ERC721`标准，来抽象非同质化的物品。这一讲，我们将介绍`ERC721`标准，并基于它发行一款`NFT`。

## EIP与ERC

这里有一个点需要理解，本节标题是`ERC721`，这里又提到了`EIP721`,这两个是什么关系呢？

`EIP`全称 `Ethereum Improvement Proposals`(以太坊改进建议), 是以太坊开发者社区提出的改进建议, 是一系列以编号排定的文件, 类似互联网上IETF的RFC。

`EIP`可以是 `Ethereum` 生态中任意领域的改进, 比如新特性、ERC、协议改进、编程工具等等。

`ERC`全称 Ethereum Request For Comment (以太坊意见征求稿), 用以记录以太坊上应用级的各种开发标准和协议。如典型的Token标准(`ERC20`, `ERC721`)、名字注册(`ERC26`, `ERC13`), URI范式(`ERC67`), Library/Package格式(`EIP82`), 钱包格式(`EIP75`,`EIP85`)。

ERC协议标准是影响以太坊发展的重要因素, 像`ERC20`, `ERC223`, `ERC721`, `ERC777`等, 都是对以太坊生态产生了很大影响。

所以最终结论：`EIP`包含`ERC`。

**在这一节学习完成后，才能明白为什么上来讲`ERC165`而不是`ERC721`，想要看结论可直接移动到最下面**

## ERC165

通过[ERC165标准](https://eips.ethereum.org/EIPS/eip-165)，智能合约可以声明它支持的接口，供其他合约检查。简单的说，ERC165就是检查一个智能合约是不是支持了`ERC721`，`ERC1155`的接口。

`IERC165`接口合约只声明了一个`supportsInterface`函数，输入要查询的`interfaceId`接口id，若合约实现了该接口id，则返回`true`：

```solidity
interface IERC165 {
    /**
     * @dev 如果合约实现了查询的`interfaceId`，则返回true
     * 规则详见：https://eips.ethereum.org/EIPS/eip-165#how-interfaces-are-identified[EIP section]
     *
     */
    function supportsInterface(bytes4 interfaceId) external view returns (bool);
}
```



我们可以看下`ERC721`是如何实现`supportsInterface()`函数的：

```solidity
    function supportsInterface(bytes4 interfaceId) external pure override returns (bool)
    {
        return
            interfaceId == type(IERC721).interfaceId ||
            interfaceId == type(IERC165).interfaceId;
    }
```



当查询的是`IERC721`或`IERC165`的接口id时，返回`true`；反之返回`false`。

## IERC721

`IERC721`是`ERC721`标准的接口合约，规定了`ERC721`要实现的基本函数。它利用`tokenId`来表示特定的非同质化代币，授权或转账都要明确`tokenId`；而`ERC20`只需要明确转账的数额即可。

```solidity
/**
 * @dev ERC721标准接口.
 */
interface IERC721 is IERC165 {
    event Transfer(address indexed from, address indexed to, uint256 indexed tokenId);
    event Approval(address indexed owner, address indexed approved, uint256 indexed tokenId);
    event ApprovalForAll(address indexed owner, address indexed operator, bool approved);

    function balanceOf(address owner) external view returns (uint256 balance);

    function ownerOf(uint256 tokenId) external view returns (address owner);

    function safeTransferFrom(
        address from,
        address to,
        uint256 tokenId,
        bytes calldata data
    ) external;

    function safeTransferFrom(
        address from,
        address to,
        uint256 tokenId
    ) external;

    function transferFrom(
        address from,
        address to,
        uint256 tokenId
    ) external;

    function approve(address to, uint256 tokenId) external;

    function setApprovalForAll(address operator, bool _approved) external;

    function getApproved(uint256 tokenId) external view returns (address operator);

    function isApprovedForAll(address owner, address operator) external view returns (bool);
}
```



### IERC721事件

`IERC721`包含3个事件，其中`Transfer`和`Approval`事件在`ERC20`中也有。

- `Transfer`事件：在转账时被释放，记录代币的发出地址`from`，接收地址`to`和`tokenid`。
- `Approval`事件：在授权时释放，记录授权地址`owner`，被授权地址`approved`和`tokenid`。
- `ApprovalForAll`事件：在批量授权时释放，记录批量授权的发出地址`owner`，被授权地址`operator`和授权与否的`approved`。

### IERC721函数

- `balanceOf`：返回某地址的NFT持有量`balance`。
- `ownerOf`：返回某`tokenId`的主人`owner`。
- `transferFrom`：普通转账，参数为转出地址`from`，接收地址`to`和`tokenId`。
- `safeTransferFrom`：安全转账（如果接收方是合约地址，会要求实现`ERC721Receiver`接口）。参数为转出地址`from`，接收地址`to`和`tokenId`。
- `approve`：授权另一个地址使用你的NFT。参数为被授权地址`approve`和`tokenId`。
- `getApproved`：查询`tokenId`被批准给了哪个地址。
- `setApprovalForAll`：将自己持有的该系列NFT批量授权给某个地址`operator`。
- `isApprovedForAll`：查询某地址的NFT是否批量授权给了另一个`operator`地址。
- `safeTransferFrom`：安全转账的重载函数，参数里面包含了`data`。

## IERC721Receiver

如果一个合约没有实现`ERC721`的相关函数，转入的`NFT`就进了黑洞，永远转不出来了。为了防止误转账，`ERC721`实现了`safeTransferFrom()`安全转账函数，目标合约必须实现了`IERC721Receiver`接口才能接收`ERC721`代币，不然会`revert`。`IERC721Receiver`接口只包含一个`onERC721Received()`函数。

```solidity
// ERC721接收者接口：合约必须实现这个接口来通过安全转账接收ERC721
interface IERC721Receiver {
    function onERC721Received(
        address operator,
        address from,
        uint tokenId,
        bytes calldata data
    ) external returns (bytes4);
}
```



我们看下`ERC721`利用`_checkOnERC721Received`来确保目标合约实现了`onERC721Received()`函数（返回`onERC721Received`的`selector`）：

```solidity
function _checkOnERC721Received(
    address operator,
    address from,
    address to,
    uint256 tokenId,
    bytes memory data
) internal {
    if (to.code.length > 0) {
        try IERC721Receiver(to).onERC721Received(operator, from, tokenId, data) returns (bytes4 retval) {
            if (retval != IERC721Receiver.onERC721Received.selector) {
                // Token rejected
                revert IERC721Errors.ERC721InvalidReceiver(to);
            }
        } catch (bytes memory reason) {
            if (reason.length == 0) {
                // non-IERC721Receiver implementer
                revert IERC721Errors.ERC721InvalidReceiver(to);
            } else {
                /// @solidity memory-safe-assembly
                assembly {
                    revert(add(32, reason), mload(reason))
                }
            }
        }
    }
}
```



## IERC721Metadata

`IERC721Metadata`是`ERC721`的拓展接口，实现了3个查询`metadata`元数据的常用函数：

- `name()`：返回代币名称。
- `symbol()`：返回代币代号。
- `tokenURI()`：通过`tokenId`查询`metadata`的链接`url`，`ERC721`特有的函数。

```solidity
interface IERC721Metadata is IERC721 {
    function name() external view returns (string memory);

    function symbol() external view returns (string memory);

    function tokenURI(uint256 tokenId) external view returns (string memory);
}
```



## ERC721主合约

`ERC721`主合约实现了`IERC721`，`IERC165`和`IERC721Metadata`定义的所有功能，包含`4`个状态变量和`17`个函数。实现都比较简单，每个函数的功能见代码注释：

```solidity
// SPDX-License-Identifier: MIT
// by 0xAA
pragma solidity ^0.8.21;

import "./IERC165.sol";
import "./IERC721.sol";
import "./IERC721Receiver.sol";
import "./IERC721Metadata.sol";
import "./String.sol";

contract ERC721 is IERC721, IERC721Metadata{
    using Strings for uint256; // 使用String库，

    // Token名称
    string public override name;
    // Token代号
    string public override symbol;
    // tokenId 到 owner address 的持有人映射
    mapping(uint => address) private _owners;
    // address 到 持仓数量 的持仓量映射
    mapping(address => uint) private _balances;
    // tokenID 到 授权地址 的授权映射
    mapping(uint => address) private _tokenApprovals;
    //  owner地址。到operator地址 的批量授权映射
    mapping(address => mapping(address => bool)) private _operatorApprovals;

    // 错误 无效的接收者
    error ERC721InvalidReceiver(address receiver);

    /**
     * 构造函数，初始化`name` 和`symbol` .
     */
    constructor(string memory name_, string memory symbol_) {
        name = name_;
        symbol = symbol_;
    }

    // 实现IERC165接口supportsInterface
    function supportsInterface(bytes4 interfaceId)
        external
        pure
        override
        returns (bool)
    {
        return
            interfaceId == type(IERC721).interfaceId ||
            interfaceId == type(IERC165).interfaceId ||
            interfaceId == type(IERC721Metadata).interfaceId;
    }

    // 实现IERC721的balanceOf，利用_balances变量查询owner地址的balance。
    function balanceOf(address owner) external view override returns (uint) {
        require(owner != address(0), "owner = zero address");
        return _balances[owner];
    }

    // 实现IERC721的ownerOf，利用_owners变量查询tokenId的owner。
    function ownerOf(uint tokenId) public view override returns (address owner) {
        owner = _owners[tokenId];
        require(owner != address(0), "token doesn't exist");
    }

    // 实现IERC721的isApprovedForAll，利用_operatorApprovals变量查询owner地址是否将所持NFT批量授权给了operator地址。
    function isApprovedForAll(address owner, address operator)
        external
        view
        override
        returns (bool)
    {
        return _operatorApprovals[owner][operator];
    }

    // 实现IERC721的setApprovalForAll，将持有代币全部授权给operator地址。调用_setApprovalForAll函数。
    function setApprovalForAll(address operator, bool approved) external override {
        _operatorApprovals[msg.sender][operator] = approved;
        emit ApprovalForAll(msg.sender, operator, approved);
    }

    // 实现IERC721的getApproved，利用_tokenApprovals变量查询tokenId的授权地址。
    function getApproved(uint tokenId) external view override returns (address) {
        require(_owners[tokenId] != address(0), "token doesn't exist");
        return _tokenApprovals[tokenId];
    }
     
    // 授权函数。通过调整_tokenApprovals来，授权 to 地址操作 tokenId，同时释放Approval事件。
    function _approve(
        address owner,
        address to,
        uint tokenId
    ) private {
        _tokenApprovals[tokenId] = to;
        emit Approval(owner, to, tokenId);
    }

    // 实现IERC721的approve，将tokenId授权给 to 地址。条件：to不是owner，且msg.sender是owner或授权地址。调用_approve函数。
    function approve(address to, uint tokenId) external override {
        address owner = _owners[tokenId];
        require(
            msg.sender == owner || _operatorApprovals[owner][msg.sender],
            "not owner nor approved for all"
        );
        _approve(owner, to, tokenId);
    }

    // 查询 spender地址是否可以使用tokenId（需要是owner或被授权地址）
    function _isApprovedOrOwner(
        address owner,
        address spender,
        uint tokenId
    ) private view returns (bool) {
        return (spender == owner ||
            _tokenApprovals[tokenId] == spender ||
            _operatorApprovals[owner][spender]);
    }

    /*
     * 转账函数。通过调整_balances和_owner变量将 tokenId 从 from 转账给 to，同时释放Transfer事件。
     * 条件:
     * 1. tokenId 被 from 拥有
     * 2. to 不是0地址
     */
    function _transfer(
        address owner,
        address from,
        address to,
        uint tokenId
    ) private {
        require(from == owner, "not owner");
        require(to != address(0), "transfer to the zero address");

        _approve(owner, address(0), tokenId);

        _balances[from] -= 1;
        _balances[to] += 1;
        _owners[tokenId] = to;

        emit Transfer(from, to, tokenId);
    }
    
    // 实现IERC721的transferFrom，非安全转账，不建议使用。调用_transfer函数
    function transferFrom(
        address from,
        address to,
        uint tokenId
    ) external override {
        address owner = ownerOf(tokenId);
        require(
            _isApprovedOrOwner(owner, msg.sender, tokenId),
            "not owner nor approved"
        );
        _transfer(owner, from, to, tokenId);
    }

    /**
     * 安全转账，安全地将 tokenId 代币从 from 转移到 to，会检查合约接收者是否了解 ERC721 协议，以防止代币被永久锁定。调用了_transfer函数和_checkOnERC721Received函数。条件：
     * from 不能是0地址.
     * to 不能是0地址.
     * tokenId 代币必须存在，并且被 from拥有.
     * 如果 to 是智能合约, 他必须支持 IERC721Receiver-onERC721Received.
     */
    function _safeTransfer(
        address owner,
        address from,
        address to,
        uint tokenId,
        bytes memory _data
    ) private {
        _transfer(owner, from, to, tokenId);
        _checkOnERC721Received(from, to, tokenId, _data);
    }

    /**
     * 实现IERC721的safeTransferFrom，安全转账，调用了_safeTransfer函数。
     */
    function safeTransferFrom(
        address from,
        address to,
        uint tokenId,
        bytes memory _data
    ) public override {
        address owner = ownerOf(tokenId);
        require(
            _isApprovedOrOwner(owner, msg.sender, tokenId),
            "not owner nor approved"
        );
        _safeTransfer(owner, from, to, tokenId, _data);
    }

    // safeTransferFrom重载函数
    function safeTransferFrom(
        address from,
        address to,
        uint tokenId
    ) external override {
        safeTransferFrom(from, to, tokenId, "");
    }

    /** 
     * 铸造函数。通过调整_balances和_owners变量来铸造tokenId并转账给 to，同时释放Transfer事件。铸造函数。通过调整_balances和_owners变量来铸造tokenId并转账给 to，同时释放Transfer事件。
     * 这个mint函数所有人都能调用，实际使用需要开发人员重写，加上一些条件。
     * 条件:
     * 1. tokenId尚不存在。
     * 2. to不是0地址.
     */
    function _mint(address to, uint tokenId) internal virtual {
        require(to != address(0), "mint to zero address");
        require(_owners[tokenId] == address(0), "token already minted");

        _balances[to] += 1;
        _owners[tokenId] = to;

        emit Transfer(address(0), to, tokenId);
    }

    // 销毁函数，通过调整_balances和_owners变量来销毁tokenId，同时释放Transfer事件。条件：tokenId存在。
    function _burn(uint tokenId) internal virtual {
        address owner = ownerOf(tokenId);
        require(msg.sender == owner, "not owner of token");

        _approve(owner, address(0), tokenId);

        _balances[owner] -= 1;
        delete _owners[tokenId];

        emit Transfer(owner, address(0), tokenId);
    }

    // _checkOnERC721Received：函数，用于在 to 为合约的时候调用IERC721Receiver-onERC721Received, 以防 tokenId 被不小心转入黑洞。
    function _checkOnERC721Received(address from, address to, uint256 tokenId, bytes memory data) private {
        if (to.code.length > 0) {
            try IERC721Receiver(to).onERC721Received(msg.sender, from, tokenId, data) returns (bytes4 retval) {
                if (retval != IERC721Receiver.onERC721Received.selector) {
                    revert ERC721InvalidReceiver(to);
                }
            } catch (bytes memory reason) {
                if (reason.length == 0) {
                    revert ERC721InvalidReceiver(to);
                } else {
                    /// @solidity memory-safe-assembly
                    assembly {
                        revert(add(32, reason), mload(reason))
                    }
                }
            }
        }
    }

    /**
     * 实现IERC721Metadata的tokenURI函数，查询metadata。
     */
    function tokenURI(uint256 tokenId) public view virtual override returns (string memory) {
        require(_owners[tokenId] != address(0), "Token Not Exist");

        string memory baseURI = _baseURI();
        return bytes(baseURI).length > 0 ? string(abi.encodePacked(baseURI, tokenId.toString())) : "";
    }

    /**
     * 计算{tokenURI}的BaseURI，tokenURI就是把baseURI和tokenId拼接在一起，需要开发重写。
     * BAYC的baseURI为ipfs://QmeSjSinHpPnmXmspMjwiXyN6zS4E9zccariGR3jxcaWtq/ 
     */
    function _baseURI() internal view virtual returns (string memory) {
        return "";
    }
}
```



## 写一个免费铸造的APE

我们来利用`ERC721`来写一个免费铸造的`WTF APE`，总量设置为`10000`，只需要重写一下`mint()`和`baseURI()`函数即可。由于`baseURI()`设置的和`BAYC`一样，元数据会直接获取无聊猿的，类似[RRBAYC](https://rrbayc.com/)：

```solidity
// SPDX-License-Identifier: MIT
// by 0xAA
pragma solidity ^0.8.21;

import "./ERC721.sol";

contract WTFApe is ERC721{
    uint public MAX_APES = 10000; // 总量

    // 构造函数
    constructor(string memory name_, string memory symbol_) ERC721(name_, symbol_){
    }

    //BAYC的baseURI为ipfs://QmeSjSinHpPnmXmspMjwiXyN6zS4E9zccariGR3jxcaWtq/ 
    function _baseURI() internal pure override returns (string memory) {
        return "ipfs://QmeSjSinHpPnmXmspMjwiXyN6zS4E9zccariGR3jxcaWtq/";
    }
    
    // 铸造函数
    function mint(address to, uint tokenId) external {
        require(tokenId >= 0 && tokenId < MAX_APES, "tokenId out of range");
        _mint(to, tokenId);
    }
}
```



## 发行`ERC721`NFT

有了`ERC721`标准后，在`ETH`链上发行NFT变得非常简单。现在，我们发行属于我们的NFT。

在`Remix`上编译好`ERC721`合约和`WTFApe`合约（按照顺序），在部署栏点击下按钮，输入构造函数的参数，`name_`和`symbol_`都设为`WTF`，然后点击`transact`键进行部署。



![NFT信息如何重点](https://www.wtf.academy/assets/images/34-1-52b218571645b6ba4b70817e795fb5d3.png)

![部署合约](https://www.wtf.academy/assets/images/34-2-6e7a2667f2e28d77d9034ca7c5b66dab.png)



这样，我们就创建好了`WTF`NFT。我们需要运行`mint()`函数来给自己铸造一些代币。在`mint`函数那一栏点开右侧的下按钮输入账户地址，和tokenid，并点击`mint`按钮，为自己铸造`0`号`WTF`NFT。

可以点开右侧的Debug按钮，具体查看下面的logs。

里面包含四个关键信息：

- 事件`Transfer`
- 铸造地址`0x0000000000000000000000000000000000000000`
- 接收地址`0x5B38Da6a701c568545dCfcB03FcB875f56beddC4`
- tokenid`0`



![铸造NFT](https://www.wtf.academy/assets/images/34-3-81f5e5e3672c54ef917b2c0d40f6b123.png)



我们利用`balanceOf()`函数来查询账户余额。输入我们当前的账户，可以看到有一个`NFT`，铸造成功。

账户信息如图左侧，右侧标注为函数执行的具体信息。



![查询NFT详情](https://www.wtf.academy/assets/images/34-4-63f3aac2ec55af6e812a598b7653bf48.png)



我们也可以利用`ownerOf()`函数来查询NFT属于哪个账户。输入`tokenid`，可以我们的地址，查询无误。



![tokenid查询拥有者详情](https://www.wtf.academy/assets/images/34-5-d16eed61e3e3c9675babf9f8133d0387.png)



## ERC165与ERC721详解

上面说到,为了防止NFT被转到一个没有能力操作NFT的合约中去,目标必须正确实现ERC721TokenReceiver接口：

```solidity
interface ERC721TokenReceiver {
    function onERC721Received(address _operator, address _from, uint256 _tokenId, bytes _data) external returns(bytes4);
}
```



拓展到编程语言的世界中去，无论是Java的interface，还是Rust的Trait(当然solidity中和trait更像的是library)，只要是和接口沾边的，都在透露着一种这样的意味：接口是某些行为的集合(在solidity中更甚，接口完全等价于函数选择器的集合)，某个类型只要实现了某个接口，就表明该类型拥有这样的一种功能。因此，只要某个contract类型实现了上述的`ERC721TokenReceiver`接口(更具体而言就是实现了`onERC721Received`这个函数),该contract类型就对外表明了自己拥有管理NFT的能力。当然操作NFT的逻辑被实现在该合约其他的函数中。 ERC721标准在执行`safeTransferFrom`的时候会检查目标合约是否实现了`onERC721Received`函数,这是一种利用ERC165思想进行的操作。
**那究竟什么是ERC165呢?**
ERC165是一种对外表明自己实现了哪些接口的技术标准。就像上面所说的，实现了一个接口就表明合约拥有种特殊能力。有一些合约与其他合约交互时，期望目标合约拥有某些功能，那么合约之间就能够通过ERC165标准对对方进行查询以检查对方是否拥有相应的能力。
以ERC721合约为例，当外部对某个合约进行检查其是否是ERC721时，[怎么做？](https://eips.ethereum.org/EIPS/eip-165#how-to-detect-if-a-contract-implements-erc-165) 。按照这个说法，检查步骤应该是首先检查该合约是否实现了ERC165, 再检查该合约实现的其他特定接口。此时该特定接口是IERC721. IERC721的是ERC721的基本接口(为什么说基本，是因为还有其他的诸如`ERC721Metadata` `ERC721Enumerable` 这样的拓展)：

```solidity
/// 注意这个**0x80ac58cd**
///  **⚠⚠⚠ Note: the ERC-165 identifier for this interface is 0x80ac58cd. ⚠⚠⚠**
interface ERC721  {
    event Transfer(address indexed _from, address indexed _to, uint256 indexed _tokenId);

    event Approval(address indexed _owner, address indexed _approved, uint256 indexed _tokenId);

    event ApprovalForAll(address indexed _owner, address indexed _operator, bool _approved);

    function balanceOf(address _owner) external view returns (uint256);

    function ownerOf(uint256 _tokenId) external view returns (address);

    function safeTransferFrom(address _from, address _to, uint256 _tokenId, bytes data) external payable;

    function safeTransferFrom(address _from, address _to, uint256 _tokenId) external payable;

    function transferFrom(address _from, address _to, uint256 _tokenId) external payable;

    function approve(address _approved, uint256 _tokenId) external payable;

    function setApprovalForAll(address _operator, bool _approved) external;

    function getApproved(uint256 _tokenId) external view returns (address);

    function isApprovedForAll(address _owner, address _operator) external view returns (bool);
}
```



**0x80ac58cd**= `bytes4(keccak256(ERC721.Transfer.selector) ^ keccak256(ERC721.Approval.selector) ^ ··· ^keccak256(ERC721.isApprovedForAll.selector))`，这是ERC165规定的计算方式。

那么，类似的，能够计算出ERC165本身的接口(它的接口里只有一个 `function supportsInterface(bytes4 interfaceID) external view returns (bool);` 函数，对其进行`bytes4(keccak256(supportsInterface.selector))` 得到**0x01ffc9a7**。此外，ERC721还定义了一些拓展接口，比如`ERC721Metadata` ，长这样：

```solidity
///  Note: the ERC-165 identifier for this interface is 0x5b5e139f.
interface ERC721Metadata // is ERC721  
{
    function name() external view returns (string _name);
    function symbol() external view returns (string _symbol);
    function tokenURI(uint256 _tokenId) external view returns (string); // 这个很重要，前端展示的小图片的链接都是这个函数返回的
}
```



这个**0x5b5e139f** 的计算就是:

```solidity
IERC721Metadata.name.selector ^ IERC721Metadata.symbol.selector ^ IERC721Metadata.tokenURI.selector
```



solamte实现的ERC721.sol是怎么完成这些ERC165要求的特性的呢？

```solidity
function supportsInterface(bytes4 interfaceId) public view virtual returns (bool) {
        return
            interfaceId == 0x01ffc9a7 || // ERC165 Interface ID for ERC165
            interfaceId == 0x80ac58cd || // ERC165 Interface ID for ERC721
            interfaceId == 0x5b5e139f; // ERC165 Interface ID for ERC721Metadata
}
```



没错就这么简单。当外界按照[link1](https://eips.ethereum.org/EIPS/eip-165#how-to-detect-if-a-contract-implements-erc-165) 的步骤去做检查的时候，如果外界想检查这个合约是否实现了165,好说，就是supportsInterface函数在入参是`0x01ffc9a7`时必须返回true，在入参是`0xffffffff`时，返回值必须是false。上述实现完美达成要求。

当外界想检查这个合约是否是ERC721的时候，好说，入参是**0x80ac58cd** 的时候表明外界想做这个检查。返回true。

当外界想检查这个合约是否实现ERC721的拓展ERC721Metadata接口时，入参是0x5b5e139f。好说，返回了true。

并且由于该函数是virtual的。因此该合约的使用者可以继承该合约，然后继续实现`ERC721Enumerable` 接口。实现完里面的什么`totalSupply` 啊之类的函数之后，把继承的`supportsInterface`重实现为

```solidity
function supportsInterface(bytes4 interfaceId) public view virtual returns (bool) {
        return
            interfaceId == 0x01ffc9a7 || // ERC165 Interface ID for ERC165
            interfaceId == 0x80ac58cd || // ERC165 Interface ID for ERC721
            interfaceId == 0x5b5e139f || // ERC165 Interface ID for ERC721Metadata
            interfaceId == 0x780e9d63;   // ERC165 Interface ID for ERC721Enumerable
}
```



**优雅，简洁，可拓展性拉满。**

## 总结

这一讲，我介绍了`ERC721`标准、接口及其实现，并在合约代码进行了中文注释。并且我们利用`ERC721`做了一个免费铸造的`WTF APE` NFT，元数据直接调用于`BAYC`。`ERC721`标准仍在不断发展中，目前比较流行的版本为`ERC721Enumerable`（提高NFT可访问性）和`ERC721A`（节约铸造`gas`）。

# 35. 荷兰拍卖

这一讲，我将介绍荷兰拍卖，并通过简化版`Azuki`荷兰拍卖代码，讲解如何通过`荷兰拍卖`发售`ERC721`标准的`NFT`。

## 荷兰拍卖

荷兰拍卖（`Dutch Auction`）是一种特殊的拍卖形式。 亦称“减价拍卖”，它是指拍卖标的的竞价由高到低依次递减直到第一个竞买人应价（达到或超过底价）时击槌成交的一种拍卖。



![荷兰拍卖](https://www.wtf.academy/assets/images/35-1-1658a69be3510565054fd7d243229f2f.png)



在币圈，很多`NFT`通过荷兰拍卖发售，其中包括`Azuki`和`World of Women`，其中`Azuki`通过荷兰拍卖筹集了超过`8000`枚`ETH`。

项目方非常喜欢这种拍卖形式，主要有两个原因

1. 荷兰拍卖的价格由最高慢慢下降，能让项目方获得最大的收入。
2. 拍卖持续较长时间（通常6小时以上），可以避免`gas war`。

## `DutchAuction`合约

代码基于`Azuki`的[代码](https://etherscan.io/address/0xed5af388653567af2f388e6224dc7c4b3241c544#code)简化而成。`DucthAuction`合约继承了之前介绍的`ERC721`和`Ownable`合约：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.21;

import "@openzeppelin/contracts/access/Ownable.sol";
import "https://github.com/AmazingAng/WTF-Solidity/blob/main/34_ERC721/ERC721.sol";

contract DutchAuction is Ownable, ERC721 {
```



### `DutchAuction`状态变量

合约中一共有`9`个状态变量，其中有`6`个和拍卖相关，他们是：

- `COLLECTOIN_SIZE`：NFT总量。
- `AUCTION_START_PRICE`：荷兰拍卖起拍价，也是最高价。
- `AUCTION_END_PRICE`：荷兰拍卖结束价，也是最低价/地板价。
- `AUCTION_TIME`：拍卖持续时长。
- `AUCTION_DROP_INTERVAL`：每过多久时间，价格衰减一次。
- `auctionStartTime`：拍卖起始时间（区块链时间戳，`block.timestamp`）。

```solidity
    uint256 public constant COLLECTOIN_SIZE = 10000; // NFT总数
    uint256 public constant AUCTION_START_PRICE = 1 ether; // 起拍价(最高价)
    uint256 public constant AUCTION_END_PRICE = 0.1 ether; // 结束价(最低价/地板价)
    uint256 public constant AUCTION_TIME = 10 minutes; // 拍卖时间，为了测试方便设为10分钟
    uint256 public constant AUCTION_DROP_INTERVAL = 1 minutes; // 每过多久时间，价格衰减一次
    uint256 public constant AUCTION_DROP_PER_STEP =
        (AUCTION_START_PRICE - AUCTION_END_PRICE) /
        (AUCTION_TIME / AUCTION_DROP_INTERVAL); // 每次价格衰减步长
    
    uint256 public auctionStartTime; // 拍卖开始时间戳
    string private _baseTokenURI;   // metadata URI
    uint256[] private _allTokens; // 记录所有存在的tokenId 
```



### `DutchAuction`函数

荷兰拍卖合约中共有`9`个函数，与`ERC721`相关的函数我们这里不再重复介绍，只介绍和拍卖相关的函数。

- 设定拍卖起始时间：我们在构造函数中会声明当前区块时间为起始时间，项目方也可以通过`setAuctionStartTime()`函数来调整：

```solidity
    constructor() ERC721("WTF Dutch Auctoin", "WTF Dutch Auctoin")
    //这里用到了构造器函数的继承
    {
        auctionStartTime = block.timestamp;
    }

    // auctionStartTime setter函数，onlyOwner
    function setAuctionStartTime(uint32 timestamp) external onlyOwner {
        auctionStartTime = timestamp;
    }
```



- 获取拍卖实时价格：`getAuctionPrice()`函数通过当前区块时间以及拍卖相关的状态变量来计算实时拍卖价格。

当`block.timestamp`小于起始时间，价格为最高价`AUCTION_START_PRICE`；

当`block.timestamp`大于结束时间，价格为最低价`AUCTION_END_PRICE`；

当`block.timestamp`处于两者之间时，则计算出当前的衰减价格。

```solidity
    // 获取拍卖实时价格
    function getAuctionPrice()
        public
        view
        returns (uint256)
    {
        if (block.timestamp < auctionStartTime) {
        return AUCTION_START_PRICE;
        }else if (block.timestamp - auctionStartTime >= AUCTION_TIME) {
        return AUCTION_END_PRICE;
        } else {
        uint256 steps = (block.timestamp - auctionStartTime) /
            AUCTION_DROP_INTERVAL;
        return AUCTION_START_PRICE - (steps * AUCTION_DROP_PER_STEP);
        }
    }
```



- 用户拍卖并铸造`NFT`：用户通过调用`auctionMint()`函数，支付`ETH`参加荷兰拍卖并铸造`NFT`。

该函数首先检查拍卖是否开始/铸造是否超出`NFT`总量。接着，合约通过`getAuctionPrice()`和铸造数量计算拍卖成本，并检查用户支付的`ETH`是否足够：如果足够，则将`NFT`铸造给用户，并退回超额的`ETH`；反之，则回退交易。

```solidity
    // 拍卖mint函数
    function auctionMint(uint256 quantity) external payable{
        uint256 _saleStartTime = uint256(auctionStartTime); // 建立local变量，减少gas花费
        require(
        _saleStartTime != 0 && block.timestamp >= _saleStartTime,
        "sale has not started yet"
        ); // 检查是否设置起拍时间，拍卖是否开始
        require(
        totalSupply() + quantity <= COLLECTOIN_SIZE,
        "not enough remaining reserved for auction to support desired mint amount"
        ); // 检查是否超过NFT上限

        uint256 totalCost = getAuctionPrice() * quantity; // 计算mint成本
        require(msg.value >= totalCost, "Need to send more ETH."); // 检查用户是否支付足够ETH
        
        // Mint NFT
        for(uint256 i = 0; i < quantity; i++) {
            uint256 mintIndex = totalSupply();
            _mint(msg.sender, mintIndex);
            _addTokenToAllTokensEnumeration(mintIndex);
        }
        // 多余ETH退款
        if (msg.value > totalCost) {
            payable(msg.sender).transfer(msg.value - totalCost); //注意一下这里是否有重入的风险
        }
    }
```

注意：在 Solidity 中，`payable` 修饰符用于指定某个地址可以接收 ETH。`msg.sender` 是当前调用合约的人，默认情况下，它是一个非 `payable` 地址。要向某个地址发送 ETH，必须确保这个地址是 `payable` 的。因此，`payable(msg.sender)` 表示将 `msg.sender` 转换为可以接收 ETH 的 `payable` 地址。

这里的 `transfer` 机制并不会产生重入攻击的风险，因为 `transfer` 方法只允许发送 2300 gas，这个 gas 数量不足以执行任何复杂的逻辑操作（包括调用其他合约）。因此，使用 `transfer` 相对安全，它不会让目标合约再次调用外部函数，防止了可能的重入攻击。



- 项目方取出筹集的`ETH`：项目方可以通过`withdrawMoney()`函数提走拍卖筹集的`ETH`。

```solidity
    // 提款函数，onlyOwner
    function withdrawMoney() external onlyOwner {
        (bool success, ) = msg.sender.call{value: address(this).balance}(""); // call函数的调用方式详见第22讲
        require(success, "Transfer failed.");
    }
```



## Remix演示

1. 合约部署：首先，部署`DutchAuction.sol`合约，并通过`setAuctionStartTime()`函数设置拍卖起始时间。 本例采用的起始时间为，2022年7月12日 1点30分，对应的utc时间为1658338200。实验时可以在工具网站（[比如这里](https://tool.chinaz.com/tools/unixtime.aspx)）自行查询对应时间。

   ![设置拍卖起始时间](https://www.wtf.academy/assets/images/35-2-c154b3ef7c1fc34372652adc743452b2.png)

   

2. 荷兰拍卖：随后，可以通过`getAuctionPrice()`函数获取到**当前**的拍卖价格。可以观察到，拍卖开始前的价格为`起拍价 AUCTION_START_PRICE`随着拍卖进行，拍卖价格在逐渐降低，直到降低至`地板价 AUCTION_END_PRICE`后不再变化。

   ![荷兰拍卖价格变化](https://www.wtf.academy/assets/images/35-3-3e750008c5f4e18236904e2fee191b90.png)

   

3. Mint操作：通过`auctionMint()`函数，完成mint，可以看见本例中，由于时间已经超过拍卖时间，因此仅耗费了`地板价`就完成了拍卖。

   ![完成荷兰拍卖](https://www.wtf.academy/assets/images/35-4-552388607fa261a1c0079634c501b5cd.png)

   

4. 提取`ETH`：直接通过`withdrawMoney()`函数，便能将筹集到的`ETH`通过`call()`发送到合约创建者的地址。

## 总结

这一讲，我们介绍了荷兰拍卖，并通过简化版`Azuki`荷兰拍卖代码，讲解如何通过`荷兰拍卖`发售`ERC721`标准的`NFT`。我拍卖到的最贵的`NFT`是音乐家`Jonathan Mann`的一首音乐`NFT`，你呢？

# 36. 默克尔树 Merkle Tree

这一讲，我将介绍`Merkle Tree`，以及如何利用`Merkle Tree`发放`NFT`白名单。

## `Merkle Tree`

`Merkle Tree`，也叫默克尔树或哈希树，是区块链的底层加密技术，被比特币和以太坊区块链广泛采用。`Merkle Tree`是一种自下而上构建的加密树，每个叶子是对应数据的哈希，而每个非叶子为它的`2`个子节点的哈希。



![Merkle Tree](https://www.wtf.academy/assets/images/36-1-de3d45c6960388feaf2f8c42ff317983.png)



`Merkle Tree`允许对大型数据结构的内容进行有效和安全的验证（`Merkle Proof`）。对于有`N`个叶子结点的`Merkle Tree`，在已知`root`根值的情况下，验证某个数据是否有效（属于`Merkle Tree`叶子结点）只需要`ceil(log₂N)`个数据（也叫`proof`），非常高效。如果数据有误，或者给的`proof`错误，则无法还原出`root`根植。 下面的例子中，叶子`L1`的`Merkle proof`为`Hash 0-1`和`Hash 1`：知道这两个值，就能验证`L1`的值是不是在`Merkle Tree`的叶子中。为什么呢？ 因为通过叶子`L1`我们就可以算出`Hash 0-0`，我们又知道了`Hash 0-1`，那么`Hash 0-0`和`Hash 0-1`就可以联合算出`Hash 0`，然后我们又知道`Hash 1`，`Hash 0`和`Hash 1`就可以联合算出`Top Hash`，也就是root节点的hash。



![Merkle Proof](https://www.wtf.academy/assets/images/36-2-b2f55f8729ae75168f71115099e8dffb.png)



## 生成`Merkle Tree`

我们可以利用[网页](https://lab.miguelmota.com/merkletreejs/example/)或者Javascript库[merkletreejs](https://github.com/miguelmota/merkletreejs)来生成`Merkle Tree`。

这里我们用网页来生成`4`个地址作为叶子结点的`Merkle Tree`。叶子结点输入：

```solidity
    [
    "0x5B38Da6a701c568545dCfcB03FcB875f56beddC4", 
    "0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2",
    "0x4B20993Bc481177ec7E8f571ceCaE8A9e22C02db",
    "0x78731D3Ca6b7E34aC0F824c42a7cC18A495cabaB"
    ]
```



在菜单里选上`Keccak-256`, `hashLeaves`和`sortPairs`选项，然后点击`Compute`，`Merkle Tree`就生成好了。`Merkle Tree`展开为：

```text
└─ 根: eeefd63003e0e702cb41cd0043015a6e26ddb38073cc6ffeb0ba3e808ba8c097
   ├─ 9d997719c0a5b5f6db9b8ac69a988be57cf324cb9fffd51dc2c37544bb520d65
   │  ├─ 叶子0：5931b4ed56ace4c46b68524cb5bcbf4195f1bbaacbe5228fbd090546c88dd229
   │  └─ 叶子1：999bf57501565dbd2fdcea36efa2b9aef8340a8901e3459f4a4c926275d36cdb
   └─ 4726e4102af77216b09ccd94f40daa10531c87c4d60bba7f3b3faf5ff9f19b3c
      ├─ 叶子2：04a10bfd00977f54cc3450c9b25c9b3a502a089eba0097ba35fc33c4ea5fcb54
      └─ 叶子3：dfbe3e504ac4e35541bebad4d0e7574668e16fefa26cd4172f93e18b59ce9486
```





![生成Merkle Tree](https://www.wtf.academy/assets/images/36-3-103c247bca0ed9063cf8d27e06f0530f.png)



## `Merkle Proof`验证

通过网站，我们可以得到`地址0`的`proof`如下，即图2中蓝色结点的哈希值：

```solidity
[
  "0x999bf57501565dbd2fdcea36efa2b9aef8340a8901e3459f4a4c926275d36cdb",
  "0x4726e4102af77216b09ccd94f40daa10531c87c4d60bba7f3b3faf5ff9f19b3c"
]
```





![Merkle Proof](https://www.wtf.academy/assets/images/36-4-d031f8985acdcbfc35b9910f04c81541.png)



我们利用`MerkleProof`库来验证：

```solidity
library MerkleProof {
    /**
     * @dev 当通过`proof`和`leaf`重建出的`root`与给定的`root`相等时，返回`true`，数据有效。
     * 在重建时，叶子节点对和元素对都是排序过的。
     */
    function verify(
        bytes32[] memory proof,
        bytes32 root,
        bytes32 leaf
    ) internal pure returns (bool) {
        return processProof(proof, leaf) == root;
    }

    /**
     * @dev Returns 通过Merkle树用`leaf`和`proof`计算出`root`. 当重建出的`root`和给定的`root`相同时，`proof`才是有效的。
     * 在重建时，叶子节点对和元素对都是排序过的。
     */
    function processProof(bytes32[] memory proof, bytes32 leaf) internal pure returns (bytes32) {
        bytes32 computedHash = leaf;
        for (uint256 i = 0; i < proof.length; i++) {
            computedHash = _hashPair(computedHash, proof[i]);
        }
        return computedHash;
    }

    // Sorted Pair Hash
    function _hashPair(bytes32 a, bytes32 b) private pure returns (bytes32) {
        return a < b ? keccak256(abi.encodePacked(a, b)) : keccak256(abi.encodePacked(b, a));
    }
}
```



`MerkleProof`库有三个函数：

1. `verify()`函数：利用`proof`数来验证`leaf`是否属于根为`root`的`Merkle Tree`中，如果是，则返回`true`。它调用了`processProof()`函数。
2. `processProof()`函数：利用`proof`和`leaf`依次计算出`Merkle Tree`的`root`。它调用了`_hashPair()`函数。
3. `_hashPair()`函数：用`keccak256()`函数计算非根节点对应的两个子节点的哈希（排序后）。

我们将`地址0`的`Hash`，`root`和对应的`proof`输入到`verify()`函数，将返回`true`。因为`地址0`的`Hash`在根为`root`的`Merkle Tree`中，且`proof`正确。如果改变了其中任意一个值，都将返回`false`。

## 利用`Merkle Tree`发放`NFT`白名单

一份拥有800个地址的白名单，更新一次所需的gas fee很容易超过1个ETH。而由于`Merkle Tree`验证时，`leaf`和`proof`可以存在后端，链上仅需存储一个`root`的值，非常节省`gas`，项目方经常用它来发放白名单。很多`ERC721`标准的`NFT`和`ERC20`标准代币的白名单/空投都是利用`Merkle Tree`发出的，比如`optimism`的空投。

这里，我们介绍如何利用`MerkleTree`合约来发放`NFT`白名单：

```solidity
contract MerkleTree is ERC721 {
    bytes32 immutable public root; // Merkle树的根
    mapping(address => bool) public mintedAddress;   // 记录已经mint的地址

    // 构造函数，初始化NFT合集的名称、代号、Merkle树的根
    constructor(string memory name, string memory symbol, bytes32 merkleroot)
    ERC721(name, symbol)
    {
        root = merkleroot;
    }

    // 利用Merkle树验证地址并完成mint
    function mint(address account, uint256 tokenId, bytes32[] calldata proof)
    external
    {
        require(_verify(_leaf(account), proof), "Invalid merkle proof"); // Merkle检验通过
        require(!mintedAddress[account], "Already minted!"); // 地址没有mint过
        _mint(account, tokenId); // mint
        mintedAddress[account] = true; // 记录mint过的地址
    }

    // 计算Merkle树叶子的哈希值
    function _leaf(address account)
    internal pure returns (bytes32)
    {
        return keccak256(abi.encodePacked(account));
    }

    // Merkle树验证，调用MerkleProof库的verify()函数
    function _verify(bytes32 leaf, bytes32[] memory proof)
    internal view returns (bool)
    {
        return MerkleProof.verify(proof, root, leaf);
    }
}
```



`MerkleTree`合约继承了`ERC721`标准，并利用了`MerkleProof`库。

### 状态变量

合约中共有两个状态变量：

- `root`存储了`Merkle Tree`的根，部署合约的时候赋值。
- `mintedAddress`是一个`mapping`，记录了已经`mint`过的地址，某地址mint成功后进行赋值。

### 函数

合约中共有4个函数：

- 构造函数：初始化`NFT`的名称和代号，还有`Merkle Tree`的`root`。
- `mint()`函数：利用白名单铸造`NFT`。参数为白名单地址`account`，铸造的`tokenId`，和`proof`。首先验证`address`是否在白名单中，验证通过则把序号为`tokenId`的`NFT`铸造给该地址，并将它记录到`mintedAddress`。此过程中调用了`_leaf()`和`_verify()`函数。
- `_leaf()`函数：计算了`Merkle Tree`的叶子地址的哈希。
- `_verify()`函数：调用了`MerkleProof`库的`verify()`函数，进行`Merkle Tree`验证。

### `remix`验证

我们使用上面例子的`4`个地址作为白名单并生成`Merkle Tree`。我们部署`MerkleTree`合约，`3`个参数分别为：

```solidity
name = "WTF MerkleTree"
symbol = "WTF"
merkleroot = 0xeeefd63003e0e702cb41cd0043015a6e26ddb38073cc6ffeb0ba3e808ba8c097
```





![部署MerkleTree合约](https://www.wtf.academy/assets/images/36-5-96aad8485660da6f8ca1f3633c12d8d9.png)



接下来运行`mint`函数给地址0铸造`NFT`，`3`个参数分别为：

```solidity
account = 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4
tokenId = 0
proof = [   "0x999bf57501565dbd2fdcea36efa2b9aef8340a8901e3459f4a4c926275d36cdb",   "0x4726e4102af77216b09ccd94f40daa10531c87c4d60bba7f3b3faf5ff9f19b3c" ]
```





![白名单mint](https://www.wtf.academy/assets/images/36-6-685e7423e08f4affd1cb0e307eb7360b.png)



我们可以用`ownerOf`函数验证`tokenId`为0的`NFT`已经铸造给了地址0，合约运行成功！



![tokenId为0的持有者改变，合约运行成功！](https://www.wtf.academy/assets/images/36-7-4896604f09eb9f0dc1daf16c0b615d94.png)



此时，若再次调用mint函数，虽然该地址能够通过`Merkle Proof`验证，但由于地址已经记录在`mintedAddress`中，因此该交易会由于`"Already minted!"`被中止。

## 总结

这一讲，我们介绍了`Merkle Tree`的概念，如何生成简单的`Merkle Tree`，如何利用智能合约验证`Merkle Tree`，以及用它来发放`NFT`白名单。

在实际使用中，复杂的`Merkle Tree`可以利用`javascript`库`merkletreejs`来生成和管理，链上只需要存储一个根值，非常节省`gas`。很多项目方都选择利用`Merkle Tree`来发放白名单。

# 37. 数字签名 Signature

这一讲，我们将简单的介绍以太坊中的数字签名`ECDSA`，以及如何利用它发放`NFT`白名单。代码中的`ECDSA`库由`OpenZeppelin`的同名库简化而成。

## 数字签名

如果你用过`opensea`交易`NFT`，对签名就不会陌生。下图是小狐狸（`metamask`）钱包进行签名时弹出的窗口，它可以证明你拥有私钥的同时不需要对外公布私钥。



![metamask签名](https://www.wtf.academy/assets/images/37-1-6c4059d562d3a3c6eeb7a39bf69dceef.png)



以太坊使用的数字签名算法叫双椭圆曲线数字签名算法（`ECDSA`），基于双椭圆曲线“私钥-公钥”对的数字签名算法。它主要起到了[三个作用](https://en.wikipedia.org/wiki/Digital_signature)：

1. **身份认证**：证明签名方是私钥的持有人。
2. **不可否认**：发送方不能否认发送过这个消息。
3. **完整性**：通过验证针对传输消息生成的数字签名，可以验证消息是否在传输过程中被篡改。

## `ECDSA`合约

`ECDSA`标准中包含两个部分：

1. 签名者利用`私钥`（隐私的）对`消息`（公开的）创建`签名`（公开的）。
2. 其他人使用`消息`（公开的）和`签名`（公开的）恢复签名者的`公钥`（公开的）并验证签名。 我们将配合`ECDSA`库讲解这两个部分。本教程所用的`私钥`，`公钥`，`消息`，`以太坊签名消息`，`签名`如下所示：

```text
私钥: 0x227dbb8586117d55284e26620bc76534dfbd2394be34cf4a09cb775d593b6f2b
公钥: 0xe16C1623c1AA7D919cd2241d8b36d9E79C1Be2A2
消息: 0x1bf2c0ce4546651a1a2feb457b39d891a6b83931cc2454434f39961345ac378c
以太坊签名消息: 0xb42ca4636f721c7a331923e764587e98ec577cea1a185f60dfcc14dbb9bd900b
签名: 0x390d704d7ab732ce034203599ee93dd5d3cb0d4d1d7c600ac11726659489773d559b12d220f99f41d17651b0c1c6a669d346a397f8541760d6b32a5725378b241c
```



### 创建签名

**1. 打包消息：** 在以太坊的`ECDSA`标准中，被签名的`消息`是一组数据的`keccak256`哈希，为`bytes32`类型。我们可以把任何想要签名的内容利用`abi.encodePacked()`函数打包，然后用`keccak256()`计算哈希，作为`消息`。我们例子中的`消息`是由一个`address`类型变量和一个`uint256`类型变量得到的：

```solidity
    /*
     * 将mint地址（address类型）和tokenId（uint256类型）拼成消息msgHash
     * _account: 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4
     * _tokenId: 0
     * 对应的消息msgHash: 0x1bf2c0ce4546651a1a2feb457b39d891a6b83931cc2454434f39961345ac378c
     */
    function getMessageHash(address _account, uint256 _tokenId) public pure returns(bytes32){
        return keccak256(abi.encodePacked(_account, _tokenId));
    }
```





![打包消息](https://www.wtf.academy/assets/images/37-2-ad582ef23fdf87fc8c17b39211b68ec2.png)



**2. 计算以太坊签名消息：** `消息`可以是能被执行的交易，也可以是其他任何形式。为了避免用户误签了恶意交易，`EIP191`提倡在`消息`前加上`"\x19Ethereum Signed Message:\n32"`字符，并再做一次`keccak256`哈希，作为`以太坊签名消息`。经过`toEthSignedMessageHash()`函数处理后的消息，不能被用于执行交易:

```solidity
    /**
     * @dev 返回 以太坊签名消息
     * `hash`：消息
     * 遵从以太坊签名标准：https://eth.wiki/json-rpc/API#eth_sign[`eth_sign`]
     * 以及`EIP191`:https://eips.ethereum.org/EIPS/eip-191`
     * 添加"\x19Ethereum Signed Message:\n32"字段，防止签名的是可执行交易。
     */
    function toEthSignedMessageHash(bytes32 hash) public pure returns (bytes32) {
        // 哈希的长度为32
        return keccak256(abi.encodePacked("\x19Ethereum Signed Message:\n32", hash));
    }
```



处理后的消息为：

```text
以太坊签名消息: 0xb42ca4636f721c7a331923e764587e98ec577cea1a185f60dfcc14dbb9bd900b
```





![以太坊签名消息](https://www.wtf.academy/assets/images/37-3-9dbf5bf835d2ac90e0965ddfcc85258a.png)



**3-1. 利用钱包签名：** 日常操作中，大部分用户都是通过这种方式进行签名。在获取到需要签名的消息之后，我们需要使用`metamask`钱包进行签名。`metamask`的`personal_sign`方法会自动把`消息`转换为`以太坊签名消息`，然后发起签名。所以我们只需要输入`消息`和`签名者钱包account`即可。需要注意的是输入的`签名者钱包account`需要和`metamask`当前连接的account一致才能使用。

因此首先把例子中的`私钥`导入到小狐狸钱包，然后打开浏览器的`console`页面：`Chrome菜单-更多工具-开发者工具-Console`。在连接钱包的状态下（如连接opensea，否则会出现错误），依次输入以下指令进行签名：

```text
ethereum.enable()
account = "0xe16C1623c1AA7D919cd2241d8b36d9E79C1Be2A2"
hash = "0x1bf2c0ce4546651a1a2feb457b39d891a6b83931cc2454434f39961345ac378c"
ethereum.request({method: "personal_sign", params: [account, hash]})
```



在返回的结果中（`Promise`的`PromiseResult`）可以看到创建好的签名。不同账户有不同的私钥，创建的签名值也不同。利用教程的私钥创建的签名如下所示：

```text
0x390d704d7ab732ce034203599ee93dd5d3cb0d4d1d7c600ac11726659489773d559b12d220f99f41d17651b0c1c6a669d346a397f8541760d6b32a5725378b241c
```





![浏览器console调用metamask进行签名](https://www.wtf.academy/assets/images/37-4-8709417544253a96137df6e8c151a15d.jpg)



**3-2. 利用web3.py签名：** 批量调用中更倾向于使用代码进行签名，以下是基于web3.py的实现。

```py
from web3 import Web3, HTTPProvider
from eth_account.messages import encode_defunct

private_key = "0x227dbb8586117d55284e26620bc76534dfbd2394be34cf4a09cb775d593b6f2b"
address = "0x5B38Da6a701c568545dCfcB03FcB875f56beddC4"
rpc = 'https://rpc.ankr.com/eth'
w3 = Web3(HTTPProvider(rpc))

#打包信息
msg = Web3.solidity_keccak(['address','uint256'], [address,0])
print(f"消息：{msg.hex()}")
#构造可签名信息
message = encode_defunct(hexstr=msg.hex())
#签名
signed_message = w3.eth.account.sign_message(message, private_key=private_key)
print(f"签名：{signed_message['signature'].hex()}")
```



运行的结果如下所示。计算得到的消息，签名和前面的案例一致。

```text
消息：0x1bf2c0ce4546651a1a2feb457b39d891a6b83931cc2454434f39961345ac378c
签名：0x390d704d7ab732ce034203599ee93dd5d3cb0d4d1d7c600ac11726659489773d559b12d220f99f41d17651b0c1c6a669d346a397f8541760d6b32a5725378b241c
```



### 验证签名

为了验证签名，验证者需要拥有`消息`，`签名`，和签名使用的`公钥`。我们能验证签名的原因是只有`私钥`的持有者才能够针对交易生成这样的签名，而别人不能。

**4. 通过签名和消息恢复公钥：**`签名`是由数学算法生成的。这里我们使用的是`rsv签名`，`签名`中包含`r, s, v`三个值的信息。而后，我们可以通过`r, s, v`及`以太坊签名消息`来求得`公钥`。下面的`recoverSigner()`函数实现了上述步骤，它利用`以太坊签名消息 _msgHash`和`签名 _signature`恢复`公钥`（使用了简单的内联汇编）：

```solidity
    // @dev 从_msgHash和签名_signature中恢复signer地址
    function recoverSigner(bytes32 _msgHash, bytes memory _signature) internal pure returns (address){
        // 检查签名长度，65是标准r,s,v签名的长度
        require(_signature.length == 65, "invalid signature length");
        bytes32 r;
        bytes32 s;
        uint8 v;
        // 目前只能用assembly (内联汇编)来从签名中获得r,s,v的值
        assembly {
            /*
            前32 bytes存储签名的长度 (动态数组存储规则)
            add(sig, 32) = sig的指针 + 32
            等效为略过signature的前32 bytes
            mload(p) 载入从内存地址p起始的接下来32 bytes数据
            */
            // 读取长度数据后的32 bytes
            r := mload(add(_signature, 0x20))
            // 读取之后的32 bytes
            s := mload(add(_signature, 0x40))
            // 读取最后一个byte
            v := byte(0, mload(add(_signature, 0x60)))
        }
        // 使用ecrecover(全局函数)：利用 msgHash 和 r,s,v 恢复 signer 地址
        return ecrecover(_msgHash, v, r, s);
    }
```



参数分别为：

```text
_msgHash：0xb42ca4636f721c7a331923e764587e98ec577cea1a185f60dfcc14dbb9bd900b
_signature：0x390d704d7ab732ce034203599ee93dd5d3cb0d4d1d7c600ac11726659489773d559b12d220f99f41d17651b0c1c6a669d346a397f8541760d6b32a5725378b241c
```





![通过签名和消息恢复公钥](https://www.wtf.academy/assets/images/37-8-50f993208c23bea33eacd5ed18de69ff.png)



**5. 对比公钥并验证签名：** 接下来，我们只需要比对恢复的`公钥`与签名者公钥`_signer`是否相等：若相等，则签名有效；否则，签名无效：

```solidity
    /**
     * @dev 通过ECDSA，验证签名地址是否正确，如果正确则返回true
     * _msgHash为消息的hash
     * _signature为签名
     * _signer为签名地址
     */
    function verify(bytes32 _msgHash, bytes memory _signature, address _signer) internal pure returns (bool) {
        return recoverSigner(_msgHash, _signature) == _signer;
    }
```



参数分别为：

```text
_msgHash：0xb42ca4636f721c7a331923e764587e98ec577cea1a185f60dfcc14dbb9bd900b
_signature：0x390d704d7ab732ce034203599ee93dd5d3cb0d4d1d7c600ac11726659489773d559b12d220f99f41d17651b0c1c6a669d346a397f8541760d6b32a5725378b241c
_signer：0xe16C1623c1AA7D919cd2241d8b36d9E79C1Be2A2
```





![对比公钥并验证签名：](https://www.wtf.academy/assets/images/37-9-2e2029b1978cafb7cd211511f2769082.png)



## 利用签名发放白名单

`NFT`项目方可以利用`ECDSA`的这个特性发放白名单。由于签名是链下的，不需要`gas`，因此这种白名单发放模式比`Merkle Tree`模式还要经济。方法非常简单，项目方利用项目方账户把白名单发放地址签名（可以加上地址可以铸造的`tokenId`）。然后`mint`的时候利用`ECDSA`检验签名是否有效，如果有效，则给他`mint`。

`SignatureNFT`合约实现了利用签名发放`NFT`白名单。

### 状态变量

合约中共有两个状态变量：

- `signer`：`公钥`，项目方签名地址。
- `mintedAddress`是一个`mapping`，记录了已经`mint`过的地址。

### 函数

合约中共有4个函数：

- 构造函数初始化`NFT`的名称和代号，还有`ECDSA`的签名地址`signer`。
- `mint()`函数接受地址`address`，`tokenId`和`_signature`三个参数，验证签名是否有效：如果有效，则把`tokenId`的`NFT`铸造给`address`地址，并将它记录到`mintedAddress`。它调用了`getMessageHash()`，`ECDSA.toEthSignedMessageHash()`和`verify()`函数。
- `getMessageHash()`函数将`mint`地址（`address`类型）和`tokenId`（`uint256`类型）拼成`消息`。
- `verify()`函数调用了`ECDSA`库的`verify()`函数，来进行`ECDSA`签名验证。

```solidity
contract SignatureNFT is ERC721 {
    address immutable public signer; // 签名地址
    mapping(address => bool) public mintedAddress;   // 记录已经mint的地址

    // 构造函数，初始化NFT合集的名称、代号、签名地址
    constructor(string memory _name, string memory _symbol, address _signer)
    ERC721(_name, _symbol)
    {
        signer = _signer;
    }

    // 利用ECDSA验证签名并mint
    function mint(address _account, uint256 _tokenId, bytes memory _signature)
    external
    {
        bytes32 _msgHash = getMessageHash(_account, _tokenId); // 将_account和_tokenId打包消息
        bytes32 _ethSignedMessageHash = ECDSA.toEthSignedMessageHash(_msgHash); // 计算以太坊签名消息
        require(verify(_ethSignedMessageHash, _signature), "Invalid signature"); // ECDSA检验通过
        require(!mintedAddress[_account], "Already minted!"); // 地址没有mint过
        _mint(_account, _tokenId); // mint
        mintedAddress[_account] = true; // 记录mint过的地址
    }

    /*
     * 将mint地址（address类型）和tokenId（uint256类型）拼成消息msgHash
     * _account: 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4
     * _tokenId: 0
     * 对应的消息: 0x1bf2c0ce4546651a1a2feb457b39d891a6b83931cc2454434f39961345ac378c
     */
    function getMessageHash(address _account, uint256 _tokenId) public pure returns(bytes32){
        return keccak256(abi.encodePacked(_account, _tokenId));
    }

    // ECDSA验证，调用ECDSA库的verify()函数
    function verify(bytes32 _msgHash, bytes memory _signature)
    public view returns (bool)
    {
        return ECDSA.verify(_msgHash, _signature, signer);
    }
}
```



### `remix`验证

- 链下通过以太坊签名获得`signature`，给`_account`地址发放`tokenId = 0`的白名单。所用的数据见<`ECDSA`合约>章节。
- 部署`SignatureNFT`合约，参数分别为：

```text
_name: WTF Signature
_symbol: WTF
_signer: 0xe16C1623c1AA7D919cd2241d8b36d9E79C1Be2A2
```





![部署SignatureNFT合约](https://www.wtf.academy/assets/images/37-5-c3dc2c97ace2988a9942cab7fca07d81.png)



- 调用`mint()`函数利用`ECDSA`验证签名并铸造，参数为：

```text
_account: 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4
_tokenId: 0
_signature: 0x390d704d7ab732ce034203599ee93dd5d3cb0d4d1d7c600ac11726659489773d559b12d220f99f41d17651b0c1c6a669d346a397f8541760d6b32a5725378b241c
```





![部署SignatureNFT合约](https://www.wtf.academy/assets/images/37-6-55ee1bf172ca54ea2ed81a512e0ae173.png)



- 调用`ownerOf()`函数，可以看到`tokenId = 0`成功铸造给了地址`_account`，合约运行成功！



![tokenId为0的持有者改变，合约运行成功！](https://www.wtf.academy/assets/images/37-7-954607676e300e7dab2b0d5c57ee3365.png)



## 总结

这一讲，我们介绍了以太坊中的数字签名`ECDSA`，如何利用`ECDSA`创建和验证签名，还有`ECDSA`合约，以及如何利用它发放`NFT`白名单。代码中的`ECDSA`库由`OpenZeppelin`的[同名库](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/cryptography/ECDSA.sol)简化而成。

- 由于签名是链下的，不需要`gas`，因此这种白名单发放模式比`Merkle Tree`模式还要经济；
- 但由于用户要请求中心化接口去获取签名，不可避免的牺牲了一部分去中心化；
- 额外还有一个好处是白名单可以动态变化，而不是提前写死在合约里面了，因为项目方的中心化后端接口可以接受任何新地址的请求并给予白名单签名。

# 38. NFT交易所

`Opensea`是以太坊上最大的`NFT`交易平台，总交易总量达到了`$300亿`。`Opensea`在交易中抽成`2.5%`，因此它通过用户交易至少获利了`$7.5亿`。另外，它的运作并不去中心化，且不准备发币补偿用户。`NFT`玩家苦`Opensea`久已，今天我们就利用智能合约搭建一个零手续费的去中心化`NFT`交易所：`NFTSwap`。

## 设计逻辑

- 卖家：出售`NFT`的一方，可以挂单`list`、撤单`revoke`、修改价格`update`。
- 买家：购买`NFT`的一方，可以购买`purchase`。
- 订单：卖家发布的`NFT`链上订单，一个系列的同一`tokenId`最多存在一个订单，其中包含挂单价格`price`和持有人`owner`信息。当一个订单交易完成或被撤单后，其中信息清零。

## `NFTSwap`合约

### 事件

合约包含`4`个事件，对应挂单`list`、撤单`revoke`、修改价格`update`、购买`purchase`这四个行为：

```solidity
    event List(address indexed seller, address indexed nftAddr, uint256 indexed tokenId, uint256 price);
    event Purchase(address indexed buyer, address indexed nftAddr, uint256 indexed tokenId, uint256 price);
    event Revoke(address indexed seller, address indexed nftAddr, uint256 indexed tokenId);    
    event Update(address indexed seller, address indexed nftAddr, uint256 indexed tokenId, uint256 newPrice);
```



### 订单

`NFT`订单抽象为`Order`结构体，包含挂单价格`price`和持有人`owner`信息。`nftList`映射记录了订单是对应的`NFT`系列（合约地址）和`tokenId`信息。

```solidity
    // 定义order结构体
    struct Order{
        address owner;
        uint256 price; 
    }
    // NFT Order映射
    mapping(address => mapping(uint256 => Order)) public nftList;
```



### 回退函数

在`NFTSwap`中，用户使用`ETH`购买`NFT`。因此，合约需要实现`fallback()`函数来接收`ETH`。

```solidity
    fallback() external payable{}
```



### onERC721Received

`ERC721`的安全转账函数会检查接收合约是否实现了`onERC721Received()`函数，并返回正确的选择器`selector`。用户下单之后，需要将`NFT`发送给`NFTSwap`合约。因此`NFTSwap`继承`IERC721Receiver`接口，并实现`onERC721Received()`函数：

```solidity
contract NFTSwap is IERC721Receiver{

    // 实现{IERC721Receiver}的onERC721Received，能够接收ERC721代币
    function onERC721Received(
        address operator,
        address from,
        uint tokenId,
        bytes calldata data
    ) external override returns (bytes4){
        return IERC721Receiver.onERC721Received.selector;
    }
```



### 交易

合约实现了`4`个交易相关的函数：

- 挂单`list()`：卖家创建`NFT`并创建订单，并释放`List`事件。参数为`NFT`合约地址`_nftAddr`，`NFT`对应的`_tokenId`，挂单价格`_price`（**注意：单位是`wei`**）。成功后，`NFT`会从卖家转到`NFTSwap`合约中。

```solidity
    // 挂单: 卖家上架NFT，合约地址为_nftAddr，tokenId为_tokenId，价格_price为以太坊（单位是wei）
    function list(address _nftAddr, uint256 _tokenId, uint256 _price) public{
        IERC721 _nft = IERC721(_nftAddr); // 声明IERC721接口合约变量
        require(_nft.getApproved(_tokenId) == address(this), "Need Approval"); // 合约得到授权
        require(_price > 0); // 价格大于0

        Order storage _order = nftList[_nftAddr][_tokenId]; //设置NF持有人和价格
        _order.owner = msg.sender;
        _order.price = _price;
        // 将NFT转账到合约
        _nft.safeTransferFrom(msg.sender, address(this), _tokenId);

        // 释放List事件
        emit List(msg.sender, _nftAddr, _tokenId, _price);
    }
```



- 撤单`revoke()`：卖家撤回挂单，并释放`Revoke`事件。参数为`NFT`合约地址`_nftAddr`，`NFT`对应的`_tokenId`。成功后，`NFT`会从`NFTSwap`合约转回卖家。

```solidity
    // 撤单： 卖家取消挂单
    function revoke(address _nftAddr, uint256 _tokenId) public {
        Order storage _order = nftList[_nftAddr][_tokenId]; // 取得Order        
        require(_order.owner == msg.sender, "Not Owner"); // 必须由持有人发起
        // 声明IERC721接口合约变量
        IERC721 _nft = IERC721(_nftAddr);
        require(_nft.ownerOf(_tokenId) == address(this), "Invalid Order"); // NFT在合约中
        
        // 将NFT转给卖家
        _nft.safeTransferFrom(address(this), msg.sender, _tokenId);
        delete nftList[_nftAddr][_tokenId]; // 删除order
      
        // 释放Revoke事件
        emit Revoke(msg.sender, _nftAddr, _tokenId);
    }
```



- 修改价格`update()`：卖家修改`NFT`订单价格，并释放`Update`事件。参数为`NFT`合约地址`_nftAddr`，`NFT`对应的`_tokenId`，更新后的挂单价格`_newPrice`（**注意：单位是`wei`**）。

```solidity
    // 调整价格: 卖家调整挂单价格
    function update(address _nftAddr, uint256 _tokenId, uint256 _newPrice) public {
        require(_newPrice > 0, "Invalid Price"); // NFT价格大于0
        Order storage _order = nftList[_nftAddr][_tokenId]; // 取得Order        
        require(_order.owner == msg.sender, "Not Owner"); // 必须由持有人发起
        // 声明IERC721接口合约变量
        IERC721 _nft = IERC721(_nftAddr);
        require(_nft.ownerOf(_tokenId) == address(this), "Invalid Order"); // NFT在合约中
        
        // 调整NFT价格
        _order.price = _newPrice;
      
        // 释放Update事件
        emit Update(msg.sender, _nftAddr, _tokenId, _newPrice);
    }
```



- 购买`purchase`：买家支付`ETH`购买挂单的`NFT`，并释放`Purchase`事件。参数为`NFT`合约地址`_nftAddr`，`NFT`对应的`_tokenId`。成功后，`ETH`将转给卖家，`NFT`将从`NFTSwap`合约转给买家。

```solidity
    // 购买: 买家购买NFT，合约为_nftAddr，tokenId为_tokenId，调用函数时要附带ETH
    function purchase(address _nftAddr, uint256 _tokenId) payable public {
        Order storage _order = nftList[_nftAddr][_tokenId]; // 取得Order        
        require(_order.price > 0, "Invalid Price"); // NFT价格大于0
        require(msg.value >= _order.price, "Increase price"); // 购买价格大于标价
        // 声明IERC721接口合约变量
        IERC721 _nft = IERC721(_nftAddr);
        require(_nft.ownerOf(_tokenId) == address(this), "Invalid Order"); // NFT在合约中

        // 将NFT转给买家
        _nft.safeTransferFrom(address(this), msg.sender, _tokenId);
        // 将ETH转给卖家，多余ETH给买家退款
        payable(_order.owner).transfer(_order.price);
        payable(msg.sender).transfer(msg.value-_order.price);

        delete nftList[_nftAddr][_tokenId]; // 删除order

        // 释放Purchase事件
        emit Purchase(msg.sender, _nftAddr, _tokenId, _order.price);
    }
```



## `Remix`实现

### 1. 部署NFT合约

参考 [ERC721](https://github.com/AmazingAng/WTF-Solidity/tree/main/34_ERC721) 教程了解NFT，并部署`WTFApe` NFT合约。



![部署NFT合约](https://www.wtf.academy/assets/images/38-1-14006b39caba3a0382fbc426dddaf3a2.png)



将首个NFT mint给自己，这里mint给自己是为了之后能够上架NFT、修改价格等一系类操作。

`mint(address to, uint tokenId)`方法有2个参数:

`to`:将 NFT mint给指定的地址，这里通常是自己的钱包地址。

`tokenId`: `WTFApe`合约定义了总量为10000个NFT，图中mint它的的第一个和第二个NFT，`tokenId`分别为`0`和`1`。



![mint NFT](https://www.wtf.academy/assets/images/38-2-da734d42ee99962cf47240bd3d0a55ce.png)



在`WTFApe`合约中，利用`ownerOf`确认自己已经获得`tokenId`为0的NFT。

`ownerOf(uint tokenId)`方法有1个参数:

`tokenId`: `tokenId`为NFT的id，本案例中为上述mint的`0`Id。



![确认自己已经获得NFT](https://www.wtf.academy/assets/images/38-3-ad0008ffbdb6bfaf971c6aa45e5642fd.png)



按照上述方法，将TokenId为 `0` 和 `1` 的NFT都mint给自己，其中`tokenId`为`0`的，我们执行更新购买操作，`tokenId`为`1`的，我们执行下架操作。

### 2. 部署`NFTSwap`合约

部署`NFTSwap`合约。



![部署`NFTSwap`合约](https://www.wtf.academy/assets/images/38-4-627b2f13382d4c07e6002c99147db0d5.png)



### 3. 将要上架的`NFT`授权给`NFTSwap`合约

在`WTFApe`合约中调用 `approve()`授权函数，将自己持有的`tokenId`为0的NFT授权给`NFTSwap`合约地址。

`approve(address to, uint tokenId)`方法有2个参数:

`to`: 将tokenId授权给 `to` 地址，本案例中将授权给`NFTSwap`合约地址。

`tokenId`: `tokenId`为NFT的id，本案例中为上述mint的`0`Id。



![img](data:image/png;base64,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)



按照上述方法，同理将`tokenId`为`1`的NFT也授权给`NFTSwap`合约地址。

### 4. 上架`NFT`

调用`NFTSwap`合约的`list()`函数，将自己持有的`tokenId`为0的NFT上架到`NFTSwap`，价格设为1 `wei`。

`list(address _nftAddr, uint256 _tokenId, uint256 _price)`方法有3个参数:

`_nftAddr`: `_nftAddr`为NFT合约地址，本案例中为`WTFApe`合约地址。

`_tokenId`: `_tokenId`为NFT的id，本案例中为上述mint的`0`Id。

`_price`: `_price`为NFT的价格，本案例中为1 `wei`。



![img](https://www.wtf.academy/assets/images/38-6-dfd1a514dbcd3e198ff3b070038d1da6.png)



按照上述方法，同理将自己持有的`tokenId`为1的NFT上架到`NFTSwap`，价格设为1 `wei`。

### 5. 查看上架NFT

调用`NFTSwap`合约的`nftList()`函数查看上架的NFT。

`nftList`:是一个NFT Order的映射，结构如下：

`nftList[_nftAddr][_tokenId]`: 输入`_nftAddr`和`_tokenId`，返回一个NFT订单。



![img](https://www.wtf.academy/assets/images/38-7-19f2c648c2fdbacc765dc516031098f2.png)



### 6. 更新`NFT`价格

调用`NFTSwap`合约的`update()`函数，将`tokenId`为0的NFT价格更新为77 `wei`

`update(address _nftAddr, uint256 _tokenId, uint256 _newPrice)`方法有3个参数:

`_nftAddr`: `_nftAddr`为NFT合约地址，本案例中为`WTFApe`合约地址。

`_tokenId`: `_tokenId`为NFT的id，本案例中为上述mint的`0`Id。

`_newPrice`: `_newPrice`为NFT的新价格，本案例中为77 `wei`。

执行`update`之后，调用`nftList` 查看更新后的价格



![img](https://www.wtf.academy/assets/images/38-8-886e56ee15d1b57973679cfe537b9384.png)



### 5. 下架NFT

调用`NFTSwap`合约的`revoke()`函数下架NFT。

上述文章中，我们上架了2个NFT，`tokenId`分别为 `0` 和 `1`。本次方法中，我们下架`tokenId`为`1`的NFT。

`revoke(address _nftAddr, uint256 _tokenId)`方法有2个参数:

`_nftAddr`: `_nftAddr`为NFT合约地址，本案例中为`WTFApe`合约地址。

`_tokenId`: `_tokenId`为NFT的id，本案例中为上述mint的`1`Id。



![img](https://www.wtf.academy/assets/images/38-9-8910ff75f2b8ff7d24a7b9e5fe092375.png)



调用`NFTSwap`合约的`nftList()`函数，可以看到`NFT`已经下架。再次上架需要重新授权。



![img](https://www.wtf.academy/assets/images/38-10-15c0167c6dd2f0b92c547f30628e1688.png)



**注意下架NFT之后，需要重新从步骤3开始，重新授权和上架NFT之后，才能进行购买**

### 6. 购买`NFT`

切换账号，调用`NFTSwap`合约的`purchase()`函数购买NFT，购买时需要输入`NFT`合约地址，`tokenId`，并输入支付的`ETH`。

我们下架了`tokenId`为`1`的NFT，现在还存在`tokenId`为`0`的NFT，所以我们可以购买`tokenId`为`0`的NFT。

`purchase(address _nftAddr, uint256 _tokenId, uint256 _wei)`方法有3个参数:

`_nftAddr`: `_nftAddr`为NFT合约地址，本案例中为`WTFApe`合约地址。

`_tokenId`: `_tokenId`为NFT的id，本案例中为上述mint的`0`Id。

`_wei`: `_wei`为支付的`ETH`数量，本案例中为77 `wei`。



![img](https://www.wtf.academy/assets/images/38-11-81e8539b32ea5d18eb8097690b760b71.png)



### 7. 验证`NFT`持有人改变

购买成功之后，调用`WTFApe`合约的`ownerOf()`函数，可以看到`NFT`持有者发生变化，购买成功！



![img](https://www.wtf.academy/assets/images/38-12-8dc7ed34b675548a77d9b60e229d1d13.png)



## 总结

这一讲，我们建立了一个零手续费的去中心化`NFT`交易所。`OpenSea`虽然对`NFT`的发展做了很大贡献，但它的缺点也非常明显：高手续费、不发币回馈用户、交易机制容易被钓鱼导致用户资产丢失。目前`Looksrare`和`dydx`等新的`NFT`交易平台正在挑战`OpenSea`的位置，`Uniswap`也在研究新的`NFT`交易所。相信不久的将来，我们会用到更好的`NFT`交易所。

# 39. 链上随机数

很多以太坊上的应用都需要用到随机数，例如`NFT`随机抽取`tokenId`、抽盲盒、`gamefi`战斗中随机分胜负等等。但是由于以太坊上所有数据都是公开透明（`public`）且确定性（`deterministic`）的，它没法像其他编程语言一样给开发者提供生成随机数的方法。这一讲我们将介绍链上（哈希函数）和链下（`chainlink`预言机）随机数生成的两种方法，并利用它们做一款`tokenId`随机铸造的`NFT`。

## 链上随机数生成

我们可以将一些链上的全局变量作为种子，利用`keccak256()`哈希函数来获取伪随机数。这是因为哈希函数具有灵敏性和均一性，可以得到“看似”随机的结果。下面的`getRandomOnchain()`函数利用全局变量`block.timestamp`，`msg.sender`和`blockhash(block.number-1)`作为种子来获取随机数：

```solidity
    /** 
    * 链上伪随机数生成
    * 利用keccak256()打包一些链上的全局变量/自定义变量
    * 返回时转换成uint256类型
    */
    function getRandomOnchain() public view returns(uint256){
        // remix运行blockhash会报错
        bytes32 randomBytes = keccak256(abi.encodePacked(block.timestamp, msg.sender, blockhash(block.number-1)));
        
        return uint256(randomBytes);
    }
```



**注意:**，这个方法并不安全：

- 首先，`block.timestamp`，`msg.sender`和`blockhash(block.number-1)`这些变量都是公开的，使用者可以预测出用这些种子生成出的随机数，并挑出他们想要的随机数执行合约。
- 其次，矿工可以操纵`blockhash`和`block.timestamp`，使得生成的随机数符合他的利益。

尽管如此，由于这种方法是最便捷的链上随机数生成方法，大量项目方依靠它来生成不安全的随机数，包括知名的项目`meebits`，`loots`等。当然，这些项目也无一例外的被[攻击](https://forum.openzeppelin.com/t/understanding-the-meebits-exploit/8281)了：攻击者可以铸造任何他们想要的稀有`NFT`，而非随机抽取。

## 链下随机数生成

我们可以在链下生成随机数，然后通过预言机把随机数上传到链上。`Chainlink`提供`VRF`（可验证随机函数）服务，链上开发者可以支付`LINK`代币来获取随机数。` Chainlink VRF`有两个版本，第二个版本需要官网注册并预付费，比第一个版本多许多操作，需要花费更多的gas，但取消订阅后可以拿回剩余的Link，这里介绍第二个版本`Chainlink VRF V2`。

### `Chainlink VRF`使用步骤



![Chainlnk VRF](https://www.wtf.academy/assets/images/39-1-8ce51bfb6a4ef7e77b54af56022d402b.png)



我们将用一个简单的合约介绍使用`Chainlink VRF`的步骤。`RandomNumberConsumer`合约可以向`VRF`请求随机数，并存储在状态变量`randomWords`中。

**1. 申请Subscription并转入`Link`代币’**

在Chainlink VRF网站[这里](https://vrf.chain.link/)上创建一个`Subscription`，其中邮箱和项目名都是选填

创建完成后往`Subscription`中转入一些`Link`代币。测试网的`LINK`代币可以从[LINK水龙头](https://faucets.chain.link/)领取。

**2. 用户合约继承`VRFConsumerBaseV2`**

为了使用`VRF`获取随机数，合约需要继承`VRFConsumerBaseV2`合约，并在构造函数中初始化`VRFCoordinatorV2Interface`和`Subscription Id`。

**注意:** 不同链对应不同的参数，在[这里](https://docs.chain.link/vrf/v2/subscription/supported-networks)查询。

教程中我们使用`Sepolia`测试网。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.21;

import "@chainlink/contracts/src/v0.8/interfaces/VRFCoordinatorV2Interface.sol";
import "@chainlink/contracts/src/v0.8/VRFConsumerBaseV2.sol";

contract RandomNumberConsumer is VRFConsumerBaseV2{

    //请求随机数需要调用VRFCoordinatorV2Interface接口
    VRFCoordinatorV2Interface COORDINATOR;
    
    // 申请后的subId
    uint64 subId;

    //存放得到的 requestId 和 随机数
    uint256 public requestId;
    uint256[] public randomWords;
    
    /**
     * 使用chainlink VRF，构造函数需要继承 VRFConsumerBaseV2
     * 不同链参数填的不一样
     * 具体可以看：https://docs.chain.link/vrf/v2/subscription/supported-networks
     * 网络: Sepolia测试网
     * Chainlink VRF Coordinator 地址: 0x8103B0A8A00be2DDC778e6e7eaa21791Cd364625
     * LINK 代币地址: 0x01BE23585060835E02B77ef475b0Cc51aA1e0709
     * 30 gwei Key Hash: 0x474e34a077df58807dbe9c96d3c009b23b3c6d0cce433e59bbf5b34f823bc56c
     * Minimum Confirmations 最小确认块数 : 3 （数字大安全性高，一般填12）
     * callbackGasLimit gas限制 : 最大 2,500,000
     * Maximum Random Values 一次可以得到的随机数个数 : 最大 500          
     */
    address vrfCoordinator = 0x8103B0A8A00be2DDC778e6e7eaa21791Cd364625;
    bytes32 keyHash = 0x474e34a077df58807dbe9c96d3c009b23b3c6d0cce433e59bbf5b34f823bc56c;
    uint16 requestConfirmations = 3;
    uint32 callbackGasLimit = 200_000;
    uint32 numWords = 3;
    
    constructor(uint64 s_subId) VRFConsumerBaseV2(vrfCoordinator){
        COORDINATOR = VRFCoordinatorV2Interface(vrfCoordinator);
        subId = s_subId;
    }
```



**2. 用户合约申请随机数**

用户可以调用从`VRFCoordinatorV2Interface`接口合约中的`requestRandomWords`函数申请随机数，并返回申请标识符`requestId`。这个申请会传递给`VRF`合约。

**注意:** 合约部署后，需要把合约加入到`Subscription`的`Consumers`中，才能发送申请。

```solidity
    /** 
     * 向VRF合约申请随机数 
     */
    function requestRandomWords() external {
        requestId = COORDINATOR.requestRandomWords(
            keyHash,
            subId,
            requestConfirmations,
            callbackGasLimit,
            numWords
        );
    }
```



**3. `Chainlink`节点链下生成随机数和[数字签名](https://github.com/AmazingAng/WTF-Solidity/blob/main/37_Signature/readme.md)，并发送给`VRF`合约**

**4. `VRF`合约验证签名有效性**

**5. 用户合约接收并使用随机数**

在`VRF`合约验证签名有效之后，会自动调用用户合约的回退函数`fulfillRandomness()`，将链下生成的随机数发送过来。用户要把消耗随机数的逻辑写在这里。

**注意:** 用户申请随机数时调用的`requestRandomness()`和`VRF`合约返回随机数时调用的回退函数`fulfillRandomness()`是两笔交易，调用者分别是用户合约和`VRF`合约，后者比前者晚几分钟（不同链延迟不一样）。

```solidity
    /**
     * VRF合约的回调函数，验证随机数有效之后会自动被调用
     * 消耗随机数的逻辑写在这里
     */
    function fulfillRandomWords(uint256 requestId, uint256[] memory s_randomWords) internal override {
        randomWords = s_randomWords;
    }
```



## `tokenId`随机铸造的`NFT`

这一节，我们将利用链上和链下随机数来做一款`tokenId`随机铸造的`NFT`。`Random`合约继承`ERC721`和`VRFConsumerBaseV2`合约。

```Solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.21;

import "https://github.com/AmazingAng/WTF-Solidity/blob/main/34_ERC721/ERC721.sol";
import "@chainlink/contracts/src/v0.8/interfaces/VRFCoordinatorV2Interface.sol";
import "@chainlink/contracts/src/v0.8/VRFConsumerBaseV2.sol";

contract Random is ERC721, VRFConsumerBaseV2{
```



### 状态变量

- ```
  NFT
  ```

  相关

  - `totalSupply`：`NFT`总供给。
  - `ids`：数组，用于计算可供`mint`的`tokenId`，见`pickRandomUniqueId()`函数。
  - `mintCount`：已经`mint`的数量。

- ```
  Chainlink VRF
  ```

  相关

  - `COORDINATOR`：调用`VRFCoordinatorV2Interface`接口
  - `vrfCoordinator`:`VRF`合约地址
  - `keyHash`:`VRF`唯一标识符。
  - `requestConfirmations`:确认块数
  - `callbackGasLimit`：`VRF`手续费。
  - `numWords`:请求的随机数个数
  - `subId`：申请的`Subscription Id`
  - `requestId`:申请标识符
  - `requestToSender`：记录申请`VRF`用于铸造的用户地址。

```solidity
    // NFT相关
    uint256 public totalSupply = 100; // 总供给
    uint256[100] public ids; // 用于计算可供mint的tokenId
    uint256 public mintCount; // 已mint数量

    // chainlink VRF参数
    
    //VRFCoordinatorV2Interface
    VRFCoordinatorV2Interface COORDINATOR;
    
    /**
     * 使用chainlink VRF，构造函数需要继承 VRFConsumerBaseV2
     * 不同链参数填的不一样
     * 网络: Sepolia测试网
     * Chainlink VRF Coordinator 地址: 0x8103B0A8A00be2DDC778e6e7eaa21791Cd364625
     * LINK 代币地址: 0x01BE23585060835E02B77ef475b0Cc51aA1e0709
     * 30 gwei Key Hash: 0x474e34a077df58807dbe9c96d3c009b23b3c6d0cce433e59bbf5b34f823bc56c
     * Minimum Confirmations 最小确认块数 : 3 （数字大安全性高，一般填12）
     * callbackGasLimit gas限制 : 最大 2,500,000
     * Maximum Random Values 一次可以得到的随机数个数 : 最大 500          
     */
    address vrfCoordinator = 0x8103B0A8A00be2DDC778e6e7eaa21791Cd364625;
    bytes32 keyHash = 0x474e34a077df58807dbe9c96d3c009b23b3c6d0cce433e59bbf5b34f823bc56c;
    uint16 requestConfirmations = 3;
    uint32 callbackGasLimit = 1_000_000;
    uint32 numWords = 1;
    uint64 subId;
    uint256 public requestId;
    
    // 记录VRF申请标识对应的mint地址
    mapping(uint256 => address) public requestToSender;
```



### 构造函数

初始化继承的`VRFConsumerBaseV2`和`ERC721`合约的相关变量。

```solidity
    constructor(uint64 s_subId) 
        VRFConsumerBaseV2(vrfCoordinator)
        ERC721("WTF Random", "WTF"){
            COORDINATOR = VRFCoordinatorV2Interface(vrfCoordinator);
            subId = s_subId;
    }
```



### 其他函数

除了构造函数以外，合约里还定义了`5`个函数。

- `pickRandomUniqueId()`：输入随机数，获取可供`mint`的`tokenId`。
- `getRandomOnchain()`：获取链上随机数（不安全）。
- `mintRandomOnchain()`：利用链上随机数铸造`NFT`，调用了`getRandomOnchain()`和`pickRandomUniqueId()`。
- `mintRandomVRF()`：申请`Chainlink VRF`用于铸造随机数。由于使用随机数铸造的逻辑在回调函数`fulfillRandomness()`，而回调函数的调用者是`VRF`合约，而非铸造`NFT`的用户，这里必须利用`requestToSender`状态变量记录`VRF`申请标识符对应的用户地址。
- `fulfillRandomWords()`：`VRF`的回调函数，由`VRF`合约在验证随机数真实性后自动调用，用返回的链下随机数铸造`NFT`。

```solidity
    /** 
    * 输入uint256数字，返回一个可以mint的tokenId
    * 算法过程可理解为：totalSupply个空杯子（0初始化的ids）排成一排，每个杯子旁边放一个球，编号为[0, totalSupply - 1]。
    每次从场上随机拿走一个球（球可能在杯子旁边，这是初始状态；也可能是在杯子里，说明杯子旁边的球已经被拿走过，则此时新的球从末尾被放到了杯子里）
    再把末尾的一个球（依然是可能在杯子里也可能在杯子旁边）放进被拿走的球的杯子里，循环totalSupply次。相比传统的随机排列，省去了初始化ids[]的gas。
    */
    function pickRandomUniqueId(uint256 random) private returns (uint256 tokenId) {
        //先计算减法，再计算++, 关注(a++，++a)区别
        uint256 len = totalSupply - mintCount++; // 可mint数量
        require(len > 0, "mint close"); // 所有tokenId被mint完了
        uint256 randomIndex = random % len; // 获取链上随机数

        //随机数取模，得到tokenId，作为数组下标，同时记录value为len-1，如果取模得到的值已存在，则tokenId取该数组下标的value
        tokenId = ids[randomIndex] != 0 ? ids[randomIndex] : randomIndex; // 获取tokenId
        ids[randomIndex] = ids[len - 1] == 0 ? len - 1 : ids[len - 1]; // 更新ids 列表
        ids[len - 1] = 0; // 删除最后一个元素，能返还gas
    }

    /** 
    * 链上伪随机数生成
    * keccak256(abi.encodePacked()中填上一些链上的全局变量/自定义变量
    * 返回时转换成uint256类型
    */
    function getRandomOnchain() public view returns(uint256){
        /*
         * 本例链上随机只依赖区块哈希，调用者地址，和区块时间，
         * 想提高随机性可以再增加一些属性比如nonce等，但是不能根本上解决安全问题
         */
        bytes32 randomBytes = keccak256(abi.encodePacked(blockhash(block.number-1), msg.sender, block.timestamp));
        return uint256(randomBytes);
    }

    // 利用链上伪随机数铸造NFT
    function mintRandomOnchain() public {
        uint256 _tokenId = pickRandomUniqueId(getRandomOnchain()); // 利用链上随机数生成tokenId
        _mint(msg.sender, _tokenId);
    }

    /** 
     * 调用VRF获取随机数，并mintNFT
     * 要调用requestRandomness()函数获取，消耗随机数的逻辑写在VRF的回调函数fulfillRandomness()中
     * 调用前，需要在Subscriptions中转入足够的Link
     */
    function mintRandomVRF() public {
        // 调用requestRandomness获取随机数
        requestId = COORDINATOR.requestRandomWords(
            keyHash,
            subId,
            requestConfirmations,
            callbackGasLimit,
            numWords
        );
        requestToSender[requestId] = msg.sender;
    }

    /**
     * VRF的回调函数，由VRF Coordinator调用
     * 消耗随机数的逻辑写在本函数中
     */
    function fulfillRandomWords(uint256 requestId, uint256[] memory s_randomWords) internal override{
        address sender = requestToSender[requestId]; // 从requestToSender中获取minter用户地址
        uint256 tokenId = pickRandomUniqueId(s_randomWords[0]); // 利用VRF返回的随机数生成tokenId
        _mint(sender, tokenId);
    }
```



## `remix`验证

### 1. 在`Chainlink VRF`上申请`Subscription`



![申请Subscription](https://www.wtf.academy/assets/images/39-2-cc6e2aa85231dbff1332f8b559553577.png)



### 2. 利用`Chainlink`水龙头获取测试网的`LINK`和`ETH`



![Sepolia测试网领取LINK和ETH](https://www.wtf.academy/assets/images/39-3-c0d36669acc0173aa23bd84d2d7f3530.png)



### 3. 在`Subscription`中转入`LINK`代币



![LINK转入Subscription](https://www.wtf.academy/assets/images/39-4-d373959ad5866cb8b0ae1973872eea22.png)



### 4. 在`Sepolia`测试网部署`Random`合约



![合约部署](https://www.wtf.academy/assets/images/39-5-75d50a1a46e9d949e9455cf3752f82c5.png)



### 5. 利用链上随机数铸造`NFT`

在`remix`界面中，点击左侧橙色函数`mintRandomOnchain`

![mintOnchain](https://www.wtf.academy/assets/images/39-6-1-131d935914236bb3e934b6bb1eba75b7.png)

在弹出的小狐狸钱包中点击确认，利用链上随机数铸造交易就开始了





![链上随机数铸造](https://www.wtf.academy/assets/images/39-6-1327a01de4fb6d2c58077d6b1cb98c0c.png)



### 6. 在`Consumers`中添加合约地址

将合约加入到`Subscription`的`Consumers`中

![添加合约](https://www.wtf.academy/assets/images/39-7-47b40a6a56d9516e3c4e6add1803361e.png)



### 7. 利用`Chainlink VRF`链下随机数铸造`NFT`

同理，在`remix`界面中，点击左侧橙色函数`mintRandomVRF`，在弹出的小狐狸钱包中点击确认，利用`Chainlink VRF`链下随机数铸造交易就开始了

**注意:** 采用`VRF`铸造`NFT`时，发起交易和铸造成功不在同一个区块



![VRF铸造开始交易](https://www.wtf.academy/assets/images/39-8-8fda90a1d537909f87cb4d329744dd05.png)

![VRF铸造成功交易](https://www.wtf.academy/assets/images/39-9-a7a203a2df0b196cf4c9ff31e0aa6499.png)



### 8. 验证`NFT`已被铸造

通过以上截图可以看出，本例中，`tokenId=4`的`NFT`被链上随机铸造出来，`tokenId=61`的`NFT`被`VRF`铸造出来。

### 9. 取消订阅

当合约不使用后可以在`Chainlink VRF`上取消订阅，取出剩余的`LINK`代币

![取消订阅](https://www.wtf.academy/assets/images/39-10-f910d9b359b71ee6b00f2e95f53eef7f.png)



## 总结

在`Solidity`中生成随机数没有其他编程语言那么容易。这一讲我们将介绍链上（哈希函数）和链下（`chainlink`预言机）随机数生成的两种方法，并利用它们做一款`tokenId`随机铸造的`NFT`。这两种方法各有利弊：使用链上随机数高效，但是不安全；而链下随机数生成依赖于第三方提供的预言机服务，比较安全，但是没那么简单经济。项目方要根据业务场景来选择适合自己的方案。

除此以外，还有一些组织在尝试RNG(Random Number Generation)的新鲜方式，如[randao](https://github.com/randao/randao)就提出以DAO的模式来提供一个`on-chain`且`true randomness`的服务

# 40. ERC1155

这一讲，我们将学习`ERC1155`标准，它支持一个合约包含多种代币。并且，我们会发行一个魔改的无聊猿 - `BAYC1155`：它包含`10,000`种代币，且元数据与`BAYC`一致。

## `EIP1155`

不论是`ERC20`还是`ERC721`标准，每个合约都对应一个独立的代币。假设我们要在以太坊上打造一个类似《魔兽世界》的大型游戏，这需要我们对每个装备都部署一个合约。上千种装备就要部署和管理上千个合约，这非常麻烦。因此，[以太坊EIP1155](https://eips.ethereum.org/EIPS/eip-1155)提出了一个多代币标准`ERC1155`，允许一个合约包含多个同质化和非同质化代币。`ERC1155`在GameFi应用最多，Decentraland、Sandbox等知名链游都使用它。

简单来说，`ERC1155`与之前介绍的非同质化代币标准[ERC721](https://github.com/AmazingAng/WTF-Solidity/tree/main/34_ERC721)类似：在`ERC721`中，每个代币都有一个`tokenId`作为唯一标识，每个`tokenId`只对应一个代币；而在`ERC1155`中，每一种代币都有一个`id`作为唯一标识，每个`id`对应一种代币。这样，代币种类就可以非同质的在同一个合约里管理了，并且每种代币都有一个网址`uri`来存储它的元数据，类似`ERC721`的`tokenURI`。下面是`ERC1155`的元数据接口合约`IERC1155MetadataURI`：

```solidity
/**
 * @dev ERC1155的可选接口，加入了uri()函数查询元数据
 */
interface IERC1155MetadataURI is IERC1155 {
    /**
     * @dev 返回第`id`种类代币的URI
     */
    function uri(uint256 id) external view returns (string memory);
```



那么怎么区分`ERC1155`中的某类代币是同质化还是非同质化代币呢？其实很简单：如果某个`id`对应的代币总量为`1`，那么它就是非同质化代币，类似`ERC721`；如果某个`id`对应的代币总量大于`1`，那么他就是同质化代币，因为这些代币都分享同一个`id`，类似`ERC20`。

## `IERC1155`接口合约

`IERC1155`接口合约抽象了`EIP1155`需要实现的功能，其中包含`4`个事件和`6`个函数。与`ERC721`不同，因为`ERC1155`包含多类代币，它实现了批量转账和批量余额查询，一次操作多种代币。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "https://github.com/AmazingAng/WTF-Solidity/blob/main/34_ERC721/IERC165.sol";

/**
 * @dev ERC1155标准的接口合约，实现了EIP1155的功能
 * 详见：https://eips.ethereum.org/EIPS/eip-1155[EIP].
 */
interface IERC1155 is IERC165 {
    /**
     * @dev 单类代币转账事件
     * 当`value`个`id`种类的代币被`operator`从`from`转账到`to`时释放.
     */
    event TransferSingle(address indexed operator, address indexed from, address indexed to, uint256 id, uint256 value);

    /**
     * @dev 批量代币转账事件
     * ids和values为转账的代币种类和数量数组
     */
    event TransferBatch(
        address indexed operator,
        address indexed from,
        address indexed to,
        uint256[] ids,
        uint256[] values
    );

    /**
     * @dev 批量授权事件
     * 当`account`将所有代币授权给`operator`时释放
     */
    event ApprovalForAll(address indexed account, address indexed operator, bool approved);

    /**
     * @dev 当`id`种类的代币的URI发生变化时释放，`value`为新的URI
     */
    event URI(string value, uint256 indexed id);

    /**
     * @dev 持仓查询，返回`account`拥有的`id`种类的代币的持仓量
     */
    function balanceOf(address account, uint256 id) external view returns (uint256);

    /**
     * @dev 批量持仓查询，`accounts`和`ids`数组的长度要想等。
     */
    function balanceOfBatch(address[] calldata accounts, uint256[] calldata ids)
        external
        view
        returns (uint256[] memory);

    /**
     * @dev 批量授权，将调用者的代币授权给`operator`地址。
     * 释放{ApprovalForAll}事件.
     */
    function setApprovalForAll(address operator, bool approved) external;

    /**
     * @dev 批量授权查询，如果授权地址`operator`被`account`授权，则返回`true`
     * 见 {setApprovalForAll}函数.
     */
    function isApprovedForAll(address account, address operator) external view returns (bool);

    /**
     * @dev 安全转账，将`amount`单位`id`种类的代币从`from`转账给`to`.
     * 释放{TransferSingle}事件.
     * 要求:
     * - 如果调用者不是`from`地址而是授权地址，则需要得到`from`的授权
     * - `from`地址必须有足够的持仓
     * - 如果接收方是合约，需要实现`IERC1155Receiver`的`onERC1155Received`方法，并返回相应的值
     */
    function safeTransferFrom(
        address from,
        address to,
        uint256 id,
        uint256 amount,
        bytes calldata data
    ) external;

    /**
     * @dev 批量安全转账
     * 释放{TransferBatch}事件
     * 要求：
     * - `ids`和`amounts`长度相等
     * - 如果接收方是合约，需要实现`IERC1155Receiver`的`onERC1155BatchReceived`方法，并返回相应的值
     */
    function safeBatchTransferFrom(
        address from,
        address to,
        uint256[] calldata ids,
        uint256[] calldata amounts,
        bytes calldata data
    ) external;
}
```



### `IERC1155`事件

- `TransferSingle`事件：单类代币转账事件，在单币种转账时释放。
- `TransferBatch`事件：批量代币转账事件，在多币种转账时释放。
- `ApprovalForAll`事件：批量授权事件，在批量授权时释放。
- `URI`事件：元数据地址变更事件，在`uri`变化时释放。

### `IERC1155`函数

- `balanceOf()`：单币种余额查询，返回`account`拥有的`id`种类的代币的持仓量。
- `balanceOfBatch()`：多币种余额查询，查询的地址`accounts`数组和代币种类`ids`数组的长度要相等。
- `setApprovalForAll()`：批量授权，将调用者的代币授权给`operator`地址。。
- `isApprovedForAll()`：查询批量授权信息，如果授权地址`operator`被`account`授权，则返回`true`。
- `safeTransferFrom()`：安全单币转账，将`amount`单位`id`种类的代币从`from`地址转账给`to`地址。如果`to`地址是合约，则会验证是否实现了`onERC1155Received()`接收函数。
- `safeBatchTransferFrom()`：安全多币转账，与单币转账类似，只不过转账数量`amounts`和代币种类`ids`变为数组，且长度相等。如果`to`地址是合约，则会验证是否实现了`onERC1155BatchReceived()`接收函数。

## `ERC1155`接收合约

与`ERC721`标准类似，为了避免代币被转入黑洞合约，`ERC1155`要求代币接收合约继承`IERC1155Receiver`并实现两个接收函数：

- `onERC1155Received()`：单币转账接收函数，接受ERC1155安全转账`safeTransferFrom` 需要实现并返回自己的选择器`0xf23a6e61`。
- `onERC1155BatchReceived()`：多币转账接收函数，接受ERC1155安全多币转账`safeBatchTransferFrom` 需要实现并返回自己的选择器`0xbc197c81`。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "https://github.com/AmazingAng/WTF-Solidity/blob/main/34_ERC721/IERC165.sol";

/**
 * @dev ERC1155接收合约，要接受ERC1155的安全转账，需要实现这个合约
 */
interface IERC1155Receiver is IERC165 {
    /**
     * @dev 接受ERC1155安全转账`safeTransferFrom` 
     * 需要返回 0xf23a6e61 或 `bytes4(keccak256("onERC1155Received(address,address,uint256,uint256,bytes)"))`
     */
    function onERC1155Received(
        address operator,
        address from,
        uint256 id,
        uint256 value,
        bytes calldata data
    ) external returns (bytes4);

    /**
     * @dev 接受ERC1155批量安全转账`safeBatchTransferFrom` 
     * 需要返回 0xbc197c81 或 `bytes4(keccak256("onERC1155BatchReceived(address,address,uint256[],uint256[],bytes)"))`
     */
    function onERC1155BatchReceived(
        address operator,
        address from,
        uint256[] calldata ids,
        uint256[] calldata values,
        bytes calldata data
    ) external returns (bytes4);
}
```

主要功能和解释：

1. **`onERC1155Received`**

- 这是用于单个代币接收的函数，当使用 `safeTransferFrom` 函数将 `ERC1155` 代币转入合约时，接收合约必须实现此函数并返回指定的选择器 `0xf23a6e61` 或通过 `keccak256` 哈希计算得出的 `bytes4` 值。该函数确保接收合约可以正确处理收到的单一代币转账。
- 参数解释：
  - `operator`: 操作此次转账的账户地址（一般是代币转出方）。
  - `from`: 代币的发送者地址。
  - `id`: 被转移代币的 ID。
  - `value`: 被转移代币的数量。
  - `data`: 可选的附加数据，提供给接收者处理。

2. **`onERC1155BatchReceived`**

- 这是用于批量代币接收的函数，当使用 `safeBatchTransferFrom` 函数进行批量代币转账时，接收合约必须实现此函数并返回指定的选择器 `0xbc197c81`，或者通过哈希计算得出的 `bytes4` 值。此函数保证批量代币接收操作的安全性。
- 参数解释：
  - `operator`: 操作此次转账的账户地址（一般是代币转出方）。
  - `from`: 代币的发送者地址。
  - `ids`: 被转移的代币种类 ID 数组。
  - `values`: 被转移的每种代币的数量数组。
  - `data`: 可选的附加数据，提供给接收者处理。

## `ERC1155`主合约

`ERC1155`主合约实现了`IERC1155`接口合约规定的函数，还有单币/多币的铸造和销毁函数。

### `ERC1155`变量

`ERC1155`主合约包含`4`个状态变量：

- `name`：代币名称
- `symbol`：代币代号
- `_balances`：代币持仓映射，记录代币种类`id`下某地址`account`的持仓量`balances`。
- `_operatorApprovals`：批量授权映射，记录持有地址给另一个地址的授权情况。

### `ERC1155`函数

`ERC1155`主合约包含`16`个函数：

- 构造函数：初始化状态变量`name`和`symbol`。
- `supportsInterface()`：实现`ERC165`标准，声明它支持的接口，供其他合约检查。
- `balanceOf()`：实现`IERC1155`的`balanceOf()`，查询持仓量。与`ERC721`标准不同，这里需要输入查询的持仓地址`account`以及币种`id`。
- `balanceOfBatch()`：实现`IERC1155`的`balanceOfBatch()`，批量查询持仓量。
- `setApprovalForAll()`：实现`IERC1155`的`setApprovalForAll()`，批量授权，释放`ApprovalForAll`事件。
- `isApprovedForAll()`：实现`IERC1155`的`isApprovedForAll()`，查询批量授权信息。
- `safeTransferFrom()`：实现`IERC1155`的`safeTransferFrom()`，单币种安全转账，释放`TransferSingle`事件。与`ERC721`不同，这里不仅需要填发出方`from`，接收方`to`，代币种类`id`，还需要填转账数额`amount`。
- `safeBatchTransferFrom()`：实现`IERC1155`的`safeBatchTransferFrom()`，多币种安全转账，释放`TransferBatch`事件。
- `_mint()`：单币种铸造函数。
- `_mintBatch()`：多币种铸造函数。
- `_burn()`：单币种销毁函数。
- `_burnBatch()`：多币种销毁函数。
- `_doSafeTransferAcceptanceCheck`：单币种转账的安全检查，被`safeTransferFrom()`调用，确保接收方为合约的情况下，实现了`onERC1155Received()`函数。
- `_doSafeBatchTransferAcceptanceCheck`：多币种转账的安全检查，，被`safeBatchTransferFrom`调用，确保接收方为合约的情况下，实现了`onERC1155BatchReceived()`函数。
- `uri()`：返回`ERC1155`的第`id`种代币存储元数据的网址，类似`ERC721`的`tokenURI`。
- `baseURI()`：返回`baseURI`，`uri`就是把`baseURI`和`id`拼接在一起，需要开发重写。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "./IERC1155.sol";
import "./IERC1155Receiver.sol";
import "./IERC1155MetadataURI.sol";
import "https://github.com/AmazingAng/WTF-Solidity/blob/main/34_ERC721/Address.sol";
import "https://github.com/AmazingAng/WTF-Solidity/blob/main/34_ERC721/String.sol";
import "https://github.com/AmazingAng/WTF-Solidity/blob/main/34_ERC721/IERC165.sol";

/**
 * @dev ERC1155多代币标准
 * 见 https://eips.ethereum.org/EIPS/eip-1155
 */
contract ERC1155 is IERC165, IERC1155, IERC1155MetadataURI {
    using Address for address; // 使用Address库，用isContract来判断地址是否为合约
    using Strings for uint256; // 使用String库
    // Token名称
    string public name;
    // Token代号
    string public symbol;
    // 代币种类id 到 账户account 到 余额balances 的映射
    mapping(uint256 => mapping(address => uint256)) private _balances;
    // address 到 授权地址 的批量授权映射
    mapping(address => mapping(address => bool)) private _operatorApprovals;

    /**
     * 构造函数，初始化`name` 和`symbol`, uri_
     */
    constructor(string memory name_, string memory symbol_) {
        name = name_;
        symbol = symbol_;
    }

    /**
     * @dev See {IERC165-supportsInterface}.
     */
    function supportsInterface(bytes4 interfaceId) public view virtual override returns (bool) {
        return
            interfaceId == type(IERC1155).interfaceId ||
            interfaceId == type(IERC1155MetadataURI).interfaceId ||
            interfaceId == type(IERC165).interfaceId;
    }

    /**
     * @dev 持仓查询 实现IERC1155的balanceOf，返回account地址的id种类代币持仓量。
     */
    function balanceOf(address account, uint256 id) public view virtual override returns (uint256) {
        require(account != address(0), "ERC1155: address zero is not a valid owner");
        return _balances[id][account];
    }

    /**
     * @dev 批量持仓查询
     * 要求:
     * - `accounts` 和 `ids` 数组长度相等.
     */
    function balanceOfBatch(address[] memory accounts, uint256[] memory ids)
        public view virtual override
        returns (uint256[] memory)
    {
        require(accounts.length == ids.length, "ERC1155: accounts and ids length mismatch");
        uint256[] memory batchBalances = new uint256[](accounts.length);
        for (uint256 i = 0; i < accounts.length; ++i) {
            batchBalances[i] = balanceOf(accounts[i], ids[i]);
        }
        return batchBalances;
    }

    /**
     * @dev 批量授权，调用者授权operator使用其所有代币
     * 释放{ApprovalForAll}事件
     * 条件：msg.sender != operator
     */
    function setApprovalForAll(address operator, bool approved) public virtual override {
        require(msg.sender != operator, "ERC1155: setting approval status for self");//调用者不能自己授予自己全权代理
        _operatorApprovals[msg.sender][operator] = approved;
        emit ApprovalForAll(msg.sender, operator, approved);
    }

    /**
     * @dev 查询批量授权.
     */
    function isApprovedForAll(address account, address operator) public view virtual override returns (bool) {
        return _operatorApprovals[account][operator];
    }

    /**
     * @dev 安全转账，将`amount`单位的`id`种类代币从`from`转账到`to`
     * 释放 {TransferSingle} 事件.
     * 要求:
     * - to 不能是0地址.
     * - from拥有足够的持仓量，且调用者拥有授权
     * - 如果 to 是智能合约, 他必须支持 IERC1155Receiver-onERC1155Received.
     */
    function safeTransferFrom(
        address from,
        address to,
        uint256 id,
        uint256 amount,
        bytes memory data
    ) public virtual override {
        address operator = msg.sender;
        // 调用者是持有者或是被授权
        require(
            from == operator || isApprovedForAll(from, operator),
            "ERC1155: caller is not token owner nor approved"
        );
        require(to != address(0), "ERC1155: transfer to the zero address");
        // from地址有足够持仓
        uint256 fromBalance = _balances[id][from];
        require(fromBalance >= amount, "ERC1155: insufficient balance for transfer");
        // 更新持仓量
        unchecked {
            _balances[id][from] = fromBalance - amount;
        }
        _balances[id][to] += amount;
        // 释放事件
        emit TransferSingle(operator, from, to, id, amount);
        // 安全检查
        _doSafeTransferAcceptanceCheck(operator, from, to, id, amount, data);    
    }

    /**
     * @dev 批量安全转账，将`amounts`数组单位的`ids`数组种类代币从`from`转账到`to`
     * 释放 {TransferSingle} 事件.
     * 要求:
     * - to 不能是0地址.
     * - from拥有足够的持仓量，且调用者拥有授权
     * - 如果 to 是智能合约, 他必须支持 IERC1155Receiver-onERC1155BatchReceived.
     * - ids和amounts数组长度相等
     */
    function safeBatchTransferFrom(
        address from,
        address to,
        uint256[] memory ids,
        uint256[] memory amounts,
        bytes memory data
    ) public virtual override {
        address operator = msg.sender;
        // 调用者是持有者或是被授权
        require(
            from == operator || isApprovedForAll(from, operator),
            "ERC1155: caller is not token owner nor approved"
        );
        require(ids.length == amounts.length, "ERC1155: ids and amounts length mismatch");
        require(to != address(0), "ERC1155: transfer to the zero address");

        // 通过for循环更新持仓  
        for (uint256 i = 0; i < ids.length; ++i) {
            uint256 id = ids[i];
            uint256 amount = amounts[i];

            uint256 fromBalance = _balances[id][from];
            require(fromBalance >= amount, "ERC1155: insufficient balance for transfer");
            unchecked {
                _balances[id][from] = fromBalance - amount;
            }
            _balances[id][to] += amount;
        }

        emit TransferBatch(operator, from, to, ids, amounts);
        // 安全检查
        _doSafeBatchTransferAcceptanceCheck(operator, from, to, ids, amounts, data);    
    }

    /**
     * @dev 铸造
     * 释放 {TransferSingle} 事件.
     */
    function _mint(
        address to,
        uint256 id,
        uint256 amount,
        bytes memory data
    ) internal virtual {
        require(to != address(0), "ERC1155: mint to the zero address");

        address operator = msg.sender;

        _balances[id][to] += amount;
        emit TransferSingle(operator, address(0), to, id, amount);

        _doSafeTransferAcceptanceCheck(operator, address(0), to, id, amount, data);
    }

    /**
     * @dev 批量铸造
     * 释放 {TransferBatch} 事件.
     */
    function _mintBatch(
        address to,
        uint256[] memory ids,
        uint256[] memory amounts,
        bytes memory data
    ) internal virtual {
        require(to != address(0), "ERC1155: mint to the zero address");
        require(ids.length == amounts.length, "ERC1155: ids and amounts length mismatch");

        address operator = msg.sender;

        for (uint256 i = 0; i < ids.length; i++) {
            _balances[ids[i]][to] += amounts[i];
        }

        emit TransferBatch(operator, address(0), to, ids, amounts);

        _doSafeBatchTransferAcceptanceCheck(operator, address(0), to, ids, amounts, data);
    }

    /**
     * @dev 销毁
     */
    function _burn(
        address from,
        uint256 id,
        uint256 amount
    ) internal virtual {
        require(from != address(0), "ERC1155: burn from the zero address");

        address operator = msg.sender;

        uint256 fromBalance = _balances[id][from];
        require(fromBalance >= amount, "ERC1155: burn amount exceeds balance");
        unchecked {
            _balances[id][from] = fromBalance - amount;
        }

        emit TransferSingle(operator, from, address(0), id, amount);
    }

    /**
     * @dev 批量销毁
     */
    function _burnBatch(
        address from,
        uint256[] memory ids,
        uint256[] memory amounts
    ) internal virtual {
        require(from != address(0), "ERC1155: burn from the zero address");
        require(ids.length == amounts.length, "ERC1155: ids and amounts length mismatch");

        address operator = msg.sender;

        for (uint256 i = 0; i < ids.length; i++) {
            uint256 id = ids[i];
            uint256 amount = amounts[i];

            uint256 fromBalance = _balances[id][from];
            require(fromBalance >= amount, "ERC1155: burn amount exceeds balance");
            unchecked {
                _balances[id][from] = fromBalance - amount;
            }
        }

        emit TransferBatch(operator, from, address(0), ids, amounts);
    }

    // @dev ERC1155的安全转账检查
    function _doSafeTransferAcceptanceCheck(
        address operator,
        address from,
        address to,
        uint256 id,
        uint256 amount,
        bytes memory data
    ) private {
        if (to.isContract()) {
            try IERC1155Receiver(to).onERC1155Received(operator, from, id, amount, data) returns (bytes4 response) {
                if (response != IERC1155Receiver.onERC1155Received.selector) {
                    revert("ERC1155: ERC1155Receiver rejected tokens");
                }
            } catch Error(string memory reason) {
                revert(reason);
            } catch {
                revert("ERC1155: transfer to non-ERC1155Receiver implementer");
            }
        }
    }

    // @dev ERC1155的批量安全转账检查
    function _doSafeBatchTransferAcceptanceCheck(
        address operator,
        address from,
        address to,
        uint256[] memory ids,
        uint256[] memory amounts,
        bytes memory data
    ) private {
        if (to.isContract()) {
            try IERC1155Receiver(to).onERC1155BatchReceived(operator, from, ids, amounts, data) returns (
                bytes4 response
            ) {
                if (response != IERC1155Receiver.onERC1155BatchReceived.selector) {
                    revert("ERC1155: ERC1155Receiver rejected tokens");
                }
            } catch Error(string memory reason) {
                revert(reason);
            } catch {
                revert("ERC1155: transfer to non-ERC1155Receiver implementer");
            }
        }
    }

    /**
     * @dev 返回ERC1155的id种类代币的uri，存储metadata，类似ERC721的tokenURI.
     */
    function uri(uint256 id) public view virtual override returns (string memory) {
        string memory baseURI = _baseURI();
        return bytes(baseURI).length > 0 ? string(abi.encodePacked(baseURI, id.toString())) : "";
    }

    /**
     * 计算{uri}的BaseURI，uri就是把baseURI和tokenId拼接在一起，需要开发重写.
     */
    function _baseURI() internal view virtual returns (string memory) {
        return "";
    }
}
```



## `BAYC`，但是`ERC1155`

我们魔改下`ERC721`标准的无聊猿`BAYC`，创建一个免费铸造的`BAYC1155`。我们修改`_baseURI()`函数，使得`BAYC1155`的`uri`和`BAYC`的`tokenURI`一样。这样，`BAYC1155`元数据会与无聊猿的相同：

```solidity
// SPDX-License-Identifier: MIT
// by 0xAA
pragma solidity ^0.8.21;

import "./ERC1155.sol";

contract BAYC1155 is ERC1155{
    uint256 constant MAX_ID = 10000; 
    // 构造函数
    constructor() ERC1155("BAYC1155", "BAYC1155"){
    }

    //BAYC的baseURI为ipfs://QmeSjSinHpPnmXmspMjwiXyN6zS4E9zccariGR3jxcaWtq/ 
    function _baseURI() internal pure override returns (string memory) {
        return "ipfs://QmeSjSinHpPnmXmspMjwiXyN6zS4E9zccariGR3jxcaWtq/";
    }
    
    // 铸造函数
    function mint(address to, uint256 id, uint256 amount) external {
        // id 不能超过10,000
        require(id < MAX_ID, "id overflow");
        _mint(to, id, amount, "");
    }

    // 批量铸造函数
    function mintBatch(address to, uint256[] memory ids, uint256[] memory amounts) external {
        // id 不能超过10,000
        for (uint256 i = 0; i < ids.length; i++) {
            require(ids[i] < MAX_ID, "id overflow");
        }
        _mintBatch(to, ids, amounts, "");
    }
}
```



## Remix演示

### 1. 部署`BAYC1155`合约



![部署](https://www.wtf.academy/assets/images/40-1-d062d6fc0778e00d4c96411e1e69b029.jpg)



### 2. 查看元数据`uri`



![查看元数据](https://www.wtf.academy/assets/images/40-2-fcb4a0fabf03d31eccaed9663930fbd1.jpg)



### 3. `mint`并查看持仓变化

`mint`一栏中输入账户地址、`id`和数量，点击`mint`按钮铸造。若数量为`1`，则为非同质化代币；若数量大于`1`，则为同质化代币。



![mint1](https://www.wtf.academy/assets/images/40-3-30cfaa852ddc8e113b4c6b079d88789a.jpg)



`blanceOf`一栏中输入账户地址和`id`查看对应持仓



![mint2](https://www.wtf.academy/assets/images/40-4-dc74ac9155657a427cbc79aeba0ff27b.jpg)



### 4. 批量`mint`并查看持仓变化

`mintBatch`一栏中输入要铸造的`ids`数组以及对应的数量，两者数组的长度必须相等



![batchmint1](https://www.wtf.academy/assets/images/40-5-bc7d70f831fde728823480ede6c74018.jpg)



将刚刚铸造好的代币`id`数组输入即可查看



![batchmint2](https://www.wtf.academy/assets/images/40-6-940acf4429fa73be7e1c8bcc212b83ed.jpg)



### 5. 批量转账并查看持仓变化

与铸造类似，不过这次要从拥有相应代币的地址转到一个新的地址，这个地址可以是普通地址也可以是合约地址，如果是合约地址会验证是否实现了`onERC1155Received()`接收函数。

这里我们转给一个普通地址，输入`ids`和`amounts`数组。



![transfer1](https://www.wtf.academy/assets/images/40-7-be7040f3ff5c6927734bfb288c82eebf.jpg)



对刚才转入的地址查看其持仓变化。



![transfer2](https://www.wtf.academy/assets/images/40-8-d0abf70e4873015098367a4dd48e2a56.jpg)



## 总结

这一讲我们学习了以太坊`EIP1155`提出的`ERC1155`多代币标准，它允许一个合约中包含多个同质化或非同质化代币。并且，我们创建了魔改版无聊猿 - `BAYC1155`：一个包含`10,000`种代币且元数据与`BAYC`相同的`ERC1155`代币。目前，`ERC1155`主要应用于`GameFi`中。但我相信随着元宇宙技术不断发展，这个标准会越来越流行。

# 41. WETH

这一讲，我们将学习`WETH`--带包装的`ETH`。

## 什么是`WETH`？



![WETH](https://www.wtf.academy/assets/images/41-1-2a413f9fb4ab4ff14e0591f0dcdabd33.gif)



`WETH` (Wrapped ETH)是`ETH`的带包装版本。我们常见的`WETH`，`WBTC`，`WBNB`，都是带包装的原生代币。那么我们为什么要包装它们？

在2015年，[ERC20](https://github.com/AmazingAng/WTF-Solidity/blob/main/20_SendETH/readme.md)标准出现，该代币标准旨在为以太坊上的代币制定一套标准化的规则，从而简化了新代币的发布，并使区块链上的所有代币相互可比。不幸的是，以太币本身并不符合`ERC20`标准。`WETH`的开发是为了提高区块链之间的互操作性 ，并使`ETH`可用于去中心化应用程序（dApps）。它就像是给原生代币穿了一件智能合约做的衣服：穿上衣服的时候，就变成了`WETH`，符合`ERC20`同质化代币标准，可以跨链，可以用于`dApp`；脱下衣服，它可1:1兑换`ETH`。

## `WETH`合约

目前在用的[主网WETH合约](https://rinkeby.etherscan.io/token/0xc778417e063141139fce010982780140aa0cd5ab?a=0xe16c1623c1aa7d919cd2241d8b36d9e79c1be2a2)写于2015年，非常老，那时候solidity是0.4版本。我们用0.8版本重新写一个`WETH`。

`WETH`符合`ERC20`标准，它比普通的`ERC20`多了两个功能：

1. 存款：包装，用户将`ETH`存入`WETH`合约，并获得等量的`WETH`。
2. 取款：拆包装，用户销毁`WETH`，并获得等量的`ETH`。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract WETH is ERC20{
    // 事件：存款和取款
    event  Deposit(address indexed dst, uint wad);
    event  Withdrawal(address indexed src, uint wad);

    // 构造函数，初始化ERC20的名字和代号
    constructor() ERC20("WETH", "WETH"){
    }

    // 回调函数，当用户往WETH合约转ETH时，会触发deposit()函数
    fallback() external payable {
        deposit();
    }
    // 回调函数，当用户往WETH合约转ETH时，会触发deposit()函数
    receive() external payable {
        deposit();
    }

    // 存款函数，当用户存入ETH时，给他铸造等量的WETH
    function deposit() public payable {
        _mint(msg.sender, msg.value);
        emit Deposit(msg.sender, msg.value);
    }

    // 提款函数，用户销毁WETH，取回等量的ETH
    function withdraw(uint amount) public {
        require(balanceOf(msg.sender) >= amount);
        _burn(msg.sender, amount);
        payable(msg.sender).transfer(amount);
        emit Withdrawal(msg.sender, amount);
    }
}
```



### 继承

`WETH`符合`ERC20`代币标准，因此`WETH`合约继承了`ERC20`合约。

### 事件

`WETH`合约共有`2`个事件：

1. `Deposit`：存款事件，在存款的时候释放。
2. `Withdraw`：取款事件，在取款的时候释放。

### 函数

除了`ERC20`标准的函数外，`WETH`合约有`5`个函数：

- 构造函数：初始化`WETH`的名字和代号。
- 回调函数：`fallback()`和`receive()`，当用户往`WETH`合约转`ETH`的时候，会自动触发`deposit()`存款函数，获得等量的`WETH`。
- `deposit()`：存款函数，当用户存入`ETH`时，给他铸造等量的`WETH`。
- `withdraw()`：取款函数，让用户销毁`WETH`，并归还等量的`ETH`。

## `Remix`演示

### 1. 部署`WETH`合约



![WETH](https://www.wtf.academy/assets/images/41-2-c259dceb5a453204f7e474a8c3e8c9dd.jpg)



### 2. 调用`deposit`，存入`1 ETH`，并查看`WETH`余额



![WETH](https://www.wtf.academy/assets/images/41-3-1e95478d5d721d1c0a1859355ac15995.jpg)



此时`WETH`余额为`1 WETH`。



![WETH](https://www.wtf.academy/assets/images/41-4-f0fb83a0cda6e47b73ac5b8200d9b71c.jpg)



### 3. 直接向`WETH`合约转入`1 ETH`，并查看`WETH`余额



![WETH](https://www.wtf.academy/assets/images/41-5-e39457e837eba3cb1c8d9a33af502357.jpg)



此时`WETH`余额为`2 WETH`。



![WETH](https://www.wtf.academy/assets/images/41-6-98c8d912644349925bd6109282be59ba.jpg)



### 4. 调用`withdraw`，取出`1.5 ETH`，并查看`WETH`余额



![WETH](https://www.wtf.academy/assets/images/41-7-743886b5bbfbc5b0c4de3cf1ab65bd2d.jpg)



此时`WETH`余额为`0.5 WETH`。



![WETH](https://www.wtf.academy/assets/images/41-8-1ec3deaba18e3eb47bb32736905f08a9.jpg)



## 总结

这一讲，我们介绍了`WETH`并实现了`WETH`合约。它就像是给原生`ETH`穿了一件智能合约做的衣服：穿上衣服的时候，就变成了`WETH`，符合`ERC20`同质化代币标准，可以跨链，可以用于`dApp`；脱下衣服，它可以1:1兑换`ETH`。

# 42. 分账

这一讲，我们介绍分账合约，该合约允许将`ETH`按权重转给一组账户中，进行分账。代码部分由OpenZeppelin库的[PaymentSplitter合约](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/finance/PaymentSplitter.sol)简化而来。

## 分账

分账就是按照一定比例分钱财。在现实中，经常会有“分赃不均”的事情发生；而在区块链的世界里，`Code is Law`，我们可以事先把每个人应分的比例写在智能合约中，获得收入后，再由智能合约来进行分账。



![分账](data:image/webp;base64,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)



## 分账合约

分账合约(`PaymentSplit`)具有以下几个特点：

1. 在创建合约时定好分账受益人`payees`和每人的份额`shares`。
2. 份额可以是相等，也可以是其他任意比例。
3. 在该合约收到的所有`ETH`中，每个受益人将能够提取与其分配的份额成比例的金额。
4. 分账合约遵循`Pull Payment`模式，付款不会自动转入账户，而是保存在此合约中。受益人通过调用`release()`函数触发实际转账。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.21;

/**
 * 分账合约 
 * @dev 这个合约会把收到的ETH按事先定好的份额分给几个账户。收到ETH会存在分账合约中，需要每个受益人调用release()函数来领取。
 */
contract PaymentSplit{
```



### 事件

分账合约中共有`3`个事件：

- `PayeeAdded`：增加受益人事件。
- `PaymentReleased`：受益人提款事件。
- `PaymentReceived`：分账合约收款事件。

```solidity
    // 事件
    event PayeeAdded(address account, uint256 shares); // 增加受益人事件
    event PaymentReleased(address to, uint256 amount); // 受益人提款事件
    event PaymentReceived(address from, uint256 amount); // 合约收款事件
```



### 状态变量

分账合约中共有`5`个状态变量，用来记录受益地址、份额、支付出去的`ETH`等变量：

- `totalShares`：总份额，为`shares`的和。
- `totalReleased`：从分账合约向受益人支付出去的`ETH`，为`released`的和。
- `payees`：`address`数组，记录受益人地址
- `shares`：`address`到`uint256`的映射，记录每个受益人的份额。
- `released`：`address`到`uint256`的映射，记录分账合约支付给每个受益人的金额。

```solidity
    uint256 public totalShares; // 总份额
    uint256 public totalReleased; // 总支付

    mapping(address => uint256) public shares; // 每个受益人的份额
    mapping(address => uint256) public released; // 支付给每个受益人的金额
    address[] public payees; // 受益人数组
```



### 函数

分账合约中共有`6`个函数：

- 构造函数：始化受益人数组`_payees`和分账份额数组`_shares`，其中数组长度不能为0，两个数组长度要相等。_shares中元素要大于0，_payees中地址不能为0地址且不能有重复地址。
- `receive()`：回调函数，在分账合约收到`ETH`时释放`PaymentReceived`事件。
- `release()`：分账函数，为有效受益人地址`_account`分配相应的`ETH`。任何人都可以触发这个函数，但`ETH`会转给受益人地址`account`。调用了releasable()函数。
- `releasable()`：计算一个受益人地址应领取的`ETH`。调用了`pendingPayment()`函数。
- `pendingPayment()`：根据受益人地址`_account`, 分账合约总收入`_totalReceived`和该地址已领取的钱`_alreadyReleased`，计算该受益人现在应分的`ETH`。
- `_addPayee()`：新增受益人函数及其份额函数。在合约初始化的时候被调用，之后不能修改。

```solidity
    /**
     * @dev 初始化受益人数组_payees和分账份额数组_shares
     * 数组长度不能为0，两个数组长度要相等。_shares中元素要大于0，_payees中地址不能为0地址且不能有重复地址
     */
    constructor(address[] memory _payees, uint256[] memory _shares) payable {
        // 检查_payees和_shares数组长度相同，且不为0
        require(_payees.length == _shares.length, "PaymentSplitter: payees and shares length mismatch");
        require(_payees.length > 0, "PaymentSplitter: no payees");
        // 调用_addPayee，更新受益人地址payees、受益人份额shares和总份额totalShares
        for (uint256 i = 0; i < _payees.length; i++) {
            _addPayee(_payees[i], _shares[i]);
        }
    }

    /**
     * @dev 回调函数，收到ETH释放PaymentReceived事件
     */
    receive() external payable virtual {
        emit PaymentReceived(msg.sender, msg.value);
    }

    /**
     * @dev 为有效受益人地址_account分帐，相应的ETH直接发送到受益人地址。任何人都可以触发这个函数，但钱会打给account地址。
     * 调用了releasable()函数。
     */
    function release(address payable _account) public virtual {
        // account必须是有效受益人
        require(shares[_account] > 0, "PaymentSplitter: account has no shares");
        // 计算account应得的eth
        uint256 payment = releasable(_account);
        // 应得的eth不能为0
        require(payment != 0, "PaymentSplitter: account is not due payment");
        // 更新总支付totalReleased和支付给每个受益人的金额released
        totalReleased += payment;
        released[_account] += payment;
        // 转账
        _account.transfer(payment);
        emit PaymentReleased(_account, payment);
    }

    /**
     * @dev 计算一个账户能够领取的eth。
     * 调用了pendingPayment()函数。
     */
    function releasable(address _account) public view returns (uint256) {
        // 计算分账合约总收入totalReceived
        uint256 totalReceived = address(this).balance + totalReleased;
        // 调用_pendingPayment计算account应得的ETH
        return pendingPayment(_account, totalReceived, released[_account]);
    }

    /**
     * @dev 根据受益人地址`_account`, 分账合约总收入`_totalReceived`和该地址已领取的钱`_alreadyReleased`，计算该受益人现在应分的`ETH`。
     */
    function pendingPayment(
        address _account,
        uint256 _totalReceived,
        uint256 _alreadyReleased
    ) public view returns (uint256) {
        // account应得的ETH = 总应得ETH - 已领到的ETH
        return (_totalReceived * shares[_account]) / totalShares - _alreadyReleased;
    }

    /**
     * @dev 新增受益人_account以及对应的份额_accountShares。只能在构造器中被调用，不能修改。
     */
    function _addPayee(address _account, uint256 _accountShares) private {
        // 检查_account不为0地址
        require(_account != address(0), "PaymentSplitter: account is the zero address");
        // 检查_accountShares不为0
        require(_accountShares > 0, "PaymentSplitter: shares are 0");
        // 检查_account不重复
        require(shares[_account] == 0, "PaymentSplitter: account already has shares");
        // 更新payees，shares和totalShares
        payees.push(_account);
        shares[_account] = _accountShares;
        totalShares += _accountShares;
        // 释放增加受益人事件
        emit PayeeAdded(_account, _accountShares);
    }
```



## `Remix`演示

### 1. 部署`PaymentSplit`分账合约，并转入`1 ETH`

在构造函数中，输入两个受益人地址，份额为`1`和`3`。



![部署](https://www.wtf.academy/assets/images/42-2-f76d741898f6510e5b4b6098b2b1796e.png)



### 2. 查看受益人地址、份额、应分到的`ETH`



![查看第一位受益人](https://www.wtf.academy/assets/images/42-3-7d663518aae651391728de7329b75d70.png)





![查看第二位受益人](https://www.wtf.academy/assets/images/42-4-5acb0433a51b7dfa836fd1c2562a1b51.png)



### 3. 函数领取`ETH`



![调用release](https://www.wtf.academy/assets/images/42-5-7443ae4dd6bba954703019b6fc03c4d1.png)



### 4. 查看总支出、受益人余额、应分到的`ETH`的变化



![查看](https://www.wtf.academy/assets/images/42-6-976368a1884ec3c168cce9835c96b971.png)



## 总结

这一讲，我们介绍了分账合约。在区块链的世界里，`Code is Law`，我们可以事先把每个人应分的比例写在智能合约中，获得收入后，由智能合约来进行分账，避免事后“分赃不均”。

# 43. 线性释放

这一讲，我们将介绍代币归属条款，并写一个线性释放`ERC20`代币的合约。代码由`OpenZeppelin`的`VestingWallet`合约简化而来。

## 代币归属条款



![部署](https://www.wtf.academy/assets/images/43-1-75303357537ccdc4aaabf980bfc04f6e.jpeg)



在传统金融领域，一些公司会向员工和管理层提供股权。但大量股权同时释放会在短期产生抛售压力，拖累股价。因此，公司通常会引入一个归属期来延迟承诺资产的所有权。同样的，在区块链领域，`Web3`初创公司会给团队分配代币，同时也会将代币低价出售给风投和私募。如果他们把这些低成本的代币同时提到交易所变现，币价将被砸穿，散户直接成为接盘侠。

所以，项目方一般会约定代币归属条款（token vesting），在归属期内逐步释放代币，减缓抛压，并防止团队和资本方过早躺平。

## 线性释放

线性释放指的是代币在归属期内匀速释放。举个例子，某私募持有365,000枚`ICU`代币，归属期为1年（365天），那么每天会释放1,000枚代币。

下面，我们就写一个锁仓并线性释放`ERC20`代币的合约`TokenVesting`。它的逻辑很简单：

- 项目方规定线性释放的起始时间、归属期和受益人。
- 项目方将锁仓的`ERC20`代币转账给`TokenVesting`合约。
- 受益人可以调用`release`函数，从合约中取出释放的代币。

### 事件

线性释放合约中共有`1`个事件。

- `ERC20Released`：提币事件，当受益人提取释放代币时释放。

```solidity
contract TokenVesting {
    // 事件
    event ERC20Released(address indexed token, uint256 amount); // 提币事件
```



### 状态变量

线性释放合约中共有`4`个状态变量。

- `beneficiary`：受益人地址。
- `start`：归属期起始时间戳。
- `duration`：归属期，单位为秒。
- `erc20Released`：代币地址->释放数量的映射，记录受益人已领取的代币数量。

```solidity
    // 状态变量
    mapping(address => uint256) public erc20Released; // 代币地址->释放数量的映射，记录已经释放的代币
    address public immutable beneficiary; // 受益人地址
    uint256 public immutable start; // 起始时间戳
    uint256 public immutable duration; // 归属期
```



### 函数

线性释放合约中共有`3`个函数。

- 构造函数：初始化受益人地址，归属期(秒), 起始时间戳。参数为受益人地址`beneficiaryAddress`和归属期`durationSeconds`。为了方便，起始时间戳用的部署时的区块链时间戳`block.timestamp`。
- `release()`：提取代币函数，将已释放的代币转账给受益人。调用了`vestedAmount()`函数计算可提取的代币数量，释放`ERC20Released`事件，然后将代币`transfer`给受益人。参数为代币地址`token`。
- `vestedAmount()`：根据线性释放公式，查询已经释放的代币数量。开发者可以通过修改这个函数，自定义释放方式。参数为代币地址`token`和查询的时间戳`timestamp`。

```solidity
    /**
     * @dev 初始化受益人地址，释放周期(秒), 起始时间戳(当前区块链时间戳)
     */
    constructor(
        address beneficiaryAddress,
        uint256 durationSeconds
    ) {
        require(beneficiaryAddress != address(0), "VestingWallet: beneficiary is zero address");
        beneficiary = beneficiaryAddress;
        start = block.timestamp;
        duration = durationSeconds;
    }

    /**
     * @dev 受益人提取已释放的代币。
     * 调用vestedAmount()函数计算可提取的代币数量，然后transfer给受益人。
     * 释放 {ERC20Released} 事件.
     */
    function release(address token) public {
        // 调用vestedAmount()函数计算可提取的代币数量
        uint256 releasable = vestedAmount(token, uint256(block.timestamp)) - erc20Released[token];
        // 更新已释放代币数量   
        erc20Released[token] += releasable; 
        // 转代币给受益人
        emit ERC20Released(token, releasable);
        IERC20(token).transfer(beneficiary, releasable);
    }

    /**
     * @dev 根据线性释放公式，计算已经释放的数量。开发者可以通过修改这个函数，自定义释放方式。
     * @param token: 代币地址
     * @param timestamp: 查询的时间戳
     */
    function vestedAmount(address token, uint256 timestamp) public view returns (uint256) {
        // 合约里总共收到了多少代币（当前余额 + 已经提取）
        uint256 totalAllocation = IERC20(token).balanceOf(address(this)) + erc20Released[token];
        // 根据线性释放公式，计算已经释放的数量
        if (timestamp < start) {
            return 0;
        } else if (timestamp > start + duration) {
            return totalAllocation;
        } else {
            return (totalAllocation * (timestamp - start)) / duration;
        }
    }
```



## `Remix`演示

### 1. 部署[第31讲](https://www.wtf.academy/docs/solidity-103/ERC20/)中的`ERC20`合约，并给自己铸造`10000`枚代币。



![部署ERC20](https://www.wtf.academy/assets/images/43-2-4484e59fec33696629044787c421f1c7.png)





![铸造10000枚代币](https://www.wtf.academy/assets/images/43-3-e21cd0ad8f1df84b85d6a073e0f2ad1c.png)



### 2. 部署`TokenVesting`线性释放合约，受益人设为自己，归属期设为`100`秒。



![部署TokenVesting](https://www.wtf.academy/assets/images/43-4-27404fa706af57107880bb64593ca548.png)



### 3. 将`10000`枚`ERC20`代币转给线性释放合约。



![转移代币](https://www.wtf.academy/assets/images/43-5-03f3b549a26f1a72d433c1d75734e29b.png)



### 4. 调用`release()`函数提取代币。



![提取代币](https://www.wtf.academy/assets/images/43-6-84f5643ae58fa6bf97636e7bf45c7940.png)



## 总结

代币短期大量解锁会对币价造成巨大压力，而约定代币归属条款可以缓解抛压，并防止团队和资本方过早躺平。这一讲，我们介绍了代币归属条款，并写了线性释放`ERC20`代币的合约。

# 44. 代币锁

这一讲，我们介绍什么是流动性提供者`LP`代币，为什么要锁定流动性，并写一个简单的`ERC20`代币锁合约。

## 代币锁



![代币锁](https://www.wtf.academy/assets/images/44-1-5f2d69009e570250cb9646501dce0026.webp)



代币锁(Token Locker)是一种简单的时间锁合约，它可以把合约中的代币锁仓一段时间，受益人在锁仓期满后可以取走代币。代币锁一般是用来锁仓流动性提供者`LP`代币的。

### 什么是`LP`代币？

区块链中，用户在去中心化交易所`DEX`上交易代币，例如`Uniswap`交易所。`DEX`和中心化交易所(`CEX`)不同，去中心化交易所使用自动做市商(`AMM`)机制，需要用户或项目方提供资金池，以使得其他用户能够即时买卖。简单来说，用户/项目方需要质押相应的币对（比如`ETH/DAI`）到资金池中，作为补偿，`DEX`会给他们铸造相应的流动性提供者`LP`代币凭证，证明他们质押了相应的份额，供他们收取手续费。

### 为什么要锁定流动性？

如果项目方毫无征兆的撤出流动性池中的`LP`代币，那么投资者手中的代币就无法变现，直接归零了。这种行为也叫`rug-pull`，仅2021年，各种`rug-pull`骗局从投资者那里骗取了价值超过28亿美元的加密货币。

但是如果`LP`代币是锁仓在代币锁合约中，在锁仓期结束以前，项目方无法撤出流动性池，也没办法`rug pull`。因此代币锁可以防止项目方过早跑路（要小心锁仓期满跑路的情况）。

## 代币锁合约

下面，我们就写一个锁仓`ERC20`代币的合约`TokenLocker`。它的逻辑很简单：

- 开发者在部署合约时规定锁仓的时间，受益人地址，以及代币合约。
- 开发者将代币转入`TokenLocker`合约。
- 在锁仓期满，受益人可以取走合约里的代币。

### 事件

`TokenLocker`合约中共有`2`个事件。

- `TokenLockStart`：锁仓开始事件，在合约部署时释放，记录受益人地址，代币地址，锁仓起始时间，和结束时间。
- `Release`：代币释放事件，在受益人取出代币时释放，记录记录受益人地址，代币地址，释放代币时间，和代币数量。

```solidity
    // 事件
    event TokenLockStart(address indexed beneficiary, address indexed token, uint256 startTime, uint256 lockTime);
    event Release(address indexed beneficiary, address indexed token, uint256 releaseTime, uint256 amount);
```



### 状态变量

`TokenLocker`合约中共有`4`个状态变量。

- `token`：锁仓代币地址。
- `beneficiary`：受益人地址。
- `locktime`：锁仓时间(秒)。
- `startTime`：锁仓起始时间戳(秒)。

```solidity
    // 被锁仓的ERC20代币合约
    IERC20 public immutable token;
    // 受益人地址
    address public immutable beneficiary;
    // 锁仓时间(秒)
    uint256 public immutable lockTime;
    // 锁仓起始时间戳(秒)
    uint256 public immutable startTime;
```



### 函数

`TokenLocker`合约中共有`2`个函数。

- 构造函数：初始化代币合约，受益人地址，以及锁仓时间。
- `release()`：在锁仓期满后，将代币释放给受益人。需要受益人主动调用`release()`函数提取代币。

```solidity
    /**
     * @dev 部署时间锁合约，初始化代币合约地址，受益人地址和锁仓时间。
     * @param token_: 被锁仓的ERC20代币合约
     * @param beneficiary_: 受益人地址
     * @param lockTime_: 锁仓时间(秒)
     */
    constructor(
        IERC20 token_,
        address beneficiary_,
        uint256 lockTime_
    ) {
        require(lockTime_ > 0, "TokenLock: lock time should greater than 0");
        token = token_;
        beneficiary = beneficiary_;
        lockTime = lockTime_;
        startTime = block.timestamp;

        emit TokenLockStart(beneficiary_, address(token_), block.timestamp, lockTime_);
    }

    /**
     * @dev 在锁仓时间过后，将代币释放给受益人。
     */
    function release() public {
        require(block.timestamp >= startTime+lockTime, "TokenLock: current time is before release time");

        uint256 amount = token.balanceOf(address(this));
        require(amount > 0, "TokenLock: no tokens to release");

        token.transfer(beneficiary, amount);

        emit Release(msg.sender, address(token), block.timestamp, amount);
    }
```



## `Remix`演示

### 1. 部署[第31讲](https://www.wtf.academy/docs/solidity-103/ERC20/)中的`ERC20`合约，并给自己铸造`10000`枚代币。



![`Remix`演示](https://www.wtf.academy/assets/images/44-2-a92be3f8708bdad0cc388dda6ef6e92c.jpg)



### 2. 部署`ToeknLocker`合约，代币地址为`ERC20`合约地址，受益人为自己，锁仓期填`180`秒。



![`Remix`演示](https://www.wtf.academy/assets/images/44-3-75a0c1e188f255cf726309c70d26c601.jpg)



### 3. 将`10000`枚代币转入合约。



![`Remix`演示](https://www.wtf.academy/assets/images/44-4-90ef58a14ef75619857a187f97536035.jpg)



### 4. 在锁仓期`180`秒内调用`release()`函数，无法取出代币。



![`Remix`演示](https://www.wtf.academy/assets/images/44-5-a15a309fdc23210d5e3fb5b0717582dc.jpg)



### 5. 在锁仓期后调用`release()`函数，成功取出代币。



![`Remix`演示](https://www.wtf.academy/assets/images/44-6-72039685b358682250b1e813cb45daf5.jpg)



## 总结

这一讲，我们介绍了代币锁合约。项目方一般在`DEX`上提供流动性，供投资者交易。项目方突然撤出`LP`会造成`rug-pull`，而将`LP`锁在代币锁合约中可以避免这种情况。

# 45. 时间锁

这一讲，我们介绍时间锁和时间锁合约。代码由Compound的[Timelock合约](https://github.com/compound-finance/compound-protocol/blob/master/contracts/Timelock.sol)简化而来。

## 时间锁



![时间锁](https://www.wtf.academy/assets/images/45-1-731706028166be3a3e237c4ea143a070.jpeg)



时间锁（Timelock）是银行金库和其他高安全性容器中常见的锁定机制。它是一种计时器，旨在防止保险箱或保险库在预设时间之前被打开，即便开锁的人知道正确密码。

在区块链，时间锁被`DeFi`和`DAO`大量采用。它是一段代码，他可以将智能合约的某些功能锁定一段时间。它可以大大改善智能合约的安全性，举个例子，假如一个黑客黑了`Uniswap`的多签，准备提走金库的钱，但金库合约加了2天锁定期的时间锁，那么黑客从创建提钱的交易，到实际把钱提走，需要2天的等待期。在这一段时间，项目方可以找应对办法，投资者可以提前抛售代币减少损失。

## 时间锁合约

下面，我们介绍一下时间锁`Timelock`合约。它的逻辑并不复杂：

- 在创建`Timelock`合约时，项目方可以设定锁定期，并把合约的管理员设为自己。
- 时间锁主要有三个功能：
  - 创建交易，并加入到时间锁队列。
  - 在交易的锁定期满后，执行交易。
  - 后悔了，取消时间锁队列中的某些交易。
- 项目方一般会把时间锁合约设为重要合约的管理员，例如金库合约，再通过时间锁操作他们。
- 时间锁合约的管理员一般为项目的多签钱包，保证去中心化。

### 事件

`Timelock`合约中共有`4`个事件。

- `QueueTransaction`：交易创建并进入时间锁队列的事件。
- `ExecuteTransaction`：锁定期满后交易执行的事件。
- `CancelTransaction`：交易取消事件。
- `NewAdmin`：修改管理员地址的事件。

```solidity
    // 事件
    // 交易取消事件
    event CancelTransaction(bytes32 indexed txHash, address indexed target, uint value, string signature,  bytes data, uint executeTime);
    // 交易执行事件
    event ExecuteTransaction(bytes32 indexed txHash, address indexed target, uint value, string signature,  bytes data, uint executeTime);
    // 交易创建并进入队列 事件
    event QueueTransaction(bytes32 indexed txHash, address indexed target, uint value, string signature, bytes data, uint executeTime);
    // 修改管理员地址的事件
    event NewAdmin(address indexed newAdmin);
```



### 状态变量

`Timelock`合约中共有`4`个状态变量。

- `admin`：管理员地址。
- `delay`：锁定期。
- `GRACE_PERIOD`：交易过期时间。如果交易到了执行的时间点，但在`GRACE_PERIOD`没有被执行，就会过期。
- `queuedTransactions`：进入时间锁队列交易的标识符`txHash`到`bool`的映射，记录所有在时间锁队列中的交易。

```solidity
    // 状态变量
    address public admin; // 管理员地址
    uint public constant GRACE_PERIOD = 7 days; // 交易有效期，过期的交易作废
    uint public delay; // 交易锁定时间 （秒）
    mapping (bytes32 => bool) public queuedTransactions; // txHash到bool，记录所有在时间锁队列中的交易
```



### 修饰器

`Timelock`合约中共有`2`个`modifier`。

- `onlyOwner()`：被修饰的函数只能被管理员执行。
- `onlyTimelock()`：被修饰的函数只能被时间锁合约执行。

```solidity
    // onlyOwner modifier
    modifier onlyOwner() {
        require(msg.sender == admin, "Timelock: Caller not admin");
        _;
    }

    // onlyTimelock modifier
    modifier onlyTimelock() {
        require(msg.sender == address(this), "Timelock: Caller not Timelock");
        _;
    }
```



### 函数

`Timelock`合约中共有`7`个函数。

- 构造函数：初始化交易锁定时间（秒）和管理员地址。

- ```
  queueTransaction()
  ```

  ：创建交易并添加到时间锁队列中。参数比较复杂，因为要描述一个完整的交易：

  - `target`：目标合约地址

  - `value`：发送ETH数额

  - `signature`：调用的函数签名（function signature）

  - `data`：交易的call data

  - `executeTime`：交易执行的区块链时间戳。

    调用这个函数时，要保证交易预计执行时间`executeTime`大于当前区块链时间戳+锁定时间`delay`。交易的唯一标识符为所有参数的哈希值，利用`getTxHash()`函数计算。进入队列的交易会更新在`queuedTransactions`变量中，并释放`QueueTransaction`事件。

- `executeTransaction()`：执行交易。它的参数与`queueTransaction()`相同。要求被执行的交易在时间锁队列中，达到交易的执行时间，且没有过期。执行交易时用到了`solidity`的低级成员函数`call`，在[第22讲](https://github.com/AmazingAng/WTF-Solidity/blob/main/22_Call/readme.md)中有介绍。

- `cancelTransaction()`：取消交易。它的参数与`queueTransaction()`相同。它要求被取消的交易在队列中，会更新`queuedTransactions`并释放`CancelTransaction`事件。

- `changeAdmin()`：修改管理员地址，只能被`Timelock`合约调用。

- `getBlockTimestamp()`：获取当前区块链时间戳。

- `getTxHash()`：返回交易的标识符，为很多交易参数的`hash`。

```solidity
    /**
     * @dev 构造函数，初始化交易锁定时间 （秒）和管理员地址
     */
    constructor(uint delay_) {
        delay = delay_;
        admin = msg.sender;
    }

    /**
     * @dev 改变管理员地址，调用者必须是Timelock合约。
     */
    function changeAdmin(address newAdmin) public onlyTimelock {
        admin = newAdmin;

        emit NewAdmin(newAdmin);
    }

    /**
     * @dev 创建交易并添加到时间锁队列中。
     * @param target: 目标合约地址
     * @param value: 发送eth数额
     * @param signature: 要调用的函数签名（function signature）
     * @param data: call data，里面是一些参数
     * @param executeTime: 交易执行的区块链时间戳
     *
     * 要求：executeTime 大于 当前区块链时间戳+delay
     */
    function queueTransaction(address target, uint256 value, string memory signature, bytes memory data, uint256 executeTime) public onlyOwner returns (bytes32) {
        // 检查：交易执行时间满足锁定时间
        require(executeTime >= getBlockTimestamp() + delay, "Timelock::queueTransaction: Estimated execution block must satisfy delay.");
        // 计算交易的唯一识别符：一堆东西的hash
        bytes32 txHash = getTxHash(target, value, signature, data, executeTime);
        // 将交易添加到队列
        queuedTransactions[txHash] = true;

        emit QueueTransaction(txHash, target, value, signature, data, executeTime);
        return txHash;
    }

    /**
     * @dev 取消特定交易。
     *
     * 要求：交易在时间锁队列中
     */
    function cancelTransaction(address target, uint256 value, string memory signature, bytes memory data, uint256 executeTime) public onlyOwner{
        // 计算交易的唯一识别符：一堆东西的hash
        bytes32 txHash = getTxHash(target, value, signature, data, executeTime);
        // 检查：交易在时间锁队列中
        require(queuedTransactions[txHash], "Timelock::cancelTransaction: Transaction hasn't been queued.");
        // 将交易移出队列
        queuedTransactions[txHash] = false;

        emit CancelTransaction(txHash, target, value, signature, data, executeTime);
    }

    /**
     * @dev 执行特定交易。
     *
     * 要求：
     * 1. 交易在时间锁队列中
     * 2. 达到交易的执行时间
     * 3. 交易没过期
     */
    function executeTransaction(address target, uint256 value, string memory signature, bytes memory data, uint256 executeTime) public payable onlyOwner returns (bytes memory) {
        bytes32 txHash = getTxHash(target, value, signature, data, executeTime);
        // 检查：交易是否在时间锁队列中
        require(queuedTransactions[txHash], "Timelock::executeTransaction: Transaction hasn't been queued.");
        // 检查：达到交易的执行时间
        require(getBlockTimestamp() >= executeTime, "Timelock::executeTransaction: Transaction hasn't surpassed time lock.");
        // 检查：交易没过期
       require(getBlockTimestamp() <= executeTime + GRACE_PERIOD, "Timelock::executeTransaction: Transaction is stale.");
        // 将交易移出队列
        queuedTransactions[txHash] = false;

        // 获取call data
        bytes memory callData;
        if (bytes(signature).length == 0) {
            callData = data;
        } else {
            callData = abi.encodePacked(bytes4(keccak256(bytes(signature))), data);
        }
        // 利用call执行交易
        (bool success, bytes memory returnData) = target.call{value: value}(callData);
        require(success, "Timelock::executeTransaction: Transaction execution reverted.");

        emit ExecuteTransaction(txHash, target, value, signature, data, executeTime);

        return returnData;
    }

    /**
     * @dev 获取当前区块链时间戳
     */
    function getBlockTimestamp() public view returns (uint) {
        return block.timestamp;
    }

    /**
     * @dev 将一堆东西拼成交易的标识符
     */
    function getTxHash(
        address target,
        uint value,
        string memory signature,
        bytes memory data,
        uint executeTime
    ) public pure returns (bytes32) {
        return keccak256(abi.encode(target, value, signature, data, executeTime));
    }
```

这个合约实现了一个典型的时间锁机制，允许通过设定的延迟时间安全地管理合约中的交易。管理员可以通过队列添加、取消和执行交易，确保操作的透明性和安全性。

## `Remix`演示

### 1. 部署`Timelock`合约，锁定期设为`120`秒。



![`Remix`演示](https://www.wtf.academy/assets/images/45-1-0b7a3de5da9a91bf99ca1ed820b9a810.jpg)



### 2. 直接调用`changeAdmin()`将报错。



![`Remix`演示](https://www.wtf.academy/assets/images/45-2-5ead07090a6a287e708513eb73680b7a.jpg)



### 3. 构造更改管理员的交易。

为了构造交易，我们要分别填入以下参数： address target, uint256 value, string memory signature, bytes memory data, uint256 executeTime

- `target`：因为调用的是`Timelock`自己的函数，填入合约地址。

- `value`：不用转入ETH，这里填`0`。

- `signature`：`changeAdmin()`的函数签名为：`"changeAdmin(address)"`。

- ```
  data
  ```

  ：这里填要传入的参数，也就是新管理员的地址。但是要把地址填充为32字节的数据，以满足以太坊ABI编码标准。可以使用hashex网站进行参数的ABI编码。例子：

  ```solidity
  编码前地址：0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2
  编码后地址：0x000000000000000000000000ab8483f64d9c6d1ecf9b849ae677dd3315835cb2
  ```
  
  
  
- ```
  executeTime
  ```

  ：先调用

  ```
  getBlockTimestamp()
  ```

  得到当前区块链时间，再在它的基础上加个150秒填入。

  ![`Remix`演示](https://www.wtf.academy/assets/images/45-3-8347d49319a57f0962e3003dd77a08a7.jpg)

### 4. 调用`queueTransaction`，将交易放入时间锁队列。



![`Remix`演示](https://www.wtf.academy/assets/images/45-4-e5b0acb46f8e3c0ea6ef8e91399e75e3.jpg)



### 5. 在锁定期内调用`executeTransaction`，调用失败。



![`Remix`演示](https://www.wtf.academy/assets/images/45-5-27fbf0d02db930ce7cc1d5a987920d0c.jpg)



### 6. 在锁定期满调用`executeTransaction`，交易成功。



![`Remix`演示](https://www.wtf.academy/assets/images/45-6-027a977e11d9d8d2f1e6a55108f09f39.jpg)



### 7. 查看新的`admin`地址。



![`Remix`演示](https://www.wtf.academy/assets/images/45-7-8f8df31229d87965ba19d94924591443.jpg)



## 总结

时间锁可以将智能合约的某些功能锁定一段时间，大大减少项目方`rug pull`和黑客攻击的机会，增加去中心化应用的安全性。它被`DeFi`和`DAO`大量采用，其中包括`Uniswap`和`Compound`。你投资的项目有使用时间锁吗？

# 46. 代理合约

这一讲，我们介绍代理合约（Proxy Contract）。教学代码由OpenZeppelin的[Proxy合约](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/proxy/Proxy.sol)简化而来。

## 代理模式

`Solidity`合约部署在链上之后，代码是不可变的（immutable）。这样既有优点，也有缺点：

- 优点：安全，用户知道会发生什么（大部分时候）。
- 坏处：就算合约中存在bug，也不能修改或升级，只能部署新合约。但是新合约的地址与旧的不一样，且合约的数据也需要花费大量gas进行迁移。

有没有办法在合约部署后进行修改或升级呢？答案是有的，那就是**代理模式**。



![代理模式](https://www.wtf.academy/assets/images/46-1-fa55b02d12372ac6d6f0cd827a426776.png)



代理模式将合约数据和逻辑分开，分别保存在不同合约中。我们拿上图中简单的代理合约为例，数据（状态变量）存储在代理合约中，而逻辑（函数）保存在另一个逻辑合约中。代理合约（Proxy）通过`delegatecall`，将函数调用全权委托给逻辑合约（Implementation）执行，再把最终的结果返回给调用者（Caller）。

代理模式主要有两个好处：

1. 可升级：当我们需要升级合约的逻辑时，只需要将代理合约指向新的逻辑合约。
2. 省gas：如果多个合约复用一套逻辑，我们只需部署一个逻辑合约，然后再部署多个只保存数据的代理合约，指向逻辑合约。

**提示**：对`delegatecall`不熟悉的朋友可以看下本教程[第23讲Delegatecall](https://github.com/AmazingAng/WTF-Solidity/tree/main/23_Delegatecall)。

## 代理合约

下面我们介绍一个简单的代理合约，它由OpenZeppelin的[Proxy合约](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/proxy/Proxy.sol)简化而来。它有三个部分：代理合约`Proxy`，逻辑合约`Logic`，和一个调用示例`Caller`。它的逻辑并不复杂：

- 首先部署逻辑合约`Logic`。
- 创建代理合约`Proxy`，状态变量`implementation`记录`Logic`合约地址。
- `Proxy`合约利用回调函数`fallback`，将所有调用委托给`Logic`合约
- 最后部署调用示例`Caller`合约，调用`Proxy`合约。
- **注意**：`Logic`合约和`Proxy`合约的状态变量存储结构相同，不然`delegatecall`会产生意想不到的行为，有安全隐患。

### 代理合约`Proxy`

`Proxy`合约不长，但是用到了内联汇编，因此比较难理解。它只有一个状态变量，一个构造函数，和一个回调函数。状态变量`implementation`，在构造函数中初始化，用于保存`Logic`合约地址。

```solidity
contract Proxy {
    address public implementation; // 逻辑合约地址。implementation合约同一个位置的状态变量类型必须和Proxy合约的相同，不然会报错。

    /**
     * @dev 初始化逻辑合约地址
     */
    constructor(address implementation_){
        implementation = implementation_;
    }
```



`Proxy`的回调函数将外部对本合约的调用委托给 `Logic` 合约。这个回调函数很别致，它利用内联汇编（inline assembly），让本来不能有返回值的回调函数有了返回值。其中用到的内联汇编操作码：

- `calldata(t, f, s)`：将calldata（输入数据）从位置`f`开始复制`s`字节到mem（内存）的位置`t`。
- `delegatecall(g, a, in, insize, out, outsize)`：调用地址`a`的合约，输入为`mem[in..(in+insize))` ，输出为`mem[out..(out+outsize))`， 提供`g`wei的以太坊gas。这个操作码在错误时返回`0`，在成功时返回`1`。
- `returndata(t, f, s)`：将returndata（输出数据）从位置`f`开始复制`s`字节到mem（内存）的位置`t`。
- `switch`：基础版`if/else`，不同的情况`case`返回不同值。可以有一个默认的`default`情况。
- `return(p, s)`：终止函数执行, 返回数据`mem[p..(p+s))`。
- `revert(p, s)`：终止函数执行, 回滚状态，返回数据`mem[p..(p+s))`。

```solidity
/**
* @dev 回调函数，将本合约的调用委托给 `implementation` 合约
* 通过assembly，让回调函数也能有返回值
*/
fallback() external payable {
    address _implementation = implementation;
    assembly {
        // 将msg.data拷贝到内存里
        // calldata操作码的参数: 内存起始位置，calldata起始位置，calldata长度
        calldata(0, 0, calldatasize())

        // 利用delegatecall调用implementation合约
        // delegatecall操作码的参数：gas, 目标合约地址，input mem起始位置，input mem长度，output area mem起始位置，output area mem长度
        // output area起始位置和长度位置，所以设为0
        // delegatecall成功返回1，失败返回0
        let result := delegatecall(gas(), _implementation, 0, calldatasize(), 0, 0)

        // 将return data拷贝到内存
        // returndata操作码的参数：内存起始位置，returndata起始位置，returndata长度
        returndata(0, 0, returndatasize())

        switch result
        // 如果delegate call失败，revert
        case 0 {
            revert(0, returndatasize())
        }
        // 如果delegate call成功，返回mem起始位置为0，长度为returndatasize()的数据（格式为bytes）
        default {
            return(0, returndatasize())
        }
    }
}
```



### 逻辑合约`Logic`

这是一个非常简单的逻辑合约，只是为了演示代理合约。它包含`2`个变量，`1`个事件，`1`个函数：

- `implementation`：占位变量，与`Proxy`合约保持一致，防止插槽冲突。
- `x`：`uint`变量，被设置为`99`。
- `CallSuccess`事件：在调用成功时释放。
- `increment()`函数：会被`Proxy`合约调用，释放`CallSuccess`事件，并返回一个`uint`，它的`selector`为`0xd09de08a`。如果直接调用`increment()`回返回`100`，但是通过`Proxy`调用它会返回`1`，大家可以想想为什么？

```solidity
/**
 * @dev 逻辑合约，执行被委托的调用
 */
contract Logic {
    address public implementation; // 与Proxy保持一致，防止插槽冲突
    uint public x = 99; 
    event CallSuccess(); // 调用成功事件

    // 这个函数会释放CallSuccess事件并返回一个uint。
    // 函数selector: 0xd09de08a
    function increment() external returns(uint) {
        emit CallSuccess();
        return x + 1;
    }
}
```



### 调用者合约`Caller`

`Caller`合约会演示如何调用一个代理合约，它也非常简单。但是要理解它，你需要先学习本教程的[第22讲 Call](https://github.com/AmazingAng/WTF-Solidity/tree/main/22_Call/readme.md)和[第27讲 ABI编码](https://github.com/AmazingAng/WTF-Solidity/tree/main/27_ABIEncode/readme.md)。

它有`1`个变量，`2`个函数：

- `proxy`：状态变量，记录代理合约地址。
- 构造函数：在部署合约时初始化`proxy`变量。
- `increase()`：利用`call`来调用代理合约的`increment()`函数，并返回一个`uint`。在调用时，我们利用`abi.encodeWithSignature()`获取了`increment()`函数的`selector`。在返回时，利用`abi.decode()`将返回值解码为`uint`类型。

```solidity
/**
 * @dev Caller合约，调用代理合约，并获取执行结果
 */
contract Caller{
    address public proxy; // 代理合约地址

    constructor(address proxy_){
        proxy = proxy_;
    }

    // 通过代理合约调用increment()函数
    function increment() external returns(uint) {
        ( , bytes memory data) = proxy.call(abi.encodeWithSignature("increment()"));
        return abi.decode(data,(uint));
    }
}
```



## `Remix`演示

1. 部署`Logic`合约。



![img](https://www.wtf.academy/assets/images/46-2-1110aab3ad36ce4382a829d946675361.jpg)



1. 调用`Logic`合约的`increment()`函数，返回`100`。



![img](https://www.wtf.academy/assets/images/46-3-0d195670b37a431996a2d57fb72c3c83.jpg)



1. 部署`Proxy`合约，初始化时填入`Logic`合约地址。



![img](https://www.wtf.academy/assets/images/46-4-38cde561d4d0557ba06a0a70cbe7b07b.jpg)



1. 调用`Proxy`合约`increment()`函数，无返回值。

   调用方法：在`Remix`部署面板中点`Proxy`合约，在最下面的`Low level interaction`中填入`increment()`函数的选择器`0xd09de08a`，并点击`Transact`。



![img](https://www.wtf.academy/assets/images/46-5-912f07b58b8f1b8a36cdcde67ecf276e.jpg)



1. 部署`Caller`合约，初始化时填入`Proxy`合约地址。



![img](https://www.wtf.academy/assets/images/46-6-a7fbf4a0f32e456f814fd5ad87eb5ba5.jpg)



1. 调用`Caller`合约`increment()`函数，返回`1`。



![img](https://www.wtf.academy/assets/images/46-7-87d87c681f88278a5eeadb3b86621bf5.jpg)



## 总结

这一讲，我们介绍了代理模式和简单的代理合约。代理合约利用`delegatecall`将函数调用委托给了另一个逻辑合约，使得数据和逻辑分别由不同合约负责。并且，它利用内联汇编黑魔法，让没有返回值的回调函数也可以返回数据。前面留给大家的问题是：为什么通过Proxy调用`increment()`会返回1呢？按照我们在[第23讲Delegatecall](https://github.com/AmazingAng/WTF-Solidity/tree/main/23_Delegatecall)中所说的，当Caller合约通过Proxy合约来`delegatecall` Logic合约的时候，如果Logic合约函数改变或读取一些状态变量的时候都会在Proxy的对应变量上操作，而这里Proxy合约的`x`变量的值是0（因为从来没有设置过`x`这个变量，即Proxy合约的storage区域所对应位置值为0），所以通过Proxy调用`increment()`会返回1。

下一讲，我们会介绍可升级代理合约。

代理合约虽然很强大，但是它非常容易出`bug`，用的时候最好直接复制[OpenZeppelin](https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/proxy)的模版合约。

# 47. 可升级合约

这一讲，我们将介绍可升级合约（Upgradeable Contract）。教学用的合约由`OpenZeppelin`中的合约简化而来，可能有安全问题，不要用于生产环境。

## 可升级合约

如果你理解了代理合约，就很容易理解可升级合约。它就是一个可以更改逻辑合约的代理合约。



![可升级模式](https://www.wtf.academy/assets/images/47-1-ebb2200310e0b3fa703ee3cd3bc93d60.png)



## 简单实现

下面我们实现一个简单的可升级合约，它包含`3`个合约：代理合约，旧的逻辑合约，和新的逻辑合约。

### 代理合约

这个代理合约比[第46讲](https://github.com/AmazingAng/WTF-Solidity/blob/main/46_ProxyContract/readme.md)中的简单。我们没有在它的`fallback()`函数中使用`内联汇编`，而仅仅用了`implementation.delegatecall(msg.data);`。因此，回调函数没有返回值，但足够教学使用了。

它包含`3`个变量：

- `implementation`：逻辑合约地址。
- `admin`：admin地址。
- `words`：字符串，可以通过逻辑合约的函数改变。

它包含`3`个函数

- 构造函数：初始化admin和逻辑合约地址。
- `fallback()`：回调函数，将调用委托给逻辑合约。
- `upgrade()`：升级函数，改变逻辑合约地址，只能由`admin`调用。

```solidity
// SPDX-License-Identifier: MIT
// wtf.academy
pragma solidity ^0.8.21;

// 简单的可升级合约，管理员可以通过升级函数更改逻辑合约地址，从而改变合约的逻辑。
// 教学演示用，不要用在生产环境
contract SimpleUpgrade {
    address public implementation; // 逻辑合约地址
    address public admin; // admin地址
    string public words; // 字符串，可以通过逻辑合约的函数改变

    // 构造函数，初始化admin和逻辑合约地址
    constructor(address _implementation){
        admin = msg.sender;
        implementation = _implementation;
    }

    // fallback函数，将调用委托给逻辑合约
    fallback() external payable {
        (bool success, bytes memory data) = implementation.delegatecall(msg.data);
    }

    // 升级函数，改变逻辑合约地址，只能由admin调用
    function upgrade(address newImplementation) external {
        require(msg.sender == admin);
        implementation = newImplementation;
    }
}
```



### 旧逻辑合约

这个逻辑合约包含`3`个状态变量，与保持代理合约一致，防止插槽冲突。它只有一个函数`foo()`，将代理合约中的`words`的值改为`"old"`。

```solidity
// 逻辑合约1
contract Logic1 {
    // 状态变量和proxy合约一致，防止插槽冲突
    address public implementation; 
    address public admin; 
    string public words; // 字符串，可以通过逻辑合约的函数改变

    // 改变proxy中状态变量，选择器： 0xc2985578
    function foo() public{
        words = "old";
    }
}
```



### 新逻辑合约

这个逻辑合约包含`3`个状态变量，与保持代理合约一致，防止插槽冲突。它只有一个函数`foo()`，将代理合约中的`words`的值改为`"new"`。

```solidity
// 逻辑合约2
contract Logic2 {
    // 状态变量和proxy合约一致，防止插槽冲突
    address public implementation; 
    address public admin; 
    string public words; // 字符串，可以通过逻辑合约的函数改变

    // 改变proxy中状态变量，选择器：0xc2985578
    function foo() public{
        words = "new";
    }
}
```



## `Remix`实现

1. 部署新旧逻辑合约`Logic1`和`Logic2`。

   ![47-2.png](https://www.wtf.academy/assets/images/47-2-ccd58960b68460757503f2201cc2ba81.png)

   ![47-3.png](https://www.wtf.academy/assets/images/47-3-74754565513d3c359ff7ddcb2c8aaec6.png)

   

2. 部署可升级合约`SimpleUpgrade`，将`implementation`地址指向把旧逻辑合约。

   ![47-4.png](https://www.wtf.academy/assets/images/47-4-c68f03a4f014f5bbd519d12d5fa57d94.png)

   

3. 利用选择器`0xc2985578`，在代理合约中调用旧逻辑合约`Logic1`的`foo()`函数，将`words`的值改为`"old"`。

   ![47-5.png](https://www.wtf.academy/assets/images/47-5-25a1ee154f04a4640c4a2be5dcad7d11.png)

   

4. 调用`upgrade()`，将`implementation`地址指向新逻辑合约`Logic2`。

   ![47-6.png](https://www.wtf.academy/assets/images/47-6-cdccc3e0d66f34b3de563550112907cd.png)

   

5. 利用选择器`0xc2985578`，在代理合约中调用新逻辑合约`Logic2`的`foo()`函数，将`words`的值改为`"new"`。

   ![47-7.png](https://www.wtf.academy/assets/images/47-7-54c9cdc28e5d2d8d07963cebf50029d5.png)

   

## 总结

这一讲，我们介绍了一个简单的可升级合约。它是一个可以改变逻辑合约的代理合约，给不可更改的智能合约增加了升级功能。但是，这个合约`有选择器冲突`的问题，存在安全隐患。之后我们会介绍解决这一隐患的可升级合约标准：透明代理和`UUPS`。

# 48. 透明代理

这一讲，我们将介绍代理合约的选择器冲突（Selector Clash），以及这一问题的解决方案：透明代理（Transparent Proxy）。教学代码由`OpenZeppelin`的[TransparentUpgradeableProxy](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/proxy/transparent/TransparentUpgradeableProxy.sol)简化而成，不应用于生产。

## 选择器冲突

智能合约中，函数选择器（selector）是函数签名的哈希的前4个字节。例如`mint(address account)`的选择器为`bytes4(keccak256("mint(address)"))`，也就是`0x6a627842`。更多关于选择器的内容见[WTF Solidity极简教程第29讲：函数选择器](https://github.com/AmazingAng/WTF-Solidity/blob/main/29_Selector/readme.md)

由于函数选择器仅有4个字节，范围很小，因此两个不同的函数可能会有相同的选择器，例如下面两个函数：

```solidity
// 选择器冲突的例子
contract Foo {
    function burn(uint256) external {}
    function collate_propagate_storage(bytes16) external {}
}
```





![48-1.png](https://www.wtf.academy/assets/images/48-1-cc33f02644ead30899b1f21626054c4e.png)



示例中，函数`burn()`和`collate_propagate_storage()`的选择器都为`0x42966c68`，是一样的，这种情况被称为“选择器冲突”。在这种情况下，`EVM`无法通过函数选择器分辨用户调用哪个函数，因此该合约无法通过编译。

由于代理合约和逻辑合约是两个合约，就算他们之间存在“选择器冲突”也可以正常编译，这可能会导致很严重的安全事故。举个例子，如果逻辑合约的`a`函数和代理合约的升级函数的选择器相同，那么管理人就会在调用`a`函数的时候，将代理合约升级成一个黑洞合约，后果不堪设想。（当管理员试图调用逻辑合约中的 `a` 函数时，由于选择器冲突，代理合约可能会错误地将调用转发到其 `upgrade` 函数）

目前，有两个可升级合约标准解决了这一问题：透明代理`Transparent Proxy`和通用可升级代理`UUPS`。

## 透明代理

透明代理的逻辑非常简单：管理员可能会因为“函数选择器冲突”，在调用逻辑合约的函数时，误调用代理合约的可升级函数。那么限制管理员的权限，不让他调用任何逻辑合约的函数，就能解决冲突：

- 管理员变为工具人，仅能调用代理合约的可升级函数对合约升级，不能通过回调函数调用逻辑合约。
- 其它用户不能调用可升级函数，但是可以调用逻辑合约的函数。

### 代理合约

这里的代理合约和[第47讲](https://github.com/AmazingAng/WTF-Solidity/blob/main/47_Upgrade/readme.md)的非常相近，只是`fallback()`函数限制了管理员地址的调用。

它包含`3`个变量：

- `implementation`：逻辑合约地址。
- `admin`：admin地址。
- `words`：字符串，可以通过逻辑合约的函数改变。

它包含`3`个函数

- 构造函数：初始化admin和逻辑合约地址。
- `fallback()`：回调函数，将调用委托给逻辑合约，不能由`admin`调用。
- `upgrade()`：升级函数，改变逻辑合约地址，只能由`admin`调用。

```solidity
// 透明可升级合约的教学代码，不要用于生产。
contract TransparentProxy {
    address implementation; // logic合约地址
    address admin; // 管理员
    string public words; // 字符串，可以通过逻辑合约的函数改变

    // 构造函数，初始化admin和逻辑合约地址
    constructor(address _implementation){
        admin = msg.sender;
        implementation = _implementation;
    }

    // fallback函数，将调用委托给逻辑合约
    // 不能被admin调用，避免选择器冲突引发意外
    fallback() external payable {
        require(msg.sender != admin);
        (bool success, bytes memory data) = implementation.delegatecall(msg.data);
    }

    // 升级函数，改变逻辑合约地址，只能由admin调用
    function upgrade(address newImplementation) external {
        if (msg.sender != admin) revert();
        implementation = newImplementation;
    }
}
```

上述代码仍然有一些潜在的问题和改进建议：

1. **没有处理 delegatecall 的失败情况**:

   - 在 

     ```
     fallback
     ```

      函数中，您没有处理 

     ```
     delegatecall
     ```

      的失败情况。这可能会导致外部调用失败而没有任何反馈。可以添加以下代码：

     ```
     require(success, "Delegatecall failed");
     ```

2. **事件记录**:

   - 在执行重要操作时（如升级合约），最好发出事件通知。这有助于后期的调试和监控。例如，在 

     ```
     upgrade
     ```

      函数中可以添加事件：

     ```
     event Upgraded(address newImplementation);
     ```

     然后在函数中发出事件：

     ```
     emit Upgraded(newImplementation);
     ```

3. **安全性最佳实践**:

   - 尽量避免使用 

     ```
     revert()
     ```

      而不提供任何信息，您可以使用自定义的错误消息：

     ```solidity
     require(msg.sender == admin, "Caller is not the admin");
     ```

### 逻辑合约

这里的新、旧逻辑合约与[第47讲](https://github.com/AmazingAng/WTF-Solidity/blob/main/47_Upgrade/readme.md)一样。逻辑合约包含`3`个状态变量，与保持代理合约一致，防止插槽冲突；包含一个函数`foo()`，旧逻辑合约会将`words`的值改为`"old"`，新的会改为`"new"`。

```solidity
// 旧逻辑合约
contract Logic1 {
    // 状态变量和proxy合约一致，防止插槽冲突
    address public implementation; 
    address public admin; 
    string public words; // 字符串，可以通过逻辑合约的函数改变

    // 改变proxy中状态变量，选择器： 0xc2985578
    function foo() public{
        words = "old";
    }
}

// 新逻辑合约
contract Logic2 {
    // 状态变量和proxy合约一致，防止插槽冲突
    address public implementation; 
    address public admin; 
    string public words; // 字符串，可以通过逻辑合约的函数改变

    // 改变proxy中状态变量，选择器：0xc2985578
    function foo() public{
        words = "new";
    }
}
```



## `Remix`实现

1. 部署新旧逻辑合约`Logic1`和`Logic2`。

   ![48-2.png](https://www.wtf.academy/assets/images/48-2-2d933ede25c143886dc303a32b618568.png)

   ![48-3.png](https://www.wtf.academy/assets/images/48-3-4e755768a69f96cc6a61517ead4c91e1.png)

   

2. 部署透明代理合约`TranparentProxy`，将`implementation`地址指向把旧逻辑合约。

   ![48-4.png](https://www.wtf.academy/assets/images/48-4-3a0663b1e73e26e735bfc25b5797c65e.png)

   

3. 利用选择器`0xc2985578`，在代理合约中调用旧逻辑合约`Logic1`的`foo()`函数。调用将失败，因为管理员不能调用逻辑合约。

   ![48-5.png](https://www.wtf.academy/assets/images/48-5-d84ed350e95f14ebdf2b0417ac6598c1.png)

   

4. 切换新钱包，利用选择器`0xc2985578`，在代理合约中调用旧逻辑合约`Logic1`的`foo()`函数，将`words`的值改为`"old"`，调用将成功。

   ![48-6.png](https://www.wtf.academy/assets/images/48-6-073646741cc2cf288b5f3516492b1bf4.png)

   

5. 切换回管理员钱包，调用`upgrade()`，将`implementation`地址指向新逻辑合约`Logic2`。

   ![48-7.png](https://www.wtf.academy/assets/images/48-7-2de214467ecc2a60e3d89b4ce4671388.png)

   

6. 切换新钱包，利用选择器`0xc2985578`，在代理合约中调用新逻辑合约`Logic2`的`foo()`函数，将`words`的值改为`"new"`。

   ![48-8.png](https://www.wtf.academy/assets/images/48-8-576ed455ea9e38821c347a28618b7fe5.png)

   

## 总结

这一讲，我们介绍了代理合约中的“选择器冲突”，以及如何利用透明代理避免这个问题。透明代理的逻辑简单，通过限制管理员调用逻辑合约解决“选择器冲突”问题。它也有缺点，每次用户调用函数时，都会多一步是否为管理员的检查，消耗更多gas。但瑕不掩瑜，透明代理仍是大多数项目方选择的方案。

下一讲，我们会介绍省gas但是也更加复杂的通用可升级代理`UUPS`。

# 49. 通用可升级代理

这一讲，我们将介绍代理合约中选择器冲突（Selector Clash）的另一个解决办法：通用可升级代理（UUPS，universal upgradeable proxy standard）。教学代码由`OpenZeppelin`的`UUPSUpgradeable`简化而成，不应用于生产。

## UUPS

我们在[上一讲](https://github.com/AmazingAng/WTF-Solidity/blob/main/48_TransparentProxy/readme.md)已经学习了"选择器冲突"（Selector Clash），即合约存在两个选择器相同的函数，可能会造成严重后果。作为透明代理的替代方案，UUPS也能解决这一问题。

UUPS（universal upgradeable proxy standard，通用可升级代理）将升级函数放在逻辑合约中。这样一来，如果有其它函数与升级函数存在“选择器冲突”，编译时就会报错。

下表中概括了普通可升级合约，透明代理，和UUPS的不同点：



![各类个升级合约](https://www.wtf.academy/assets/images/49-1-6d28dd55317040f7cbd5866bd4ec613d.png)



## UUPS合约

首先我们要复习一下[WTF Solidity极简教程第23讲：Delegatecall](https://github.com/AmazingAng/WTF-Solidity/blob/main/23_Delegatecall/readme.md)。如果用户A通过合约B（代理合约）去`delegatecall`合约C（逻辑合约），上下文仍是合约B的上下文，`msg.sender`仍是用户A而不是合约B。因此，UUPS合约可以将升级函数放在逻辑合约中，并检查调用者是否为管理员。



![delegatecall](https://www.wtf.academy/assets/images/49-2-f49e18de33692532b7b8aed640212fe3.png)



### UUPS的代理合约

UUPS的代理合约看起来像是个不可升级的代理合约，非常简单，因为升级函数被放在了逻辑合约中。它包含`3`个变量：

- `implementation`：逻辑合约地址。
- `admin`：admin地址。
- `words`：字符串，可以通过逻辑合约的函数改变。

它包含`2`个函数

- 构造函数：初始化admin和逻辑合约地址。
- `fallback()`：回调函数，将调用委托给逻辑合约。

```solidity
contract UUPSProxy {
    address public implementation; // 逻辑合约地址
    address public admin; // admin地址
    string public words; // 字符串，可以通过逻辑合约的函数改变

    // 构造函数，初始化admin和逻辑合约地址
    constructor(address _implementation){
        admin = msg.sender;
        implementation = _implementation;
    }

    // fallback函数，将调用委托给逻辑合约
    fallback() external payable {
        (bool success, bytes memory data) = implementation.delegatecall(msg.data);
    }
}
```



### UUPS的逻辑合约

UUPS的逻辑合约与[第47讲](https://github.com/AmazingAng/WTF-Solidity/blob/main/47_Upgrade/readme.md)中的不同是多了个升级函数。UUPS逻辑合约包含`3`个状态变量，与保持代理合约一致，防止插槽冲突。它包含`2`个

- `upgrade()`：升级函数，将改变逻辑合约地址`implementation`，只能由`admin`调用。
- `foo()`：旧UUPS逻辑合约会将`words`的值改为`"old"`，新的会改为`"new"`。

```solidity
// UUPS逻辑合约（升级函数写在逻辑合约内）
contract UUPS1{
    // 状态变量和proxy合约一致，防止插槽冲突
    address public implementation; 
    address public admin; 
    string public words; // 字符串，可以通过逻辑合约的函数改变

    // 改变proxy中状态变量，选择器： 0xc2985578
    function foo() public{
        words = "old";
    }

    // 升级函数，改变逻辑合约地址，只能由admin调用。选择器：0x0900f010
    // UUPS中，逻辑合约中必须包含升级函数，不然就不能再升级了。
    function upgrade(address newImplementation) external {
        require(msg.sender == admin);
        implementation = newImplementation;
    }
}

// 新的UUPS逻辑合约
contract UUPS2{
    // 状态变量和proxy合约一致，防止插槽冲突
    address public implementation; 
    address public admin; 
    string public words; // 字符串，可以通过逻辑合约的函数改变

    // 改变proxy中状态变量，选择器： 0xc2985578
    function foo() public{
        words = "new";
    }

    // 升级函数，改变逻辑合约地址，只能由admin调用。选择器：0x0900f010
    // UUPS中，逻辑合约中必须包含升级函数，不然就不能再升级了。
    function upgrade(address newImplementation) external {
        require(msg.sender == admin);
        implementation = newImplementation;
    }
}
```



## `Remix`实现

1. 部署UUPS新旧逻辑合约`UUPS1`和`UUPS2`。



![demo](https://www.wtf.academy/assets/images/49-3-58cd3d8f3ea3c5a13d5a30e811ec066b.jpg)



1. 部署UUPS代理合约`UUPSProxy`，将`implementation`地址指向旧逻辑合约`UUPS1`。



![demo](https://www.wtf.academy/assets/images/49-4-b9370b74616a320c5ca485fb671fb40d.jpg)



1. 利用选择器`0xc2985578`，在代理合约中调用旧逻辑合约`UUPS1`的`foo()`函数，将`words`的值改为`"old"`。



![demo](https://www.wtf.academy/assets/images/49-5-7bc8fe4a2e94e5b8879194661b8c49cf.jpg)



1. 利用在线ABI编码器[HashEx](https://abi.hashex.org/)获得二进制编码，调用升级函数`upgrade()`，将`implementation`地址指向新逻辑合约`UUPS2`。



![编码](https://www.wtf.academy/assets/images/49-3-0b950623ffe1b3b82c7f9051e1bc58b6.png)





![demo](https://www.wtf.academy/assets/images/49-6-8ee85b7877953e433784f6a3504f9ad3.jpg)



1. 利用选择器`0xc2985578`，在代理合约中调用新逻辑合约`UUPS2`的`foo()`函数，将`words`的值改为`"new"`。



![demo](https://www.wtf.academy/assets/images/49-7-9d0569ae2479a42875792c04e2ba39e3.jpg)



## 总结

这一讲，我们介绍了代理合约“选择器冲突”的另一个解决方案：UUPS。与透明代理不同，UUPS将升级函数放在了逻辑合约中，从而使得"选择器冲突"不能通过编译。相比透明代理，UUPS更省gas，但也更复杂。

# 50. 多签钱包

V神曾说过，多签钱包要比硬件钱包更加安全（[推文](https://twitter.com/VitalikButerin/status/1558886893995134978?s=20&t=4WyoEWhwHNUtAuABEIlcRw)）。这一讲，我们将介绍多签钱包，并且写一个极简版多签钱包合约。教学代码（150行代码）由gnosis safe合约（几千行代码）简化而成。



![V神说](https://www.wtf.academy/assets/images/50-1-284acc58760abb75b1a1af092692df11.png)



## 多签钱包

多签钱包是一种电子钱包，特点是交易被多个私钥持有者（多签人）授权后才能执行：例如钱包由`3`个多签人管理，每笔交易需要至少`2`人签名授权。多签钱包可以防止单点故障（私钥丢失，单人作恶），更加去中心化，更加安全，被很多DAO采用。

Gnosis Safe多签钱包是以太坊最流行的多签钱包，管理近400亿美元资产，合约经过审计和实战测试，支持多链（以太坊，BSC，Polygon等），并提供丰富的DAPP支持。更多信息可以阅读我在21年12月写的[Gnosis Safe使用教程](https://peopledao.mirror.xyz/nFCBXda8B5ZxQVqSbbDOn2frFDpTxNVtdqVBXGIjj0s)。

## 多签钱包合约

在以太坊上的多签钱包其实是智能合约，属于合约钱包。下面我们写一个极简版多签钱包`MultisigWallet`合约，它的逻辑非常简单：

1. 设置多签人和门槛（链上）：部署多签合约时，我们需要初始化多签人列表和执行门槛（至少n个多签人签名授权后，交易才能执行）。Gnosis Safe多签钱包支持增加/删除多签人以及改变执行门槛，但在咱们的极简版中不考虑这一功能。

2. 创建交易（链下）：一笔待授权的交易包含以下内容

   - `to`：目标合约。
   - `value`：交易发送的以太坊数量。
   - `data`：calldata，包含调用函数的选择器和参数。
   - `nonce`：初始为`0`，随着多签合约每笔成功执行的交易递增的值，可以防止签名重放攻击。
   - `chainid`：链id，防止不同链的签名重放攻击。

3. 收集多签签名（链下）：将上一步的交易ABI编码并计算哈希，得到交易哈希，然后让多签人签名，并拼接到一起的到打包签名。对ABI编码和哈希不了解的，可以看WTF Solidity极简教程[第27讲](https://github.com/AmazingAng/WTF-Solidity/blob/main/27_ABIEncode/readme.md)和[第28讲](https://github.com/AmazingAng/WTF-Solidity/blob/main/28_Hash/readme.md)。

   ```solidity
   交易哈希: 0xc1b055cf8e78338db21407b425114a2e258b0318879327945b661bfdea570e66
   
   多签人A签名: 0x014db45aa753fefeca3f99c2cb38435977ebb954f779c2b6af6f6365ba4188df542031ace9bdc53c655ad2d4794667ec2495196da94204c56b1293d0fbfacbb11c
   
   多签人B签名: 0xbe2e0e6de5574b7f65cad1b7062be95e7d73fe37dd8e888cef5eb12e964ddc597395fa48df1219e7f74f48d86957f545d0fbce4eee1adfbaff6c267046ade0d81c
   
   打包签名：
   0x014db45aa753fefeca3f99c2cb38435977ebb954f779c2b6af6f6365ba4188df542031ace9bdc53c655ad2d4794667ec2495196da94204c56b1293d0fbfacbb11cbe2e0e6de5574b7f65cad1b7062be95e7d73fe37dd8e888cef5eb12e964ddc597395fa48df1219e7f74f48d86957f545d0fbce4eee1adfbaff6c267046ade0d81c
   ```

   

4. 调用多签合约的执行函数，验证签名并执行交易（链上）。对验证签名和执行交易不了解的，可以看WTF Solidity极简教程[第22讲](https://github.com/AmazingAng/WTF-Solidity/blob/main/22_Call/readme.md)和[第37讲](https://github.com/AmazingAng/WTF-Solidity/blob/main/37_Signature/readme.md)。

### 事件

`MultisigWallet`合约有`2`个事件，`ExecutionSuccess`和`ExecutionFailure`，分别在交易成功和失败时释放，参数为交易哈希。

```solidity
    event ExecutionSuccess(bytes32 txHash);    // 交易成功事件
    event ExecutionFailure(bytes32 txHash);    // 交易失败事件
```



### 状态变量

`MultisigWallet`合约有`5`个状态变量：

1. `owners`：多签持有人数组
2. `isOwner`：`address => bool`的映射，记录一个地址是否为多签持有人。
3. `ownerCount`：多签持有人数量
4. `threshold`：多签执行门槛，交易至少有n个多签人签名才能被执行。
5. `nonce`：初始为`0`，随着多签合约每笔成功执行的交易递增的值，可以防止签名重放攻击。

```solidity
    address[] public owners;                   // 多签持有人数组 
    mapping(address => bool) public isOwner;   // 记录一个地址是否为多签持有人
    uint256 public ownerCount;                 // 多签持有人数量
    uint256 public threshold;                  // 多签执行门槛，交易至少有n个多签人签名才能被执行。
    uint256 public nonce;                      // nonce，防止签名重放攻击
```



### 函数

`MultisigWallet`合约有`6`个函数：

1. 构造函数：调用`_setupOwners()`，初始化和多签持有人和执行门槛相关的变量。

   ```solidity
   // 构造函数，初始化owners, isOwner, ownerCount, threshold 
   constructor(        
       address[] memory _owners,
       uint256 _threshold
   ) {
       _setupOwners(_owners, _threshold);
   }
   ```

   

2. `_setupOwners()`：在合约部署时被构造函数调用，初始化`owners`，`isOwner`，`ownerCount`，`threshold`状态变量。传入的参数中，执行门槛需大于等于`1`且小于等于多签人数；多签地址不能为`0`地址且不能重复。

   ```solidity
   /// @dev 初始化owners, isOwner, ownerCount,threshold 
   /// @param _owners: 多签持有人数组
   /// @param _threshold: 多签执行门槛，至少有几个多签人签署了交易
   function _setupOwners(address[] memory _owners, uint256 _threshold) internal {
       // threshold没被初始化过
       require(threshold == 0, "WTF5000");
       // 多签执行门槛 小于 多签人数
       require(_threshold <= _owners.length, "WTF5001");
       // 多签执行门槛至少为1
       require(_threshold >= 1, "WTF5002");
   
       for (uint256 i = 0; i < _owners.length; i++) {
           address owner = _owners[i];
           // 多签人不能为0地址，本合约地址，不能重复
           require(owner != address(0) && owner != address(this) && !isOwner[owner], "WTF5003");
           owners.push(owner);
           isOwner[owner] = true;
       }
       ownerCount = _owners.length;
       threshold = _threshold;
   }
   ```

   > [!NOTE]
   >
   > 主要逻辑说明
   >
   > 1. 执行门槛检查
   >
   > 2. 遍历 `_owners` 数组并进行验证
   >
   > 3. ```solidity
   >    for (uint256 i = 0; i < _owners.length; i++) {
   >        address owner = _owners[i];
   >        require(owner != address(0) && owner != address(this) && !isOwner[owner], "WTF5003");
   >        owners.push(owner);
   >        isOwner[owner] = true;
   >    }
   >    
   >    ```
   >
   >    - 该 `for` 循环遍历每一个持有人地址，确保每个地址满足以下条件：
   >
   >    1. **不能为零地址**：`address(0)` 通常代表无效地址，不能作为持有人。
   >    2. **不能为合约自身地址**：避免合约的逻辑混乱，合约不能自己作为多签持有人。
   >    3. **不能重复**：每个持有人只能出现一次，防止一个地址多次添加。
   >
   >    如果任意条件不满足，则抛出 `WTF5003` 错误。否则，将持有人地址加入到 `owners` 数组中，并将 `isOwner[owner]` 设为 `true`，标记该地址为合法的多签持有人。
   >
   > 4. 设置状态变量
   >
   >    - 遍历完所有持有人地址后，将 `ownerCount` 设置为持有人数组的长度，表示持有人总数。然后设置 `threshold`，代表需要多少个签名才能执行交易。
   >
   > 错误码解释
   >
   > - `WTF5000`: 表示 `threshold` 已经初始化，不能再次初始化。
   > - `WTF5001`: 表示签名执行门槛大于持有人数量，不合理。
   > - `WTF5002`: 表示签名执行门槛不能小于 1。
   > - `WTF5003`: 表示持有人地址无效，如为零地址、合约地址或重复地址。

   

3. `execTransaction()`：在收集足够的多签签名后，验证签名并执行交易。传入的参数为目标地址`to`，发送的以太坊数额`value`，数据`data`，以及打包签名`signatures`。打包签名就是将收集的多签人对交易哈希的签名，按多签持有人地址从小到大顺序，打包到一个[bytes]数据中。这一步调用了`encodeTransactionData()`编码交易，调用了`checkSignatures()`检验签名是否有效、数量是否达到执行门槛。

   ```solidity
   /// @dev 在收集足够的多签签名后，执行交易
   /// @param to 目标合约地址
   /// @param value msg.value，支付的以太坊
   /// @param data calldata
   /// @param signatures 打包的签名，对应的多签地址由小到达，方便检查。 ({bytes32 r}{bytes32 s}{uint8 v}) (第一个多签的签名, 第二个多签的签名 ... )
   function execTransaction(
       address to,
       uint256 value,
       bytes memory data,
       bytes memory signatures
   ) public payable virtual returns (bool success) {
       // 编码交易数据，计算哈希
       bytes32 txHash = encodeTransactionData(to, value, data, nonce, block.chainid);
       nonce++;  // 增加nonce
       checkSignatures(txHash, signatures); // 检查签名
       // 利用call执行交易，并获取交易结果
       (success, ) = to.call{value: value}(data);
       require(success , "WTF5004");
       if (success) emit ExecutionSuccess(txHash);
       else emit ExecutionFailure(txHash);
   }
   ```

   > [!NOTE]
   >
   > 这段 `execTransaction` 函数是多签钱包中用于执行交易的核心部分。当足够的签名被收集后，该函数将目标合约地址、以太坊金额以及交易数据打包并执行。让我们详细解析每一步的功能：
   >
   > 函数参数
   >
   > 1. `address to`: 目标合约地址，表示将要进行交易的接收者地址。
   > 2. `uint256 value`: 交易中将要支付的以太币数量，即 `msg.value`。
   > 3. `bytes memory data`: 调用目标合约所需要的 `calldata`，通常是合约函数的调用参数。
   > 4. `bytes memory signatures`: 已经收集到的多签持有人的签名，按顺序排列，每个签名使用 `(r, s, v)` 格式。
   >
   > 函数步骤解析
   >
   > 1. **编码交易数据并计算哈希：**
   >
   >    ```solidity
   >    bytes32 txHash = encodeTransactionData(to, value, data, nonce, block.chainid);
   >    nonce++;  // 增加nonce
   >    ```
   >
   >    - `txHash`: 使用 `encodeTransactionData` 函数对交易数据（目标地址、以太坊数量、调用数据、`nonce`、链ID）进行编码并计算哈希。这个哈希值将用于签名验证。
   >    - `nonce`: 每次交易执行后 `nonce` 自增，保证每笔交易都有唯一的哈希，防止重放攻击。
   >    - `block.chainid`: 区块链的链 ID 是为了确保交易只在特定的链上有效，防止跨链重放攻击。
   >
   > 2. **检查签名：**
   >
   >    ```solidity
   >    checkSignatures(txHash, signatures); // 检查签名
   >    ```
   >
   >    - `checkSignatures`: 验证 `signatures` 中的签名是否有效，即检查每个签名是否是多签持有人的有效签名，确保持有人的批准。如果验证失败，交易会被拒绝。
   >
   > 3. **利用 `call` 执行交易并获取交易结果：**
   >
   >    ```solidity
   >    (success, ) = to.call{value: value}(data);
   >    require(success , "WTF5004");
   >    ```
   >
   >    - 使用 `call` 来调用目标合约，并附带 `msg.value` 中指定的以太币。这个调用可能会执行目标合约的某个函数，传入的数据即为 `data`。
   >    - `success`: 该变量记录交易是否成功执行。如果执行失败，将抛出错误 `WTF5004` 并终止交易。
   >
   > 4. **记录并发出交易结果事件：**
   >
   >    ```solidity
   >    if (success) emit ExecutionSuccess(txHash);
   >    else emit ExecutionFailure(txHash);
   >    ```
   >
   >    - `emit ExecutionSuccess(txHash)`: 如果交易执行成功，发出 `ExecutionSuccess` 事件，记录交易哈希。
   >    - `emit ExecutionFailure(txHash)`: 如果交易失败，发出 `ExecutionFailure` 事件，通知交易失败，并将其交易哈希存储在事件中以供分析和调试。
   >
   > 错误码
   >
   > - **WTF5004**: 当调用目标合约的 `call` 操作失败时，抛出该错误，表示交易未成功。
   >
   > 总结
   >
   > `execTransaction` 是多签钱包中执行交易的关键函数。它会：
   >
   > 1. 通过 `encodeTransactionData` 生成唯一的交易哈希值，确保交易的唯一性。
   > 2. 验证多签持有人对交易的签名是否合法。
   > 3. 使用 `call` 来执行交易，将以太币和 `calldata` 传递到目标合约。
   > 4. 交易成功时发出成功事件，失败时发出失败事件。

   

4. `checkSignatures()`：检查签名和交易数据的哈希是否对应，数量是否达到门槛，若否，交易会revert。单个签名长度为65字节，因此打包签名的长度要长于`threshold * 65`。调用了`signatureSplit()`分离出单个签名。这个函数的大致思路：

   - 用ecdsa获取签名地址.
   - 利用 `currentOwner > lastOwner` 确定签名来自不同多签（多签地址递增）。
   - 利用`isOwner[currentOwner]`确定签名者为多签持有人。

   ```solidity
   /**
    * @dev 检查签名和交易数据是否对应。如果是无效签名，交易会revert
    * @param dataHash 交易数据哈希
    * @param signatures 几个多签签名打包在一起
    */
   function checkSignatures(
       bytes32 dataHash,
       bytes memory signatures
   ) public view {
       // 读取多签执行门槛
       uint256 _threshold = threshold;
       require(_threshold > 0, "WTF5005");
   
       // 检查签名长度足够长
       require(signatures.length >= _threshold * 65, "WTF5006");
   
       // 通过一个循环，检查收集的签名是否有效
       // 大概思路：
       // 1. 用ecdsa先验证签名是否有效
       // 2. 利用 currentOwner > lastOwner 确定签名来自不同多签（多签地址递增）
       // 3. 利用 isOwner[currentOwner] 确定签名者为多签持有人
       address lastOwner = address(0); 
       address currentOwner;
       uint8 v;
       bytes32 r;
       bytes32 s;
       uint256 i;
       for (i = 0; i < _threshold; i++) {
           (v, r, s) = signatureSplit(signatures, i);
           // 利用ecrecover检查签名是否有效
           currentOwner = ecrecover(keccak256(abi.encodePacked("\x19Ethereum Signed Message:\n32", dataHash)), v, r, s);
           require(currentOwner > lastOwner && isOwner[currentOwner], "WTF5007");
           lastOwner = currentOwner;
       }
   }
   ```

   > [!NOTE]
   >
   > 这段代码用于检查多签钱包中签名的有效性，确保收集到的签名满足执行交易的门槛。具体思路如下：
   >
   > ### 函数参数
   >
   > 1. **`bytes32 dataHash`**: 交易数据的哈希值，是需要验证的内容。通过将交易数据编码并哈希得到。
   > 2. **`bytes memory signatures`**: 多个多签持有人的签名被打包在一起，每个签名由 `v`, `r`, `s` 组成，总长度是 `threshold * 65` 字节。
   >
   > ### 具体逻辑解析
   >
   > 1. **检查签名门槛是否大于0：**
   >
   >    ```solidity
   >    uint256 _threshold = threshold;
   >    require(_threshold > 0, "WTF5005");
   >    ```
   >
   >    - 读取合约中设置的多签执行门槛 `threshold`。如果门槛为 0，交易无效。
   >
   > 2. **验证签名长度：**
   >
   >    ```solidity
   >    require(signatures.length >= _threshold * 65, "WTF5006");
   >    ```
   >
   >    - 每个签名由 `65` 字节组成，打包的签名长度应该不小于 `threshold * 65`，即至少包含满足门槛数量的签名。
   >
   > 3. **通过循环逐一验证签名：**
   >
   >    ```solidity
   >    address lastOwner = address(0); 
   >    address currentOwner;
   >    uint8 v;
   >    bytes32 r;
   >    bytes32 s;
   >    uint256 i;
   >    for (i = 0; i < _threshold; i++) {
   >        (v, r, s) = signatureSplit(signatures, i);
   >        currentOwner = ecrecover(keccak256(abi.encodePacked("\x19Ethereum Signed Message:\n32", dataHash)), v, r, s);
   >        require(currentOwner > lastOwner && isOwner[currentOwner], "WTF5007");
   >        lastOwner = currentOwner;
   >    }
   >    ```
   >
   >    - **循环迭代签名**：通过 `signatureSplit()` 函数来拆分打包的签名，得到 `v`, `r`, `s` 三个部分。
   >    - **签名验证**：使用 `ecrecover` 函数从签名中恢复出签名者的地址。`ecrecover` 是一个 Solidity 内置函数，通过 `(v, r, s)` 来从消息的哈希中还原签名者。
   >      - `keccak256(abi.encodePacked("\x19Ethereum Signed Message:\n32", dataHash))` 这一步是对数据哈希进行签名前的标准处理，符合以太坊 EIP-191 签名格式，确保与用户实际签名的消息匹配。
   >    - **确保签名者是多签持有人**：签名者必须是 `isOwner` 数组中的合法多签持有人，否则交易将被拒绝（`WTF5007`）。
   >    - **防止签名重复**：签名地址必须递增 (`currentOwner > lastOwner`)，确保每个签名都来自不同的多签持有人，这样可以防止同一个持有人重复签名。
   >    - **更新 `lastOwner`**：每次验证一个签名后，将其设置为 `lastOwner`，保证下一次循环的持有人地址递增。
   >
   > ### 错误码
   >
   > - **WTF5005**: 当 `threshold` 为 0 时抛出，说明没有设置有效的多签门槛。
   > - **WTF5006**: 当签名长度不足以满足门槛要求时抛出，表明签名数量不够。
   > - **WTF5007**: 当签名不符合条件（例如地址不在多签持有人列表或签名顺序不符合递增要求）时抛出。
   >
   > ### 总结
   >
   > `checkSignatures` 函数确保每个签名都经过验证，且签名者是合法的多签持有人。它通过递增的签名顺序和签名地址验证来保证交易的安全性，并通过 `ecrecover` 来检查签名的有效性。如果签名不满足条件或顺序错误，交易将会被 `revert`，保证安全性。

   

5. `signatureSplit()`：将单个签名从打包的签名分离出来，参数分别为打包签名`signatures`和要读取的签名位置`pos`。利用了内联汇编，将签名的`r`，`s`，和`v`三个值分离出来。

   ```solidity
   /// 将单个签名从打包的签名分离出来
   /// @param signatures 打包签名
   /// @param pos 要读取的多签index.
   function signatureSplit(bytes memory signatures, uint256 pos)
       internal
       pure
       returns (
           uint8 v,
           bytes32 r,
           bytes32 s
       )
   {
       // 签名的格式：{bytes32 r}{bytes32 s}{uint8 v}
       assembly {
           let signaturePos := mul(0x41, pos)
           r := mload(add(signatures, add(signaturePos, 0x20)))
           s := mload(add(signatures, add(signaturePos, 0x40)))
           v := and(mload(add(signatures, add(signaturePos, 0x41))), 0xff)
       }
   }
   ```

   > [!NOTE]
   >
   > `signatureSplit()` 函数通过内联汇编（`assembly`）将单个签名从打包的签名数据中分离出来，分别获取签名的 `r`、`s` 和 `v` 值。这些值用于通过 `ecrecover` 恢复签名者地址。
   >
   > ### 参数解析
   >
   > - **`signatures`**: 多个打包在一起的签名数据。
   > - **`pos`**: 当前要读取的签名在打包数据中的索引位置。因为签名是按顺序排列的，所以需要根据 `pos` 确定签名的位置。
   >
   > ### 签名结构
   >
   > 在以太坊中，ECDSA 签名的标准格式是：
   >
   > - **`r`**: 32字节。
   > - **`s`**: 32字节。
   > - **`v`**: 1字节。
   >
   > 每个签名占 65 字节，其中 `r` 和 `s` 为 32 字节，`v` 为 1 字节。
   >
   > ### 内联汇编解析
   >
   > 内联汇编通过 `mload` 指令从 `signatures` 中提取 `r`、`s` 和 `v` 值。代码中进行了如下操作：
   >
   > ```solidity
   > let signaturePos := mul(0x41, pos)
   > ```
   >
   > - 每个签名占 `0x41`（即 65）字节，`signaturePos` 计算当前签名的起始位置，`pos` 代表签名的索引。
   >
   > ```solidity
   > r := mload(add(signatures, add(signaturePos, 0x20)))
   > ```
   >
   > - 通过 `mload` 从打包的签名数据中加载 `r` 的值。`add(signatures, 0x20)` 表示在打包数据的起点处移动 32 字节偏移（Solidity 的动态数组存储数据的第一项是长度），再加上 `signaturePos` 来定位具体的签名。
   >
   > ```solidity
   > s := mload(add(signatures, add(signaturePos, 0x40)))
   > ```
   >
   > - 通过 `mload` 获取 `s` 值，这里我们偏移了 64 字节（`0x40`），即跳过了 `r` 的32字节。
   >
   > ```solidity
   > v := and(mload(add(signatures, add(signaturePos, 0x41))), 0xff)
   > ```
   >
   > - 获取 `v` 的值，它位于签名的第 65 字节。使用 `and` 与 `0xff` 进行按位与操作，是为了确保只获取 `v` 的低 8 位。
   >
   > ### 总结
   >
   > `signatureSplit()` 函数通过内联汇编逐一从打包的签名数据中提取出 ECDSA 签名的 `r`、`s` 和 `v`，方便后续利用这些值进行签名验证。

   

6. `encodeTransactionData()`：将交易数据打包并计算哈希，利用了`abi.encode()`和`keccak256()`函数。这个函数可以计算出一个交易的哈希，然后在链下让多签人签名并收集，再调用`execTransaction()`函数执行。

   ```solidity
   /// @dev 编码交易数据
   /// @param to 目标合约地址
   /// @param value msg.value，支付的以太坊
   /// @param data calldata
   /// @param _nonce 交易的nonce.
   /// @param chainid 链id
   /// @return 交易哈希bytes.
   function encodeTransactionData(
       address to,
       uint256 value,
       bytes memory data,
       uint256 _nonce,
       uint256 chainid
   ) public pure returns (bytes32) {
       bytes32 safeTxHash =
           keccak256(
               abi.encode(
                   to,
                   value,
                   keccak256(data),
                   _nonce,
                   chainid
               )
           );
       return safeTxHash;
   }
   ```

   > [!NOTE]
   >
   > `encodeTransactionData()` 函数用于对一笔交易进行编码，计算出其哈希值（`hash`），以便用于多签名验证。在链下收集多签人对交易哈希的签名后，可以通过 `execTransaction()` 函数在链上执行交易。这个函数在多签钱包中非常常见，确保交易的不可篡改性。
   >
   > ### 参数解析
   > - **`to`**: 交易的目标合约地址，表示要调用的合约或接收以太坊的地址。
   > - **`value`**: 交易中传递的以太币数量（`msg.value`）。
   > - **`data`**: 传递给目标合约的 `calldata`，包含具体的函数调用和参数。
   > - **`_nonce`**: 用于防止重放攻击的 nonce 值。每笔交易的 nonce 必须唯一，确保相同交易不会重复执行。
   > - **`chainid`**: 当前链的链 ID，用来防止跨链重放攻击。
   >
   > ### 编码与哈希计算过程
   > 1. **编码交易数据**：
   >    ```solidity
   >    abi.encode(to, value, keccak256(data), _nonce, chainid)
   >    ```
   >    - 这里使用 `abi.encode()` 将交易的多个参数组合成一个二进制序列。
   >    - `data`（即 `calldata`）被 `keccak256` 哈希后再进行编码，避免直接将原始的 `calldata` 编码，因为数据可能非常长且复杂。
   >    - `abi.encode()` 是 Solidity 提供的内建函数，用于将多个参数序列化为标准的二进制格式。
   >
   > 2. **计算哈希**：
   >    ```solidity
   >    keccak256(abi.encode(...))
   >    ```
   >    - 整个编码后的数据通过 `keccak256` 哈希算法计算出交易的哈希值，这个哈希值就是该交易的唯一标识符。
   >
   > 3. **返回哈希值**：
   >    ```solidity
   >    return safeTxHash;
   >    ```
   >    - 返回的 `safeTxHash` 是交易的哈希，后续可以用于验证签名或其他用途。
   >
   > ### 函数作用
   > 这个函数生成的哈希值用于以下用途：
   > - **签名验证**：多签人可以根据该哈希离线签署该笔交易，收集足够的签名后，合约才能执行该笔交易。
   > - **防篡改**：通过哈希计算保证交易数据完整，任何修改都会导致不同的哈希，从而使签名无效。
   > - **防止重放攻击**：结合 `nonce` 和 `chainid`，可以防止相同交易在不同链或多次重复执行。
   
   

## `Remix`演示

1. 部署多签合约，`2`个多签地址，交易执行门槛设为`2`。

   ```solidity
   多签地址1: 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4
   多签地址2: 0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2
   ```

   

   

   ![部署](https://www.wtf.academy/assets/images/50-2-d5cc6acfb8fc899b88e84b9bddd33552.png)

   

2. 转账`1 ETH`到多签合约地址。

   

   ![转账](https://www.wtf.academy/assets/images/50-3-475a0c198952a20ba3abd4404c57fe88.png)

   

3. 调用`encodeTransactionData()`，编码并计算向多签地址1转账`1 ETH`的交易哈希。

   ```solidity
   参数
   to: 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4
   value: 1000000000000000000
   data: 0x
   _nonce: 0
   chainid: 1
   
   结果
   交易哈希： 0xb43ad6901230f2c59c3f7ef027c9a372f199661c61beeec49ef5a774231fc39b
   ```

   

   

   ![计算交易哈希](https://www.wtf.academy/assets/images/50-4-b7466a86a9352531cfd532542d67a52c.png)

   

4. 利用Remix中ACCOUNT旁边的笔记图案的按钮进行签名，内容输入上面的交易哈希，获得签名，两个钱包都要签。

   ```text
   多签地址1的签名: 0xa3f3e4375f54ad0a8070f5abd64e974b9b84306ac0dd5f59834efc60aede7c84454813efd16923f1a8c320c05f185bd90145fd7a7b741a8d13d4e65a4722687e1b
   
   多签地址2的签名: 0x6b228b6033c097e220575f826560226a5855112af667e984aceca50b776f4c885e983f1f2155c294c86a905977853c6b1bb630c488502abcc838f9a225c813811c
   
   讲两个签名拼接到一起，得到打包签名:  0xa3f3e4375f54ad0a8070f5abd64e974b9b84306ac0dd5f59834efc60aede7c84454813efd16923f1a8c320c05f185bd90145fd7a7b741a8d13d4e65a4722687e1b6b228b6033c097e220575f826560226a5855112af667e984aceca50b776f4c885e983f1f2155c294c86a905977853c6b1bb630c488502abcc838f9a225c813811c
   ```

   

   

   ![签名](https://www.wtf.academy/assets/images/50-5-0e84c3861502f80d740ed8d7bf31fcff.png)

   

5. 调用`execTransaction()`函数执行交易，将第3步中的交易参数和打包签名作为参数传入。可以看到交易执行成功，`ETH`被转出多签。

   

   ![执行多签钱包交易](https://www.wtf.academy/assets/images/50-6-8d28ef5e86f95f5d5edeb6d6ffc448f1.png)

   

## 总结

这一讲，我们介绍了多签钱包，并写了一个极简版的多签钱包合约，仅有不到150行代码。

我与多签钱包很有缘分，2021年因为PeopleDAO创建国库而学习了Gnosis Safe并写了中英文的[使用教程](https://peopledao.mirror.xyz/nFCBXda8B5ZxQVqSbbDOn2frFDpTxNVtdqVBXGIjj0s)，之后很幸运的做了3个国库的多签人维护资产安全，现在又成为了Safe的守护者深度参与治理。希望大家的资产都更加安全。

# 51. ERC4626 代币化金库标准

我们经常说 DeFi 是货币乐高，可以通过组合多个协议来创造新的协议；但由于 DeFi 缺乏标准，严重影响了它的可组合性。而 ERC4626 扩展了 ERC20 代币标准，旨在推动收益金库的标准化。这一讲，我们将介绍 DeFi 新一代标准 ERC4626，并写一个简单的金库合约。教学代码参考 openzeppelin 和 solmate 中的 ERC4626 合约，仅用作教学。

## 金库

金库合约是 DeFi 乐高中的基础，它允许你把基础资产（代币）质押到合约中，换取一定收益，包括以下应用场景:

- 收益农场: 在 Yearn Finance 中，你可以质押 `USDT` 获取利息。
- 借贷: 在 AAVE 中，你可以出借 `ETH` 获取存款利息和贷款。
- 质押: 在 Lido 中，你可以质押 `ETH` 参与 ETH 2.0 质押，得到可以生息的 `stETH`。

## ERC4626



![img](https://www.wtf.academy/assets/images/51-1-84f12e4d93a3689acc7ee1a5802cdbaf.png)



由于金库合约缺乏标准，写法五花八门，一个收益聚合器需要写很多接口对接不同的 DeFi 项目。ERC4626 代币化金库标准（Tokenized Vault Standard）横空出世，使得 DeFi 能够轻松扩展。它具有以下优点:

1. 代币化: ERC4626 继承了 ERC20，向金库存款时，将得到同样符合 ERC20 标准的金库份额，比如质押 ETH，自动获得 stETH。
2. 更好的流通性: 由于代币化，你可以在不取回基础资产的情况下，利用金库份额做其他事情。拿 Lido 的 stETH 为例，你可以用它在 Uniswap 上提供流动性或交易，而不需要取出其中的 ETH。
3. 更好的可组合性: 有了标准之后，用一套接口可以和所有 ERC4626 金库交互，让基于金库的应用、插件、工具开发更容易。

总而言之，ERC4626 对于 DeFi 的重要性不亚于 ERC721 对于 NFT 的重要性。

### ERC4626 要点

ERC4626 标准主要实现了一下几个逻辑：

1. ERC20: ERC4626 继承了 ERC20，金库份额就是用 ERC20 代币代表的：用户将特定的 ERC20 基础资产（比如 WETH）存进金库，合约会给他铸造特定数量的金库份额代币；当用户从金库中提取基础资产时，会销毁相应数量的金库份额代币。`asset()` 函数会返回金库的基础资产的代币地址。
2. 存款逻辑：让用户存入基础资产，并铸造相应数量的金库份额。相关函数为 `deposit()` 和 `mint()`。`deposit(uint assets, address receiver)` 函数让用户存入 `assets` 单位的资产，并铸造相应数量的金库份额给 `receiver` 地址。`mint(uint shares, address receiver)` 与它类似，只不过是以将铸造的金库份额作为参数。
3. 提款逻辑：让用户销毁金库份额，并提取金库中相应数量的基础资产。相关函数为 `withdraw()` 和 `redeem()`，前者以取出基础资产数量为参数，后者以销毁的金库份额为参数。
4. 会计和限额逻辑：ERC4626 标准中其他的函数是为了统计金库中的资产，存款/提款限额，和存款/提款的基础资产和金库份额数量。

### IERC4626 接口合约

IERC4626 接口合约共包含 `2` 个事件:

- `Deposit` 事件: 存款时触发。
- `Withdraw` 事件: 取款时触发。

IERC4626 接口合约还包含 `16` 个函数，根据功能分为 `4` 大类：元数据，存款/提款逻辑，会计逻辑，和存款/提款限额逻辑。

- 元数据
  - `asset()`: 返回金库的基础资产代币地址，用于存款，取款。
- 存款/提款逻辑
  - `deposit()`: 存款函数，用户向金库存入 `assets` 单位的基础资产，然后合约铸造 `shares` 单位的金库额度给 `receiver` 地址。会释放 `Deposit` 事件。
  - `mint()`: 铸造函数（也是存款函数），用户指定想获得的 `shares` 单位的金库额度，函数经过计算后得出需要存入的 `assets` 单位的基础资产数量，然后合约从用户账户转出 `assets` 单位的基础资产，再给 `receiver` 地址铸造指定数量的金库额度。会释放 `Deposit` 事件。
  - `withdraw()`: 提款函数，`owner` 地址销毁 `share` 单位的金库额度，然后合约将相应数量的基础资产发送给 `receiver` 地址。
  - `redeem()`: 赎回函数（也是提款函数），`owner` 地址销毁 `shares` 数量的金库额度，然后合约将相应单位的基础资产发给 `receiver` 地址
- 会计逻辑
  - `totalAssets()`: 返回金库中管理的基础资产代币总额。
  - `convertToShares()`: 返回利用一定数额基础资产可以换取的金库额度。
  - `convertToAssets()`: 返回利用一定数额金库额度可以换取的基础资产。
  - `previewDeposit()`: 用于用户在当前链上环境模拟存款一定数额的基础资产能够获得的金库额度。
  - `previewMint()`: 用于用户在当前链上环境模拟铸造一定数额的金库额度需要存款的基础资产数量。
  - `previewWithdraw()`: 用于用户在当前链上环境模拟提款一定数额的基础资产需要赎回的金库份额。
  - `previewRedeem()`: 用于链上和链下用户在当前链上环境模拟销毁一定数额的金库额度能够赎回的基础资产数量。
- 存款/提款限额逻辑
  - `maxDeposit()`: 返回某个用户地址单次存款可存的最大基础资产数额。
  - `maxMint()`: 返回某个用户地址单次铸造可以铸造的最大金库额度。
  - `maxWithdraw()`: 返回某个用户地址单次取款可以提取的最大基础资产额度。
  - `maxRedeem()`: 返回某个用户地址单次赎回可以销毁的最大金库额度。

```solidity
// SPDX-License-Identifier: MIT
// Author: 0xAA from WTF Academy

pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/IERC20.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol";

/**
 * @dev ERC4626 "代币化金库标准"的接口合约
 * https://eips.ethereum.org/EIPS/eip-4626[ERC-4626].
 */
interface IERC4626 is IERC20, IERC20Metadata {
    ///////////////////////////////////////////////////////////////
                              //   事件
    ///////////////////////////////////////////////////////////////
    // 存款时触发
    event Deposit(address indexed sender, address indexed owner, uint256 assets, uint256 shares);

    // 取款时触发
    event Withdraw(
        address indexed sender,
        address indexed receiver,
        address indexed owner,
        uint256 assets,
        uint256 shares
    );

    ///////////////////////////////////////////////////////////////
                            元数据
    ///////////////////////////////////////////////////////////////
    /**
     * @dev 返回金库的基础资产代币地址 （用于存款，取款）
     * - 必须是 ERC20 代币合约地址.
     * - 不能revert
     */
    function asset() external view returns (address assetTokenAddress);

    ///////////////////////////////////////////////////////////////
                       // 存款/提款逻辑
    ///////////////////////////////////////////////////////////////
    /**
     * @dev 存款函数: 用户向金库存入 assets 单位的基础资产，然后合约铸造 shares 单位的金库额度给 receiver 地址
     *
     * - 必须释放 Deposit 事件.
     * - 如果资产不能存入，必须revert，比如存款数额大大于上限等。
     */
     
    function deposit(uint256 assets, address receiver) external returns (uint256 shares);

    /**
     * @dev 铸造函数: 用户需要存入 assets 单位的基础资产，然后合约给 receiver 地址铸造 share 数量的金库额度
     * - 必须释放 Deposit 事件.
     * - 如果全部金库额度不能铸造，必须revert，比如铸造数额大大于上限等。
     */
    function mint(uint256 shares, address receiver) external returns (uint256 assets);

    /**
     * @dev 提款函数: owner 地址销毁 share 单位的金库额度，然后合约将 assets 单位的基础资产发送给 receiver 地址
     * - 释放 Withdraw 事件
     * - 如果全部基础资产不能提取，将revert
     */
    function withdraw(uint256 assets, address receiver, address owner) external returns (uint256 shares);

    /**
     * @dev 赎回函数: owner 地址销毁 shares 数量的金库额度，然后合约将 assets 单位的基础资产发给 receiver 地址
     * - 释放 Withdraw 事件
     * - 如果金库额度不能全部销毁，则revert
     */
    function redeem(uint256 shares, address receiver, address owner) external returns (uint256 assets);

    /**//////////////////////////////////////////////////////////////
                            会计逻辑
    //////////////////////////////////////////////////////////////*/

    /**
     * @dev 返回金库中管理的基础资产代币总额
     * - 要包含利息
     * - 要包含费用
     * - 不能revert
     */
    function totalAssets() external view returns (uint256 totalManagedAssets);

    /**
     * @dev 返回利用一定数额基础资产可以换取的金库额度
     * - 不要包含费用
     * - 不包含滑点
     * - 不能revert
     */
    function convertToShares(uint256 assets) external view returns (uint256 shares);

    /**
     * @dev 返回利用一定数额金库额度可以换取的基础资产
     * - 不要包含费用
     * - 不包含滑点
     * - 不能revert
     */
    function convertToAssets(uint256 shares) external view returns (uint256 assets);

    /**
     * @dev 用于链上和链下用户在当前链上环境模拟存款一定数额的基础资产能够获得的金库额度
     * - 返回值要接近且不大于在同一交易进行存款得到的金库额度
     * - 不要考虑 maxDeposit 等限制，假设用户的存款交易会成功
     * - 要考虑费用
     * - 不能revert
     * NOTE: 可以利用 convertToAssets 和 previewDeposit 返回值的差值来计算滑点
     */
    function previewDeposit(uint256 assets) external view returns (uint256 shares);

    /**
     * @dev 用于链上和链下用户在当前链上环境模拟铸造 shares 数额的金库额度需要存款的基础资产数量
     * - 返回值要接近且不小于在同一交易进行铸造一定数额金库额度所需的存款数量
     * - 不要考虑 maxMint 等限制，假设用户的存款交易会成功
     * - 要考虑费用
     * - 不能revert
     */
    function previewMint(uint256 shares) external view returns (uint256 assets);

    /**
     * @dev 用于链上和链下用户在当前链上环境模拟提款 assets 数额的基础资产需要赎回的金库份额
     * - 返回值要接近且不大于在同一交易进行提款一定数额基础资产所需赎回的金库份额
     * - 不要考虑 maxWithdraw 等限制，假设用户的提款交易会成功
     * - 要考虑费用
     * - 不能revert
     */
    function previewWithdraw(uint256 assets) external view returns (uint256 shares);

    /**
     * @dev 用于链上和链下用户在当前链上环境模拟销毁 shares 数额的金库额度能够赎回的基础资产数量
     * - 返回值要接近且不小于在同一交易进行销毁一定数额的金库额度所能赎回的基础资产数量
     * - 不要考虑 maxRedeem 等限制，假设用户的赎回交易会成功
     * - 要考虑费用
     * - 不能revert.
     */
    function previewRedeem(uint256 shares) external view returns (uint256 assets);

    /**//////////////////////////////////////////////////////////////
                     存款/提款限额逻辑
    //////////////////////////////////////////////////////////////*/
    /**
     * @dev 返回某个用户地址单次存款可存的最大基础资产数额。
     * - 如果有存款上限，那么返回值应该是个有限值
     * - 返回值不能超过 2 ** 256 - 1 
     * - 不能revert
     */
    function maxDeposit(address receiver) external view returns (uint256 maxAssets);

    /**
     * @dev 返回某个用户地址单次铸造可以铸造的最大金库额度
     * - 如果有铸造上限，那么返回值应该是个有限值
     * - 返回值不能超过 2 ** 256 - 1 
     * - 不能revert
     */
    function maxMint(address receiver) external view returns (uint256 maxShares);

    /**
     * @dev 返回某个用户地址单次取款可以提取的最大基础资产额度
     * - 返回值应该是个有限值
     * - 不能revert
     */
    function maxWithdraw(address owner) external view returns (uint256 maxAssets);

    /**
     * @dev 返回某个用户地址单次赎回可以销毁的最大金库额度
     * - 返回值应该是个有限值
     * - 如果没有其他限制，返回值应该是 balanceOf(owner)
     * - 不能revert
     */
    function maxRedeem(address owner) external view returns (uint256 maxShares);
}
```



### ERC4626 合约

下面，我们实现一个极简版的代币化金库合约：

- 构造函数初始化基础资产的合约地址，金库份额的代币名称和符号。注意，金库份额的代币名称和符号要和基础资产有关联，比如基础资产叫 `WTF`，金库份额最好叫 `vWTF`。
- 存款时，当用户向金库存 `x` 单位的基础资产，会铸造 `x` 单位（等量）的金库份额。
- 取款时，当用户销毁 `x` 单位的金库份额，会提取 `x` 单位（等量）的基础资产。

**注意**: 在实际使用时，要特别小心和会计逻辑相关函数的计算是向上取整还是向下取整，可以参考 [openzeppelin](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/extensions/ERC4626.sol) 和 [solmate](https://github.com/transmissions11/solmate/blob/main/src/mixins/ERC4626.sol) 的实现。本节的教学例子中不考虑它。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity >=0.8.0;

import {IERC4626} from "./IERC4626.sol";
import {ERC20, IERC20Metadata} from "@openzeppelin/contracts/token/ERC20/ERC20.sol";

/**
 * @dev ERC4626 "代币化金库标准"合约，仅供教学使用，不要用于生产
 */
contract ERC4626 is ERC20, IERC4626 {
    /**
                    状态变量
	*/
    ERC20 private immutable _asset; // 
    uint8 private immutable _decimals;

    constructor(
        ERC20 asset_,
        string memory name_,
        string memory symbol_
    ) ERC20(name_, symbol_) {
        _asset = asset_;
        _decimals = asset_.decimals();

    }

    /** @dev See {IERC4626-asset}. 
    */
    function asset() public view virtual override returns (address) {
        return address(_asset);
    }

    /**
     * See {IERC20Metadata-decimals}.
     */
    function decimals() public view virtual override(IERC20Metadata, ERC20) returns (uint8) {
        return _decimals;
    }

    /**//////////////////////////////////////////////////////////////
                        存款/提款逻辑
    //////////////////////////////////////////////////////////////*/
    /** @dev See {IERC4626-deposit}. 
    */
    function deposit(uint256 assets, address receiver) public virtual returns (uint256 shares) {
        // 利用 previewDeposit() 计算将获得的金库份额
        shares = previewDeposit(assets);

        // 先 transfer 后 mint，防止重入
        _asset.transferFrom(msg.sender, address(this), assets);
        _mint(receiver, shares);

        // 释放 Deposit 事件
        emit Deposit(msg.sender, receiver, assets, shares);
    }

    /** @dev See {IERC4626-mint}.
    */
    function mint(uint256 shares, address receiver) public virtual returns (uint256 assets) {
        // 利用 previewMint() 计算需要存款的基础资产数额
        assets = previewMint(shares);

        // 先 transfer 后 mint，防止重入
        _asset.transferFrom(msg.sender, address(this), assets);
        _mint(receiver, shares);

        // 释放 Deposit 事件
        emit Deposit(msg.sender, receiver, assets, shares);

    }

    /** @dev See {IERC4626-withdraw}. 
    */
    function withdraw(
        uint256 assets,
        address receiver,
        address owner
    ) public virtual returns (uint256 shares) {
        // 利用 previewWithdraw() 计算将销毁的金库份额
        shares = previewWithdraw(assets);

        // 如果调用者不是 owner，则检查并更新授权
        if (msg.sender != owner) {
            _spendAllowance(owner, msg.sender, shares);
        }

        // 先销毁后 transfer，防止重入
        _burn(owner, shares);
        _asset.transfer(receiver, assets);

        // 释放 Withdraw 事件
        emit Withdraw(msg.sender, receiver, owner, assets, shares);
    }

    /** @dev See {IERC4626-redeem}. 
    */
    function redeem(
        uint256 shares,
        address receiver,
        address owner
    ) public virtual returns (uint256 assets) {
        // 利用 previewRedeem() 计算能赎回的基础资产数额
        assets = previewRedeem(shares);

        // 如果调用者不是 owner，则检查并更新授权
        if (msg.sender != owner) {
            _spendAllowance(owner, msg.sender, shares);
        }

        // 先销毁后 transfer，防止重入
        _burn(owner, shares);
        _asset.transfer(receiver, assets);

        // 释放 Withdraw 事件       
        emit Withdraw(msg.sender, receiver, owner, assets, shares);
    }

    /**//////////////////////////////////////////////////////////////
                            会计逻辑
    //////////////////////////////////////////////////////////////*/
    /** @dev See {IERC4626-totalAssets}. 
    */
    function totalAssets() public view virtual returns (uint256){
        // 返回合约中基础资产持仓
        return _asset.balanceOf(address(this));
    }

    /** @dev See {IERC4626-convertToShares}. 
    */
    function convertToShares(uint256 assets) public view virtual returns (uint256) {
        uint256 supply = totalSupply();
        // 如果 supply 为 0，那么 1:1 铸造金库份额
        // 如果 supply 不为0，那么按比例铸造
        return supply == 0 ? assets : assets * supply / totalAssets();
    }

    /** @dev See {IERC4626-convertToAssets}. 
    */
    function convertToAssets(uint256 shares) public view virtual returns (uint256) {
        uint256 supply = totalSupply();
        // 如果 supply 为 0，那么 1:1 赎回基础资产
        // 如果 supply 不为0，那么按比例赎回
        return supply == 0 ? shares : shares * totalAssets() / supply;
    }

    /** @dev See {IERC4626-previewDeposit}.
    */
    function previewDeposit(uint256 assets) public view virtual returns (uint256) {
        return convertToShares(assets);
    }

    /** @dev See {IERC4626-previewMint}. 
    */
    function previewMint(uint256 shares) public view virtual returns (uint256) {
        return convertToAssets(shares);
    }

    /** @dev See {IERC4626-previewWithdraw}. 
    */
    function previewWithdraw(uint256 assets) public view virtual returns (uint256) {
        return convertToShares(assets);
    }

    /** @dev See {IERC4626-previewRedeem}. 
    */
    function previewRedeem(uint256 shares) public view virtual returns (uint256) {
        return convertToAssets(shares);
    }

    /**//////////////////////////////////////////////////////////////
                     存款/提款限额逻辑
    //////////////////////////////////////////////////////////////*/
    /** @dev See {IERC4626-maxDeposit}. 
    */
    function maxDeposit(address) public view virtual returns (uint256) {
        return type(uint256).max;
    }

    /** @dev See {IERC4626-maxMint}. 
    */
    function maxMint(address) public view virtual returns (uint256) {
        return type(uint256).max;
    }
    
    /** @dev See {IERC4626-maxWithdraw}. 
    */
    function maxWithdraw(address owner) public view virtual returns (uint256) {
        return convertToAssets(balanceOf(owner));
    }
    
    /** @dev See {IERC4626-maxRedeem}. 
    */
    function maxRedeem(address owner) public view virtual returns (uint256) {
        return balanceOf(owner);
    }
}
```



## `Remix`演示

**注意:** 以下运行示例使用了remix中第二个账户,即`0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2`, 来部署合约, 调用合约方法.

1. 部署 `ERC20` 代币合约，将代币名称和符号均设为 `WTF`，并给自己铸造 `10000` 代币。

   ![img](https://www.wtf.academy/assets/images/51-2-1-a7465b3d1a5e629593d42d568b1232ed.png)

   ![img](https://www.wtf.academy/assets/images/51-2-2-ef114477c426fd782550b86c71e52a7b.png)

   

2. 部署 `ERC4626` 代币合约，将基础资产的合约地址设为 `WTF` 的地址，名称和符号均设为 `vWTF`。

   ![img](https://www.wtf.academy/assets/images/51-3-41408998e89f04fbadec1ed902ed259d.png)

   

3. 调用 `ERC20` 合约的 `approve()` 函数，将代币授权给 `ERC4626` 合约。

   ![img](https://www.wtf.academy/assets/images/51-4-50abd8f1a8336a29b52eceee6d9d176c.png)

   

4. 调用 `ERC4626` 合约的 `deposit()` 函数，存款 `1000` 枚代币。然后调用 `balanceOf()` 函数，查看自己的金库份额变为 `1000`。

   ![img](https://www.wtf.academy/assets/images/51-5-d3fcec60a0351dbaf19100e47a724f92.png)

   

5. 调用 `ERC4626` 合约的 `mint()` 函数，存款 `1000` 枚代币。然后调用 `balanceOf()` 函数查看自己的金库份额变为 `2000`。

   ![img](https://www.wtf.academy/assets/images/51-6-8bb827155971ceb36978c06ea8aa362d.png)

   

6. 调用 `ERC4626` 合约的 `withdraw()` 函数，取款 `1000` 枚代币。然后调用 `balanceOf()` 函数查看自己的金库份额变为 `1000`。

   ![img](https://www.wtf.academy/assets/images/51-7-815e01c0138249334a58825a795a59f2.png)

   

7. 调用 `ERC4626` 合约的 `redeem()` 函数，取款 `1000` 枚代币。然后调用 `balanceOf()` 函数查看自己的金库份额变为 `0`。

   ![img](https://www.wtf.academy/assets/images/51-8-c104c712f9938f8279dc16e19266eeb2.png)

   

## 总结

这一讲，我们介绍了代币化金库标准 ERC4626，并写了一个简单的金库合约，可以将基础资产 1:1 的转换为金库份额代币。ERC4626 为 DeFi 提升流动性和可组合性，未来将逐渐普及。你会用 ERC4626 做什么应用呢？

# 52. EIP712 类型化数据签名

这一讲，我们介绍一种更先进、安全的签名方法，EIP712 类型化数据签名。

## EIP712

之前我们介绍了 [EIP191 签名标准（personal sign）](https://github.com/AmazingAng/WTF-Solidity/blob/main/37_Signature/readme.md) ，它可以给一段消息签名。但是它过于简单，当签名数据比较复杂时，用户只能看到一串十六进制字符串（数据的哈希），无法核实签名内容是否与预期相符。



![img](https://www.wtf.academy/assets/images/52-1-70c125dd74c4dfbde3fd3a1da43ce01c.png)



[EIP712类型化数据签名](https://eips.ethereum.org/EIPS/eip-712)是一种更高级、更安全的签名方法。当支持 EIP712 的 Dapp 请求签名时，钱包会展示签名消息的原始数据，用户可以在验证数据符合预期之后签名。



![img](https://www.wtf.academy/assets/images/52-2-6348478f80387a4ca1f75303ebf5687c.png)



## EIP712 使用方法

EIP712 的应用一般包含链下签名（前端或脚本）和链上验证（合约）两部分，下面我们用一个简单的例子 `EIP712Storage` 来介绍 EIP712 的使用方法。`EIP712Storage` 合约有一个状态变量 `number`，需要验证 EIP712 签名才可以更改。

### 链下签名

1. EIP712 签名必须包含一个 `EIP712Domain` 部分，它包含了合约的 name，version（一般约定为 “1”），chainId，和 verifyingContract（验证签名的合约地址）。

   ```js
   EIP712Domain: [
       { name: "name", type: "string" },
       { name: "version", type: "string" },
       { name: "chainId", type: "uint256" },
       { name: "verifyingContract", type: "address" },
   ]
   ```

   

   这些信息会在用户签名时显示，并确保只有特定链的特定合约才能验证签名。你需要在脚本中传入相应参数。

   ```js
   const domain = {
       name: "EIP712Storage",
       version: "1",
       chainId: "1",
       verifyingContract: "0xf8e81D47203A594245E36C48e151709F0C19fBe8",
   };
   ```

   

2. 你需要根据使用场景自定义一个签名的数据类型，他要与合约匹配。在 `EIP712Storage` 例子中，我们定义了一个 `Storage` 类型，它有两个成员: `address` 类型的 `spender`，指定了可以修改变量的调用者；`uint256` 类型的 `number`，指定了变量修改后的值。

   ```js
   const types = {
       Storage: [
           { name: "spender", type: "address" },
           { name: "number", type: "uint256" },
       ],
   };
   ```

   

3. 创建一个 `message` 变量，传入要被签名的类型化数据。

   ```js
   const message = {
       spender: "0x5B38Da6a701c568545dCfcB03FcB875f56beddC4",
       number: "100",
   };
   ```

   

   

   ![img](https://www.wtf.academy/assets/images/52-3-403d427c1b1cd7474469cb682aafea6a.png)

   

4. 调用钱包对象的 `signTypedData()` 方法，传入前面步骤中的 `domain`，`types`，和 `message` 变量进行签名（这里使用 `ethersjs v6`）。

   ```js
   // 获得provider
   const provider = new ethers.BrowserProvider(window.ethereum)
   // 获得signer后调用signTypedData方法进行eip712签名
   const signature = await signer.signTypedData(domain, types, message);
   console.log("Signature:", signature);
   ```

   

   

   ![img](https://www.wtf.academy/assets/images/52-4-42c190293956740615755e9d35bbe6cd.png)

   

### 链上验证

接下来就是 `EIP712Storage` 合约部分，它需要验证签名，如果通过，则修改 `number` 状态变量。它有 `5` 个状态变量。

1. `EIP712DOMAIN_TYPEHASH`: `EIP712Domain` 的类型哈希，为常量。
2. `STORAGE_TYPEHASH`: `Storage` 的类型哈希，为常量。
3. `DOMAIN_SEPARATOR`: 这是混合在签名中的每个域 (Dapp) 的唯一值，由 `EIP712DOMAIN_TYPEHASH` 以及 `EIP712Domain` （name, version, chainId, verifyingContract）组成，在 `constructor()` 中初始化。
4. `number`: 合约中存储值的状态变量，可以被 `permitStore()` 方法修改。
5. `owner`: 合约所有者，在 `constructor()` 中初始化，在 `permitStore()` 方法中验证签名的有效性。

另外，`EIP712Storage` 合约有 `3` 个函数。

1. 构造函数: 初始化 `DOMAIN_SEPARATOR` 和 `owner`。
2. `retrieve()`: 读取 `number` 的值。
3. `permitStore`: 验证 EIP712 签名，并修改 `number` 的值。首先，它先将签名拆解为 `r`, `s`, `v`。然后用 `DOMAIN_SEPARATOR`, `STORAGE_TYPEHASH`, 调用者地址，和输入的 `_num` 参数拼出签名的消息文本 `digest`。最后利用 `ECDSA` 的 `recover()` 方法恢复出签名者地址，如果签名有效，则更新 `number` 的值。

```solidity
// SPDX-License-Identifier: MIT
// By 0xAA 
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/utils/cryptography/ECDSA.sol";

contract EIP712Storage {
    using ECDSA for bytes32;

    bytes32 private constant EIP712DOMAIN_TYPEHASH = keccak256("EIP712Domain(string name,string version,uint256 chainId,address verifyingContract)");
    bytes32 private constant STORAGE_TYPEHASH = keccak256("Storage(address spender,uint256 number)");
    bytes32 private DOMAIN_SEPARATOR;
    uint256 number;
    address owner;

    constructor(){
        DOMAIN_SEPARATOR = keccak256(abi.encode(
            EIP712DOMAIN_TYPEHASH, // type hash
            keccak256(bytes("EIP712Storage")), // name
            keccak256(bytes("1")), // version
            block.chainid, // chain id
            address(this) // contract address
        ));
        owner = msg.sender;
    }

    /**
     * @dev Store value in variable
     */
    function permitStore(uint256 _num, bytes memory _signature) public {
        // 检查签名长度，65是标准r,s,v签名的长度
        require(_signature.length == 65, "invalid signature length");
        bytes32 r;
        bytes32 s;
        uint8 v;
        // 目前只能用assembly (内联汇编)来从签名中获得r,s,v的值
        assembly {
            /*
            前32 bytes存储签名的长度 (动态数组存储规则)
            add(sig, 32) = sig的指针 + 32
            等效为略过signature的前32 bytes
            mload(p) 载入从内存地址p起始的接下来32 bytes数据
            */
            // 读取长度数据后的32 bytes
            r := mload(add(_signature, 0x20))
            // 读取之后的32 bytes
            s := mload(add(_signature, 0x40))
            // 读取最后一个byte
            v := byte(0, mload(add(_signature, 0x60)))
        }

        // 获取签名消息hash
        bytes32 digest = keccak256(abi.encodePacked(
            "\x19\x01",
            DOMAIN_SEPARATOR,
            keccak256(abi.encode(STORAGE_TYPEHASH, msg.sender, _num))
        )); 
        
        address signer = digest.recover(v, r, s); // 恢复签名者
        require(signer == owner, "EIP712Storage: Invalid signature"); // 检查签名

        // 修改状态变量
        number = _num;
    }

    /**
     * @dev Return value 
     * @return value of 'number'
     */
    function retrieve() public view returns (uint256){
        return number;
    }    
}
```



## Remix 复现

1. 部署 `EIP712Storage` 合约。

2. 运行 `eip712storage.html`，将 `Contract Address` 改为部署的 `EIP712Storage` 合约地址，然后依次点击 `Connect Metamask` 和 `Sign Permit` 按钮签名。签名要使用部署合约的钱包，比如 Remix 测试钱包：

   ```js
   public_key: 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4
   private_key: 503f38a9c967ed597e47fe25643985f032b072db8075426a92110f82df48dfcb
   ```

   

3. 调用合约的 `permitStore()` 方法，输入相应的 `_num` 和签名，修改 `number` 的值。

4. 调用合约的 `retrieve()` 方法，看到 `number` 的值已经改变。

## 总结

这一讲，我们介绍了 EIP712 类型化数据签名，一种更先进、安全的签名标准。在请求签名时，钱包会展示签名消息的原始数据，用户可以在验证数据后签名。该标准应用广泛，在 Metamask，Uniswap 代币对，DAI 稳定币等场景均有使用，希望大家好好掌握。

# 53. ERC-2612 ERC20Permit

这一讲，我们介绍 ERC20 代币的一个拓展，ERC20Permit，支持使用签名进行授权，改善用户体验。它在 EIP-2612 中被提出，已纳入以太坊标准，并被 `USDC`，`ARB` 等代币使用。

## ERC20

我们在[31讲](https://github.com/AmazingAng/WTF-Solidity/blob/main/31_ERC20/readme.md)中介绍了ERC20，以太坊最流行的代币标准。它流行的一个主要原因是 `approve` 和 `transferFrom` 两个函数搭配使用，使得代币不仅可以在外部拥有账户（EOA）之间转移，还可以被其他合约使用。

但是，ERC20的 `approve` 函数限制了只有代币所有者才能调用，这意味着所有 `ERC20` 代币的初始操作必须由 `EOA` 执行。举个例子，用户 A 在去中心化交易所使用 `USDT` 交换 `ETH`，必须完成两个交易：第一步用户 A 调用 `approve` 将 `USDT` 授权给合约，第二步用户 A 调用合约进行交换。非常麻烦，并且用户必须持有 `ETH` 用于支付交易的 gas。

## ERC20Permit

EIP-2612 提出了 ERC20Permit，扩展了 ERC20 标准，添加了一个 `permit` 函数，允许用户通过 EIP-712 签名修改授权，而不是通过 `msg.sender`。这有两点好处：

1. 授权这步仅需用户在链下签名，减少一笔交易。
2. 签名后，用户可以委托第三方进行后续交易，不需要持有 ETH：用户 A 可以将签名发送给 拥有gas的第三方 B，委托 B 来执行后续交易。



![img](https://www.wtf.academy/assets/images/53-1-7312c63e982de067e367df439530252e.png)



## 合约

### IERC20Permit 接口合约

首先，让我们学习下 ERC20Permit 的接口合约，它定义了 3 个函数：

- `permit()`: 根据 `owner` 的签名, 将 `owenr` 的ERC20代币余额授权给 `spender`，数量为 `value`。要求：
  - `spender` 不能是零地址。
  - `deadline` 必须是未来的时间戳。
  - `v`，`r` 和 `s` 必须是 `owner` 对 EIP712 格式的函数参数的有效 `secp256k1` 签名。
  - 签名必须使用 `owner` 当前的 nonce。

- `nonces()`: 返回 `owner` 的当前 nonce。每次为 `permit()` 函数生成签名时，都必须包括此值。每次成功调用 `permit()` 函数都会将 `owner` 的 nonce 增加 1，防止多次使用同一个签名。
- `DOMAIN_SEPARATOR()`: 返回用于编码 `permit()` 函数的签名的域分隔符（domain separator），如 [EIP712](https://github.com/AmazingAng/WTF-Solidity/blob/main/52_EIP712/readme.md) 所定义。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

/**
 * @dev ERC20 Permit 扩展的接口，允许通过签名进行批准，如 https://eips.ethereum.org/EIPS/eip-2612[EIP-2612]中定义。
 */
interface IERC20Permit {
    /**
     * @dev 根据owner的签名, 将 `owenr` 的ERC20余额授权给 `spender`，数量为 `value`
     */
    function permit(
        address owner,
        address spender,
        uint256 value,
        uint256 deadline,
        uint8 v,
        bytes32 r,
        bytes32 s
    ) external;

    /**
     * @dev 返回 `owner` 的当前 nonce。每次为 {permit} 生成签名时，都必须包括此值。
     */
    function nonces(address owner) external view returns (uint256);

    /**
     * @dev 返回用于编码 {permit} 的签名的域分隔符（domain separator）
     */
    // solhint-disable-next-line func-name-mixedcase
    function DOMAIN_SEPARATOR() external view returns (bytes32);
}
```

> [!NOTE]
>
> 这个 `IERC20Permit` 接口定义了一个允许通过签名进行授权的机制，基于 EIP-2612 扩展 ERC20 标准。它的设计可以通过离线签名来批准代币转账，而不需要持有代币的人主动发起链上交易，减少了 gas 费用。以下是该接口各个部分的详细解释：
>
> ### 1. `permit` 函数
> ```solidity
> function permit(
>     address owner,
>     address spender,
>     uint256 value,
>     uint256 deadline,
>     uint8 v,
>     bytes32 r,
>     bytes32 s
> ) external;
> ```
> - **作用**: 通过签名授权 `spender` 可以使用 `owner` 的 `value` 数量的代币，类似于传统的 `approve` 方法，但是 `permit` 使用签名来进行授权。
> - **参数**:
>   - `owner`: 代币的持有者，签名的创建者。
>   - `spender`: 被授权的地址。
>   - `value`: 被授权转账的代币数量。
>   - `deadline`: 签名的有效期截止时间，通常以 Unix 时间戳表示。如果时间超出该值，签名就会失效。
>   - `v`, `r`, `s`: 这三者组成了 `owner` 对消息进行签名后产生的椭圆曲线数字签名（ECDSA）。
> - **目的**: 通过将交易和授权的过程分离，可以让 `owner` 通过签名来提前授权，而 `spender` 可以在链上使用这个授权去进行代币转账，而不需要 `owner` 额外付费或发起链上交易。
>
> ### 2. `nonces` 函数
> ```solidity
> function nonces(address owner) external view returns (uint256);
> ```
> - **作用**: 返回 `owner` 的当前 nonce（即一个单调递增的值，用来防止重放攻击）。
> - **意义**: 每次调用 `permit` 函数生成签名时，都会包含这个 nonce 值。这样在链上就能验证签名的有效性，防止同一个签名被多次使用（即防止重放攻击）。每次 `permit` 成功调用后，nonce 会自动增加。
>
> ### 3. `DOMAIN_SEPARATOR` 函数
> ```solidity
> function DOMAIN_SEPARATOR() external view returns (bytes32);
> ```
> - **作用**: 返回签名消息的域分隔符。该分隔符用于 EIP-712 签名的消息域，防止跨链、跨合约的签名混淆。
> - **意义**: 这是 EIP-712 中重要的部分，防止不同合约或不同网络上的签名被滥用。域分隔符包含了合约的地址、链 ID 等信息，确保签名只能在特定的环境下有效。
>
> ### 总结
> `IERC20Permit` 是对 ERC20 的一种扩展，允许通过 EIP-2612 标准的签名机制进行代币的授权操作，减少了链上交互的需求。通过这个接口，代币持有者可以利用离线签名授权代币使用，减少了交易成本，特别适合在 DeFi 等场景中使用。



### ERC20Permit 合约

下面，让我们写一个简单的 ERC20Permit 合约，它实现了 IERC20Permit 定义的所有接口。合约包含 2 个状态变量:

- `_nonces`: `address -> uint` 的映射，记录了所有用户当前的 nonce 值，
- `_PERMIT_TYPEHASH`: 常量，记录了 `permit()` 函数的类型哈希。

合约包含 5 个函数:

- 构造函数: 初始化代币的 `name` 和 `symbol`。
- **`permit()`**: ERC20Permit 最核心的函数，实现了 IERC20Permit 的 `permit()` 。它首先检查签名是否过期，然后用 `_PERMIT_TYPEHASH`, `owner`, `spender`, `value`, `nonce`, `deadline` 还原签名消息，并验证签名是否有效。如果签名有效，则调用ERC20的 `_approve()` 函数进行授权操作。
- `nonces()`: 实现了 IERC20Permit 的 `nonces()` 函数。
- `DOMAIN_SEPARATOR()`: 实现了 IERC20Permit 的 `DOMAIN_SEPARATOR()` 函数。
- `_useNonce()`: 消费 `nonce` 的函数，返回用户当前的 `nonce`，并增加 1。

```solidity
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

import "./IERC20Permit.sol";
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/utils/cryptography/ECDSA.sol";
import "@openzeppelin/contracts/utils/cryptography/EIP712.sol";

/**
 * @dev ERC20 Permit 扩展的接口，允许通过签名进行批准，如 https://eips.ethereum.org/EIPS/eip-2612[EIP-2612]中定义。
 *
 * 添加了 {permit} 方法，可以通过帐户签名的消息更改帐户的 ERC20 余额（参见 {IERC20-allowance}）。通过不依赖 {IERC20-approve}，代币持有者的帐户无需发送交易，因此完全不需要持有 Ether。
 */
contract ERC20Permit is ERC20, IERC20Permit, EIP712 {
    mapping(address => uint) private _nonces;

    bytes32 private constant _PERMIT_TYPEHASH =
        keccak256("Permit(address owner,address spender,uint256 value,uint256 nonce,uint256 deadline)");

    /**
     * @dev 初始化 EIP712 的 name 以及 ERC20 的 name 和 symbol
     */
    constructor(string memory name, string memory symbol) EIP712(name, "1") ERC20(name, symbol){}

    /**
     * @dev See {IERC20Permit-permit}.
     */
    function permit(
        address owner,
        address spender,
        uint256 value,
        uint256 deadline,
        uint8 v,
        bytes32 r,
        bytes32 s
    ) public virtual override {
        // 检查 deadline
        require(block.timestamp <= deadline, "ERC20Permit: expired deadline");

        // 拼接 Hash
        bytes32 structHash = keccak256(abi.encode(_PERMIT_TYPEHASH, owner, spender, value, _useNonce(owner), deadline));
        bytes32 hash = _hashTypedDataV4(structHash);
        
        // 从签名和消息计算 signer，并验证签名
        address signer = ECDSA.recover(hash, v, r, s);
        require(signer == owner, "ERC20Permit: invalid signature");
        
        // 授权
        _approve(owner, spender, value);
    }

    /**
     * @dev See {IERC20Permit-nonces}.
     */
    function nonces(address owner) public view virtual override returns (uint256) {
        return _nonces[owner];
    }

    /**
     * @dev See {IERC20Permit-DOMAIN_SEPARATOR}.
     */
    function DOMAIN_SEPARATOR() external view override returns (bytes32) {
        return _domainSeparatorV4();
    }

    /**
     * @dev "消费nonce": 返回 `owner` 当前的 `nonce`，并增加 1。
     */
    function _useNonce(address owner) internal virtual returns (uint256 current) {
        current = _nonces[owner];
        _nonces[owner] += 1;
    }
}
```

> [!NOTE]
>
> 这个 `ERC20Permit` 合约实现了 ERC20 代币的扩展，允许通过签名进行代币授权，遵循 EIP-2612 标准。以下是合约的关键部分和功能的详细解析：
>
> ### 1. 合约继承
> ```solidity
> contract ERC20Permit is ERC20, IERC20Permit, EIP712 {
> ```
> - **继承的合约**:
>   - `ERC20`: 标准的 ERC20 代币实现。
>   - `IERC20Permit`: 接口，定义了 `permit`、`nonces` 和 `DOMAIN_SEPARATOR` 方法。
>   - `EIP712`: 实现了 EIP-712 的相关功能，用于支持安全的结构化数据签名。
>
> ### 2. 状态变量
> ```solidity
> mapping(address => uint) private _nonces;
> 
> bytes32 private constant _PERMIT_TYPEHASH = keccak256("Permit(address owner,address spender,uint256 value,uint256 nonce,uint256 deadline)");
> ```
> - **_nonces**: 记录每个地址的当前 nonce，以防止重放攻击。
> - **_PERMIT_TYPEHASH**: 生成 `Permit` 结构的哈希值，用于在签名时标识结构内容。
>
> ### 3. 构造函数
> ```solidity
> constructor(string memory name, string memory symbol) EIP712(name, "1") ERC20(name, symbol) {}
> ```
> - **初始化**: 传入 ERC20 代币的名称和符号，并初始化 EIP-712 的名称和版本。
>
> ### 4. `permit` 函数
> ```solidity
> function permit(
>     address owner,
>     address spender,
>     uint256 value,
>     uint256 deadline,
>     uint8 v,
>     bytes32 r,
>     bytes32 s
> ) public virtual override {
>     // 检查 deadline
>     require(block.timestamp <= deadline, "ERC20Permit: expired deadline");
> 
>     // 拼接 Hash
>     bytes32 structHash = keccak256(abi.encode(_PERMIT_TYPEHASH, owner, spender, value, _useNonce(owner), deadline));
>     bytes32 hash = _hashTypedDataV4(structHash);
>     
>     // 从签名和消息计算 signer，并验证签名
>     address signer = ECDSA.recover(hash, v, r, s);
>     require(signer == owner, "ERC20Permit: invalid signature");
>     
>     // 授权
>     _approve(owner, spender, value);
> }
> ```
> - **作用**: 允许 `owner` 通过签名授权 `spender` 使用一定数量的代币。
> - **步骤**:
>   1. **检查有效期**: 确保当前时间在授权的截止时间 `deadline` 之前。
>   2. **构建消息哈希**: 使用 `_PERMIT_TYPEHASH` 和相关参数（`owner`、`spender`、`value`、`nonce` 和 `deadline`）生成结构哈希。
>   3. **使用 EIP-712 计算哈希**: 通过 `_hashTypedDataV4` 生成最终的哈希，确保该哈希具有 EIP-712 的域分隔符。
>   4. **恢复签名者地址**: 使用 `ECDSA.recover` 验证签名，并确保签名者是 `owner`。
>   5. **调用 `_approve`**: 授权 `spender` 使用 `value` 数量的代币。
>
> ### 5. `nonces` 函数
> ```solidity
> function nonces(address owner) public view virtual override returns (uint256) {
>     return _nonces[owner];
> }
> ```
> - **作用**: 返回 `owner` 当前的 nonce 值。
>
> ### 6. `DOMAIN_SEPARATOR` 函数
> ```solidity
> function DOMAIN_SEPARATOR() external view override returns (bytes32) {
>     return _domainSeparatorV4();
> }
> ```
> - **作用**: 返回合约的域分隔符，确保签名只在特定合约上有效。
>
> ### 7. `_useNonce` 函数
> ```solidity
> function _useNonce(address owner) internal virtual returns (uint256 current) {
>     current = _nonces[owner];
>     _nonces[owner] += 1;
> }
> ```
> - **作用**: 消耗当前的 nonce 并将其增加 1，以确保每个签名都是唯一的。
>
> ### 总结
> `ERC20Permit` 合约通过引入签名机制，允许用户在不需要持有以太坊的情况下进行代币的授权操作。这种机制提高了用户体验，减少了链上交易的需求，适合于 DeFi 和其他需要代币授权的场景。通过遵循 EIP-2612 标准，确保了合约的安全性和兼容性。



## Remix 复现

1. 部署 `ERC20Permit` 合约，将 `name` 和 `symbol` 均设为 `WTFPermit`。

2. 运行 `signERC20Permit.html`，将 `Contract Address` 改为部署的 `ERC20Permit` 合约地址，其他信息下面给出。然后依次点击 `Connect Metamask` 和 `Sign Permit` 按钮签名，并获取 `r`，`s`，`v`，用于合约验证。签名要使用部署合约的钱包，比如 Remix 测试钱包：

   ```js
   owner: 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4    spender: 0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2
   value: 100
   deadline: 115792089237316195423570985008687907853269984665640564039457584007913129639935
   private_key: 503f38a9c967ed597e47fe25643985f032b072db8075426a92110f82df48dfcb
   ```

   



![img](https://www.wtf.academy/assets/images/53-2-a5c2f90ae66c5174bd825b4b9b70837b.png)



1. 调用合约的 `permit()` 方法，输入相应参数，进行授权。
2. 调用合约的 `allowance()` 方法，输入相应的 `owner` 和 `spender`，可以看到授权成功。

## 安全注意

ERC20Permit 利用链下签名进行授权给用户带来了便利，同时带来了风险。一些黑客会利用这一特性进行钓鱼攻击，骗取用户签名并盗取资产。2023年4月的一起针对 USDC 的签名[钓鱼攻击](https://twitter.com/0xAA_Science/status/1652880488095440897?s=20)让一位用户损失了 228w u 的资产。

**签名时，一定要谨慎的阅读签名内容！**

同时，一些合约在集成`permit`时，也会带来DoS（拒绝服务）的风险。因为`permit`在执行时会用掉当前的`nonce`值，如果合约的函数中包含`permit`操作，则攻击者可以通过抢跑执行`permit`从而使得目标交易因为`nonce`被占用而回滚。

## 总结

这一讲，我们介绍了 ERC20Permit，一个 ERC20 代币标准的拓展，支持用户使用链下签名进行授权操作，改善了用户体验，被很多项目采用。但同时，它也带来了更大的风险，一个签名就能将你的资产卷走。大家在签名时一定要更加谨慎。

# 54. 跨链桥

这一讲，我们介绍跨链桥，能将资产从一条区块链转移到另一条区块链的基础设施，并实现一个简单的跨链桥。

## 1. 什么是跨链桥

跨链桥是一种区块链协议，它允许在两个或多个区块链之间移动数字资产和信息。例如，一个在以太坊主网上运行的ERC20代币，可以通过跨链桥转移到其他兼容以太坊的侧链或独立链。

同时，跨链桥不是区块链原生支持的，跨链操作需要可信第三方来执行，这也带来了风险。近两年，针对跨链桥的攻击已造成超过**20亿美元**的用户资产损失。

## 2. 跨链桥的种类

跨链桥主要有以下三种类型：

- **Burn/Mint**：在源链上销毁（burn）代币，然后在目标链上创建（mint）同等数量的代币。此方法好处是代币的总供应量保持不变，但是需要跨链桥拥有代币的铸造权限，适合项目方搭建自己的跨链桥。

  

  ![img](https://www.wtf.academy/assets/images/54-1-c656a6cd8e6ca290ca0f5db7d3e413d0.png)

  

- **Stake/Mint**：在源链上锁定（stake）代币，然后在目标链上创建（mint）同等数量的代币（凭证）。源链上的代币被锁定，当代币从目标链移回源链时再解锁。这是一般跨链桥使用的方案，不需要任何权限，但是风险也较大，当源链的资产被黑客攻击时，目标链上的凭证将变为空气。

  

  ![img](https://www.wtf.academy/assets/images/54-2-16f3c3af966aab6fd5ea0523c91fdc00.png)

  

- **Stake/Unstake**：在源链上锁定（stake）代币，然后在目标链上释放（unstake）同等数量的代币，在目标链上的代币可以随时兑换回源链的代币。这个方法需要跨链桥在两条链都有锁定的代币，门槛较高，一般需要激励用户在跨链桥锁仓。

  

  ![img](https://www.wtf.academy/assets/images/54-3-686312adb830290d3ffce32a57943e3b.png)

  

## 3. 搭建一个简单的跨链桥

为了更好理解这个跨链桥，我们将搭建一个简单的跨链桥，并实现Goerli测试网和Sepolia测试网之间的ERC20代币转移。我们使用的是burn/mint方式，源链上的代币将被销毁，并在目标链上创建。这个跨链桥由一个智能合约（部署在两条链上）和一个Ethers.js脚本组成。

> **请注意**，这是一个非常简单的跨链桥实现，仅用于教学目的。它没有处理一些可能出现的问题，如交易失败、链的重组等。在生产环境中，建议使用专业的跨链桥解决方案或其他经过充分测试和审计的框架。

### 3.1 跨链代币合约

首先，我们需要在Goerli和Sepolia测试网上部署一个ERC20代币合约，`CrossChainToken`。这个合约中定义了代币的名字、符号和总供应量，还有一个用于跨链转移的`bridge()`函数。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract CrossChainToken is ERC20, Ownable {
    
    // Bridge event
    event Bridge(address indexed user, uint256 amount);
    // Mint event
    event Mint(address indexed to, uint256 amount);

    /**
     * @param name Token Name
     * @param symbol Token Symbol
     * @param totalSupply Token Supply
     */
    constructor(
        string memory name,
        string memory symbol,
        uint256 totalSupply
    ) payable ERC20(name, symbol) Ownable(msg.sender) {
        _mint(msg.sender, totalSupply);
    }

    /**
     * Bridge function
     * @param amount: burn amount of token on the current chain and mint on the other chain
     */
    function bridge(uint256 amount) public {
        _burn(msg.sender, amount);
        emit Bridge(msg.sender, amount);
    }

    /**
     * Mint function
     */
    function mint(address to, uint amount) external onlyOwner {
        _mint(to, amount);
        emit  Mint(to, amount);
    }
}
```



这个合约有三个主要的函数：

- `constructor()`: 构造函数，在部署合约时会被调用一次，用于初始化代币的名字、符号和总供应量。
- `bridge()`: 用户调用此函数进行跨链转移，它会销毁用户指定数量的代币，并释放`Bridge`事件。
- `mint()`: 只有合约的所有者才能调用此函数，用于处理跨链事件，并释放`Mint`事件。当用户在另一条链调用`bridge()`函数销毁代币，脚本会监听`Bridge`事件，并给用户在目标链铸造代币。

### 3.2 跨链脚本

有了代币合约之后，我们需要一个服务器来处理跨链事件。我们可以编写一个ethers.js脚本（v6版本）监听`Bridge`事件，当事件被触发时，在目标链上创建同样数量的代币。如果你不了解Ethers.js，可以阅读[WTF Ethers极简教程](https://github.com/WTFAcademy/WTF-Ethers)。

```javascript
import { ethers } from "ethers";

// 初始化两条链的provider
const providerGoerli = new ethers.JsonRpcProvider("Goerli_Provider_URL");
const providerSepolia = new ethers.JsonRpcProvider("Sepolia_Provider_URL://eth-sepolia.g.alchemy.com/v2/RgxsjQdKTawszh80TpJ-14Y8tY7cx5W2");

// 初始化两条链的signer
// privateKey填管理者钱包的私钥
const privateKey = "Your_Key";
const walletGoerli = new ethers.Wallet(privateKey, providerGoerli);
const walletSepolia = new ethers.Wallet(privateKey, providerSepolia);

// 合约地址和ABI
const contractAddressGoerli = "0xa2950F56e2Ca63bCdbA422c8d8EF9fC19bcF20DD";
const contractAddressSepolia = "0xad20993E1709ed13790b321bbeb0752E50b8Ce69";

const abi = [
    "event Bridge(address indexed user, uint256 amount)",
    "function bridge(uint256 amount) public",
    "function mint(address to, uint amount) external",
];

// 初始化合约实例
const contractGoerli = new ethers.Contract(contractAddressGoerli, abi, walletGoerli);
const contractSepolia = new ethers.Contract(contractAddressSepolia, abi, walletSepolia);

const main = async () => {
    try{
        console.log(`开始监听跨链事件`)

        // 监听chain Sepolia的Bridge事件，然后在Goerli上执行mint操作，完成跨链
        contractSepolia.on("Bridge", async (user, amount) => {
            console.log(`Bridge event on Chain Sepolia: User ${user} burned ${amount} tokens`);

            // 在执行burn操作
            let tx = await contractGoerli.mint(user, amount);
            await tx.wait();

            console.log(`Minted ${amount} tokens to ${user} on Chain Goerli`);
        });

        // 监听chain Goerli的Bridge事件，然后在Sepolia上执行mint操作，完成跨链
        contractGoerli.on("Bridge", async (user, amount) => {
            console.log(`Bridge event on Chain Goerli: User ${user} burned ${amount} tokens`);

            // 在执行burn操作
            let tx = await contractSepolia.mint(user, amount);
            await tx.wait();

            console.log(`Minted ${amount} tokens to ${user} on Chain Sepolia`);
        });
    } catch(e) {
        console.log(e);
    } 
}

main();
```



## Remix 复现

1. 在Goerli和Sepolia测试链部署分别部署`CrossChainToken`合约，合约会自动给我们铸造 10000 枚代币

   

   ![img](https://www.wtf.academy/assets/images/54-4-a06f651db3425e88ad97d4e8a88fe90c.png)

   

2. 补全跨链脚本 `crosschain.js` 中的RPC节点URL和管理员私钥，将部署在Goerli和Sepolia的代币合约地址填写到相应位置，并运行脚本。

3. 调用Goerli链上代币合约的`bridge()`函数，跨链100枚代币。

   

   ![img](https://www.wtf.academy/assets/images/54-6-97aa62cfdfd935f6cacde0b99db52551.png)

   

4. 脚本监听到跨链事件，并在Sepolia链上铸造100枚代币。

   

   ![img](https://www.wtf.academy/assets/images/54-7-6d6e9b5cc07382b2a4d8ba26d569d9f5.png)

   

5. 在Sepolia链上调用`balance()`查询余额，发现代币余额变为10100枚，跨链成功！

   

   ![img](https://www.wtf.academy/assets/images/54-8-20b481958957a812f5222fabb422cd14.png)

   

## 总结

这一讲我们介绍了跨链桥，它允许在两个或多个区块链之间移动数字资产和信息，方便用户在多链操作资产。同时，它也有很大的风险，近两年针对跨链桥的攻击已造成超过**20亿美元**的用户资产损失。在本教程中，我们搭建一个简单的跨链桥，并实现Goerli测试网和Sepolia测试网之间的ERC20代币转移。相信通过本教程，你对跨链桥会有更深的理解。

# 55. 多重调用

这一讲，我们将介绍 MultiCall 多重调用合约，它的设计目的在于一次交易中执行多个函数调用，这样可以显著降低交易费用并提高效率。

## MultiCall

在Solidity中，MultiCall（多重调用）合约的设计能让我们在一次交易中执行多个函数调用。它的优点如下：

1. 方便性：MultiCall能让你在一次交易中对不同合约的不同函数进行调用，同时这些调用还可以使用不同的参数。比如你可以一次性查询多个地址的ERC20代币余额。
2. 节省gas：MultiCall能将多个交易合并成一次交易中的多个调用，从而节省gas。
3. 原子性：MultiCall能让用户在一笔交易中执行所有操作，保证所有操作要么全部成功，要么全部失败，这样就保持了原子性。比如，你可以按照特定的顺序进行一系列的代币交易。

## MultiCall 合约

接下来让我们一起来研究一下MultiCall合约，它由 MakerDAO 的 [MultiCall](https://github.com/mds1/multicall/blob/main/src/Multicall3.sol) 简化而成。

MultiCall 合约定义了两个结构体:

- `Call`: 这是一个调用结构体，包含要调用的目标合约 `target`，指示是否允许调用失败的标记 `allowFailure`，和要调用的字节码 `call data`。
- `Result`: 这是一个结果结构体，包含了指示调用是否成功的标记 `success`和调用返回的字节码 `return data`。

该合约只包含了一个函数，用于执行多重调用：

- `multicall()`: 这个函数的参数是一个由Call结构体组成的数组，这样做可以确保传入的target和data的长度一致。函数通过一个循环来执行多个调用，并在调用失败时回滚交易。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

contract Multicall {
    // Call结构体，包含目标合约target，是否允许调用失败allowFailure，和call data
    struct Call {
        address target;
        bool allowFailure;
        bytes callData;
    }

    // Result结构体，包含调用是否成功和return data
    struct Result {
        bool success;
        bytes returnData;
    }

    /// @notice 将多个调用（支持不同合约/不同方法/不同参数）合并到一次调用
    /// @param calls Call结构体组成的数组
    /// @return returnData Result结构体组成的数组
    function multicall(Call[] calldata calls) public returns (Result[] memory returnData) {
        uint256 length = calls.length;
        returnData = new Result[](length);
        Call calldata calli;
        
        // 在循环中依次调用
        for (uint256 i = 0; i < length; i++) {
            Result memory result = returnData[i];
            calli = calls[i];
            (result.success, result.returnData) = calli.target.call(calli.callData);
            // 如果 calli.allowFailure 和 result.success 均为 false，则 revert
            if (!(calli.allowFailure || result.success)){
                revert("Multicall: call failed");
            }
        }
    }
}
```



## Remix 复现

1. 我们先部署一个非常简单的ERC20代币合约 `MCERC20`，并记录下合约地址。

   ```solidity
   // SPDX-License-Identifier: MIT
   pragma solidity ^0.8.19;
   import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
   
   contract MCERC20 is ERC20{
       constructor(string memory name_, string memory symbol_) ERC20(name_, symbol_){}
   
       function mint(address to, uint amount) external {
           _mint(to, amount);
       }
   }
   ```

   

2. 部署 `MultiCall` 合约。

3. 获取要调用的`calldata`。我们会给给2个地址分别铸造 50 和 100 单位的代币，你可以在 remix 的调用页面将`mint()` 的参数填入，然后点击 **Calldata** 按钮，将编码好的calldata复制下来。例子:

   ```solidity
   to: 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4
   amount: 50
   calldata: 0x40c10f190000000000000000000000005b38da6a701c568545dcfcb03fcb875f56beddc40000000000000000000000000000000000000000000000000000000000000032
   ```

   

   .

   如果你不了解`calldata`，可以阅读WTF Solidity的[第29讲]。

4. 利用 `MultiCall` 的 `multicall()` 函数调用ERC20代币合约的 `mint()` 函数，给2个地址分别铸造 50 和 100 单位的代币。例子:

   ```solidity
   calls: [["0x0fC5025C764cE34df352757e82f7B5c4Df39A836", true, "0x40c10f190000000000000000000000005b38da6a701c568545dcfcb03fcb875f56beddc40000000000000000000000000000000000000000000000000000000000000032"], ["0x0fC5025C764cE34df352757e82f7B5c4Df39A836", false, "0x40c10f19000000000000000000000000ab8483f64d9c6d1ecf9b849ae677dd3315835cb20000000000000000000000000000000000000000000000000000000000000064"]]
   ```

   

5. 利用 `MultiCall` 的 `multicall()` 函数调用ERC20代币合约的 `balanceOf()` 函数，查询刚才铸造2个地址的余额。`balanceOf()`函数的selector为`0x70a08231`。例子:

   ```solidity
   [["0x0fC5025C764cE34df352757e82f7B5c4Df39A836", true, "0x70a082310000000000000000000000005b38da6a701c568545dcfcb03fcb875f56beddc4"], ["0x0fC5025C764cE34df352757e82f7B5c4Df39A836", false, "0x70a08231000000000000000000000000ab8483f64d9c6d1ecf9b849ae677dd3315835cb2"]]
   ```

   

   可以在`decoded output`中查看调用的返回值，两个地址的余额分别为 `0x0000000000000000000000000000000000000000000000000000000000000032` 和 `0x0000000000000000000000000000000000000000000000000000000000000064`，也就是 50 和 100，调用成功！ .

## 总结

这一讲，我们介绍了 MultiCall 多重调用合约，允许你在一次交易中执行多个函数调用。要注意的是，不同的 MultiCall 合约在参数和执行逻辑上有一些不同，使用时要仔细阅读源码。

# [56. 去中心化交易所](https://www.wtf.academy/docs/solidity-103/DEX/)

这一讲，我们将介绍恒定乘积自动做市商（Constant Product Automated Market Maker, CPAMM），它是去中心化交易所的核心机制，被Uniswap，PancakeSwap等一系列DEX采用。教学合约由[Uniswap-v2](https://github.com/Uniswap/v2-core)合约简化而来，包括了CPAMM最核心的功能。

## 自动做市商

自动做市商（Automated Market Maker，简称 AMM）是一种算法，或者说是一种在区块链上运行的智能合约，它允许数字资产之间的去中心化交易。AMM 的引入开创了一种全新的交易方式，无需传统的买家和卖家进行订单匹配，而是通过一种预设的数学公式（比如，常数乘积公式）创建一个流动性池，使得用户可以随时进行交易。



![img](https://www.wtf.academy/assets/images/56-1-7a6b9433532809baf867b5c6065f6f04.png)



接下来，我们以可乐（COLA）和美元（USD）的市场为例，给大家介绍 AMM。为了方便，我们规定一下符号: x和 y 分别表示市场中可乐和美元的总量， Δx和 Δy分别表示一笔交易中可乐和美元的变化量，L和 ΔL表示总流动性和流动性的变化量。

### 恒定总和自动做市商

恒定总和自动做市商（Constant Sum Automated Market Maker, CSAMM）是最简单的自动做市商模型，我们从它开始。它在交易时的约束为:

k=x+y=*x*+*y*

其中 k*k* 为常数。也就是说，在交易前后市场中可乐和美元数量的总和保持不变。举个例子，市场中流动性有 10 瓶可乐和 10 美元，此时 k=20*k*=20，可乐的价格为 1 美元/瓶。我很渴，想拿出 2 美元来换可乐。交易后市场中的美元总量变为 12，根据约束k=20*k*=20，交易后市场中有 8 瓶可乐，价格为 1 美元/瓶。我在交易中得到了 2 瓶可乐，价格为 1 美元/瓶。

CSAMM 的优点是可以保证代币的相对价格不变，这点在稳定币兑换中很重要，大家都希望 1 USDT 总能兑换出 1 USDC。但它的缺点也很明显，它的流动性很容易耗尽：我只需要 10 美元，就可以把市场上可乐的流动性耗尽，其他想喝可乐的用户就没法交易了。

下面我们介绍拥有”无限“流动性的恒定乘积自动做市商。

### 恒定乘积自动做市商

恒定乘积自动做市商（CPAMM）是最流行的自动做市商模型，最早被 Uniswap 采用。它在交易时的约束为:

k=x∗y*k*=*x*∗*y*

其中 k*k* 为常数。也就是说，在交易前后市场中可乐和美元数量的乘积保持不变。同样的例子，市场中流动性有 10 瓶可乐和 10 美元，此时 k=100*k*=100，可乐的价格为 1 美元/瓶。我很渴，想拿出 10 美元来换可乐。如果在 CSAMM 中，我的交易会换来 10 瓶可乐，并耗尽市场上可乐的流动性。但在 CPAMM 中，交易后市场中的美元总量变为 20，根据约束 k=100*k*=100，交易后市场中有 5 瓶可乐，价格为 20/5=420/5=4 美元/瓶。我在交易中得到了 5 瓶可乐，价格为 10/5=210/5=2 美元/瓶。

CPAMM 的优点是拥有“无限”流动性：代币的相对价格会随着买卖而变化，越稀缺的代币相对价格会越高，避免流动性被耗尽。上面的例子中，交易让可乐从 1 美元/瓶 上涨到 4 美元/瓶，从而避免市场上的可乐被买断。

下面，让我们建立一个基于 CPAMM 的极简的去中心化交易所。

## 去中心化交易所

下面，我们用智能合约写一个去中心化交易所 `SimpleSwap`，支持用户交易一对代币。

`SimpleSwap` 继承了 ERC20 代币标准，方便记录流动性提供者提供的流动性。在构造器中，我们指定一对代币地址 `token0` 和 `token1`，交易所仅支持这对代币。`reserve0` 和 `reserve1` 记录了合约中代币的储备量。

```solidity
contract SimpleSwap is ERC20 {
    // 代币合约
    IERC20 public token0;
    IERC20 public token1;

    // 代币储备量
    uint public reserve0;
    uint public reserve1;
    
    // 构造器，初始化代币地址
    constructor(IERC20 _token0, IERC20 _token1) ERC20("SimpleSwap", "SS") {
        token0 = _token0;
        token1 = _token1;
    }
}
```



交易所主要有两类参与者：流动性提供者（Liquidity Provider，LP）和交易者（Trader）。下面我们分别实现这两部分的功能。

### 流动性提供

流动性提供者给市场提供流动性，让交易者获得更好的报价和流动性，并收取一定费用。

首先，我们需要实现添加流动性的功能。当用户向代币池添加流动性时，合约要记录添加的LP份额。根据 Uniswap V2，LP份额如下计算：

1. 代币池被首次添加流动性时，LP份额 ΔLΔ*L* 由添加代币数量乘积的平方根决定:

   ΔL=Δx∗ΔyΔ*L*=Δ*x*∗Δ*y*

2. 非首次添加流动性时，LP份额由添加代币数量占池子代币储备量的比例决定（两个代币的比例取更小的那个）:

   ΔL=L∗min⁡(Δxx,Δyy)Δ*L*=*L*∗min(*x*Δ*x*,*y*Δ*y*)

因为 `SimpleSwap` 合约继承了 ERC20 代币标准，在计算好LP份额后，可以将份额以代币形式铸造给用户。

下面的 `addLiquidity()` 函数实现了添加流动性的功能，主要步骤如下：

1. 将用户添加的代币转入合约，需要用户事先给合约授权。
2. 根据公式计算添加的流动性份额，并检查铸造的LP数量。
3. 更新合约的代币储备量。
4. 给流动性提供者铸造LP代币。
5. 释放 `Mint` 事件。

```solidity
event Mint(address indexed sender, uint amount0, uint amount1);

// 添加流动性，转进代币，铸造LP
// @param amount0Desired 添加的token0数量
// @param amount1Desired 添加的token1数量
function addLiquidity(uint amount0Desired, uint amount1Desired) public returns(uint liquidity){
    // 将添加的流动性转入Swap合约，需事先给Swap合约授权
    token0.transferFrom(msg.sender, address(this), amount0Desired);
    token1.transferFrom(msg.sender, address(this), amount1Desired);
    // 计算添加的流动性
    uint _totalSupply = totalSupply();
    if (_totalSupply == 0) {
        // 如果是第一次添加流动性，铸造 L = sqrt(x * y) 单位的LP（流动性提供者）代币
        liquidity = sqrt(amount0Desired * amount1Desired);
    } else {
        // 如果不是第一次添加流动性，按添加代币的数量比例铸造LP，取两个代币更小的那个比例
        liquidity = min(amount0Desired * _totalSupply / reserve0, amount1Desired * _totalSupply /reserve1);
    }

    // 检查铸造的LP数量
    require(liquidity > 0, 'INSUFFICIENT_LIQUIDITY_MINTED');

    // 更新储备量
    reserve0 = token0.balanceOf(address(this));
    reserve1 = token1.balanceOf(address(this));

    // 给流动性提供者铸造LP代币，代表他们提供的流动性
    _mint(msg.sender, liquidity);
    
    emit Mint(msg.sender, amount0Desired, amount1Desired);
}
```



接下来，我们需要实现移除流动性的功能。当用户从池子中移除流动性 ΔLΔ*L* 时，合约要销毁LP份额代币，并按比例将代币返还给用户。返还代币的计算公式如下:

Δx=ΔLL∗xΔ*x*=*L*Δ*L*∗*x* Δy=ΔLL∗yΔ*y*=*L*Δ*L*∗*y*

下面的 `removeLiquidity()` 函数实现移除流动性的功能，主要步骤如下：

1. 获取合约中的代币余额。
2. 按LP的比例计算要转出的代币数量。
3. 检查代币数量。
4. 销毁LP份额。
5. 将相应的代币转账给用户。
6. 更新储备量。
7. 释放 `Burn` 事件。

```solidity
// 移除流动性，销毁LP，转出代币
// 转出数量 = (liquidity / totalSupply_LP) * reserve
// @param liquidity 移除的流动性数量
function removeLiquidity(uint liquidity) external returns (uint amount0, uint amount1) {
    // 获取余额
    uint balance0 = token0.balanceOf(address(this));
    uint balance1 = token1.balanceOf(address(this));
    // 按LP的比例计算要转出的代币数量
    uint _totalSupply = totalSupply();
    amount0 = liquidity * balance0 / _totalSupply;
    amount1 = liquidity * balance1 / _totalSupply;
    // 检查代币数量
    require(amount0 > 0 && amount1 > 0, 'INSUFFICIENT_LIQUIDITY_BURNED');
    // 销毁LP
    _burn(msg.sender, liquidity);
    // 转出代币
    token0.transfer(msg.sender, amount0);
    token1.transfer(msg.sender, amount1);
    // 更新储备量
    reserve0 = token0.balanceOf(address(this));
    reserve1 = token1.balanceOf(address(this));

    emit Burn(msg.sender, amount0, amount1);
}
```



至此，合约中与流动性提供者相关的功能完成了，接下来是交易的部分。

### 交易

在Swap合约中，用户可以使用一种代币交易另一种。那么我用 ΔxΔ*x*单位的 token0，可以交换多少单位的 token1 呢？下面我们来简单推导一下。

根据恒定乘积公式，交易前：

k=x∗y*k*=*x*∗*y*

交易后，有：

k=(x+Δx)∗(y+Δy)*k*=(*x*+Δ*x*)∗(*y*+Δ*y*)

交易前后 k*k* 值不变，联立上面等式，可以得到：

Δy=−Δx∗yx+ΔxΔ*y*=−*x*+Δ*x*Δ*x*∗*y*

因此，可以交换到的代币数量 ΔyΔ*y* 由 ΔxΔ*x*，x*x*，和 y*y* 决定。注意 ΔxΔ*x* 和 ΔyΔ*y* 的符号相反，因为转入会增加代币储备量，而转出会减少。

下面的 `getAmountOut()` 实现了给定一个资产的数量和代币对的储备，计算交换另一个代币的数量。

```solidity
// 给定一个资产的数量和代币对的储备，计算交换另一个代币的数量
function getAmountOut(uint amountIn, uint reserveIn, uint reserveOut) public pure returns (uint amountOut) {
    require(amountIn > 0, 'INSUFFICIENT_AMOUNT');
    require(reserveIn > 0 && reserveOut > 0, 'INSUFFICIENT_LIQUIDITY');
    amountOut = amountIn * reserveOut / (reserveIn + amountIn);
}
```



有了这一核心公式后，我们可以着手实现交易功能了。下面的 `swap()` 函数实现了交易代币的功能，主要步骤如下：

1. 用户在调用函数时指定用于交换的代币数量，交换的代币地址，以及换出另一种代币的最低数量。
2. 判断是 token0 交换 token1，还是 token1 交换 token0。
3. 利用上面的公式，计算交换出代币的数量。
4. 判断交换出的代币是否达到了用户指定的最低数量，这里类似于交易的滑点。
5. 将用户的代币转入合约。
6. 将交换的代币从合约转给用户。
7. 更新合约的代币储备量。
8. 释放 `Swap` 事件。

```solidity
// swap代币
// @param amountIn 用于交换的代币数量
// @param tokenIn 用于交换的代币合约地址
// @param amountOutMin 交换出另一种代币的最低数量
function swap(uint amountIn, IERC20 tokenIn, uint amountOutMin) external returns (uint amountOut, IERC20 tokenOut){
    require(amountIn > 0, 'INSUFFICIENT_OUTPUT_AMOUNT');
    require(tokenIn == token0 || tokenIn == token1, 'INVALID_TOKEN');
    
    uint balance0 = token0.balanceOf(address(this));
    uint balance1 = token1.balanceOf(address(this));

    if(tokenIn == token0){
        // 如果是token0交换token1
        tokenOut = token1;
        // 计算能交换出的token1数量
        amountOut = getAmountOut(amountIn, balance0, balance1);
        require(amountOut > amountOutMin, 'INSUFFICIENT_OUTPUT_AMOUNT');
        // 进行交换
        tokenIn.transferFrom(msg.sender, address(this), amountIn);
        tokenOut.transfer(msg.sender, amountOut);
    }else{
        // 如果是token1交换token0
        tokenOut = token0;
        // 计算能交换出的token1数量
        amountOut = getAmountOut(amountIn, balance1, balance0);
        require(amountOut > amountOutMin, 'INSUFFICIENT_OUTPUT_AMOUNT');
        // 进行交换
        tokenIn.transferFrom(msg.sender, address(this), amountIn);
        tokenOut.transfer(msg.sender, amountOut);
    }

    // 更新储备量
    reserve0 = token0.balanceOf(address(this));
    reserve1 = token1.balanceOf(address(this));

    emit Swap(msg.sender, amountIn, address(tokenIn), amountOut, address(tokenOut));
}
```



## Swap 合约

`SimpleSwap` 的完整代码如下：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract SimpleSwap is ERC20 {
    // 代币合约
    IERC20 public token0;
    IERC20 public token1;

    // 代币储备量
    uint public reserve0;
    uint public reserve1;
    
    // 事件 
    event Mint(address indexed sender, uint amount0, uint amount1);
    event Burn(address indexed sender, uint amount0, uint amount1);
    event Swap(
        address indexed sender,
        uint amountIn,
        address tokenIn,
        uint amountOut,
        address tokenOut
        );

    // 构造器，初始化代币地址
    constructor(IERC20 _token0, IERC20 _token1) ERC20("SimpleSwap", "SS") {
        token0 = _token0;
        token1 = _token1;
    }

    // 取两个数的最小值
    function min(uint x, uint y) internal pure returns (uint z) {
        z = x < y ? x : y;
    }

    // 计算平方根 babylonian method (https://en.wikipedia.org/wiki/Methods_of_computing_square_roots#Babylonian_method)
    function sqrt(uint y) internal pure returns (uint z) {
        if (y > 3) {
            z = y;
            uint x = y / 2 + 1;
            while (x < z) {
                z = x;
                x = (y / x + x) / 2;
            }
        } else if (y != 0) {
            z = 1;
        }
    }

    // 添加流动性，转进代币，铸造LP
    // 如果首次添加，铸造的LP数量 = sqrt(amount0 * amount1)
    // 如果非首次，铸造的LP数量 = min(amount0/reserve0, amount1/reserve1)* totalSupply_LP
    // @param amount0Desired 添加的token0数量
    // @param amount1Desired 添加的token1数量
    function addLiquidity(uint amount0Desired, uint amount1Desired) public returns(uint liquidity){
        // 将添加的流动性转入Swap合约，需事先给Swap合约授权
        token0.transferFrom(msg.sender, address(this), amount0Desired);
        token1.transferFrom(msg.sender, address(this), amount1Desired);
        // 计算添加的流动性
        uint _totalSupply = totalSupply();
        if (_totalSupply == 0) {
            // 如果是第一次添加流动性，铸造 L = sqrt(x * y) 单位的LP（流动性提供者）代币
            liquidity = sqrt(amount0Desired * amount1Desired);
        } else {
            // 如果不是第一次添加流动性，按添加代币的数量比例铸造LP，取两个代币更小的那个比例
            liquidity = min(amount0Desired * _totalSupply / reserve0, amount1Desired * _totalSupply /reserve1);
        }

        // 检查铸造的LP数量
        require(liquidity > 0, 'INSUFFICIENT_LIQUIDITY_MINTED');

        // 更新储备量
        reserve0 = token0.balanceOf(address(this));
        reserve1 = token1.balanceOf(address(this));

        // 给流动性提供者铸造LP代币，代表他们提供的流动性
        _mint(msg.sender, liquidity);
        
        emit Mint(msg.sender, amount0Desired, amount1Desired);
    }

    // 移除流动性，销毁LP，转出代币
    // 转出数量 = (liquidity / totalSupply_LP) * reserve
    // @param liquidity 移除的流动性数量
    function removeLiquidity(uint liquidity) external returns (uint amount0, uint amount1) {
        // 获取余额
        uint balance0 = token0.balanceOf(address(this));
        uint balance1 = token1.balanceOf(address(this));
        // 按LP的比例计算要转出的代币数量
        uint _totalSupply = totalSupply();
        amount0 = liquidity * balance0 / _totalSupply;
        amount1 = liquidity * balance1 / _totalSupply;
        // 检查代币数量
        require(amount0 > 0 && amount1 > 0, 'INSUFFICIENT_LIQUIDITY_BURNED');
        // 销毁LP
        _burn(msg.sender, liquidity);
        // 转出代币
        token0.transfer(msg.sender, amount0);
        token1.transfer(msg.sender, amount1);
        // 更新储备量
        reserve0 = token0.balanceOf(address(this));
        reserve1 = token1.balanceOf(address(this));

        emit Burn(msg.sender, amount0, amount1);
    }

    // 给定一个资产的数量和代币对的储备，计算交换另一个代币的数量
    // 由于乘积恒定
    // 交换前: k = x * y
    // 交换后: k = (x + delta_x) * (y + delta_y)
    // 可得 delta_y = - delta_x * y / (x + delta_x)
    // 正/负号代表转入/转出
    function getAmountOut(uint amountIn, uint reserveIn, uint reserveOut) public pure returns (uint amountOut) {
        require(amountIn > 0, 'INSUFFICIENT_AMOUNT');
        require(reserveIn > 0 && reserveOut > 0, 'INSUFFICIENT_LIQUIDITY');
        amountOut = amountIn * reserveOut / (reserveIn + amountIn);
    }

    // swap代币
    // @param amountIn 用于交换的代币数量
    // @param tokenIn 用于交换的代币合约地址
    // @param amountOutMin 交换出另一种代币的最低数量
    function swap(uint amountIn, IERC20 tokenIn, uint amountOutMin) external returns (uint amountOut, IERC20 tokenOut){
        require(amountIn > 0, 'INSUFFICIENT_OUTPUT_AMOUNT');
        require(tokenIn == token0 || tokenIn == token1, 'INVALID_TOKEN');
        
        uint balance0 = token0.balanceOf(address(this));
        uint balance1 = token1.balanceOf(address(this));

        if(tokenIn == token0){
            // 如果是token0交换token1
            tokenOut = token1;
            // 计算能交换出的token1数量
            amountOut = getAmountOut(amountIn, balance0, balance1);
            require(amountOut > amountOutMin, 'INSUFFICIENT_OUTPUT_AMOUNT');
            // 进行交换
            tokenIn.transferFrom(msg.sender, address(this), amountIn);
            tokenOut.transfer(msg.sender, amountOut);
        }else{
            // 如果是token1交换token0
            tokenOut = token0;
            // 计算能交换出的token1数量
            amountOut = getAmountOut(amountIn, balance1, balance0);
            require(amountOut > amountOutMin, 'INSUFFICIENT_OUTPUT_AMOUNT');
            // 进行交换
            tokenIn.transferFrom(msg.sender, address(this), amountIn);
            tokenOut.transfer(msg.sender, amountOut);
        }

        // 更新储备量
        reserve0 = token0.balanceOf(address(this));
        reserve1 = token1.balanceOf(address(this));

        emit Swap(msg.sender, amountIn, address(tokenIn), amountOut, address(tokenOut));
    }
}
```



## Remix 复现

1. 部署两个ERC20代币合约（token0 和 token1），并记录它们的合约地址。
2. 部署 `SimpleSwap` 合约，并将上面的代币地址填入。
3. 调用两个ERC20代币的`approve()`函数，分别给 `SimpleSwap` 合约授权 1000 单位代币。
4. 调用 `SimpleSwap` 合约的 `addLiquidity()` 函数给交易所添加流动性，token0 和 token1 分别添加 100 单位。
5. 调用 `SimpleSwap` 合约的 `balanceOf()` 函数查看用户的LP份额，这里应该为 100。（100∗100=100100∗100=100）
6. 调用 `SimpleSwap` 合约的 `swap()` 函数进行代币交易，用 100 单位的 token0。
7. 调用 `SimpleSwap` 合约的 `reserve0` 和 `reserve1` 函数查看合约中的代币储备粮，应为 200 和 50。上一步我们利用 100 单位的 token0 交换了 50 单位的 token 1（100∗100100+100=50100+100100∗100=50）。

## 总结

这一讲，我们介绍了恒定乘积自动做市商，并写了一个极简的去中心化交易所。在极简Swap合约中，我们有很多没有考虑的部分，例如交易费用以及治理部分。如果你对去中心化交易所感兴趣，推荐你阅读 [Programming DeFi: Uniswap V2](https://jeiwan.net/posts/programming-defi-uniswapv2-1/) 和 [Uniswap v3 book](https://y1cunhui.github.io/uniswapV3-book-zh-cn/) ，更深入的学习。

# 57. 闪电贷

“闪电贷攻击”这个词大家一定听说过，但是什么是闪电贷？如何编写闪电贷合约？这一讲，我们将介绍区块链中的闪电贷，实现基于Uniswap V2，Uniswap V3，和AAVE V3的闪电贷合约，并使用Foundry进行测试。

## 闪电贷

你第一次听说"闪电贷"一定是在Web3，因为Web2没有这个东西。闪电贷（Flashloan）是DeFi的一种创新，它允许用户在一个交易中借出并迅速归还资金，而无需提供任何抵押。

想象一下，你突然在市场中发现了一个套利机会，但是需要准备100万u的资金才能完成套利。在Web2，你去银行申请贷款，需要审批，很可能错过套利的机会。另外，如果套利失败，你不光要支付利息，还需要归还损失的本金。

而在Web3，你可以在DeFI平台（Uniswap，AAVE，Dodo）中进行闪电贷获取资金，就可以在无担保的情况下借100万u的代币，执行链上套利，最后再归还贷款和利息。

闪电贷利用了以太坊交易的原子性：一个交易（包括其中的所有操作）要么完全执行，要么完全不执行。如果一个用户尝试使用闪电贷并在同一个交易中没有归还资金，那么整个交易都会失败并被回滚，就像它从未发生过一样。因此，DeFi平台不需要担心借款人还不上款，因为还不上的话就意味着钱没借出去；同时，借款人也不用担心套利不成功，因为套利不成功的话就还不上款，也就意味着借钱没成功。



![img](https://www.wtf.academy/assets/images/57-1-63e0fc0a099b9ec65f7558bf17ffd1e3.png)



## 闪电贷实战

下面，我们分别介绍如何在Uniswap V2，Uniswap V3，和AAVE V3的实现闪电贷合约。

### 1. Uniswap V2闪电贷

[Uniswap V2 Pair](https://github.com/Uniswap/v2-core/blob/master/contracts/UniswapV2Pair.sol#L159)合约的`swap()`函数支持闪电贷。与闪电贷业务相关的代码如下：

```solidity
function swap(uint amount0Out, uint amount1Out, address to, bytes calldata data) external lock {
    // 其他逻辑...

    // 乐观的发送代币到to地址
    if (amount0Out > 0) _safeTransfer(_token0, to, amount0Out);
    if (amount1Out > 0) _safeTransfer(_token1, to, amount1Out);

    // 调用to地址的回调函数uniswapV2Call
    if (data.length > 0) IUniswapV2Callee(to).uniswapV2Call(msg.sender, amount0Out, amount1Out, data);

    // 其他逻辑...

    // 通过k=x*y公式，检查闪电贷是否归还成功
    require(balance0Adjusted.mul(balance1Adjusted) >= uint(_reserve0).mul(_reserve1).mul(1000**2), 'UniswapV2: K');
}
```



在`swap()`函数中：

1. 先将池子中的代币乐观的转移给了`to`地址。
2. 如果传入的`data`长度大于`0`，就会调用`to`地址的回调函数`uniswapV2Call`，执行闪电贷逻辑。
3. 最后通过`k=x*y`检查闪电贷是否归还成功，如果不成功，则回滚交易。

> [!NOTE]
>
> 在这一段代码中，实现了 Uniswap V2 中的交换（swap）功能。这个函数包含了多个重要的逻辑步骤，确保代币的安全转移和闪电贷的正确归还。以下是对每个部分的详细解释：
>
> ### 函数签名
>
> ```solidity
> function swap(uint amount0Out, uint amount1Out, address to, bytes calldata data) external lock
> ```
>
> - **参数**:
>   - `amount0Out`: 要发送的第一个代币的数量（`_token0`）。
>   - `amount1Out`: 要发送的第二个代币的数量（`_token1`）。
>   - `to`: 接收代币的地址。
>   - `data`: 附加的数据，用于回调。
>
> - **修饰符**:
>   - `lock`: 通常用于防止重入攻击，确保函数在执行时不会被其他交易干扰。
>
> ### 主要逻辑
>
> 1. **发送代币到目标地址**:
>    ```solidity
>    if (amount0Out > 0) _safeTransfer(_token0, to, amount0Out);
>    if (amount1Out > 0) _safeTransfer(_token1, to, amount1Out);
>    ```
>    - 在进行代币转移时，首先检查要发送的代币数量是否大于零。若是，则调用 `_safeTransfer` 函数将代币安全地发送到目标地址 `to`。
>
> 2. **调用目标地址的回调函数**:
>    ```solidity
>    if (data.length > 0) IUniswapV2Callee(to).uniswapV2Call(msg.sender, amount0Out, amount1Out, data);
>    ```
>    - 如果 `data` 的长度大于零，表示需要进行回调。在这里，通过目标地址 `to` 调用 `IUniswapV2Callee` 接口的 `uniswapV2Call` 函数，传递当前合约的地址（`msg.sender`）、要发送的代币数量和附加数据。这一过程通常用于处理复杂的操作，如套利或闪电贷等。
>
> 3. **检查闪电贷是否归还成功**:
>    ```solidity
>    require(balance0Adjusted.mul(balance1Adjusted) >= uint(_reserve0).mul(_reserve1).mul(1000**2), 'UniswapV2: K');
>    ```
>    - 通过使用 \( k = x \cdot y \) 的公式来验证流动性是否得到了适当的管理。这里的 `balance0Adjusted` 和 `balance1Adjusted` 是代币的当前余额，`_reserve0` 和 `_reserve1` 是流动性池的初始储备。
>    - `1000**2` 是用于将池的价格调整为一定的精度（通常为千分之一），确保闪电贷的合规性。
>
> ### 总结
>
> - 这个 `swap` 函数的核心目的是在 Uniswap V2 中处理代币交换，并确保任何通过闪电贷获得的代币都能在相同的交易中归还。
> - 它不仅处理代币转移，还允许合约调用其他合约的回调函数，从而实现复杂的跨合约交互。
> - 最后，使用 `require` 语句确保合约的状态符合预期，从而避免任何意外的资产损失。这种设计非常关键，以防止闪电贷攻击等潜在风险。



下面，我们完成闪电贷合约`UniswapV2Flashloan.sol`。我们让它继承`IUniswapV2Callee`，并将闪电贷的核心逻辑写在回调函数`uniswapV2Call`中。

整体逻辑很简单，在闪电贷函数`flashloan()`中，我们从Uniswap V2的`WETH-DAI`池子借`WETH`。触发闪电贷之后，回调函数`uniswapV2Call`会被Pair合约调用，我们不进行套利，仅在计算利息后归还闪电贷。Uniswap V2闪电贷的利息为每笔`0.3%`。

**注意**：回调函数一定要做好权限控制，确保只有Uniswap的Pair合约可以调用，否则的话合约中的资金会被黑客盗光。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "./Lib.sol";

// UniswapV2闪电贷回调接口
interface IUniswapV2Callee {
    function uniswapV2Call(address sender, uint amount0, uint amount1, bytes calldata data) external;
}

// UniswapV2闪电贷合约
contract UniswapV2Flashloan is IUniswapV2Callee {
    address private constant UNISWAP_V2_FACTORY =
        0x5C69bEe701ef814a2B6a3EDD4B1652CB9cc5aA6f;

    address private constant DAI = 0x6B175474E89094C44Da98b954EedeAC495271d0F;
    address private constant WETH = 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2;

    IUniswapV2Factory private constant factory = IUniswapV2Factory(UNISWAP_V2_FACTORY);

    IERC20 private constant weth = IERC20(WETH);

    IUniswapV2Pair private immutable pair;

    constructor() {
        pair = IUniswapV2Pair(factory.getPair(DAI, WETH));
    }

    // 闪电贷函数
    function flashloan(uint wethAmount) external {
        // calldata长度大于1才能触发闪电贷回调函数
        bytes memory data = abi.encode(WETH, wethAmount);

        // amount0Out是要借的DAI, amount1Out是要借的WETH
        pair.swap(0, wethAmount, address(this), data);
    }

    // 闪电贷回调函数，只能被 DAI/WETH pair 合约调用
    function uniswapV2Call(
        address sender,
        uint amount0,
        uint amount1,
        bytes calldata data
    ) external {
        // 确认调用的是 DAI/WETH pair 合约
        address token0 = IUniswapV2Pair(msg.sender).token0(); // 获取token0地址
        address token1 = IUniswapV2Pair(msg.sender).token1(); // 获取token1地址
        assert(msg.sender == factory.getPair(token0, token1)); // ensure that msg.sender is a V2 pair

        // 解码calldata
        (address tokenBorrow, uint256 wethAmount) = abi.decode(data, (address, uint256));

        // flashloan 逻辑，这里省略
        require(tokenBorrow == WETH, "token borrow != WETH");

        // 计算flashloan费用
        // fee / (amount + fee) = 3/1000
        // 向上取整
        uint fee = (amount1 * 3) / 997 + 1;
        uint amountToRepay = amount1 + fee;

        // 归还闪电贷
        weth.transfer(address(pair), amountToRepay);
    }
}
```

> [!NOTE]
>
> ### 代码分段解释
>
> #### 1. 导入和接口定义
> ```solidity
> import "./Lib.sol";
> 
> // UniswapV2闪电贷回调接口
> interface IUniswapV2Callee {
>     function uniswapV2Call(address sender, uint amount0, uint amount1, bytes calldata data) external;
> }
> ```
> - **导入依赖文件 `Lib.sol`**: 这个文件中可能包含辅助函数或库，用于闪电贷逻辑的实现。
> - **定义 `IUniswapV2Callee` 接口**: 该接口用于支持 Uniswap V2 的闪电贷功能，定义了 `uniswapV2Call` 函数。Uniswap V2 在执行闪电贷时，会调用该函数，将相关交易数据传递给调用合约。
>
> #### 2. 定义合约和常量
> ```solidity
> contract UniswapV2Flashloan is IUniswapV2Callee {
>     address private constant UNISWAP_V2_FACTORY =
>         0x5C69bEe701ef814a2B6a3EDD4B1652CB9cc5aA6f;
> 
>     address private constant DAI = 0x6B175474E89094C44Da98b954EedeAC495271d0F;
>     address private constant WETH = 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2;
> 
>     IUniswapV2Factory private constant factory = IUniswapV2Factory(UNISWAP_V2_FACTORY);
> 
>     IERC20 private constant weth = IERC20(WETH);
> ```
> - **常量定义**:
>   - `UNISWAP_V2_FACTORY`: Uniswap V2 工厂合约的地址，用于查找具体交易对合约。
>   - `DAI` 和 `WETH`: 定义了 WETH 和 DAI 的代币合约地址。
>   - **`factory` 和 `weth`**: 分别是 Uniswap 工厂和 WETH 的接口实例，通过这些实例可以与合约进行交互。
>
> #### 3. Pair 初始化
> ```solidity
>     IUniswapV2Pair private immutable pair;
> 
>     constructor() {
>         pair = IUniswapV2Pair(factory.getPair(DAI, WETH));
>     }
> ```
> - **初始化交易对合约 `pair`**:
>   - 在构造函数中，通过工厂合约查询 `DAI-WETH` 交易对的地址，并创建 `IUniswapV2Pair` 接口实例，存储在 `pair` 中。这个 `pair` 是后续进行闪电贷操作的目标合约。
>
> #### 4. 闪电贷函数
> ```solidity
>     // 闪电贷函数
>     function flashloan(uint wethAmount) external {
>         // calldata长度大于1才能触发闪电贷回调函数
>         bytes memory data = abi.encode(WETH, wethAmount);
> 
>         // amount0Out是要借的DAI, amount1Out是要借的WETH
>         pair.swap(0, wethAmount, address(this), data);
>     }
> ```
> - **`flashloan` 函数**:
>   - **`flashloan(uint wethAmount)`**: 用户调用该函数进行闪电贷，指定借出的 WETH 数量 `wethAmount`。
>   - **编码数据**: 使用 `abi.encode` 将要借的代币（`WETH`）和借出金额编码为 `bytes` 类型数据，用于传递给 Uniswap 的回调函数。
>   - **调用 `pair.swap`**: 调用 `swap` 函数触发闪电贷操作，借入 `wethAmount` 的 WETH（`amount1Out`），并将回调数据传递给合约的回调函数 `uniswapV2Call`。
>
> #### 5. 闪电贷回调函数
> ```solidity
>     function uniswapV2Call(
>         address sender,
>         uint amount0,
>         uint amount1,
>         bytes calldata data
>     ) external {
>         // 确认调用的是 DAI/WETH pair 合约
>         address token0 = IUniswapV2Pair(msg.sender).token0(); // 获取token0地址
>         address token1 = IUniswapV2Pair(msg.sender).token1(); // 获取token1地址
>         assert(msg.sender == factory.getPair(token0, token1)); // ensure that msg.sender is a V2 pair
> ```
> - **回调函数 `uniswapV2Call`**:
>   - 该函数是闪电贷的核心逻辑。Uniswap V2 交易对合约在闪电贷开始后会调用这个函数，传递 `amount0` 和 `amount1`，分别表示借出的 DAI 和 WETH。
>   - **验证调用来源**: 通过 `msg.sender` 检查调用者是否为 DAI-WETH 交易对合约，以确保回调函数只被合法的 Uniswap 交易对调用。
>
> #### 6. 解码数据和计算利息
> ```solidity
>         // 解码calldata
>         (address tokenBorrow, uint256 wethAmount) = abi.decode(data, (address, uint256));
> 
>         // flashloan 逻辑，这里省略
>         require(tokenBorrow == WETH, "token borrow != WETH");
> 
>         // 计算flashloan费用
>         // fee / (amount + fee) = 3/1000
>         // 向上取整
>         uint fee = (amount1 * 3) / 997 + 1;
>         uint amountToRepay = amount1 + fee;
> 
>         // 归还闪电贷
>         weth.transfer(address(pair), amountToRepay);
>     }
> }
> ```
> - **解码数据**: 使用 `abi.decode` 解码先前在 `flashloan` 中编码的数据，获取代币地址 `tokenBorrow` 和借入的 WETH 数量 `wethAmount`。
> - **验证代币**: 确保借入的代币是 WETH，如果不是则交易失败。
> - **计算利息**: 利息按照 Uniswap V2 固定费率 `0.3%` 计算，计算公式为 `fee / (amount + fee) = 3/1000`，并向上取整。
> - **归还闪电贷**: 使用 `weth.transfer` 将借出的 WETH 和利息归还给 Uniswap V2 的 `pair` 合约。
>
> ### 总结
> 这个合约通过 Uniswap V2 的闪电贷功能，借入 WETH 并在回调中归还借款和利息。整个过程中，回调函数 `uniswapV2Call` 需要确保权限控制，防止恶意合约调用该函数。
>
> ### 为什么要先编码再解码？
>
> ### 1. **编码数据传递信息**
>
> 在调用 `flashloan()` 时，合约需要将一些额外的信息传递给回调函数 `uniswapV2Call`，这些信息包括：
> - 借贷的代币地址（WETH）。
> - 借贷的代币数量（`wethAmount`）。
>
> Uniswap 的 `pair.swap()` 函数有一个 `data` 参数，用于传递给回调函数。`pair.swap` 调用时不会知道具体需要传递的数据结构，所以需要将这些数据编码成 `bytes` 类型的通用形式。因此，使用 `abi.encode` 来将这些参数打包成 `bytes`。
>
> ```solidity
> bytes memory data = abi.encode(WETH, wethAmount);
> ```
>
> 这段代码做了以下事情：
> - 把 `WETH` 的地址和 `wethAmount`（借贷的 WETH 数量）打包成 `bytes` 类型的数据。
> - 这个 `data` 会被传递给 `pair.swap()`，并最终传递给回调函数 `uniswapV2Call`。
>
> ### 2. **解码数据解析信息**
>
> 当 `pair.swap()` 调用回调函数 `uniswapV2Call` 时，Uniswap 将之前编码的 `data` 传递给这个回调函数。为了在 `uniswapV2Call` 中使用这些信息，需要将 `bytes` 类型的数据解码成原来的数据结构。
>
> ```solidity
> (address tokenBorrow, uint256 wethAmount) = abi.decode(data, (address, uint256));
> ```
>
> 这段代码做了以下事情：
> - **解码 `data`**: 之前打包的 `WETH` 和 `wethAmount` 被还原成原始的数据类型，即 `address` 和 `uint256`。
> - **解析结果**: 解码后可以直接使用这两个变量 `tokenBorrow` 和 `wethAmount`，其中 `tokenBorrow` 是借贷的代币地址（应该是 WETH），`wethAmount` 是借贷的数量。
>
> ### 为什么要这样做？
>
> 1. **灵活性**: 由于 Uniswap 的 `pair.swap()` 函数是通用的，它无法知道调用者需要传递什么样的数据结构。通过使用 `abi.encode` 将数据编码成 `bytes`，就可以在回调时传递任意复杂的数据。
>    
> 2. **可扩展性**: 如果将来需要传递更多信息，比如多个参数或不同的数据类型，使用 `abi.encode` 和 `abi.decode` 可以轻松处理复杂的结构，而不必修改合约的整体框架。
>

Foundry测试合约`UniswapV2Flashloan.t.sol`：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "forge-std/Test.sol";
import "../src/UniswapV2Flashloan.sol";

address constant WETH = 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2;

contract UniswapV2FlashloanTest is Test {
    IWETH private weth = IWETH(WETH);

    UniswapV2Flashloan private flashloan;

    function setUp() public {
        flashloan = new UniswapV2Flashloan();
    }

    function testFlashloan() public {
        // 换weth，并转入flashloan合约，用做手续费
        weth.deposit{value: 1e18}();
        weth.transfer(address(flashloan), 1e18);
        // 闪电贷借贷金额
        uint amountToBorrow = 100 * 1e18;
        flashloan.flashloan(amountToBorrow);
    }

    // 手续费不足，会revert
    function testFlashloanFail() public {
        // 换weth，并转入flashloan合约，用做手续费
        weth.deposit{value: 1e18}();
        weth.transfer(address(flashloan), 3e17);
        // 闪电贷借贷金额
        uint amountToBorrow = 100 * 1e18;
        // 手续费不足
        vm.expectRevert();
        flashloan.flashloan(amountToBorrow);
    }
}
```

> [!NOTE]
>
> 这个测试合约使用了 `forge-std` 提供的 `Test` 合约来测试 `UniswapV2Flashloan` 的功能，主要分为两个测试用例：
>
> ### 1. **`setUp()` 函数**
> `setUp` 函数是在每个测试执行前都会运行的初始化函数，用来部署 `UniswapV2Flashloan` 合约。
> ```solidity
> function setUp() public {
>     flashloan = new UniswapV2Flashloan();
> }
> ```
> 每次测试运行时，都会创建一个新的 `UniswapV2Flashloan` 合约实例，确保每个测试的环境是独立的。
>
> ### 2. **`testFlashloan()` 测试闪电贷成功的场景**
> 这是一个基本的闪电贷测试，假设合约有足够的 WETH 用于支付手续费。
>
> #### 关键步骤：
> 1. **存入 WETH**：
>    ```solidity
>    weth.deposit{value: 1e18}();
>    ```
>    这里调用 WETH 合约的 `deposit()` 函数，将 `1 ETH` 换成等值的 `1 WETH`。WETH 是可转账的 ERC20 代币，代表了等值的 ETH。
>
> 2. **转移 WETH**：
>    ```solidity
>    weth.transfer(address(flashloan), 1e18);
>    ```
>    将 1 WETH 转移到 `flashloan` 合约地址，用于支付闪电贷的手续费。
>
> 3. **发起闪电贷**：
>    ```solidity
>    flashloan.flashloan(amountToBorrow);
>    ```
>    通过 `flashloan()` 函数发起借贷，这里假设要借 `100 WETH`。
>
> ### 3. **`testFlashloanFail()` 测试手续费不足导致失败的场景**
> 这个测试检查闪电贷失败的情况，特别是当支付的手续费不足时，是否会正确地回滚交易。
>
> #### 关键步骤：
> 1. **存入较少的 WETH**：
>    ```solidity
>    weth.deposit{value: 1e18}();
>    weth.transfer(address(flashloan), 3e17);
>    ```
>    这里只转移了 `0.3 WETH` 给 `flashloan` 合约，这不足以支付手续费（0.3%）。
>
> 2. **预期回滚**：
>    ```solidity
>    vm.expectRevert();
>    flashloan.flashloan(amountToBorrow);
>    ```
>    使用 `vm.expectRevert()` 来检测 `flashloan()` 是否会失败，因为手续费不足。闪电贷在无法支付手续费的情况下会 revert，因此测试应该通过。
>
> ### 总结：
> - `testFlashloan()` 模拟了成功的闪电贷流程，测试合约是否能正确借贷并支付手续费。
> - `testFlashloanFail()` 模拟了手续费不足的场景，验证了当手续费不够时，合约是否会正确回滚交易。
>
> 这些测试用例有助于确保闪电贷功能在不同的场景下正常工作，包括手续费充足和不足的情况下。

在测试合约中，我们分别测试了手续费充足和不足的情况，你可以在安装Foundry后使用下面的命令行进行测试（你可以将RPC换成其他以太坊RPC）：

```shell
FORK_URL=https://singapore.rpc.blxrbdn.com
forge test  --fork-url $FORK_URL --match-path test/UniswapV2Flashloan.t.sol -vv
```



### 2. Uniswap V3闪电贷

与Uniswap V2在`swap()`交换函数中间接支持闪电贷不同，Uniswap V3在[Pool池合约](https://github.com/Uniswap/v3-core/blob/main/contracts/UniswapV3Pool.sol#L791C1-L835C1)中加入了`flash()`函数直接支持闪电贷，核心代码如下：

```solidity
function flash(
    address recipient,
    uint256 amount0,
    uint256 amount1,
    bytes calldata data
) external override lock noDelegateCall {
    // 其他逻辑...

    // 乐观的发送代币到to地址
    if (amount0 > 0) TransferHelper.safeTransfer(token0, recipient, amount0);
    if (amount1 > 0) TransferHelper.safeTransfer(token1, recipient, amount1);

    // 调用to地址的回调函数uniswapV3FlashCallback
    IUniswapV3FlashCallback(msg.sender).uniswapV3FlashCallback(fee0, fee1, data);

    // 检查闪电贷是否归还成功
    uint256 balance0After = balance0();
    uint256 balance1After = balance1();
    require(balance0Before.add(fee0) <= balance0After, 'F0');
    require(balance1Before.add(fee1) <= balance1After, 'F1');

    // sub is safe because we know balanceAfter is gt balanceBefore by at least fee
    uint256 paid0 = balance0After - balance0Before;
    uint256 paid1 = balance1After - balance1Before;

    // 其他逻辑...
}
```

> [!NOTE]
>
> Uniswap V3 的 `flash()` 函数相比 Uniswap V2 的 `swap()` 函数，更直接地支持了闪电贷功能。核心逻辑如下：
>
> ### 1. **传递参数**
> ```solidity
> function flash(
>     address recipient,
>     uint256 amount0,
>     uint256 amount1,
>     bytes calldata data
> ) external override lock noDelegateCall {
> ```
> - `recipient`：闪电贷接收资产的地址。
> - `amount0` 和 `amount1`：分别表示 `token0` 和 `token1` 的借款数量。
> - `data`：用于回调函数的参数，在闪电贷过程中传递给 `uniswapV3FlashCallback`。
>
> ### 2. **乐观地发送借款**
> ```solidity
> if (amount0 > 0) TransferHelper.safeTransfer(token0, recipient, amount0);
> if (amount1 > 0) TransferHelper.safeTransfer(token1, recipient, amount1);
> ```
> 如果请求借款 `amount0` 或 `amount1` 大于 0，则将相应数量的 `token0` 和 `token1` 安全地转移到 `recipient` 地址。这一步是乐观的，即先将代币发出。
>
> ### 3. **调用回调函数**
> ```solidity
> IUniswapV3FlashCallback(msg.sender).uniswapV3FlashCallback(fee0, fee1, data);
> ```
> 在借款发出之后，合约会调用 `recipient` 实现的 `uniswapV3FlashCallback` 回调函数。该回调函数需要由调用方实现，并负责执行闪电贷的核心逻辑，例如利用借来的资金进行交易或套利。`fee0` 和 `fee1` 是借款的手续费，调用者必须在回调函数中处理这些费用，并在交易结束时归还借款及手续费。
>
> ### 4. **检查借款归还情况**
> ```solidity
> uint256 balance0After = balance0();
> uint256 balance1After = balance1();
> require(balance0Before.add(fee0) <= balance0After, 'F0');
> require(balance1Before.add(fee1) <= balance1After, 'F1');
> ```
> 回调函数执行完毕后，`flash()` 会检查借款是否已归还。通过检查当前的合约余额是否至少等于借款加上手续费，来确保闪电贷交易完成。
>
> - `balance0After` 和 `balance1After` 分别是合约在交易后的代币余额。
> - `fee0` 和 `fee1` 是分别对应 `token0` 和 `token1` 的手续费。
> - 通过 `require` 语句检查借款是否已成功归还，否则会触发回滚。
>
> ### 5. **计算已支付的费用**
> ```solidity
> uint256 paid0 = balance0After - balance0Before;
> uint256 paid1 = balance1After - balance1Before;
> ```
> 这一步计算合约在交易过程中实际收到的款项，确保用户归还了闪电贷的本金和费用。
>
> ### 总结：
> Uniswap V3 的 `flash()` 函数通过直接提供闪电贷接口，简化了闪电贷的调用流程。核心逻辑是：
> 1. 先乐观地将代币发送给调用者。
> 2. 通过回调函数让调用者执行套利或其他操作。
> 3. 最终检查是否已归还代币及手续费，确保交易的原子性。
>
> 这种设计使得用户无需通过 `swap()` 函数来间接触发闪电贷，而是可以通过专用的 `flash()` 函数，更加高效、直接地发起闪电贷。

下面，我们完成闪电贷合约`UniswapV3Flashloan.sol`。我们让它继承`IUniswapV3FlashCallback`，并将闪电贷的核心逻辑写在回调函数`uniswapV3FlashCallback`中。

整体逻辑与V2的类似，在闪电贷函数`flashloan()`中，我们从Uniswap V3的`WETH-DAI`池子借`WETH`。触发闪电贷之后，回调函数`uniswapV3FlashCallback`会被Pool合约调用，我们不进行套利，仅在计算利息后归还闪电贷。Uniswap V3每笔闪电贷的手续费与交易手续费一致。

**注意**：回调函数一定要做好权限控制，确保只有Uniswap的Pair合约可以调用，否则的话合约中的资金会被黑客盗光。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "./Lib.sol";

// UniswapV3闪电贷回调接口
// 需要实现并重写uniswapV3FlashCallback()函数
interface IUniswapV3FlashCallback {
    /// 在实现中，你必须偿还池中由 flash 发送的代币及计算出的费用金额。
    /// 调用此方法的合约必须经由官方 UniswapV3Factory 部署的 UniswapV3Pool 检查。
    /// @param fee0 闪电贷结束时，应支付给池的 token0 的费用金额
    /// @param fee1 闪电贷结束时，应支付给池的 token1 的费用金额
    /// @param data 通过 IUniswapV3PoolActions#flash 调用由调用者传递的任何数据
    function uniswapV3FlashCallback(
        uint256 fee0,
        uint256 fee1,
        bytes calldata data
    ) external;
}

// UniswapV3闪电贷合约
contract UniswapV3Flashloan is IUniswapV3FlashCallback {
    address private constant UNISWAP_V3_FACTORY = 0x1F98431c8aD98523631AE4a59f267346ea31F984;

    address private constant DAI = 0x6B175474E89094C44Da98b954EedeAC495271d0F;
    address private constant WETH = 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2;
    uint24 private constant poolFee = 3000;

    IERC20 private constant weth = IERC20(WETH);
    IUniswapV3Pool private immutable pool;

    constructor() {
        pool = IUniswapV3Pool(getPool(DAI, WETH, poolFee));
    }

    function getPool(
        address _token0,
        address _token1,
        uint24 _fee
    ) public pure returns (address) {
        PoolAddress.PoolKey memory poolKey = PoolAddress.getPoolKey(
            _token0,
            _token1,
            _fee
        );
        return PoolAddress.computeAddress(UNISWAP_V3_FACTORY, poolKey);
    }

    // 闪电贷函数
    function flashloan(uint wethAmount) external {
        bytes memory data = abi.encode(WETH, wethAmount);
        IUniswapV3Pool(pool).flash(address(this), 0, wethAmount, data);
    }

    // 闪电贷回调函数，只能被 DAI/WETH pair 合约调用
    function uniswapV3FlashCallback(
        uint fee0,
        uint fee1,
        bytes calldata data
    ) external {
        // 确认调用的是 DAI/WETH pair 合约
        require(msg.sender == address(pool), "not authorized");
        
        // 解码calldata
        (address tokenBorrow, uint256 wethAmount) = abi.decode(data, (address, uint256));

        // flashloan 逻辑，这里省略
        require(tokenBorrow == WETH, "token borrow != WETH");

        // 归还闪电贷
        weth.transfer(address(pool), wethAmount + fee1);
    }
}
```

> [!NOTE]
>
> 这个 `UniswapV3Flashloan` 合约的设计与 Uniswap V2 闪电贷类似，但它使用了 Uniswap V3 的 `flash()` 函数进行闪电贷。核心逻辑如下：
>
> ### 1. **接口定义**
> ```solidity
> interface IUniswapV3FlashCallback {
>     function uniswapV3FlashCallback(
>         uint256 fee0,
>         uint256 fee1,
>         bytes calldata data
>     ) external;
> }
> ```
> 这是 Uniswap V3 的回调接口定义。`uniswapV3FlashCallback` 函数将在闪电贷调用后触发，借款人必须在回调函数中归还本金及手续费。
>
> ### 2. **合约状态变量**
> ```solidity
> address private constant UNISWAP_V3_FACTORY = 0x1F98431c8aD98523631AE4a59f267346ea31F984;
> address private constant DAI = 0x6B175474E89094C44Da98b954EedeAC495271d0F;
> address private constant WETH = 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2;
> uint24 private constant poolFee = 3000;
> IERC20 private constant weth = IERC20(WETH);
> IUniswapV3Pool private immutable pool;
> ```
> - `UNISWAP_V3_FACTORY`: Uniswap V3 工厂合约地址，用于查询池地址。
> - `DAI` 和 `WETH`: 分别是 DAI 和 WETH 代币的合约地址。
> - `poolFee`: 交易费用设置为 0.3%（即 3000 基点）。
> - `weth`: 引用 WETH 的 ERC20 接口实例。
> - `pool`: 保存 DAI/WETH 池的实例。
>
> ### 3. **构造函数和获取池地址**
> ```solidity
> constructor() {
>     pool = IUniswapV3Pool(getPool(DAI, WETH, poolFee));
> }
> ```
> - `getPool`: 计算 DAI/WETH 池地址并赋值给 `pool` 变量。调用 `PoolAddress.computeAddress` 从 Uniswap V3 工厂获取池地址。
>
> ### 4. **闪电贷函数**
> ```solidity
> function flashloan(uint wethAmount) external {
>     bytes memory data = abi.encode(WETH, wethAmount);
>     IUniswapV3Pool(pool).flash(address(this), 0, wethAmount, data);
> }
> ```
> - `flashloan`: 用于执行闪电贷操作，指定借款的 `wethAmount`（WETH 借款数量）。`abi.encode` 将代币地址和借款数量编码传递给回调函数。
> - `IUniswapV3Pool(pool).flash`: 调用 Uniswap V3 的 `flash()` 函数，借取 `wethAmount` 数量的 WETH，0 表示不借 DAI。`data` 会被传递到回调函数中。
>
> ### 5. **回调函数**
> ```solidity
> function uniswapV3FlashCallback(
>     uint fee0,
>     uint fee1,
>     bytes calldata data
> ) external {
>     require(msg.sender == address(pool), "not authorized");
>     
>     (address tokenBorrow, uint256 wethAmount) = abi.decode(data, (address, uint256));
> 
>     require(tokenBorrow == WETH, "token borrow != WETH");
> 
>     weth.transfer(address(pool), wethAmount + fee1);
> }
> ```
> - `uniswapV3FlashCallback`: 该函数在闪电贷借款后被池合约调用。
>   - `require(msg.sender == address(pool))`: 确保只有正确的 Uniswap V3 池合约可以调用回调函数，防止恶意调用。
>   - `abi.decode(data, (address, uint256))`: 解码传递的数据，获取借款代币地址和数量。
>   - `require(tokenBorrow == WETH)`: 确认借款的是 WETH。
>   - `weth.transfer(address(pool), wethAmount + fee1)`: 归还借款和手续费。手续费 `fee1` 由池合约计算。
>
> ### 总结：
> Uniswap V3 的闪电贷通过 `flash()` 函数直接借款，并调用回调函数要求用户在交易结束时归还借款和手续费。合约中的回调函数 `uniswapV3FlashCallback` 负责处理这些逻辑，确保正确归还资金并防止外部恶意调用。

Foundry测试合约`UniswapV3Flashloan.t.sol`：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import {Test, console2} from "forge-std/Test.sol";
import "../src/UniswapV3Flashloan.sol";

address constant WETH = 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2;

contract UniswapV2FlashloanTest is Test {
    IWETH private weth = IWETH(WETH);

    UniswapV3Flashloan private flashloan;

    function setUp() public {
        flashloan = new UniswapV3Flashloan();
    }

    function testFlashloan() public {
        // 换weth，并转入flashloan合约，用做手续费
        weth.deposit{value: 1e18}();
        weth.transfer(address(flashloan), 1e18);
                
        uint balBefore = weth.balanceOf(address(flashloan));
        console2.logUint(balBefore);
        // 闪电贷借贷金额
        uint amountToBorrow = 1 * 1e18;
        flashloan.flashloan(amountToBorrow);
    }

    // 手续费不足，会revert
    function testFlashloanFail() public {
        // 换weth，并转入flashloan合约，用做手续费
        weth.deposit{value: 1e18}();
        weth.transfer(address(flashloan), 1e17);
        // 闪电贷借贷金额
        uint amountToBorrow = 100 * 1e18;
        // 手续费不足
        vm.expectRevert();
        flashloan.flashloan(amountToBorrow);
    }
}
```



在测试合约中，我们分别测试了手续费充足和不足的情况，你可以在安装Foundry后使用下面的命令行进行测试（你可以将RPC换成其他以太坊RPC）：

```shell
FORK_URL=https://singapore.rpc.blxrbdn.com
forge test  --fork-url $FORK_URL --match-path test/UniswapV3Flashloan.t.sol -vv
```



### 3. AAVE V3闪电贷

AAVE是去中心的借贷平台，它的[Pool合约](https://github.com/aave/aave-v3-core/blob/master/contracts/protocol/pool/Pool.sol#L424)通过`flashLoan()`和`flashLoanSimple()`两个函数支持单资产和多资产的闪电贷。这里，我们仅利用`flashLoan()`实现单个资产（`WETH`）的闪电贷。

下面，我们完成闪电贷合约`AaveV3Flashloan.sol`。我们让它继承`IFlashLoanSimpleReceiver`，并将闪电贷的核心逻辑写在回调函数`executeOperation`中。

整体逻辑与V2的类似，在闪电贷函数`flashloan()`中，我们从AAVE V3的`WETH`池子借`WETH`。触发闪电贷之后，回调函数`executeOperation`会被Pool合约调用，我们不进行套利，仅在计算利息后归还闪电贷。AAVE V3闪电贷的手续费默认为每笔`0.05%`，比Uniswap的要低。

**注意**：回调函数一定要做好权限控制，确保只有AAVE的Pool合约可以调用，并且发起者是本合约，否则的话合约中的资金会被黑客盗光。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "./Lib.sol";

interface IFlashLoanSimpleReceiver {
    /**
    * @notice 在接收闪电借款资产后执行操作
    * @dev 确保合约能够归还债务 + 额外费用，例如，具有
    *      足够的资金来偿还，并已批准 Pool 提取总金额
    * @param asset 闪电借款资产的地址
    * @param amount 闪电借款资产的数量
    * @param premium 闪电借款资产的费用
    * @param initiator 发起闪电贷款的地址
    * @param params 初始化闪电贷款时传递的字节编码参数
    * @return 如果操作的执行成功则返回 True，否则返回 False
    */
    function executeOperation(
        address asset,
        uint256 amount,
        uint256 premium,
        address initiator,
        bytes calldata params
    ) external returns (bool);
}

// AAVE V3闪电贷合约
contract AaveV3Flashloan {
    address private constant AAVE_V3_POOL =
        0x87870Bca3F3fD6335C3F4ce8392D69350B4fA4E2;

    address private constant WETH = 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2;

    ILendingPool public aave;

    constructor() {
        aave = ILendingPool(AAVE_V3_POOL);
    }

    // 闪电贷函数
    function flashloan(uint256 wethAmount) external {
        aave.flashLoanSimple(address(this), WETH, wethAmount, "", 0);
    }

    // 闪电贷回调函数，只能被 pool 合约调用
    function executeOperation(address asset, uint256 amount, uint256 premium, address initiator, bytes calldata)
        external
        returns (bool)
    {   
        // 确认调用的是 DAI/WETH pair 合约
        require(msg.sender == AAVE_V3_POOL, "not authorized");
        // 确认闪电贷发起者是本合约
        require(initiator == address(this), "invalid initiator");

        // flashloan 逻辑，这里省略

        // 计算flashloan费用
        // fee = 5/1000 * amount
        uint fee = (amount * 5) / 10000 + 1;
        uint amountToRepay = amount + fee;

        // 归还闪电贷
        IERC20(WETH).approve(AAVE_V3_POOL, amountToRepay);

        return true;
    }
}
```

> [!NOTE]
>
> 这个 `AaveV3Flashloan` 合约展示了如何通过 Aave V3 实现闪电贷，核心逻辑包含了借款、回调操作以及借款的归还。下面是代码的详细解释：
>
> ### 1. **接口定义**
> ```solidity
> interface IFlashLoanSimpleReceiver {
>     function executeOperation(
>         address asset,
>         uint256 amount,
>         uint256 premium,
>         address initiator,
>         bytes calldata params
>     ) external returns (bool);
> }
> ```
> 这是 Aave V3 闪电贷回调接口 `IFlashLoanSimpleReceiver`，需要实现 `executeOperation` 函数。当闪电贷完成后，Aave 会调用该函数，合约必须在此函数内处理借款逻辑并归还借款和费用。
>
> ### 2. **合约状态变量**
> ```solidity
> address private constant AAVE_V3_POOL = 0x87870Bca3F3fD6335C3F4ce8392D69350B4fA4E2;
> address private constant WETH = 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2;
> ILendingPool public aave;
> ```
> - `AAVE_V3_POOL`: Aave V3 的池合约地址，用于触发闪电贷。
> - `WETH`: WETH 的代币合约地址。
> - `aave`: Aave 的闪电贷池实例。
>
> ### 3. **构造函数**
> ```solidity
> constructor() {
>     aave = ILendingPool(AAVE_V3_POOL);
> }
> ```
> 构造函数初始化 Aave V3 的 `aave` 池合约，借助 `AAVE_V3_POOL` 地址。
>
> ### 4. **闪电贷函数**
> ```solidity
> function flashloan(uint256 wethAmount) external {
>     aave.flashLoanSimple(address(this), WETH, wethAmount, "", 0);
> }
> ```
> - `flashloan`: 发起闪电贷的函数，借入 `wethAmount` 数量的 WETH。
>   - `aave.flashLoanSimple`: 触发 Aave V3 的闪电贷。参数：
>     - `address(this)`: 触发闪电贷的地址，也就是当前合约。
>     - `WETH`: 借款的代币。
>     - `wethAmount`: 借款的数量。
>     - `""`: 附加数据，可以传递额外的信息，当前未使用。
>     - `0`: 闪电贷的引用。
>
> ### 5. **回调函数 `executeOperation`**
> ```solidity
> function executeOperation(
>     address asset,
>     uint256 amount,
>     uint256 premium,
>     address initiator,
>     bytes calldata
> ) external returns (bool) {
>     require(msg.sender == AAVE_V3_POOL, "not authorized");
>     require(initiator == address(this), "invalid initiator");
> 
>     uint fee = (amount * 5) / 10000 + 1;
>     uint amountToRepay = amount + fee;
> 
>     IERC20(WETH).approve(AAVE_V3_POOL, amountToRepay);
> 
>     return true;
> }
> ```
> 这是闪电贷的核心回调逻辑，执行后需要归还借款和手续费：
> - `require(msg.sender == AAVE_V3_POOL)`: 确保只有 Aave V3 的池合约可以调用此函数，防止外部恶意调用。
> - `require(initiator == address(this))`: 验证闪电贷发起者是本合约，确保安全性。
> - `fee`: 计算闪电贷的手续费，Aave V3 的手续费为 0.05%。
>
>   - 在计算 `fee` 时，`+1` 的目的是为了确保手续费的计算精确，避免因整数除法导致的舍入误差。以 Solidity 中的整数运算规则为基础，所有的计算都是整数操作，舍弃小数部分。例如，`(amount * 5) / 10000` 会在有小数时自动向下舍入，这会导致实际支付的手续费比应支付的少。
>
>     加上 `+1` 是为了应对这种舍入导致的潜在不足，确保即使舍入后手续费仍然能够覆盖实际费用，从而避免归还借款时因手续费不足导致交易失败。
>
> - `amountToRepay`: 借款数量加上手续费。
> - `IERC20(WETH).approve(AAVE_V3_POOL, amountToRepay)`: 批准池合约从合约中提取 WETH 用于归还借款。
>
> ### 总结：
> 这个合约展示了如何在 Aave V3 上发起闪电贷，并在回调函数中处理闪电贷的逻辑。重要的是，在 `executeOperation` 回调函数中验证调用者和发起者的身份，确保安全后归还借款和手续费。

Foundry测试合约`AaveV3Flashloan.t.sol`：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "forge-std/Test.sol";
import "../src/AaveV3Flashloan.sol";

address constant WETH = 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2;

contract UniswapV2FlashloanTest is Test {
    IWETH private weth = IWETH(WETH);

    AaveV3Flashloan private flashloan;

    function setUp() public {
        flashloan = new AaveV3Flashloan();
    }

    function testFlashloan() public {
        // 换weth，并转入flashloan合约，用做手续费
        weth.deposit{value: 1e18}();
        weth.transfer(address(flashloan), 1e18);
        // 闪电贷借贷金额
        uint amountToBorrow = 100 * 1e18;
        flashloan.flashloan(amountToBorrow);
    }

    // 手续费不足，会revert
    function testFlashloanFail() public {
        // 换weth，并转入flashloan合约，用做手续费
        weth.deposit{value: 1e18}();
        weth.transfer(address(flashloan), 4e16);
        // 闪电贷借贷金额
        uint amountToBorrow = 100 * 1e18;
        // 手续费不足
        vm.expectRevert();
        flashloan.flashloan(amountToBorrow);
    }
}
```



在测试合约中，我们分别测试了手续费充足和不足的情况，你可以在安装Foundry后使用下面的命令行进行测试（你可以将RPC换成其他以太坊RPC）：

```shell
FORK_URL=https://singapore.rpc.blxrbdn.com
forge test  --fork-url $FORK_URL --match-path test/AaveV3Flashloan.t.sol -vv
```



## 总结

这一讲，我们介绍了闪电贷，它允许用户在一个交易中借出并迅速归还资金，而无需提供任何抵押。并且，我们分别实现了Uniswap V2，Uniswap V3，和AAVE的闪电贷合约。

通过闪电贷，我们能够无抵押的撬动海量资金进行无风险套利或漏洞攻击。你准备用闪电贷做些什么呢？