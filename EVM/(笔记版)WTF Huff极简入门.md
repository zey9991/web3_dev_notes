# References

[01. Hello Huff | WTF Academy](https://www.wtf.academy/docs/huff-101/HelloHuff/)

# 01. Hello Huff

这一讲，我们将介绍Huff语言，并使用Foundry运行模版合约。

## Huff

大家可能很熟悉Solidity，但是几乎没听说过Huff。Huff是一个低级的、为Ethereum智能合约设计的编程语言，它允许开发者编写高度优化的EVM字节码。Huff的两大特点：

1. 难学: Huff不像Solidity抽象了EVM的底层工作原理，而是让开发者直接操作EVM的堆栈、内存、和存储。
2. 高效: Huff像是给EVM Opcodes套了一层壳，几乎是直接在字节码层面编写合约，gas优化到极致。

因此，你在学习Huff前需要熟悉Solidity和EVM的工作原理。推荐的先修课程：

1. [WTF Solidity](https://github.com/WTFAcademy/WTF-Solidity)
2. [WTF EVM Opcodes](https://github.com/WTFAcademy/WTF-EVM-Opcodes)

## Hello Huff

下面我们通过一个简单的合约`SimpleStore.huff`来学习Huff合约的结构。

```c
/* 接口 */
#define function setValue(uint256) nonpayable returns ()
#define function getValue() view returns (uint256)

/* 存储槽位 */
#define constant VALUE_LOCATION = FREE_STORAGE_POINTER()

/* 方法 */
#define macro SET_VALUE() = takes (0) returns (0) {
    0x04 calldataload   // [value]
    [VALUE_LOCATION]    // [ptr, value]
    sstore              // []
    stop                // []
}

#define macro GET_VALUE() = takes (0) returns (0) {
    // 从存储中加载值
    [VALUE_LOCATION]   // [ptr]
    sload                // [value]

    // 将值存入内存
    0x00 mstore

    // 返回值
    0x20 0x00 return
}

// 合约的主入口，判断调用的是哪个函数
#define macro MAIN() = takes (0) returns (0) {
    // 通过selector判断要调用哪个函数
    0x00 calldataload 0xE0 shr
    dup1 __FUNC_SIG(setValue) eq set jumpi
    dup1 __FUNC_SIG(getValue) eq get jumpi
    // 如果没有匹配的函数，就revert
    0x00 0x00 revert

    set:
        SET_VALUE()
    get:
        GET_VALUE()
}
```



下面，我们分段来学习这个huff合约。

首先，你需要定义合约的接口，像Solidity的接口一样，需要使用`#define`关键字。

```c
/* 接口 */
#define function setValue(uint256) nonpayable returns ()
#define function getValue() view returns (uint256)
```



接下来，你需要声明存储槽位（storage slot），就像在Solidity合约中声明状态变量一样。`FREE_STORAGE_POINTER()`指向合约中未使用的存储槽（free storage）。

```c
/* 存储槽位 */
#define constant VALUE_LOCATION = FREE_STORAGE_POINTER()
```



最后一部分要写合约中的方法（函数），本合约有`3`个方法：

1. `SET_VALUE()`: 改变`VALUE_LOCATION`存储的值。它先使用`calldataload`从calldata中读取变量的新值，然后使用`sstore`将新值存储到`VALUE_LOCATION`。
2. `GET_VALUE()`: 读取`VALUE_LOCATION`存储的值。它利用`sload`将`VALUE_LOCATION`存储的值推入堆栈，然后利用`mstore`将值存到内存，最后使用`return`返回。
3. `MAIN()`: 主宏，定义了合约的主入口。当对合约进行外部调用时，会运行这段代码来确定应该调用哪个函数。他先用`0x00 calldataload 0xE0 shr`读取calldata中的函数选择器，然后查看它是否与`SET_VALUE()`或`GET_VALUE()`匹配。如果匹配，就调用相应的函数；否则，回滚交易。

```c
/* 方法 */
#define macro SET_VALUE() = takes (0) returns (0) {
    0x04 calldataload   // [value]
    [VALUE_LOCATION]    // [ptr, value]
    sstore              // []
    stop                // []
}

#define macro GET_VALUE() = takes (0) returns (0) {
    // 从存储中加载值
    [VALUE_LOCATION]   // [ptr]
    sload                // [value]

    // 将值存入内存
    0x00 mstore

    // 返回值
    0x20 0x00 return
}

// 合约的主入口，判断调用的是哪个函数
#define macro MAIN() = takes (0) returns (0) {
    // 通过selector判断要调用哪个函数
    0x00 calldataload 0xE0 shr
    dup1 __FUNC_SIG(setValue) eq set jumpi
    dup1 __FUNC_SIG(getValue) eq get jumpi
    // 如果没有匹配的函数，就revert
    0x00 0x00 revert

    set:
        SET_VALUE()
    get:
        GET_VALUE()
}
```



## 运行模版项目

下面，我们介绍如何使用Foundry的插件foundry-huff运行模版项目。

### 配置环境

首先，你需要在本地安装以下内容：

- Git
  - 如果您可以运行`git --version`，则说明您已正确安装。
- Foundry / Foundryup
  - 这将会安装`forge`，`cast`和`anvil`
  - 通过运行`forge --version`并获取类似`forge 0.2.0 (92f8951 2022-08-06T00:09:32.96582Z)`的输出，您可以检测是否已正确安装。
  - 要获取每个工具的最新版本，只需运行`foundryup`。
- Huff Compiler
  - 如果您可以运行`huffc --version`并获取类似`huffc 0.3.0`的输出，则说明您已正确安装。

### 快速开始

1. 克隆[https://github.com/WTFAcademy/WTF-Huff]或[Huff模版仓库](https://github.com/huff-language/huff-project-template)。

运行：

```text
git clone https://github.com/WTFAcademy/WTF-Huff
cd WTF-Huff
```



1. 安装依赖

克隆并进入您的仓库后，您需要安装必要的依赖项。为此，只需运行：

```shell
forge install
```



1. 构建 & 测试

要构建并测试您的合约，您可以运行：

```shell
forge build
forge test
```





![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051310080.png)



1. 使用`huffc`打印huff合约的字节码：

```shell
huffc src/SimpleStore.huff -b
```



控制台输会输出合约的字节码（creation code）:

```text
602e8060093d393df35f3560e01c8063552410771461001e5780632096525514610025575f5ffd5b6004355f55005b5f545f5260205ff3
```



如果想获取runtime code，可以使用`huffc -r`。

有关如何使用Foundry的更多信息，请查看[Foundry Github Repository](https://github.com/foundry-rs/foundry/tree/master/forge)和[foundry-huff library repository](https://github.com/huff-language/foundry-huff)。

### 项目结构图

```ml
lib
├─ forge-std — https://github.com/foundry-rs/forge-std
├─ foundry-huff — https://github.com/huff-language/foundry-huff
scripts
├─ Deploy.s.sol — 部署脚本
src
├─ SimpleStore — Huff中的简单存储合约
test
└─ SimpleStore.t — SimpleStore测试
```



## 总结

这一讲，我们介绍了Huff语言，学习了Huff合约结构，并运行了一个模版项目。Huff是一个低级的、为以太坊智能合约设计的编程语言，学习它不仅可以让你写出更优化的合约，还可以让你深入理解EVM。

# 02. 存储

这一讲，我们将介绍Huff中的存储，特别是`FREE_STORAGE_POINTER`关键字。

## Huff中的存储

EVM中的存储（storage）是一种持久化存储空间，存在其中的数据在交易之间可以保持。它是EVM状态的一部分，支持以256 bit为单位的读写。



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051310299.png)



### 声明存储槽

Huff中的存储并不复杂，可以通过`FREE_STORAGE_POINTER()`关键字来跟踪合约中未使用的存储槽（free storage）。下面，我们声明了`2`个存储槽`STORAGE_SLOT0`和`STORAGE_SLOT1`：

```c
#define constant STORAGE_SLOT0 = FREE_STORAGE_POINTER()
#define constant STORAGE_SLOT1 = FREE_STORAGE_POINTER()
```



EVM的存储使用键值对存储数据，存储槽是其中的键。在Huff中，编译器将在编译时从0开始分配自由存储槽。在上面的例子中，会将`0`分配给`STORAGE_SLOT0`，将`1`分配给`STORAGE_SLOT1`。

## 使用存储槽

我们可以通过将存储槽括在方括号中来在代码中引用该槽 - 就像这样`[STORAGE_SLOT0]`。在下面的代码中，我们在`MAIN()`宏中将`0x69`存入`STORAGE_SLOT0`，然后将`0x420`存入`STORAGE_SLOT1`。

```c
#define macro MAIN() = takes(0) returns(0) {
    0x69             // [0x69] 
    [STORAGE_SLOT0]         // [value_slot0_pointer, 0x69]
    sstore          // []

    0x420             // [0x420] 
    [STORAGE_SLOT1]         // [value_slot1_pointer, 0x420]
    sstore          // []
}
```



## 分析合约字节码

我们可以使用`huffc`命令获取上面合约的runtime code:

```shell
huffc src/02_Storage.huff -r
```



打印出的bytecode为：

```text
60695f55610420600155
```



直接看字节码可能有些令人头大，我们将它转换成下面的表格：

| pc   | op      | opcode      | stack  |
| ---- | ------- | ----------- | ------ |
| [00] | 60 69   | PUSH1 0x69  | 0x69   |
| [02] | 5f      | PUSH0       | 0 0x69 |
| [03] | 55      | SSTORE      |        |
| [04] | 61 0420 | PUSH2 0x420 | 0x0420 |
| [07] | 60 01   | PUSH1 0x01  | 0x01   |
| [09] | 55      | SSTORE      |        |

可以看到，字节码用了两次`SSTORE`，分别将`0x69`和`0x420`存入存储槽`0`和`1`。

## 总结

这一讲，我们介绍了如何在Huff中使用存储，特别是`FREE_STORAGE_POINTER()`关键字，它可以跟踪合约中未使用的存储槽，并在编译时分配它们。

# 03. 常量

这一讲，我们将介绍Huff中的常量和`constant`关键字。

## 常量

Huff的常量和Solidity中的相似，它们不会被包含在存储（storage）中，而是在编译时在合约内调用（包含在字节码中）。常量可以是最多32字节的数据或是`FREE_STORAGE_POINTER()`关键字（代表合约中尚未使用的存储槽）。

### 声明常量

你可以使用`constant`关键字在合约中声明常量：

```c
#define constant NUM = 0x69
#define constant STORAGE_SLOT0 = FREE_STORAGE_POINTER()
```



### 使用常量

你可以使用括号表示法`[CONSTANT]`将常量压入堆栈。

```c
#define macro MAIN() = takes(0) returns(0) {
    [NUM]             // [0x69] 
    [STORAGE_SLOT0]         // [value_slot0_pointer, 0x69]
    sstore          // []
}
```



在上面的`MAIN()`宏中，我们将常量`NUM`（值为`0x69`）和`STORAGE_SLOT0`（值为`0`）压入堆栈，然后使用`sstore`指令将`0x69`存入存储槽`0`。

## 分析合约字节码

我们可以使用`huffc`命令获取上面合约的runtime code:

```shell
huffc src/03_Constant.huff -r
```



打印出的bytecode为：

```text
60695f55
```



转换成格式化的表格：

| pc   | op    | opcode     | stack  |
| ---- | ----- | ---------- | ------ |
| [00] | 60 69 | PUSH1 0x69 | 0x69   |
| [02] | 5f    | PUSH0      | 0 0x69 |
| [03] | 55    | SSTORE     |        |

我们可以看到，这个合约做的就是使用`SSTORE`指令将`0x69`存储在存储槽`0`中。

## 总结

这一讲，我们介绍了Huff中的常量和`constant`关键字。常量不会占用存储，而是会在编译时被调用。

# 04. 宏

这一讲，我们将介绍Huff中的宏和`macro`关键字。

## 宏

Huff中有两种可以将字节码组合起来的方法，一种叫宏`Macros`，另一种叫函数`Functions`。两者之间有一些差异，但是大多数时候开发者应该使用宏，而不是函数。定义宏时需要使用`macro`关键字，规则如下：

```c
#define macro MACRO_NAME(arguments) = takes (1) returns (3) {
    // ...
}
```



其中:

- `MACRO_NAME`: 宏的名称。
- `arguments`: 宏的参数，可以没有。
- `takes (1)`: 指定宏/函数接受的堆栈输入数量，可以没有，默认为`0`。
- `returns (3)`: 指定宏/函数输出的堆栈元素数量，可以没有，默认为`0`。

> 比较奇怪的是，当前的huff编译器并不会检查`takes`和`returns`的数量，所以当前它们只是个摆设。未来版本可能会加上检查？

在下面的例子中，`SAVE()`宏接受一个参数`value`，然后将它的值存储在存储槽`STORAGE_SLOT0`。在宏中，我们使用`<value>`来使用参数的值。

```c
#define constant STORAGE_SLOT0 = FREE_STORAGE_POINTER()

// 这个宏接受一个参数 value，然后将它的值存储在 STORAGE_SLOT0
#define macro SAVE(value) = takes(0) returns(0) {
    <value>                 // [value]
    [STORAGE_SLOT0]         // [value_slot0_pointer, value]
    sstore          // []
}

#define macro MAIN() = takes(0) returns(0) {
    SAVE(0x420)          // []
}
```



## 分析合约字节码

我们可以使用`huffc`命令获取上面合约的runtime code:

```shell
huffc src/04_Macro.huff -r
```



打印出的bytecode为：

```text
6104205f55
```



转换成格式化的表格：

| pc   | op      | opcode       | stack    |
| ---- | ------- | ------------ | -------- |
| [00] | 61 0420 | PUSH2 0x0420 | 0x0420   |
| [03] | 5f      | PUSH0        | 0 0x0420 |
| [04] | 55      | SSTORE       |          |

我们可以看到，这个合约做的就是使用`SSTORE`指令将`0x0420`存储在存储槽`0`中。

## 总结

这一讲，我们介绍了Huff中的宏和`macro`关键字。Huff中的宏和函数很相似，但是开发者大多数时间应该使用宏，而不是函数。

# 05. Main宏

这一讲，我们将介绍Huff中的`MAIN`宏，它是合约的主入口。

## Main 宏

`Main`宏是一个特殊的宏，作为合约的主入口，每个Huff合约必须有一个。它的作用类似于Solidity中的`fallback`函数，当对合约进行外部调用时，会运行这段代码来确定应该调用哪个函数。

声明时需要用`MAIN()`关键字：

```c
#define macro MAIN() = takes (0) returns (0) {
    // ...
}
```



下面我们写一个简单的合约：

```c
#define macro PUSH_69() = takes(0) returns(1) {
    push1 0x69                 // [0x69]
}

#define macro SAVE() = takes(1) returns(0) {
    // [0x69]
    [STORAGE_SLOT0]         // [value_slot0_pointer, 0x69]
    sstore          // []

}

#define macro MAIN() = takes(0) returns(0) {
    PUSH_69()          // []
    SAVE()
}
```



上面合约中的`PUSH_69()`宏会将`0x69`压入堆栈中（`returns(1)`），而`SAVE()`宏（`takes(1)`）会将堆栈顶端的值保存到存储槽`STORAGE_SLOT0`。在`Main`宏中，我们一次调用了`PUSH_69()`和`SAVE()`。

## 分析合约字节码

我们可以使用`huffc`命令获取上面合约的runtime code:

```shell
huffc src/05_Main.huff -r
```



打印出的bytecode为：

```text
60695f55
```



转换成格式化的表格：

| pc   | op    | opcode     | stack  |
| ---- | ----- | ---------- | ------ |
| [00] | 60 69 | PUSH2 0x69 | 0x69   |
| [02] | 5f    | PUSH0      | 0 0x69 |
| [03] | 55    | SSTORE     |        |

我们可以看到，这个合约实际上做的就是使用`SSTORE`指令将`0x69`存储在存储槽`0`中。

## 总结

这一讲，我们介绍了Huff中的`Main`宏和`MAIN`关键字。Huff中的`Main`宏是合约的主入口，每个合约必须包含它，功能与Solidity中的`fallback`函数类似。

# 06. 控制流

这一讲，我们将介绍Huff中的控制流，包括跳转标签和`JUMPDEST`指令。

## 控制流

EVM底层主要是使用跳转指令`JUMP`，`JUMPI`，和`JUMPDEST`进行代码的流程控制。如果你对它们不了解，建议阅读[WTF EVM Opcodes教程第9讲](https://github.com/WTFAcademy/WTF-EVM-Opcodes/tree/main/09_FlowOp)。

为了方便开发者使用跳转指令，Huff提供了跳转标签，可以在宏或函数哪定义，由冒号后跟一个单词表示。注意，虽然看起来标签是由于缩进而作为代码块的作用域，但它们实际上只是字节码中的跳转目的地。如果标签下面存在操作，除非程序计数器被更改或执行由`revert`、`return`、`stop`或`selfdestruct`操作码中断，否则它们将被执行。

```text
#define macro MAIN() = takes (0) returns (0) {
    // 从 calldata 读取值
    0x00 calldataload        // [calldata @ 0x00]
    0 eq
    jump_one jumpi

    // 如果到达此点，则revert
    0x00 0x00 revert

    // 跳转标签1
    jump_one:
        jump_two jump
        // 如果到达此点，则revert
        0x00 0x00 revert

    // 跳转标签2
    jump_two:
        0x00 0x00 return
}
```



在合约中，`Main`宏先会读取调用的`calldata`，如果为`0`，则先跳转到`jump_one`，接着跳转到`jump_two`；如果不为`0`，则不会跳转，继续运行到`revert`回滚交易。

## 分析合约字节码

我们可以使用`huffc`命令获取上面合约的runtime code:

```shell
huffc src/06_ControlFlow.huff -r
```



打印出的bytecode为：

```text
5f355f1461000b575f5ffd5b610013565f5ffd5b5f5ff3
```



转换成格式化的表格：

| pc   | op      | opcode       | stack         |
| ---- | ------- | ------------ | ------------- |
| [00] | 5f      | PUSH0        | 0x00          |
| [01] | 35      | CALLDATALOAD | calldata      |
| [02] | 5f      | PUSH0        | 0x00 calldata |
| [03] | 14      | EQ           | suc           |
| [04] | 61 000b | PUSH2 0x000b | 0x000b suc    |
| [07] | 57      | JUMPI        |               |
| [08] | 5f      | PUSH0        | 0x00          |
| [09] | 5f      | PUSH0        | 0x00 0x00     |
| [0a] | fd      | REVERT       |               |
| [0b] | 5b      | JUMPDEST     |               |
| [0c] | 61 0013 | PUSH2 0x0013 | 0x0013        |
| [0e] | 56      | JUMP         |               |
| [10] | 5f      | PUSH0        | 0x00          |
| [11] | 5f      | PUSH0        | 0x00 0x00     |
| [12] | fd      | REVERT       |               |
| [13] | 5b      | JUMPDEST     |               |
| [14] | 5f      | PUSH0        | 0x00          |
| [15] | 5f      | PUSH0        | 0x00 0x00     |
| [16] | f3      | RETURN       |               |

我们可以看到，这段字节码的功能：

1. `CALLDATALOAD`从`calldata`中读取值
2. 用`EQ`对比数据是否为`0`。若`calldata`为`0`，`suc = 1`，程序计数器（PC）通过`JUMPI`跳转到`0x0b`位置，也就时跳转标签`jump_one`标记的地方。若`calldata`不为`0`，则会继续运行，直到在`0xfd`的`REVERT`指令回滚交易。
3. 在`0x0b`继续运行，程序会遇到`JUMP`指令，PC跳转到`0x13`位置，也就是跳转标签`jump_two`标记的地方。
4. 在`0x13`继续运行，见到`RETURN`，返回数据并结束交易。

可以看到Huff的编译器在这里并没有做到最优，因为合约中`JUMPDEST`的位置可以用`1`字节表示，但它却用了`2`字节，`0x000b`和`0x0013`，浪费了gas。

## 总结

这一讲，我们介绍了Huff中的控制流。Huff提供了跳转标签，方便开发者使用`JUMP`和`JUMPI`进行流程控制。

# 07. 接口

这一讲，我们将介绍Huff中的接口，它可以用来生成Solidity接口合约/ABI，并且方便我们在合约中使用函数选择器（function selector）和事件哈希（event hash）。

## 接口

类似Solidity，你可以在Huff合约的接口中定义函数`functions`，事件`events`，和错误`errors`。接口主要有两个作用：

1. 定义接口后，函数名可以用作内置函数`__FUNC_SIG`（获取函数选择器），`__EVENT_HASH`（事件选择器），和`__ERROR`（错误选择器）的参数
2. 生成 Solidity 接口/合约 ABI。

接口中的函数可以是`view`、`pure`、`payable`或`nonpayable`类型。并且，只有外部可见的函数需要在接口中定义，内部函数不需要。接口中的事件可以包含索引值（使用`indexed`关键字）和非索引值。

Huff接口的例子：

```c
#define function testFunction(uint256, bytes32) view returns (bytes memory)

#define event TestEvent(address indexed, uint256)
```



## Simple Store合约

现在，让我们重温第一讲中介绍的`Simple Store`合约。学到这里，你应该能看懂它了。

我们把合约分为两部分，第一部分定义了合约的接口，存储槽，并用宏实现了接口中定义的`SET_VALUE()`和`GET_VALUE`方法。

- `SET_VALUE()`: 先使用`calldataload`从`calldata`读出了新值，然后使用`sstore`将值保存在存储槽`VALUE_LOCATION`中。注意，第一行`0x04 calldataload`读取值的时候略去了前`4`字节，因为它们是函数选择器。
- `GET_VALUE()`: 先使用`sload`读取存储槽`VALUE_LOCATION`的值，使用`mstore`将值存入内存，再使用`return`返回。

> 注意，一定要确保每个方法被正确的结束，代码以`return`，`revert`，`stop`，`invalid`指令结尾，不然可能会有漏洞。

```c
/* 接口 */
#define function setValue(uint256) nonpayable returns ()
#define function getValue() view returns (uint256)

/* 存储槽位 */
#define constant VALUE_LOCATION = FREE_STORAGE_POINTER()

/* 方法 */
#define macro SET_VALUE() = takes (0) returns (0) {
    0x04 calldataload   // [value]
    [VALUE_LOCATION]    // [ptr, value]
    sstore              // []
    stop                // []
}

#define macro GET_VALUE() = takes (0) returns (0) {
    // 从存储中加载值
    [VALUE_LOCATION]   // [ptr]
    sload                // [value]

    // 将值存入内存
    0x00 mstore

    // 返回值
    0x20 0x00 return
}
```



第二部分是Main宏，合约的主入口，判断外部调用的是哪个函数。

```c
// 合约的主入口，判断调用的是哪个函数
#define macro MAIN() = takes (0) returns (0) {
    // 通过selector判断要调用哪个函数
    0x00 calldataload 0xE0 shr
    dup1 __FUNC_SIG(setValue) eq set jumpi
    dup1 __FUNC_SIG(getValue) eq get jumpi
    // 如果没有匹配的函数，就revert
    0x00 0x00 revert

    set:
        SET_VALUE()
    get:
        GET_VALUE()
}
```



1. 第一行，我们使用`0x00 calldataload 0xE0 shr`读取`calldata`中前`4`字节，也就是函数选择器。这段代码我们会经常使用，你可以想一想它是怎么工作的。
2. 获取`selector`后，我们要通过比对`setValue()`和`getValue()`进行跳转，如果没有匹配的函数，则`revert`。由于我们在接口中定义了这两个函数，我们可以使用内置函数`__FUNC_SIG()`获取他们的`selector`并推入堆栈，然后使用`eq`进行比对。不然的话，就要使用`__FUNC_SIG("function setValue(uint256) nonpayable returns ()")`，很繁琐。
3. 在`set`和`get`两个跳转标签之后，我们分别运行`SET_VALUE()`和`GET_VALUE()`方法，执行相应的逻辑。

## 输出Solidity接口/ABI

我们可以使用`huffc -g`命令将Huff合约的接口转为Solidity合约接口/ABI:

```shell
huffc src/07_Interface.huff -g
```



输出的接口将保存在和`07_Interface.huff`相同的文件夹下，例如`src/I07_Iterface.sol`，内容：

```solidity
interface I07_Interface {
    function getValue() external view returns (uint256);
    function setValue(uint256) external;
}
```



## 分析合约字节码

我们可以使用`huffc`命令获取上面合约的runtime code:

```shell
huffc src/07_Interface.huff -r
```



打印出的bytecode为：

```text
5f3560e01c8063552410771461001e5780632096525514610025575f5ffd5b6004355f55005b5f545f5260205ff3
```



转换成格式化的表格：

| pc   | op          | opcode           | stack                        |
| ---- | ----------- | ---------------- | ---------------------------- |
| [00] | 5f          | PUSH0            | 0x00                         |
| [01] | 35          | CALLDATALOAD     | calldata                     |
| [02] | 60e0        | PUSH1 0xE0       | 0xE0 calldata                |
| [04] | 1c          | SHR              | selector                     |
| [05] | 80          | DUP1             | selector selector            |
| [06] | 63 55241077 | PUSH4 0x55241077 | 0x55241077 selector selector |
| [0a] | 14          | EQ               | suc selector                 |
| [0b] | 61 001e     | PUSH2 0x001E     | 0x001E suc selector          |
| [0e] | 57          | JUMPI            | selector                     |
| [0f] | 80          | DUP1             | selector selector            |
| [10] | 63 209652   | PUSH4 0x20965255 | 0x20965255 selector selector |
| [14] | 14          | EQ               | suc selector                 |
| [15] | 61 0024     | PUSH2 0x0024     | 0x0024 suc selector          |
| [18] | 57          | JUMPI            | selector                     |
| [19] | 5f          | PUSH0            | 0x00 selector                |
| [1a] | 5f          | PUSH0            | 0x00 0x00 selector           |
| [1b] | fd          | REVERT           | selector                     |
| [1c] | 5b          | JUMPDEST         | selector                     |
| [1d] | 60 04       | PUSH1 0x04       | 0x04 selector                |
| [1f] | 35          | CALLDATALOAD     | calldata@0x04 selector       |
| [20] | 5f          | PUSH0            | 0x00 calldata@0x04 selector  |
| [21] | 55          | SSTORE           | selector                     |
| [22] | 00          | STOP             | selector                     |
| [23] | 5b          | JUMPDEST         | selector                     |
| [24] | 5f          | PUSH0            | 0x00 selector                |
| [25] | 54          | SLOAD            | value selector               |
| [26] | 5f          | PUSH0            | 0x00 value selector          |
| [27] | 52          | MSTORE           | selector                     |
| [28] | 60 20       | PUSH1 0x20       | 0x20 selector                |
| [2a] | 5f          | PUSH0            | 0x00 0x20 selector           |
| [2b] | f3          | RETURN           | selector                     |

我们可以看到，这段字节码的功能：

1. 使用`CALLDATALOAD`从`calldata`中读取值，然后使用`SHR`获取前`4`字节的函数选择器。
2. 用`EQ`对比`calldata`中的函数选择器是否为`0x55241077`或`0x20965255`，若匹配，则将PC跳转到相应的`JUMPDEST`，执行`SET_VALUE()`或`GET_VALUE()`方法。

## 总结

这一讲，我们介绍了Huff中的接口，它可以用来生成Solidity接口合约/ABI，并且方便我们在合约中使用函数选择器和事件哈希。

# 08. 事件

这一讲，我们将介绍Huff中的事件，和Solidity中的事件一样，它可以将数据存储在`EVM`的日志中。

## 事件

在Solidity中，我们常常使用`event`来定义和触发事件。当这些事件被触发时，它们会生成日志，将数据永久存储在区块链上。日志分为主题（`topic`）和数据（`data`）。第一个主题通常是事件签名的哈希值，后面的主题是由`indexed`修饰的事件参数。如果你对`event`不了解，请阅读WTF Solidity的[相应章节](https://github.com/AmazingAng/WTF-Solidity/tree/main/12_Event)。

EVM中的`LOG`指令用于创建这些日志。指令`LOG0`到`LOG4`的区别在于它们包含的主题数量。例如，`LOG0`没有主题，而`LOG4`有四个主题。如果你不了解它们，请阅读[WTF EVM Opcodes第15讲](https://github.com/WTFAcademy/WTF-EVM-Opcodes/blob/main/15_LogOp/readme.md)。

## Huff中的事件

下面我们改造上一讲的`Simple Store`合约，在调用`SET_VALUE()`方法改变值的时候，会释放一个`ValueChanged`事件，将新值记录到EVM日志中。

首先你可以在Huff接口中定义合约的事件：

```c
#define event ValueChanged(uint256 indexed)
```



接下来我们在`SET_VALUE()`方法中释放`ValueChanged`事件。首先，要确定我们要用哪个`LOG`指令来释放事件。因为我们事件只有一个被索引的数据，再加上事件哈希，就是`2`个主题，应使用`log2`，输入堆栈为`[0, 0, sig, value]`。接下来，我们只需要在方法中构造所需的堆栈，再在结尾使用`log2`输出日志即可。我们可以使用内置函数`__EVENT_HASH()`将事件哈希压入堆栈。

```c
#define macro SET_VALUE() = takes (0) returns (0) {
    0x04 calldataload   // [value]
    dup1                // [value, value]
    [VALUE_LOCATION]    // [ptr, value, value]
    sstore              // [value]
    // 释放事件
    __EVENT_HASH(ValueChanged) // [sig, value]
    push0 push0         // [0, 0, sig, value]
    log2                // []
    stop                // []
}
```



## 输出Solidity接口/ABI

我们可以使用`huffc -g`命令将Huff合约的接口转为Solidity合约接口/ABI:

```shell
huffc src/08_Event.huff -g
```



输出的接口将保存在和`08_Event.huff`相同的文件夹下，例如`src/I08_Event.sol`。可以看到，我们定义的事件已经被包含在接口中：

```solidity
interface I08_Event {
    event ValueChanged(uint256 indexed);
    function getValue() external view returns (uint256);
    function setValue(uint256) external;
}
```



## 分析合约字节码

我们可以使用`huffc`命令获取上面合约的runtime code:

```shell
huffc src/08_Events.huff -r
```



打印出的bytecode为：

```text
5f3560e01c8063552410771461001e578063209652551461004a575f5ffd5b600435805f557fd9ce50fb8c432a73c4ed7e62e6128c95e62f29d3ee56042781a0368f192ccdb45f5fa2005b5f545f5260205ff3
```



转换成格式化的表格（后半部分在`stack`中省略了一个用不上的`selector`）：

| pc   | op          | opcode            | stack                            |
| ---- | ----------- | ----------------- | -------------------------------- |
| [00] | 5f          | PUSH0             | 0x00                             |
| [01] | 35          | CALLDATALOAD      | calldata                         |
| [02] | 60 e0       | PUSH1 0xE0        | 0xE0 calldata                    |
| [04] | 1c          | SHR               | selector                         |
| [05] | 80          | DUP1              | selector selector                |
| [06] | 63 55241077 | PUSH4 0x55241077  | 0x55241077 selector selector     |
| [0a] | 14          | EQ                | suc selector                     |
| [0b] | 61 001e     | PUSH2 0x001E      | 0x001E suc selector              |
| [0e] | 57          | JUMPI             | selector                         |
| [0f] | 80          | DUP1              | selector selector                |
| [10] | 63 209652   | PUSH4 0x20965255  | 0x20965255 selector selector     |
| [14] | 14          | EQ                | suc selector                     |
| [15] | 61 0049     | PUSH2 0x0049      | 0x0049 suc selector              |
| [18] | 57          | JUMPI             | selector                         |
| [19] | 5f          | PUSH0             | 0x00                             |
| [1a] | 5f          | PUSH0             | 0x00 0x00                        |
| [1b] | fd          | REVERT            |                                  |
| [1c] | 5b          | JUMPDEST          |                                  |
| [1d] | 60 04       | PUSH1 0x04        | 0x04                             |
| [1f] | 35          | CALLDATALOAD      | calldata@0x04                    |
| [20] | 5f          | PUSH0             | 0x00 calldata@0x04               |
| [21] | 55          | SSTORE            |                                  |
| [22] | 5b          | JUMPDEST          |                                  |
| [23] | 60 04       | PUSH1 0x04        | 0x04                             |
| [25] | 35          | CALLDATALOAD      | calldata@0x04                    |
| [26] | 80          | DUP1              | calldata@0x04 calldata@0x04      |
| [27] | 5f          | PUSH0             | 0x00 calldata@0x04 calldata@0x04 |
| [28] | 55          | SSTORE            | calldata@0x04                    |
| [29] | 7f d9ce50.  | PUSH32 0xd9ce50.. | 0xd9ce50.. calldata@0x04         |
| [46] | 5f          | PUSH0             | 0x00 0xd9ce50 calldata@0x04      |
| [47] | 5f          | PUSH0             | 0x00 0x00 0xd9ce50 calldata@0x04 |
| [48] | a2          | LOG2              |                                  |
| [49] | 00          | STOP              |                                  |
| [4a] | 5b          | JUMPDEST          |                                  |
| [4b] | 5f          | PUSH0             | 0x00                             |
| [4c] | 54          | SLOAD             | value                            |
| [4d] | 5f          | PUSH0             | 0x00 value                       |
| [4e] | 52          | MSTORE            |                                  |
| [4f] | 60 20       | PUSH1 0x20        | 0x20                             |
| [51] | 5f          | PUSH0             | 0x00 0x20                        |
| [52] | f3          | RETURN            |                                  |

其中，`[22]-[49]`是`SET_VALUE()`方法的字节码。我们可以看到，这段代码在准备好堆栈`[0x00 0x00 0xd9ce50 calldata@0x04]`之后，使用`log2`释放事件。

## 总结

这一讲，我们介绍了Huff中的事件，它与Solidity的事件一样，可以将数据记录在EVM日志中。Huff提供了内置方法`__EVENT_HASH()`，方便我们计算事件哈希并将它压入堆栈。

# 09. Error

Huff允许你在合约自定义错误`Error`，这一讲我们将介绍它。

## Error

Solidity中有三种抛出异常的方法`error`，`require`和`assert`，他们都是基于`EVM`的`revert`指令。在Huff中，我们可以直接使用`revert`指令来抛出错误并返回错误信息。

### 定义错误

你可以在合约接口中定义错误：

```c
/* 接口 */
#define function getError() view returns (uint256)
#define error CustomError(uint256)
```



### 使用错误

在方法中，你可以使用内置函数`__ERROR()`将错误选择器（error selector）推到堆栈上。

```c
#define macro GET_ERROR() = takes (0) returns (0) {
    __ERROR(PanicError)   // [panic_error_selector, panic_code]
    0x00 mstore           // [panic_code]
    0x04 mstore           // []
    0x24 0x00 revert
}
```



然后我们写一个Main宏作为合约的入口：

```c
// 合约的主入口，判断调用的是哪个函数
#define macro MAIN() = takes (0) returns (0) {
    // 通过selector判断要调用哪个函数
    0x00 calldataload 0xE0 shr
    dup1 __FUNC_SIG(GET_ERROR) eq get_error jumpi
    // 如果没有匹配的函数，就revert
    0x00 0x00 revert

    get_error:
        GET_ERROR()
}
```



## 分析合约字节码

我们可以使用`huffc`命令获取上面合约的runtime code:

```shell
huffc src/09_Error.huff -r
```



打印出的bytecode为：

```text
5f3560e01c8063ee23e35814610013575f5ffd5b60697f110b3655000000000000000000000000000000000000000000000000000000005f5260045260245ffd
```



转换成格式化的表格（后半部分在`stack`中省略了一个用不上的`selector`）：

| pc   | op           | opcode           | stack                        |
| ---- | ------------ | ---------------- | ---------------------------- |
| [00] | 5f           | PUSH0            | 0x00                         |
| [01] | 35           | CALLDATALOAD     | calldata                     |
| [02] | 60 e0        | PUSH1 0xE0       | 0xE0 calldata                |
| [04] | 1c           | SHR              | selector                     |
| [05] | 80           | DUP1             | selector selector            |
| [06] | 63 ee23e358  | PUSH4 0xEE23E358 | 0xEE23E358 selector selector |
| [0b] | 14           | EQ               | suc selector                 |
| [0c] | 61 0013      | PUSH2 0x0013     | 0x0013 suc selector          |
| [0f] | 57           | JUMPI            | selector                     |
| [10] | 5f           | PUSH0            | 0x00 selector                |
| [11] | 5f           | PUSH0            | 0x00 0x00 selector           |
| [12] | fd           | REVERT           | selector                     |
| [13] | 5b           | JUMPDEST         |                              |
| [14] | 60 69        | PUSH1 0x69       | 0x69                         |
| [16] | 7f 0x110b... | PUSH32 0x110b... | 0x69 0x110b...               |
| [2d] | 5f           | PUSH0            | 0x00 0x69 0x110b...          |
| [2e] | 52           | MSTORE           | 0x110b...                    |
| [2f] | 60 04        | PUSH1 0x04       | 0x04 0x110b...               |
| [31] | 52           | MSTORE           |                              |
| [32] | 60 24        | PUSH1 0x24       | 0x24                         |
| [34] | 5f           | PUSH0            | 0x00 0x24                    |
| [35] | fd           | REVERT           |                              |

从`[16]`可以看到，目前内置函数`__ERROR`并没有被优化的很好，因为它会先计算出`4`字节的`error selector`（此处为`0x110b3655`），然后再将它转换为`32`字节的数据（右填充`0`，变为`110b365500000000000000000000000000000000000000000000000000000000`），最后使用`PUSH32`压入堆栈。但实际上，我们需要的只是前`4`字节，这样造成了gas浪费。

## 总结

这一讲，我们介绍了如何在Huff中自定义错误并使用它。Huff提供了内置函数`__ERROR`来获取错误选择器，但它没有被很好的优化。

# 10. Constructor

这一讲，我们介绍Huff中的`Constructor`，它可以在部署时用来初始化合约。

## Constructor

Huff中的`CONSTRUCTOR`宏和Solidity的构造函数类似，它不是必须的，但是可以在部署时用来初始化合约状态变量。如果你不了解以太坊是如何通过交易创建合约的，可以阅读[WTF EVM Opcodes第21讲](https://github.com/WTFAcademy/WTF-EVM-Opcodes/tree/main/21_Create)。

在下面的例子中，我们使用`CONSTRUCTOR`宏在合约部署时将存储槽`VALUE_LOCATION`的值初始化为`0x69`。

```c
/* 接口 */
#define function getValue() view returns (uint256)

/* 存储槽位 */
#define constant VALUE_LOCATION = FREE_STORAGE_POINTER()

/* 方法 */
// Constructor
#define macro CONSTRUCTOR() = takes (0) returns (0) {
    0x69
    [VALUE_LOCATION]
    sstore              // []
}

#define macro GET_VALUE() = takes (0) returns (0) {
    // 从存储中加载值
    [VALUE_LOCATION]   // [ptr]
    sload                // [value]

    // 将值存入内存
    0x00 mstore

    // 返回值
    0x20 0x00 return
}

// 合约的主入口，判断调用的是哪个函数
#define macro MAIN() = takes (0) returns (0) {
    // 通过selector判断要调用哪个函数
    0x00 calldataload 0xE0 shr
    dup1 __FUNC_SIG(getValue) eq get jumpi
    // 如果没有匹配的函数，就revert
    0x00 0x00 revert

    get:
        GET_VALUE()
}
```



## 分析合约字节码

我们可以使用`huffc`命令获取上面合约的creation code:

```shell
huffc src/10_Constructor.huff -b
```



打印出的bytecode为：

```text
60695f55601c80600d3d393df35f3560e01c80632096525514610013575f5ffd5b5f545f5260205ff3
```



将这段字节码复制到[evm.codes playground](https://www.evm.codes/playground?fork=shanghai)，并点击运行。可以看到存储槽`0`被初始化为`69`，并且返回了合约的runtime code: `5f3560e01c80632096525514610013575f5ffd5b5f545f5260205ff3`，说明合约初始化成功！



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051312456.png)



## 总结

这一讲，我们介绍了如何在Huff中使用`Constructor`宏，它与Solidity中的构造函数类似，可以在部署时用来初始化合约。