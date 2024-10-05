# Reference

[01. Hello Opcodes | WTF Academy](https://www.wtf.academy/docs/evm-opcodes-101/HelloOpcodes/)

[EVM Codes - An Ethereum Virtual Machine Opcodes Interactive Reference](https://www.evm.codes/)

[EVM Codes - Playground](https://www.evm.codes/playground)

# 1. Hello Opcodes

这一讲，我们将介绍Opcodes和EVM基础，为之后的课程做准备。

## Opcodes 简介

Opcodes（操作码）是以太坊智能合约的基本单元。大家写的Solidity智能合约会被编译为字节码（bytecode），然后才能在EVM（以太坊虚拟机）上运行。而字节码就是由一系列Opcodes组成的。当用户在EVM中调用这个智能合约的函数时，EVM会解析并执行这些Opcodes，以实现合约逻辑。

例如，我们看一下几个常见的Opcodes：

- `PUSH1`: 将一个字节的数据压入堆栈。例如，`PUSH1 0x60` 就是将 0x60 压入堆栈。
- `DUP1`: 复制堆栈顶部的一个元素。
- `SWAP1`: 交换堆栈顶部的前两个元素。

下面是一个简单的Solidity智能合约，它只有一个`add()`函数，计算`1+1`的结果并返回。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Add {
    function add() public pure returns (uint256 result) {
        result = 1+1;
    }
}
```



将合约编译后，我们可以得到合约对应的bytecode:

```text
60806040523480156100...
```



通过bytecode，我们可以得到合约对应的opcodes为:

```text
PUSH1 0x80 PUSH1 0x40 MSTORE CALLVALUE DUP1 ...
```



如果你想理解这些opcodes在做什么，那么这个教程就适合你，那我们现在开始吧。

## EVM 基础

由于Opcodes直接操作EVM的资源，比如堆栈、内存、存储，因此了解EVM基础很重要。

类似Java的JVM，以太坊智能合约的运行时环境就是EVM。EVM的基本架构主要包括堆栈，内存，存储，EVM字节码，和燃料费，下面我们逐个讲解：



![img](https://www.wtf.academy/assets/images/1-1-61fe45f03c38da6b8e70f57aa3bcdc1b.png)



### 1. 堆栈 Stack

EVM是基于堆栈的，这意味着它处理数据的方式是使用堆栈数据结构进行大多数计算。堆栈是一种“后进先出”（LIFO）的数据结构，高效而简洁。你可以把它想像成一叠盘子，当你需要添加一个盘子时，你只能把它放在堆栈的最上面，我们把这个动作叫压入`PUSH`；而当你需要取一个盘子时，你只能取最上面的那一个，我们称之为弹出`POP`。许多操作码涉及将数据压入堆栈或从堆栈弹出数据。

在堆栈中，每个元素长度为256位（32字节），最大深度为1024元素，但是==每个操作只能操作堆栈顶的16个元素==。这也是为什么有时Solidity会报`Stack too deep`错误。



![img](https://www.wtf.academy/assets/images/1-2-3b6aabf2d8ef960b9e402b47d90b98aa.png)



### 2. 内存 Memory

堆栈虽然计算高效，但是存储能力有限，因此EVM使用内存来支持交易执行期间的数据存储和读取。EVM的内存是一个线性寻址存储器，你可以把它理解为一个动态字节数组，可以根据需要动态扩展。它支持以8或256 bit写入（`MSTORE8`/`MSTORE`），但只支持以256 bit读取（`MLOAD`）。

需要注意的是，**EVM的内存是“易失性”的：交易开始时，所有内存位置的值均为0；交易执行期间，值被更新；交易结束时，内存中的所有数据都会被清除，不会被持久化**。如果需要永久保存数据，就需要使用EVM的存储



![img](https://www.wtf.academy/assets/images/1-3-5230a60e83ef5972f265f01c60dfbba6.png)



### 3. 存储 Storage

EVM的账户存储（Account Storage）是一种映射（mapping，键值对存储），每个键和值都是256 bit的数据，它支持256 bit的读和写。这种存储在每个合约账户上都存在，并且是持久的，它的数据会保持在区块链上，直到被明确地修改。

对存储的读取（`SLOAD`）和写入（`SSTORE`）都需要gas，并且比内存操作更昂贵。这样设计可以防止滥用存储资源，因为所有的存储数据都需要在每个以太坊节点上保存。



![img](https://www.wtf.academy/assets/images/1-4-8ebb455c825d792d5e3a9543ad26917c.png)



### 4. EVM 字节码

我们之前提到，Solidity智能合约会被编译为EVM字节码，然后才能在EVM上运行。这个字节码是由一系列的Opcodes组成的，通常表现为一串十六进制的数字。EVM字节码在执行的时候，会按照顺序一个一个地读取并执行每个Opcode。

例如，字节码`6001600101`可以被解码为：

```text
PUSH1 0x01
PUSH1 0x01
ADD
```



这段Opcodes的含义是将两个1相加，得到结果2。

### 5. Gas

Gas是以太坊中执行交易和运行合约的"燃料"。每个交易或合约调用都需要消耗一定数量的Gas，这个数量取决于它们进行的计算的复杂性和数据存储的大小。

EVM上每笔交易的gas是如何计算的呢？其实是通过opcodes。**以太坊规定了每个opcode的gas消耗，复杂度越高的opcodes消耗越多的gas**，比如：

- `ADD`操作消耗3 gas
- `SSTORE`操作消耗20000 gas
- `SLOAD`操作消耗200 Gas

一笔交易的gas消耗等于其中所有opcodes的gas成本总和。当你调用一个合约函数时，你需要预估这个函数执行所需要的Gas，并在交易中提供足够的Gas。如果提供的Gas不够，那么函数执行会在中途停止，已经消耗的Gas不会退回。



![img](https://www.wtf.academy/assets/images/1-5-48c1f7bd4298da96242256e1fa69e61a.png)



### 6. 执行模型

最后，咱们串联一下以上的内容，介绍EVM的执行模型。它可以概括为以下步骤：

1. 当一个交易被接收并准备执行时，以太坊会初始化一个新的执行环境并加载合约的字节码。
2. 字节码被翻译成Opcode，被逐一执行。每个Opcodes代表一种操作，比如算术运算、逻辑运算、存储操作或者跳转到其他操作码。
3. 每执行一个Opcodes，都要消耗一定数量的Gas。如果Gas耗尽或者执行出错，执行就会立即停止，所有的状态改变（除了已经消耗的Gas）都会被回滚。
4. 执行完成后，交易的结果会被记录在区块链上，包括Gas的消耗、交易日志等信息。



![img](https://www.wtf.academy/assets/images/1-6-b13d296bab49cf4cce6790c1a4f85e0f.png)



## 总结

这一讲，我们介绍了EVM和Opcodes的基础知识，在之后的教程中，我们将继续学习Opcodes！

# 2. Opcodes分类

这一讲，我们将介绍Opcodes的分类，对Opcodes进行分类，并使用这些操作码来创建一个简单的程序，执行`1+1`的计算。

## Opcodes分类

Opcodes可以根据功能分为以下几类:

- **堆栈（Stack）指令**: 这些指令直接操作EVM堆栈。这包括将元素压入堆栈（如`PUSH1`）和从堆栈中弹出元素（如`POP`）。
- **算术（Arithmetic）指令**: 这些指令用于在EVM中执行基本的数学运算，如加法（`ADD`）、减法（`SUB`）、乘法（`MUL`）和除法（`DIV`）。
- **比较（Comparison）指令**: 这些指令用于比较堆栈顶部的两个元素。例如，大于（`GT`）和小于（`LT`）。
- **位运算（Bitwise）指令**: 这些指令用于在位级别上操作数据。例如，按位与（`AND`）和按位或（`OR`）。
- **内存（Memory）指令**: 这些指令用于操作EVM的内存。例如，将内存中的数据读取到堆栈（`MLOAD`）和将堆栈中的数据存储到内存（`MSTORE`）。
- **存储（Storage）指令**: 这些指令用于操作EVM的账户存储。例如，将存储中的数据读取到堆栈（`SLOAD`）和将堆栈中的数据保存到存储（`SSTORE`）。这类指令的gas消耗比内存指令要大。
- **控制流（Control Flow）指令**: 这些指令用于EVM的控制流操作，比如跳转`JUMP`和跳转目标`JUMPDEST`。
- **上下文（Context）指令**: 这些指令用于获取交易和区块的上下文信息。例如，获取msg.sender（`CALLER`）和当前可用的gas（`GAS`）。

## evm.codes

我们在WTF-Opcodes教程的入门部分会使用[evm.codes](https://www.evm.codes/?fork=shanghai)来运行Opcodes程序。

### 1. Opcode列表

evm.codes提供了完整的Opcodes列表，这对于学习Opcodes非常有用。它包括每个Opcode的编号（例如，`ADD`的编号是`0x01`）、名称、gas消耗、堆栈输入和输出以及一个简短的描述。



![img](https://www.wtf.academy/assets/images/2-1-45e455f054087f7d5b72286586fe3342.png)



### 2. Playground

evm.codes还提供了一个在线的Opcodes[playground](https://www.evm.codes/playground)，你可以在这里运行Opcodes代码。Playground分为三部分：左上角的编辑器，右上角的执行界面，以及右下角的状态界面，它们分别显示你的代码、代码的执行过程和执行结果。



![img](https://www.wtf.academy/assets/images/2-2-2bc4ff51fef27e1949c292cbfe926ea7.png)



## 示例： 1+1

我们现在来用Opcodes编写一个简单的程序，这个程序将在堆栈中计算1+1，并将结果保存到内存中。代码如下：

```go
PUSH1 0x01
PUSH1 0x01
ADD
PUSH0
MSTORE
```



我们来逐行分析这个程序，同时展示每行指令执行后堆栈和内存的状态：

1. 第1-2行：`PUSH1`指令将一个长度为1字节的数据压入堆栈顶部。

   ```go
   PUSH1 0x01
   // stack: [1]
   PUSH1 0x01
   // stack: [1, 1]
   ```

   

2. 第3行：`ADD`指令会弹出堆栈顶部的两个元素，计算它们的和，然后将结果压入堆栈。

   ```go
   ADD
   // stack: [2]
   ```

   

3. 第4行: `PUSH0`指令将0压入堆栈。

   ```go
   PUSH0
   // stack: [0, 2]
   ```

   

4. 第5行: `MSTORE` 属于内存指令，它会弹出堆栈顶的两个数据 `[offset, value]`（偏移量和值），然后将`value`（长度为32字节）保存到内存索引（偏移量）为`offset`的位置。

   ```go
   MSTORE
   // stack: []
   // memory: [0: 2]
   ```

   

你可以在evm.codes中验证执行过程和结果。



![img](https://www.wtf.academy/assets/images/2-3-5bb33d6623f238004bcfba0a103d8357.png)



## 总结

这一讲，我们介绍了Opcodes的功能分类，并使用opcodes写了第一个程序，计算`1+1`。接下来，我们会按分类介绍所有的opcodes。

# 3. 堆栈指令

这一讲，我们介绍EVM中的程序计数器（Program Counter）和堆栈指令，同时用Python实现一个简化版的EVM，可以执行`PUSH`和`POP`指令。

## 程序计数器

在EVM中，程序计数器（通常缩写为 PC）是一个用于跟踪当前执行指令位置的寄存器。每执行一条指令（opcode），程序计数器的值会自动增加，以指向下一个待执行的指令。但是，这个过程并不总是线性的，在执行跳转指令（`JUMP`和`JUMPI`）时，程序计数器会被设置为新的值。

下面我们使用Python创建一个简单的EVM程序计数器：

```python
class EVM:
    # 初始化
    def __init__(self, code):
        self.code = code # 初始化字节码，bytes对象
        self.pc = 0  # 初始化程序计数器为0
        self.stack = [] # 堆栈初始为空

    # 获取当前指令
    def next_instruction(self):
        op = self.code[self.pc]  # 获取当前指令
        self.pc += 1  # 递增
        return op

    def run(self):
        while self.pc < len(self.code):
            op = self.next_instruction() # 获取当前指令
```



上面的示例代码很简单，它的功能就是利用程序计数器遍历字节码中的opcode，在接下来的部分，我们将为它添加更多的功能。

```python
code = b"\x01\x02\x03"
evm = EVM(code)
evm.run()
```



## 堆栈指令

EVM是基于堆栈的，堆栈遵循 LIFO（后入先出）原则，最后一个被放入堆栈的元素将是第一个被取出的元素。PUSH和POP指令就是用来操作堆栈的。

### PUSH

在EVM中，PUSH是一系列操作符，共有32个（在以太坊上海升级前），从`PUSH1`，`PUSH2`，一直到`PUSH32`，操作码范围为`0x60`到`0x7F`。它们将一个字节大小为1到32字节的值从字节码压入堆栈（堆栈中每个元素的长度为32字节），每种指令的gas消耗都是3。

以`PUSH1`为例，它的操作码为`0x60`，它会将字节码中的下一个字节压入堆栈。例如，字节码`0x6001`就表示把`0x01`压入堆栈。`PUSH2`就是将字节码中的下两个字节压入堆栈，例如，`0x610101`就是把`0x0101`压入堆栈。其他的PUSH指令类似。

以太坊上海升级新加入了`PUSH0`，操作码为`0x5F`（即`0x60`的前一位），用于将`0`压入堆栈，gas消耗为2，比其他的PUSH指令更省gas。

下面我们用python实现`PUSH0`到`PUSH32`，主要逻辑见`push()`和`run()`函数:

```python
PUSH0 = 0x5F
PUSH1 = 0x60
PUSH32 = 0x7F

class EVM:
    def __init__(self, code):
        self.code = code # 初始化字节码，bytes对象
        self.pc = 0  # 初始化程序计数器为0
        self.stack = [] # 堆栈初始为空

    def next_instruction(self):
        op = self.code[self.pc]  # 获取当前指令
        self.pc += 1  # 递增
        return op

    def push(self, size):
        data = self.code[self.pc:self.pc + size] # 按照size从code中获取数据
        value = int.from_bytes(data, 'big') # 将bytes转换为int
        self.stack.append(value) # 压入堆栈
        self.pc += size # pc增加size单位

    def run(self):
        while self.pc < len(self.code):
            op = self.next_instruction()

            if PUSH1 <= op <= PUSH32:
                size = op - PUSH1 + 1
                self.push(size)
            elif op == PUSH0:
                self.stack.append(0)
```

> [!NOTE]
>
> 这个 `EVM` 类的代码实现了对 `PUSH0` 到 `PUSH32` 操作码的处理。`PUSH` 指令是 EVM（以太坊虚拟机）中用来将数据压入堆栈的操作。不同的 `PUSH` 指令会将不同长度的字节数据推入堆栈，比如 `PUSH1` 推入1个字节，`PUSH32` 推入32个字节，而 `PUSH0` 直接推入0。
>
> 我们逐步分析一下：
>
> ### 1. `next_instruction()` 函数
> - **作用**: 从字节码中获取当前操作码并移动程序计数器 `pc`，以便指向下一条指令。
> - **关键逻辑**: 
>    - `self.code[self.pc]` 获取当前操作码。
>    - `self.pc += 1` 表示程序计数器前进，准备处理下一条指令。
>
> ### 2. `push()` 函数
> - **作用**: 根据操作码的类型，读取从字节码中指定长度的数据，并将其转换为整数后压入堆栈。
> - **关键逻辑**:
>    - `self.code[self.pc:self.pc + size]` 获取从当前 `pc` 开始的 `size` 个字节。
>    - `int.from_bytes(data, 'big')` 将字节数组转换为大端序的整数。
>    - `self.stack.append(value)` 将数据压入堆栈。
>    - `self.pc += size` 更新 `pc`，跳过读取的数据部分。
>
> ### 3. `run()` 函数
> - **作用**: 运行 EVM，逐条解析指令。
> - **关键逻辑**:
>    - `if PUSH1 <= op <= PUSH32:`：如果操作码在 `PUSH1` 到 `PUSH32` 之间，则根据 `op` 计算出要推入的数据长度（`size = op - PUSH1 + 1`），然后调用 `push(size)` 处理。
>    - `elif op == PUSH0:`：对于 `PUSH0`，直接推入值 `0`。
>
> ### 示例用法
> 假设我们有以下字节码：
> ```python
> code = bytes([0x60, 0x01, 0x61, 0x00, 0xFF, 0x5F])  # PUSH1 0x01, PUSH2 0x00FF, PUSH0
> ```
> 解释：
> 1. `0x60 0x01` -> `PUSH1 0x01`，推入 `1`。
> 2. `0x61 0x00 0xFF` -> `PUSH2 0x00FF`，推入 `255`。
> 3. `0x5F` -> `PUSH0`，推入 `0`。
>
> 运行代码：
> ```python
> evm = EVM(code)
> evm.run()
> print(evm.stack)  # 输出堆栈的内容
> ```
> 最终堆栈内容应为 `[1, 255, 0]`，因为我们依次推入了 `1`, `255`, 和 `0`。
>

字节码`0x60016001`（PUSH1 1 PUSH1 1）会将两个1压入堆栈，下面我们执行一下：

```python
code = b"\x60\x01\x60\x01"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: [1, 1]
```

> [!NOTE]
>
> 运行结果确实如预期，字节码 `0x60016001` 对应两个 `PUSH1 1`，将两个 `1` 压入堆栈，最终堆栈的内容为 `[1, 1]`。

你也可以在evm.codes上验证（注意要把字节码开头的`0x`去掉）：



![img](https://www.wtf.academy/assets/images/3-1-354716e5d43607b3f2f929dbe5ed0a61.png)



### POP

在EVM中，`POP`指令（操作码`0x50`，gas消耗`2`）用于移除栈顶元素；如果当前堆栈为空，就抛出一个异常。

下面我们将`POP`指令加入到之前的代码中，主要逻辑见`pop()`和`run()`函数:

```python
PUSH0 = 0x5F
PUSH1 = 0x60
PUSH32 = 0x7F
POP = 0x50

class EVM:
    def __init__(self, code):
        self.code = code # 初始化字节码，bytes对象
        self.pc = 0  # 初始化程序计数器为0
        self.stack = [] # 堆栈初始为空

    def next_instruction(self):
        op = self.code[self.pc]  # 获取当前指令
        self.pc += 1  # 递增
        return op

    def push(self, size):
        data = self.code[self.pc:self.pc + size] # 按照size从code中获取数据
        value = int.from_bytes(data, 'big') # 将bytes转换为int
        self.stack.append(value) # 压入堆栈
        self.pc += size # pc增加size单位

    def pop(self):
        if len(self.stack) == 0:
            raise Exception('Stack underflow')
        return self.stack.pop() # 弹出堆栈

    def run(self):
        while self.pc < len(self.code):
            op = self.next_instruction()

            if PUSH1 <= op <= PUSH32: # 如果为PUSH1-PUSH32
                size = op - PUSH1 + 1
                self.push(size)
            elif op == PUSH0: # 如果为PUSH0
                self.stack.append(0)
                self.pc += size
            elif op == POP: # 如果为POP
                self.pop()
```

> [!NOTE]
>
> 在你的代码中，`POP` 指令已经被正确添加。下面是对 `POP` 指令的处理和逻辑细节：
>
> ### 1. `pop()` 函数
> - **作用**: 移除并返回堆栈的栈顶元素。如果堆栈为空时尝试 `POP`，则抛出一个 `Stack underflow` 异常。
> - **关键逻辑**:
>   - `if len(self.stack) == 0:` 检查堆栈是否为空。
>   - `self.stack.pop()` 从栈顶移除一个元素并返回该元素。
>
> ### 2. `run()` 函数中 `POP` 的处理
> - **作用**: 如果遇到 `POP` 操作码（`0x50`），则调用 `pop()` 函数，移除栈顶元素。
> - **逻辑**: 
>   - `elif op == POP:` 分支检测当前指令是否为 `POP`，并调用 `self.pop()` 移除栈顶元素。
>

字节码`0x6001600150`（PUSH1 1 PUSH1 1 POP）会将两个1压入堆栈，然后再弹出一个1。下面我们执行一下：

```python
code = b"\x60\x01\x60\x01\x50"
evm = EVM(code)
evm.run()
evm.stack
# output: [1]
```



你也可以在evm.codes上验证（注意要把字节码开头的`0x`去掉）：



![img](https://www.wtf.academy/assets/images/3-2-f335497e5080b8e84a3c73f5a3ee92cb.png)



## 总结

这一讲，我们主要介绍了EVM中的程序计数器和堆栈指令，特别是`PUSH`和`POP`指令。并且参考[evm-from-scratch](https://github.com/w1nt3r-eth/evm-from-scratch)，我们使用Python实现了一个简化版的EVM，能够处理`PUSH`和`POP`指令。在后续的教程中，我们将继续探索更多的opcodes，从而进一步完善我们的EVM实现。

# 4. 算数指令

这一讲，我们将介绍EVM中用于基础算术运算的11个指令，包括`ADD`（加法），`MUL`（乘法），`SUB`（减法），和`DIV`（除法）。并且，我们将在用Python写的极简版EVM中添加对他们的支持。

## ADD (加法)

`ADD`指令从堆栈中弹出两个元素，将它们相加，然后将结果推入堆栈。如果堆栈元素不足两个，那么会抛出异常。这个指令的操作码是`0x01`，gas消耗为`3`。

我们可以将`ADD`指令的实现添加到我们的EVM模拟器中：

```python
def add(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    a = self.stack.pop()
    b = self.stack.pop()
    res = (a + b) % (2**256) # 加法结果需要模2^256，防止溢出
    self.stack.append(res)
```



我们在`run()`函数中添加对`ADD`指令的处理：

```python
def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()

        if PUSH1 <= op <= PUSH32:
            size = op - PUSH1 + 1
            self.push(size)
        elif op == PUSH0:
            self.stack.append(0)
            self.pc += size
        elif op == POP:
            self.pop()
        elif op == ADD: # 处理ADD指令
            self.add()
```

> [!NOTE]
>
> ### 1. 堆栈检查
>
> - **作用**: EVM 的加法操作需要至少两个元素在堆栈中。
>
> - 逻辑
>
>   :
>
>   - `if len(self.stack) < 2:` 检查堆栈是否有足够的元素，如果少于两个元素则抛出 `Stack underflow` 异常。
>
> ### 2. 执行加法
>
> - 操作
>
>   :
>
>   - `a = self.stack.pop()` 和 `b = self.stack.pop()`：从堆栈中弹出两个操作数 `a` 和 `b`。
>   - `res = (a + b) % (2**256)`：将 `a` 和 `b` 相加，结果对 `2^256` 取模，这是 EVM 的标准行为，用于防止数值溢出。
>
> ### 3. 压回结果
>
> - **作用**: 将加法后的结果压回堆栈。
> - **逻辑**: `self.stack.append(res)` 将计算结果压入堆栈。

现在，我们可以尝试运行一个包含`ADD`指令的字节码：`0x6002600301`（PUSH1 2 PUSH1 3 ADD）。这个字节码将`2`和`3`推入堆栈，然后将它们相加。

```python
code = b"\x60\x02\x60\x03\x01"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: [5]
```



## MUL (乘法)

`MUL`指令和`ADD`类似，但是它将堆栈的顶部两个元素相乘。操作码是`0x02`，gas消耗为`5`。

我们将`MUL`指令的实现添加到EVM模拟器：

```python
def mul(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    a = self.stack.pop()
    b = self.stack.pop()
    res = (a * b) % (2**256) # 乘法结果需要模2^256，防止溢出
    self.stack.append(res)
```



我们在`run()`函数中添加对`MUL`指令的处理：

```python
def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()

        if PUSH1 <= op <= PUSH32:
            size = op - PUSH1 + 1
            self.push(size)
        elif op == PUSH0:
            self.stack.append(0)
            self.pc += size
        elif op == POP:
            self.pop()
        elif op == ADD:
            self.add()
        elif op == MUL: # 处理MUL指令
            self.mul()
```



现在，我们可以尝试运行一个包含`MUL`指令的字节码：`0x6002600302`（PUSH1 2 PUSH1 3 MUL）。这个字节码将`2`和`3`推入堆栈，然后将它们相乘。

```python
code = b"\x60\x02\x60\x03\x02"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: [6]
```



## SUB (减法)

`SUB`指令从堆栈顶部弹出两个元素，然后计算第二个元素减去第一个元素，最后将结果推入堆栈。这个指令的操作码是`0x03`，gas消耗为`3`。

我们将`SUB`指令的实现添加到EVM模拟器：

```python
def sub(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    a = self.stack.pop()
    b = self.stack.pop()
    res = (b - a) % (2**256) # 结果需要模2^256，防止溢出
    self.stack.append(res)
```



我们在`run()`函数中添加对`SUB`指令的处理：

```python
def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()

        if PUSH1 <= op <= PUSH32:
            size = op - PUSH1 + 1
            self.push(size)
        elif op == PUSH0:
            self.stack.append(0)
            self.pc += size
        elif op == POP:
            self.pop()
        elif op == ADD:
            self.add()
        elif op == MUL:
            self.mul()
        elif op == SUB: # 处理SUB指令
            self.sub()
```



现在，我们可以尝试运行一个包含`SUB`指令的字节码：`0x6002600303`（PUSH1 2 PUSH1 3 SUB）。这个字节码将`2`和`3`推入堆栈，然后将它们相减。

```python
code = b"\x60\x03\x60\x02\x03"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: [1]
```



## DIV (除法)

`DIV`指令从堆栈顶部弹出两个元素，然后将第二个元素除以第一个元素，最后将结果推入堆栈。如果第一个元素（除数）为0，则将0推入堆栈。这个指令的操作码是`0x04`，gas消耗为`5`。

我们将`DIV`指令的实现添加到EVM模拟器：

```python
def div(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    a = self.stack.pop()
    b = self.stack.pop()
    if a == 0:
        res = 0
    else:
        res =  (b // a) % (2**256)
    self.stack.append(res)
```



我们在`run()`函数中添加对`DIV`指令的处理：

```python
def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()

        if PUSH1 <= op <= PUSH32:
            size = op - PUSH1 + 1
            self.push(size)
        elif op == PUSH0:
            self.stack.append(0)
            self.pc += size
        elif op == POP:
            self.pop()
        elif op == ADD:
            self.add()
        elif op == MUL:
            self.mul()
        elif op == SUB:
            self.sub()
        elif op == DIV: # 处理DIV指令
            self.div()
```



现在，我们可以尝试运行一个包含`DIV`指令的字节码：`0x6002600304`（PUSH1 2 PUSH1 3 DIV）。这个字节码将`2`和`3`推入堆栈，然后将它们相除。

```python
code = b"\x60\x06\x60\x03\x04"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: [2]
```



## 其他算数指令

1. **SDIV**: 带符号整数的除法指令。与`DIV`类似，这个指令会从堆栈中弹出两个元素，然后将第二个元素除以第一个元素，结果带有符号。如果第一个元素（除数）为0，结果为0。它的操作码是`0x05`，gas消耗为5。要注意，EVM字节码中的负数是用二进制补码（two’s complement）形式，比如`-1`表示为`0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff`，它加一等于0。

   ```python
   def sdiv(self):
       if len(self.stack) < 2:
           raise Exception('Stack underflow')
       a = self.stack.pop()
       b = self.stack.pop()
       res = b//a % (2**256) if a!=0 else 0
       self.stack.append(res)
   ```

   > [!NOTE]
   >
   > 在 EVM 中，**带符号整数的除法**（`SDIV`）使用二进制补码表示负数。二进制补码是一种处理带符号整数的编码方式，它的核心特点是：
   >
   > - 正数和负数在二进制中的表示是对称的。
   > - 正数与无符号整数的表示相同。
   > - 负数的补码表示是通过对该数字的绝对值取反再加一得到的。
   >
   > ### 二进制补码求法
   >
   > 对于一个给定的位宽（如 256 位）：
   >
   > 1. **正数**的补码表示与无符号整数相同。例如，`1` 的 256 位表示是 `0x000000...01`。
   >
   > 2. 负数
   >
   >    的补码表示：
   >
   >    - 取该负数的绝对值的二进制表示。
   >    - 逐位取反（即将 `0` 变成 `1`，将 `1` 变成 `0`）。
   >    - 取反后加 `1`，得到负数的补码。
   >
   > ### 例子
   >
   > #### 表示 `-1`：
   >
   > - 绝对值 `1` 的二进制表示是 `0x0000...01`（256 位）。
   > - 逐位取反：`0xFFFF...FFFE`。
   > - 加 `1`：`0xFFFF...FFFF`（即 `-1` 的补码表示）。
   >
   > #### 表示 `-2`：
   >
   > - 绝对值 `2` 的二进制表示是 `0x0000...02`。
   > - 逐位取反：`0xFFFF...FFFD`。
   > - 加 `1`：`0xFFFF...FFFE`（即 `-2` 的补码表示）。

   

2. **MOD**: 取模指令。这个指令会从堆栈中弹出两个元素，然后将第二个元素除以第一个元素的余数推入堆栈。如果第一个元素（除数）为0，结果为0。它的操作码是`0x06`，gas消耗为5。

   ```python
   def mod(self):
       if len(self.stack) < 2:
           raise Exception('Stack underflow')
       a = self.stack.pop()
       b = self.stack.pop()
       res = b % a if a != 0 else 0
       self.stack.append(res)
   ```

   

3. **SMOD**: 带符号的取模指令。这个指令会从堆栈中弹出两个元素，然后将第二个元素除以第一个元素的余数推入堆栈，结果带有第二个元素的符号。如果第一个元素（除数）为0，结果为0。它的操作码是`0x07`，gas消耗为5。

   ```python
   def smod(self):
       if len(self.stack) < 2:
           raise Exception('Stack underflow')
       a = self.stack.pop()
       b = self.stack.pop()
       res = b % a if a != 0 else 0
       self.stack.append(res)
   ```

   

4. **ADDMOD**: 模加法指令。这个指令会从堆栈中弹出三个元素，将前两个元素相加，然后对第三个元素取模，将结果推入堆栈。如果第三个元素（模数）为0，结果为0。它的操作码是`0x08`，gas消耗为8。

   ```python
   def addmod(self):
       if len(self.stack) < 3:
           raise Exception('Stack underflow')
       a = self.stack.pop()
       b = self.stack.pop()
       n = self.stack.pop()
       res = (a + b) % n if n != 0 else 0
       self.stack.append(res)
   ```

   

5. **MULMOD**: 模乘法指令。这个指令会从堆栈中弹出三个元素，将前两个元素相乘，然后对第三个元素取模，将结果推入堆栈。如果第三个元素（模数）为0，结果为0。它的操作码是`0x09`，gas消耗为5。

   ```python
   def mulmod(self):
       if len(self.stack) < 3:
           raise Exception('Stack underflow')
       a = self.stack.pop()
       b = self.stack.pop()
       n = self.stack.pop()
       res = (a * b) % n if n != 0 else 0
       self.stack.append(res)
   ```

   

6. **EXP**: 指数运算指令。这个指令会从堆栈中弹出两个元素，将第二个元素作为底数，第一个元素作为指数，进行指数运算，然后将结果推入堆栈。它的操作码是`0x0A`，gas消耗为10。

   ```python
   def exp(self):
       if len(self.stack) < 2:
           raise Exception('Stack underflow')
       a = self.stack.pop()
       b = self.stack.pop()
       res = pow(b, a) % (2**256)
       self.stack.append(res)
   ```

   

7. **SIGNEXTEND**: 符号位扩展指令，即在保留数字的符号（正负性）及数值的情况下，增加二进制数字位数的操作。举个例子，若计算机使用8位二进制数表示数字“0000 1010”，且此数字需要将字长符号扩充至16位，则扩充后的值为“0000 0000 0000 1010”。此时，数值与符号均保留了下来。`SIGNEXTEND`指令会从堆栈中弹出两个元素，对第二个元素进行符号扩展，扩展的位数由第一个元素决定，然后将结果推入堆栈。它的操作码是`0x0B`，gas消耗为5。

   ```python
   def signextend(self):
       if len(self.stack) < 2:
           raise Exception('Stack underflow')
       b = self.stack.pop()
       x = self.stack.pop()
       if b < 32: # 如果b>=32，则不需要扩展
           sign_bit = 1 << (8 * b - 1) # b 字节的最高位（符号位）对应的掩码值，将用来检测 x 的符号位是否为1
           x = x & ((1 << (8 * b)) - 1)  # 对 x 进行掩码操作，保留 x 的前 b+1 字节的值，其余字节全部置0
           if x & sign_bit:  # 检查 x 的符号位是否为1
               x = x | ~((1 << (8 * b)) - 1)  # 将 x 的剩余部分全部置1
       self.stack.append(x)
   ```

   > [!NOTE]
   >
   > `1 << (8 * b - 1)` 是一个**位移操作**。具体地说，`<<` 是**左移操作符**，它将二进制数字向左移动指定的位数。下面是具体解释：
   >
   > ### 1. `<<` 左移操作符
   > `<<` 表示将一个数的二进制表示向左移动指定的位数，相当于将这个数乘以 2 的相应次方。例如：
   > - `1 << 1`：将 `1` 向左移动 1 位，相当于 `1 * 2^1 = 2`，即 `0b10`。
   > - `1 << 2`：将 `1` 向左移动 2 位，相当于 `1 * 2^2 = 4`，即 `0b100`。
   >
   > ### 2. `1 << (8 * b - 1)` 的含义
   > 假设 `b` 是一个正整数，表达式 `1 << (8 * b - 1)` 的含义是：
   > - 计算 `8 * b - 1`，这表示需要左移的位数。
   > - `1` 表示二进制的 `0b1`，即最右边只有一个 `1` 的二进制数。
   > - 左移 `8 * b - 1` 位，意味着将 `1` 向左移动这些位数，结果是一个二进制数，这个数的第 `8 * b` 位是 `1`，其右边的所有位都是 `0`。
   >
   > ### 具体例子
   > 1. **当 `b = 1` 时**：
   >    - `1 << (8 * 1 - 1)` 相当于 `1 << 7`，结果为 `0b10000000`，即十进制的 `128`。这表示 1 字节（8 位）长度的最高位为 `1`，这是符号位。
   >
   > 2. **当 `b = 2` 时**：
   >    - `1 << (8 * 2 - 1)` 相当于 `1 << 15`，结果为 `0b1000000000000000`，即十进制的 `32768`。这表示 2 字节（16 位）长度的最高位为 `1`。
   >
   > ### 在符号扩展中的作用
   > `1 << (8 * b - 1)` 是用来计算第 `b` 字节的**符号位**掩码。例如：
   > - 如果 `b = 1`，则符号位是 `8` 位数的第 7 位（`0b10000000`）。
   > - 如果 `b = 2`，则符号位是 `16` 位数的第 15 位（`0b1000000000000000`）。
   >
   > 这个掩码可以帮助判断符号位是否为 `1`，从而决定是否进行符号扩展。
   >
   > ### 总结
   > - `<<` 是左移操作符，它将二进制数向左移动指定的位数。
   > - `1 << (8 * b - 1)` 计算的是第 `b` 字节的符号位对应的掩码，用来检测符号位是否为 `1`，从而决定是否进行符号扩展。
   
   > [!NOTE]
   >
   > 表达式 `x = x & ((1 << (8 * b)) - 1)` 是一个**位运算**，用于对变量 `x` 进行掩码操作。下面是对这条语句的逐步解释：
   >
   > ### 1. 计算 `(1 << (8 * b))`
   > - `1 << (8 * b)`：这个表达式首先计算 `8 * b`，然后将 `1` 向左移动这个结果位数。对于一个给定的 `b`，这表示创建一个二进制数，其左侧有 `8 * b` 位数为 `0`，而最右边的第一个位为 `1`。
   > - 例如：
   >   - 如果 `b = 1`，则 `8 * b = 8`，所以 `1 << 8` 结果为 `0b100000000`（即 `256`）。
   >   - 如果 `b = 2`，则 `8 * b = 16`，所以 `1 << 16` 结果为 `0b100000000000000000`（即 `65536`）。
   >
   > ### 2. 计算 `((1 << (8 * b)) - 1)`
   > - `((1 << (8 * b)) - 1)`：这一步从前一步的结果中减去 `1`。这个操作会将所有的位设置为 `1`，也就是产生一个全为 `1` 的二进制数，长度为 `8 * b` 位。例如：
   >   - 当 `b = 1` 时，`1 << 8` 为 `256`，`256 - 1` 结果为 `255`，即 `0b11111111`（8位全为1）。
   >   - 当 `b = 2` 时，`1 << 16` 为 `65536`，`65536 - 1` 结果为 `65535`，即 `0b1111111111111111`（16位全为1）。
   >
   > ### 3. `x & ((1 << (8 * b)) - 1)`
   > - `x & ...`：这个操作使用**按位与**运算符 `&`，将 `x` 和前一步计算的掩码进行按位与运算。
   > - 按位与运算会将 `x` 中的高于 `8 * b` 位的部分置为 `0`，而保留低于 `8 * b` 位的部分。例如：
   >   - 如果 `x` 是一个整数，且假设其二进制表示为 `0b1010101010101010`，而 `b = 1`，则掩码为 `0b11111111`（8个1），执行 `x & 0b11111111` 后，只保留 `x` 的最低 8 位，其余位被置为 `0`。
   >
   > ### 4. 整体效果
   > 因此，这条语句的作用是：
   > - **掩码** `x` 以保留它的前 `8 * b` 位的数值，并将其余高位清零。这样做可以确保在进行符号扩展时，只处理 `x` 的前 `b` 字节的值，防止扩展时影响到不必要的位。
   >
   > ### 总结
   > `x = x & ((1 << (8 * b)) - 1)` 通过生成一个掩码来提取 `x` 的前 `b` 字节的值，从而在符号扩展时只保留相关的位数。
   
   

## 总结

这一讲，我们介绍了EVM中的11个算数指令，并在极简版EVM中添加了对他们的支持。课后习题: 写出`0x60036004600209`对应的指令形式，并给出运行后的堆栈状态。

# 5. 比较指令

这一讲，我们将介绍EVM中用于比较运算的6个指令，包括`LT`（小于），`GT`（大于），和`EQ`（相等）。并且，我们将在用Python写的极简版EVM中添加对他们的支持。

## LT (小于)

`LT`指令从堆栈中弹出两个元素，比较第二个元素是否小于第一个元素。如果是，那么将`1`推入堆栈，否则将`0`推入堆栈。如果堆栈元素不足两个，那么会抛出异常。这个指令的操作码是`0x10`，gas消耗为`3`。

我们可以将`LT`指令的实现添加到我们的极简EVM中：

```python
def lt(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    a = self.stack.pop()
    b = self.stack.pop()
    self.stack.append(int(b < a)) # 注意这里的比较顺序
```



我们在`run()`函数中添加对`LT`指令的处理：

```python
def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()

        # ... 其他指令的处理 ...

        elif op == LT: # 处理LT指令
            self.lt()
```



现在，我们可以尝试运行一个包含`LT`指令的字节码：`0x6002600310`（PUSH1 2 PUSH1 3 LT）。这个字节码将`2`和`3`推入堆栈，然后比较`2`是否小于`3`。

```python
code = b"\x60\x02\x60\x03\x10"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: [1]
```



## GT (大于)

`GT`指令和`LT`指令非常类似，不过它比较的是第二个元素是否大于第一个元素。操作码是`0x11`，gas消耗为`3`。

我们将`GT`指令的实现添加到极简EVM：

```python
def gt(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    a = self.stack.pop()
    b = self.stack.pop()
    self.stack.append(int(b > a)) # 注意这里的比较顺序
```



我们在`run()`函数中添加对`GT`指令的处理：

```python
def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()

        # ... 其他指令的处理 ...

        elif op == GT: # 处理GT指令
            self.gt()
```



现在，我们可以运行一个包含`GT`指令的字节码：`0x6002600311`（PUSH1 2 PUSH1 3 GT）。这个字节码将`2`和`3`推入堆栈，然后比较`2`是否大于`3`。

```python
code = b"\x60\x02\x60\x03\x11"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: [0]
```



## EQ (等于)

`EQ`指令从堆栈中弹出两个元素，如果两个元素相等，那么将`1`推入堆栈，否则将`0`推入堆栈。该指令的操作码是`0x14`，gas消耗为`3`。

我们将`EQ`指令的实现添加到极简EVM：

```python
def eq(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    a = self.stack.pop()
    b = self.stack.pop()
    self.stack.append(int(a == b))
```



我们在`run()`函数中添加对`EQ`指令的处理：

```python
elif op == EQ: 
    self.eq()
```



现在，我们可以运行一个包含`EQ`指令的字节码：`0x6002600314`（PUSH1 2 PUSH1 3 EQ）。这个字节码将`2`和`3`推入堆栈，然后比较两者是否相等。

```python
code = b"\x60\x02\x60\x03\x14"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: [0]
```



## ISZERO (是否为零)

`ISZERO`指令从堆栈中弹出一个元素，如果元素为0，那么将`1`推入堆栈，否则将`0`推入堆栈。该指令的操作码是`0x15`，gas消耗为`3`。

我们将`ISZERO`指令的实现添加到极简EVM：

```python
def iszero(self):
    if len(self.stack) < 1:
        raise Exception('Stack underflow')
    a = self.stack.pop()
    self.stack.append(int(a == 0))
```



我们在`run()`函数中添加对`ISZERO`指令的处理：

```python
elif op == ISZERO: 
    self.iszero()
```



现在，我们可以运行一个包含`ISZERO`指令的字节码：`0x600015`（PUSH1 0 ISZERO）。这个字节码将`0`推入堆栈，然后检查其是否为0。

```python
code = b"\x60\x00\x15"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: [1]
```



## 其他比较指令

1. **SLT (有符号小于)**: 这个指令会从堆栈中弹出两个元素，然后比较第二个元素是否小于第一个元素，结果以有符号整数形式返回。如果第二个元素小于第一个元素，将`1`推入堆栈，否则将`0`推入堆栈。它的操作码是`0x12`，gas消耗为`3`。

   ```python
   def slt(self):
       if len(self.stack) < 2:
           raise Exception('Stack underflow')
       a = self.stack.pop()
       b = self.stack.pop()
       self.stack.append(int(b < a)) # 极简evm stack中的值已经是以有符号整数存储了，所以和lt一样实现
   ```

   

2. **SGT (有符号大于)**: 这个指令会从堆栈中弹出两个元素，然后比较第二个元素是否大于第一个元素，结果以有符号整数形式返回。如果第二个元素大于第一个元素，将`1`推入堆栈，否则将`0`推入堆栈。它的操作码是`0x13`，gas消耗为`3`。

   ```python
   def sgt(self):
       if len(self.stack) < 2:
           raise Exception('Stack underflow')
       a = self.stack.pop()
       b = self.stack.pop()
       self.stack.append(int(b > a)) # 极简evm stack中的值已经是以有符号整数存储了，所以和gt一样实现
   ```

   

## 总结

这一讲，我们介绍了EVM中的6个比较指令，并在极简版EVM中添加了对他们的支持。课后习题: 写出`0x6003600414`对应的指令形式，并给出运行后的堆栈状态。

# 6. 位级指令

这一讲，我们将介绍EVM中用于位级运算的8个指令，包括`AND`（与），`OR`（或），和`XOR`（异或）。并且，我们将在用Python写的极简版EVM中添加对他们的支持。

## AND (与)

`AND`指令从堆栈中弹出两个元素，对它们进行位与运算，并将结果推入堆栈。操作码是`0x16`，gas消耗为`3`。

我们将`AND`指令的实现添加到我们的EVM模拟器中：

```python
def and_op(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    a = self.stack.pop()
    b = self.stack.pop()
    self.stack.append(a & b)
```



我们在`run()`函数中添加对`AND`指令的处理：

```python
def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()

        # ... 其他指令的处理 ...
        
        elif op == AND:  # 处理AND指令
            self.and_op()
```



现在，我们可以尝试运行一个包含`AND`指令的字节码：`0x6002600316`（PUSH1 2 PUSH1 3 AND）。这个字节码将`2`（0000 0010）和`3`（0000 0011）推入堆栈，然后进行位级与运算，结果应该为`2`（0000 0010）。

```python
code = b"\x60\x02\x60\x03\x16"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: [2]
```



## OR (或)

`OR`指令与`AND`指令类似，但执行的是位或运算。操作码是`0x17`，gas消耗为`3`。

我们将`OR`指令的实现添加到EVM模拟器：

```python
def or_op(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    a = self.stack.pop()
    b = self.stack.pop()
    self.stack.append(a | b)
```



我们在`run()`函数中添加对`OR`指令的处理：

```python
def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()

        # ... 其他指令的处理 ...

        elif op == OR:  # 处理OR指令
            self.or_op()
```



现在，我们可以尝试运行一个包含`OR`指令的字节码：`0x6002600317`（PUSH1 2 PUSH1 3 OR）。这个字节码将`2`（0000 0010）和`3`（0000 0011）推入堆栈，然后进行位级与运算，结果应该为`3`（0000 0011）。

```python
code = b"\x60\x02\x60\x03\x17"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: [3]
```



## XOR (异或)

`XOR`指令与`AND`和`OR`指令类似，但执行的是异或运算。操作码是`0x18`，gas消耗为`3`。

我们将`XOR`指令的实现添加到EVM模拟器：

```python
def xor_op(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    a = self.stack.pop()
    b = self.stack.pop()
    self.stack.append(a ^ b)
```



我们在`run()`函数中添加对`XOR`指令的处理：

```python
def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()

        # ... 其他指令的处理 ...

        elif op == XOR:  # 处理XOR指令
            self.xor_op()
```



现在，我们可以尝试运行一个包含`XOR`指令的字节码：`0x6002600318`（PUSH1 2 PUSH1 3 XOR）。这个字节码将`2`（0000 0010）和`3`（0000 0011）推入堆栈，然后进行位级与运算，结果应该为`1`（0000 0001）。

```python
code = b"\x60\x02\x60\x03\x18"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: [1]
```



## NOT

`NOT` 指令执行按位非操作，取栈顶元素的补码，然后将结果推回栈顶。它的操作码是`0x19`，gas消耗为`3`。

我们将`NOT`指令的实现添加到EVM模拟器：

```python
def not_op(self):
    if len(self.stack) < 1:
        raise Exception('Stack underflow')
    a = self.stack.pop()
    self.stack.append(~a % (2**256)) # 按位非操作的结果需要模2^256，防止溢出
```



在`run()`函数中添加对`NOT`指令的处理：

```python
elif op == NOT: # 处理NOT指令
    self.not_op()
```



现在，我们可以尝试运行一个包含`NOT`指令的字节码：`0x600219`（PUSH1 2 NOT）。这个字节码将`2`（0000 0010）推入堆栈，然后进行位级非运算，结果应该为`很大的数`（0xfffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffd）。

```python
# NOT
code = b"\x60\x02\x19"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: [很大的数] (fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffd)
```



## SHL

`SHL`指令执行左移位操作，从堆栈中弹出两个元素，将第二个元素左移第一个元素位数，然后将结果推回栈顶。它的操作码是`0x1B`，gas消耗为`3`。

我们将`SHL`指令的实现添加到EVM模拟器：

```python
def shl(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    a = self.stack.pop()
    b = self.stack.pop()
    self.stack.append((b << a) % (2**256)) # 左移位操作的结果需要模2^256
```



在`run()`函数中添加对`SHL`指令的处理：

```python
elif op == SHL: # 处理SHL指令
    self.shl()
```



现在，我们可以尝试运行一个包含`XOR`指令的字节码：`0x600260031B`（PUSH1 2 PUSH1 3 SHL）。这个字节码将`2`（0000 0010）和`3`（0000 0011）推入堆栈，然后将`2`左移`3`位，结果应该为`16`（0001 0000）。

```python
code = b"\x60\x02\x60\x03\x1B"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: [16] (0x000000010 << 3 => 0x00010000)
```



## SHR

`SHR`指令执行右移位操作，从堆栈中弹出两个元素，将第二个元素右移第一个元素位数，然后将结果推回栈顶。它的操作码是`0x1C`，gas消耗为`3`。

我们将`SHR`指令的实现添加到EVM模拟器：

```python
def shr(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    a = self.stack.pop()
    b = self.stack.pop()
    self.stack.append(b >> a) # 右移位操作
```



在`run()`函数中添加对`SHR`指令的处理：

```python
elif op == SHR: # 处理SHR指令
    self.shr()
```



现在，我们可以尝试运行一个包含`XOR`指令的字节码：`0x601060031C`（PUSH1 16 PUSH1 3 SHL）。这个字节码将`16`（0001 0000）和`3`（0000 0011）推入堆栈，然后将`16`右移`3`位，结果应该为`2`（0000 0010）。

```python
code = b"\x60\x10\x60\x03\x1C"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: [2] (0x00010000 >> 3 => 0x000000010)
```



## 其他位级指令

1. **BYTE**: `BYTE`指令从堆栈中弹出两个元素（`a`和`b`），将第二个元素（`b`）看作一个字节数组，并返回该字节数组中第一个元素指定索引的字节（`b[a]`），并压入堆栈。如果索引大于或等于字节数组的长度，则返回`0`。操作码是`0x1a`，gas消耗为`3`。

   ```python
   def byte_op(self):
       if len(self.stack) < 2:
           raise Exception('Stack underflow')
       position = self.stack.pop()
       value = self.stack.pop()
       if position >= 32:
           res = 0
       else:
           res = (value // pow(256, 31 - position)) & 0xFF 
       self.stack.append(res)
   ```

   > [!NOTE]
   >
   > 这段代码是 EVM 中的 `BYTE` 操作的实现，用于获取栈顶数字中某个字节的位置，然后将该位置的字节压入堆栈。我们逐步解析这段代码的逻辑：
   >
   > ### 1. **检查堆栈**
   > ```python
   > if len(self.stack) < 2:
   >     raise Exception('Stack underflow')
   > ```
   > 这段代码确保堆栈中至少有两个元素。如果堆栈元素不足，则抛出 `Stack underflow` 异常。
   >
   > ### 2. **获取位置和值**
   > ```python
   > position = self.stack.pop()
   > value = self.stack.pop()
   > ```
   > 从堆栈中弹出两个值：
   > - `position` 是需要检查的字节位置，表示我们想要获取的字节在数字中的位置。
   > - `value` 是需要操作的数字，我们要从中提取出指定位置的字节。
   >
   > ### 3. **检查位置是否越界**
   > ```python
   > if position >= 32:
   >     res = 0
   > ```
   > 如果 `position` 大于或等于 32，则返回 `0`。这是因为在 EVM 中，一个数字最多有 32 个字节（256 位），所以如果位置超过 31（从 0 开始计数），这个位置没有字节可取，结果就是 `0`。
   >
   > ### 4. **提取指定字节**
   > ```python
   > else:
   >     res = (value // pow(256, 31 - position)) & 0xFF
   > ```
   > 如果位置在有效范围内（即小于 32），这段代码用于从 `value` 中提取出对应的字节：
   > - `pow(256, 31 - position)`：表示要右移 `31 - position` 字节，以便将我们需要的字节移到最低有效字节位置。每个字节是 256 位，所以每右移一字节，相当于将数字除以 `256`。
   >   - 举个例子，如果 `position = 0`，即想要取出最左边的字节，我们就需要将 `value` 右移 31 个字节（乘以 256^31），以使最左边的字节移到最低有效位。
   >   - 如果 `position = 31`，则无需右移，因为这个字节已经在最低有效位。
   >   
   > - `value // pow(256, 31 - position)`：此操作将 `value` 右移指定字节数，使目标字节移到最低位。
   >
   > - `& 0xFF`：这是一个掩码操作，取出 `value` 的最低有效字节，即对应的8位。
   >
   > ### 5. **结果入栈**
   > ```python
   > self.stack.append(res)
   > ```
   > 最后，将结果 `res`（目标字节）压入堆栈。
   >
   > ### 总结
   > - **作用**：这段代码实现了 EVM 中的 `BYTE` 操作，提取 `value` 中指定 `position` 的字节，并将其压入堆栈。
   > - **逻辑**：
   >   - 如果位置超出 32 字节，则结果为 `0`。
   >   - 否则，通过将 `value` 右移，将目标字节移到最低有效位，然后用 `& 0xFF` 掩码操作提取该字节。

   > [!NOTE]
   >
   > ### 解释 `pow(256, 31)`
   >
   > `256` 在这里不是指 **256 位**，而是指 **256** 这个数。它代表的是字节的进制基数（即 `2^8`），也就是说每个字节的可能值范围是 `0-255`，一共 256 个不同的值。【每个字节2^8=256位，共有32个字节】
   >
   > 在表达式 `pow(256, 31)` 中：
   >
   > - `256` 表示字节的进制基数，也就是每个字节有 `256` 个可能的值。
   > - `31` 表示将要右移的 **字节数**，而不是位数。
   >
   > 所以 `pow(256, 31)` 相当于计算 `256` 的 `31` 次方，也就是 `256^31`，这意味着将 `value` 右移 `31` 个字节。
   >
   > ### 提取特定字节
   >
   > 假设我们有一个 256 位（32 字节）的大整数 `value`，例如：value = 0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef
   >
   > 我们要提取某个字节，比如索引为 `position = 31` 的字节，这个字节是最低字节（即 `0xef`）。
   >
   > 使用 `pow(256, 31)`，我们将 `value` 右移 31 个字节，使最低字节移动到最低有效位，然后用 `& 0xFF` 提取它。
   >
   > #### 操作解释：
   >
   > - `pow(256, 31)` 相当于右移 31 个字节，也就是右移 31 * 8 = 248 位。
   > - 通过 `value // pow(256, 31)`，我们可以把 `value` 的最低字节移到最低位。
   > - 最后，通过 `& 0xFF`，我们掩码掉其他字节，只保留最低字节的 8 位（即 1 个字节）。
   >
   > #### 更多例子：
   >
   > 假设 `value = 0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef`，我们要提取第 0 个字节（最高字节）。
   >
   > 1. 计算右移位数：`31 - position = 31 - 0 = 31`，需要右移 31 个字节（也就是 248 位）。
   > 2. 右移后，最高字节 `0x12` 会移动到最低位。
   > 3. 用 `& 0xFF` 掩码操作提取出最低位，最终结果是 `0x12`。

   

1. **SAR**: `SAR`指令执行算术右移位操作，与`SHR`类似，但考虑符号位：如果我们对一个负数进行算术右移，那么在右移的过程中，最左侧（符号位）会被填充`F`以保持数字的负值。它从堆栈中弹出两个元素，将第二个元素以符号位填充的方式右移第一个元素位数，然后将结果推回栈顶。它的操作码是`0x1D`。由于Python的`>>`操作符已经是算术右移，我们可以直接复用`shr`函数的代码。

   ```python
   def sar(self):
       if len(self.stack) < 2:
           raise Exception('Stack underflow')
       a = self.stack.pop()
       b = self.stack.pop()
       self.stack.append(b >> a) # 右移位操作
   ```

   

## 总结

这一讲，我们介绍了EVM中的8个位级指令，并在极简版EVM中添加了对他们的支持。课后习题: 写出`0x6002600160011B1B`对应的指令形式，并给出运行后的堆栈状态。

# 7. 内存指令

在这一讲，我们将介绍EVM中用于内存（Memory）操作的4个指令，包括`MSTORE`，`MSTORE8`，`MLOAD`，和`MSIZE`。我们将在用Python写的极简版EVM中添加对这些操作的支持。

## EVM中的内存

我们在[第一讲](https://github.com/WTFAcademy/WTF-Opcodes/blob/main/01_HelloOpcodes/readme.md)介绍了EVM的内存，它是一个线性寻址存储器，类似一个动态的字节数组，可以根据需求动态扩展。它的另一个特点就是易失性，交易结束时所有数据都会被清零。它支持以8或256 bit写入（`MSTORE8`/`MSTORE`），但只支持以256 bit取（`MLOAD`）。



![img](https://www.wtf.academy/assets/images/7-1-5230a60e83ef5972f265f01c60dfbba6.png)



我们可以用Python内置的`bytearray`来代表内存：

```python
def __init__(self, code):
    self.code = code
    self.pc = 0
    self.stack = []
    self.memory = bytearray()  # 内存初始化为空
```



内存的读写比存储（Storage）的读写要便宜的多，每次读写有固定费用3 gas，另外如果首次访问了新的内存位置（内存拓展），则需要付额外的费用（由当前偏移量和历史最大偏移量决定），计算方法见[链接](https://www.evm.codes/about#accesssets)。

## MSTORE （内存写）

`MSTORE`指令用于将一个256位（32字节）的值存储到内存中。它从堆栈中弹出两个元素，第一个元素为内存的地址（偏移量 offset），第二个元素为存储的值（value）。操作码是`0x52`，gas消耗根据实际内存使用情况计算（3+X）。

```python
def mstore(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    offset = self.stack.pop()
    value = self.stack.pop()
    while len(self.memory) < offset + 32:
        self.memory.append(0) # 内存扩展
    self.memory[offset:offset+32] = value.to_bytes(32, 'big')
```

> [!NOTE]
>
> 这段代码实现了 EVM 中的 `MSTORE` 操作，它将一个 32 字节的值存储在内存的特定位置。让我们逐步解释代码的逻辑：
>
> ### 代码解释：
>
> 1. **检查堆栈的长度是否足够**：
>     ```python
>     if len(self.stack) < 2:
>         raise Exception('Stack underflow')
>     ```
>     - 在执行 `MSTORE` 操作之前，确保堆栈中至少有两个元素。`MSTORE` 操作需要两个值：
>       - 一个用于指定 **内存的偏移量**（`offset`）。
>       - 另一个是要存储的 **32 字节的值**（`value`）。
>
> 2. **从堆栈中弹出 `offset` 和 `value`**：
>     ```python
>     offset = self.stack.pop()
>     value = self.stack.pop()
>     ```
>     - 从堆栈中弹出两个值：首先是偏移量 `offset`，然后是要存储的值 `value`。
>
> 3. **内存扩展**：
>     ```python
>     while len(self.memory) < offset + 32:
>         self.memory.append(0)
>     ```
>     - `MSTORE` 操作将 32 字节的值存储在内存的某个偏移量位置。此时需要确保内存空间足够存储 32 字节。
>     - 如果当前内存长度小于 `offset + 32`（即目标位置超出了当前内存大小），代码通过 `self.memory.append(0)` 扩展内存，并将新分配的内存初始化为 0。
>
> 4. **存储 32 字节的值**：
>     ```python
>     self.memory[offset:offset+32] = value.to_bytes(32, 'big')
>     ```
>     - `value.to_bytes(32, 'big')`：将 `value` 转换为 32 字节的大端序字节表示。大端序意味着字节从最重要位（高位）到最不重要位（低位）进行存储。
>     - 然后将这 32 字节的数据存储到 `self.memory[offset:offset+32]` 范围内，也就是从 `offset` 开始的 32 字节区域。
>
> ### 核心概念：
> - **内存扩展**：EVM 的内存是动态分配的，因此当目标偏移超出当前内存时，需要扩展内存。每次扩展时，新分配的字节会被初始化为 0。
> - **32 字节存储**：EVM 中的 `MSTORE` 操作总是将值作为 32 字节的块来存储，即使该值小于 32 字节，它也会在前面填充 0 来达到 32 字节。
>
> ### 示例：
> 假设堆栈中的值为 `offset = 64` 和 `value = 123456`，则内存会从位置 64 开始，存储 `value` 的 32 字节表示。
>
> 如果内存不足 64 + 32 字节，代码会通过循环 `self.memory.append(0)` 来扩展内存并将新空间初始化为 0。

我们在`run()`函数中添加对`MSTORE`指令的处理：

```python
def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()

        # ... 其他指令的处理 ...

        elif op == MSTORE: # 处理MSTORE指令
            self.mstore()
```



现在，我们可以尝试运行一个包含`MSTORE`指令的字节码：`0x6002602052`（PUSH1 2 PUSH1 0x20 MSTORE）。这个字节码将`2`和`0x20`（32）推入堆栈，然后进行`MSTORE`，将`2`存到偏移量为`0x20`的地方。

```python
# MSTORE
code = b"\x60\x02\x60\x20\x52"
evm = EVM(code)
evm.run()
print(evm.memory[0x20:0x40])  
# 输出: [0, 0, 0, ..., 0, 2]
```



## MSTORE8 （内存8位写）

`MSTORE8`指令用于将一个8位（1字节）的值存储到内存中。与`MSTORE`类似，但只使用最低8位。操作码是`0x53`，gas消耗根据实际内存使用情况计算（3+X）。

```python
def mstore8(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    offset = self.stack.pop()
    value = self.stack.pop()
    while len(self.memory) < offset + 32:
        self.memory.append(0) # 内存扩展
    self.memory[offset] = value & 0xFF # 取最低有效字节
```



我们在`run()`函数中添加对`MSTORE8`指令的处理：

```python
elif op == MSTORE8: # 处理MSTORE8指令
    self.mstore8()
```



现在，我们可以尝试运行一个包含`MSTORE8`指令的字节码：`0x6002602053`（PUSH1 2 PUSH1 0x20 MSTORE8）。这个字节码将`2`和`0x20`（32）推入堆栈，然后进行`MSTORE8`，将`2`存到偏移量为`0x20`的地方。

```python
# MSTORE8
code = b"\x60\x02\x60\x20\x53"
evm = EVM(code)
evm.run()
print(evm.memory[0x20:0x40])  
# 输出: [2, 0, 0, ..., 0, 0]
```



## MLOAD （内存读）

`MLOAD`指令从内存中加载一个256位的值并推入堆栈。它从堆栈中弹出一个元素，从该元素表示的内存地址中加载32字节，并将其推入堆栈。操作码是`0x51`，gas消耗根据实际内存使用情况计算（3+X）。

```python
def mload(self):
    if len(self.stack) < 1:
        raise Exception('Stack underflow')
    offset = self.stack.pop()
    while len(self.memory) < offset + 32:
        self.memory.append(0) # 内存扩展
    value = int.from_bytes(self.memory[offset:offset+32], 'big')
    self.stack.append(value)
```

> [!NOTE]
>
> 这里的 `self.memory[offset:offset+32]` 提取了从 `offset` 开始的 32 个字节。接着，`int.from_bytes()` 将这 32 个字节按照 **大端序** 解释为一个整数，并将结果存储在 `value` 中。

我们在`run()`函数中添加对`MLOAD`指令的处理：

```python
elif op == MLOAD: 
    self.mload()
```



现在，我们可以尝试运行一个包含`MLOAD`指令的字节码：`0x6002602052602051`（PUSH1 2 PUSH1 0x20 MSTORE PUSH1 0x20 MLOAD）。这个字节码将`2`和`0x20`（32）推入堆栈，然后进行`MSTORE`，将`2`存到偏移量为`0x20`的地方；然后将`0x20`推入堆栈，然后进行`MLOAD`，将刚才存储在内存的值读取出来。

```python
# MSTORE
code = b"\x60\x02\x60\x20\x52\x60\x20\x51"
evm = EVM(code)
evm.run()
print(evm.memory[0x20:0x40])  
# 输出: [0, 0, 0, ..., 0, 2]
print(evm.stack)  
# output: [2]
```



## MSIZE （内存大小）

`MSIZE`指令将当前的内存大小（以字节为单位）压入堆栈。操作码是`0x59`，gas消耗为2。

```python
def msize(self):
    self.stack.append(len(self.memory))
```



## 总结

这一讲，我们介绍了EVM中的内存操作指令，并在极简版EVM中添加了对它们的支持。这些操作允许我们在EVM的内存中存储和读取值，为更复杂的合约逻辑提供基础。

课后习题: 写出`0x6002602053602051`对应的指令形式，并给出运行后的堆栈和内存状态。

# 8. 存储指令

在这一讲，我们将介绍EVM中用于存储（Storage）操作的2个指令：`SSTORE`和`SLOAD`。并且，我们将在用Python写的极简版EVM中添加对这些操作的支持。

## EVM中的存储

我们在[第一讲](https://github.com/WTFAcademy/WTF-Opcodes/blob/main/01_HelloOpcodes/readme.md)介绍了EVM的存储，和内存不同，它是一种持久化存储空间，存在存储中的数据在交易之间可以保持。它是EVM的状态存储的一部分，支持以256 bit为单位的读写。



![img](https://www.wtf.academy/assets/images/8-1-8ebb455c825d792d5e3a9543ad26917c.png)



由于存储使用键值对存储数据，每个键和值都是256 bit，因此我们可以用Python内置的`dict`（字典）来代表存储：

```python
def __init__(self, code):
    self.code = code
    self.pc = 0
    self.stack = []
    self.memory = bytearray()  # 内存初始化为空
    self.storage = {}  # 存储初始化为空字典
```



对存储的读取（`SLOAD`）和写入（`SSTORE`）都需要gas，并且比内存操作更昂贵。这样设计可以防止滥用存储资源，因为所有的存储数据都需要在每个以太坊节点上保存。

## SSTORE (存储写)

`SSTORE`指令用于将一个256位（32字节）的值写入到存储。它从堆栈中弹出两个元素，第一个元素为存储的地址（key），第二个元素为存储的值（value）。操作码是`0x55`，gas消耗根据实际改变的数据计算（下面给出）。

```python
def sstore(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    key = self.stack.pop()
    value = self.stack.pop()
    self.storage[key] = value
```



我们在`run()`函数中添加对`SSTORE`指令的处理：

```python
def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()

        # ... 其他指令的处理 ...

        elif op == SSTORE: # 处理SSTORE指令
            self.sstore()
```



现在，我们可以尝试运行一个包含`SSTORE`指令的字节码：`0x6002600055`（PUSH1 2 PUSH1 0 SSTORE）。这个字节码将`2`和`0`推入堆栈，然后进行`SSTORE`，将`2`存到键为`0x0`的存储槽。

```python
# SSTORE
code = b"\x60\x02\x60\x00\x55"
evm = EVM(code)
evm.run()
print(evm.storage)  
# Output: {0: 2}
```



## SLOAD (存储读)

`SLOAD`指令从存储中读取一个256位（32字节）的值并推入堆栈。它从堆栈中弹出一个元素，从该元素表示的存储槽中加载值，并将其推入堆栈。操作码是`0x54`，gas消耗后面给出。

```python
def sload(self):
    if len(self.stack) < 1:
        raise Exception('Stack underflow')
    key = self.stack.pop()
    value = self.storage.get(key, 0) # 如果键不存在，返回0
    self.stack.append(value)
```



我们在`run()`函数中添加对`SLOAD`指令的处理：

```python
elif op == SLOAD: 
    self.sload()
```



现在，我们可以尝试运行一个包含`SLOAD`指令的字节码：`0x6002600055600054`（PUSH1 2 PUSH1 0 SSTORE PUSH1 0 SLOAD）。这个字节码将`2`和`0`推入堆栈，然后进行`SSTORE`，将`2`存到键为`0`的地方；然后将`0`推入堆栈，然后进行`SLOAD`，将刚才写入`0x0`存储槽的值读取出来。

```python
# SLOAD
code = b"\x60\x02\x60\x00\x55\x60\x00\x54"
evm = EVM(code)
evm.run()
print(evm.storage)  
# 输出: {0: 2}
print(evm.stack)  
# 输出: [2]
```



## 访问集 EIP-2929

访问集（Access Sets）是[EIP-2929](https://eips.ethereum.org/EIPS/eip-2929)提出的一种新概念，它的引入有助于优化Gas计费和以太坊的网络性能。访问集是在每个外部交易中定义的，并且在交易过程中会跟踪和记录每个交易访问过的合约地址和存储槽（slot）。

- 合约地址：在执行交易过程中，任何被访问到的地址都会被添加到访问集中。
- 存储槽：这个列表包含了一个交易在执行过程中访问过的所有存储槽。

如果一个地址或存储槽在访问集中，我们称它为"warm"，否则称之为"cold"。一个地址或存储槽在一次交易中首次被访问时，它会从"cold"变为"warm"。在交易执行期间，如果一个指令需要访问一个"cold"的地址或存储槽，那么这个指令的Gas消耗会更高。而对 "warm" 的地址或存储槽的访问，则会有较低的 Gas 消耗，因为相关数据已经被缓存了。

### Gas Cost

对于`SLOAD`（存储读），如果读取的存储槽为"cold"（即这是交易中首次访问），那么`SLOAD`的gas消耗为2100 gas；如果为 "warm"（即在交易中已经访问过），那么`SLOAD`的gas消耗为100 gas。

对于`SSTORE`（存储写），gas计算公式更为复杂，分为gas消耗和gas返还两部分。

1. `SSTORE`的gas消耗：简单来说，如果存储槽为`cold`，则需要多花2100 gas；如果存储槽初始值为0，那么将它改为非0值的gas消耗最大，为22100 gas。

   具体计算公式如下：

   ```python
   static_gas = 0
   
   if value == current_value
       base_dynamic_gas = 100
   else if current_value == original_value
       if original_value == 0
           base_dynamic_gas = 20000
       else
           base_dynamic_gas = 2900
   else
       base_dynamic_gas = 100
   
   if key is not warm
       base_dynamic_gas += 2100
   ```

   

   其中`value`为要存储的新值，`current_value`为存储槽当前值，`original_value`为交易开始时存储槽的原始值，`base_dynamic_gas`为gas消耗。

   > [!NOTE]
   >
   > #### 1. **`value == current_value`**:
   >
   > - 如果新的存储值 `value` 和当前存储槽的值 `current_value` 相同，`SSTORE` 操作只需要 100 gas。这种情况下不需要任何修改，因为存储的值没有改变。
   >
   > #### 2. **`current_value == original_value`**:
   >
   > - 如果当前存储槽中的值 
   >
   >   ```
   >   current_value
   >   ```
   >
   >    和原始值 
   >
   >   ```
   >   original_value
   >   ```
   >
   >    相同，存储槽会根据 
   >
   >   ```
   >   original_value
   >   ```
   >
   >    是否为 0 来决定消耗多少 gas：
   >
   >   - **原始值为 0**：如果 `original_value` 为 0（也就是说，之前的存储槽是空的），将其改为非 0 值会消耗大量的 gas，具体为 **20000 gas**。
   >   - **原始值非 0**：如果 `original_value` 为非 0，消耗 gas 为 **2900 gas**。
   >
   > #### 3. **`else` 条件**（`current_value != original_value`）:
   >
   > - 如果当前值和原始值不相同（已经进行过存储槽的修改），再修改存储值时消耗 **100 gas**。
   >
   > #### 4. **Cold/Warm 存储访问**:
   >
   > - 如果存储槽是 **"cold"**（即该存储槽在当前交易中首次被访问），则会额外消耗 **2100 gas**。这与 EVM 中的存储访问优化有关。每个存储槽首次访问时的开销较高，但在后续的访问中成本更低。

   

2. `SSTORE`的gas返还：当要存储的新值不等于存储槽的当前值时，可能触发gas返还。简单来说，将存储槽的非0值改为0，返还的gas最多高达 19900 gas。

   ```python
   if value != current_value
       if current_value == original_value
           if original_value != 0 and value == 0
               gas_refunds += 4800
       else
           if original_value != 0
               if current_value == 0
                   gas_refunds -= 4800
               else if value == 0
                   gas_refunds += 4800
           if value == original_value
               if original_value == 0
                       gas_refunds += 19900
               else
                   if key is warm
                       gas_refunds += 5000 - 2100 - 100
                   else
                       gas_refunds += 4900
   ```

   

   其中`value`为要存储的新值，`current_value`为存储槽当前值，`original_value`为交易开始时存储槽的原始值，`gas_refunds`为gas返还。
   
   > [!NOTE]
   >
   > 这个逻辑是用来计算 `SSTORE` 操作在 **EVM** 中涉及的 gas refund（gas 退款）机制的。退款机制旨在鼓励开发者通过操作将存储槽设置为 0，从而释放空间。我们来逐步解释这个逻辑：
   >
   > ### 逻辑解释：
   >
   > 1. **`if value != current_value`**:
   >    - 如果新的存储值 `value` 不等于当前的存储值 `current_value`，表示要执行写操作，并可能会触发退款逻辑。
   >
   > 2. **`if current_value == original_value`**:
   >    - 如果当前值 `current_value` 等于原始值 `original_value`，表示存储槽尚未发生过更改，此时根据接下来的条件检查是否要处理退款逻辑。
   >
   >    - **`if original_value != 0 and value == 0`**:
   >      - 如果原始值 `original_value` 不为 0 且新值 `value` 为 0，表示从非 0 值变为 0。此时会 **增加 4800 gas 的退款**，这是为了鼓励将存储槽重置为 0 的操作。
   >
   > 3. **`else`** (即 `current_value != original_value`):
   >    - 如果当前值与原始值不同，表示已经对存储槽做过修改。接下来的逻辑会进一步检查 `current_value` 和 `value` 是否触发退款：
   >
   >    - **`if original_value != 0`**:
   >      - 如果原始值不为 0，表示存储槽一开始是非 0 的。
   >
   >        - **`if current_value == 0`**:
   >          - 如果当前值为 0，表示之前已经执行了一次将存储槽设置为 0 的操作，这意味着需要 **减少 4800 gas 的退款**，因为已经触发了之前的退款逻辑。
   >
   >        - **`else if value == 0`**:
   >          - 如果新的存储值为 0，表示要将当前值重置为 0。此时会 **增加 4800 gas 的退款**，因为清空存储槽节省了存储空间。
   >
   > 4. **`if value == original_value`**:
   >    - 如果新值 `value` 恢复为原始值 `original_value`，则根据不同情况可能会触发进一步的退款：
   >
   >    - **`if original_value == 0`**:
   >      - 如果原始值为 0（即初始是空的存储槽），并且新的值也是 0，表示回到了最初的状态。这种情况下，可能需要 **增加 19900 gas 的退款**，因为从非 0 回到 0。
   >
   >    - **`else`** (即 `original_value != 0`):
   >      - 如果原始值不为 0，进入这个分支：
   >
   >        - **`if key is warm`**:
   >          - 如果存储槽是 warm（即在当前交易中已经被访问过），则会执行较低的 gas 退款，具体为 **5000 gas 减去 2100 和 100 gas**。
   >
   >        - **`else`** (即存储槽是 cold):
   >          - 如果存储槽是 cold，则会 **增加 4900 gas 的退款**。
   >
   > ### 总结：
   >
   > - 当存储值从 **非 0 变为 0** 时，通常会触发 **4800 gas** 的退款。
   > - 如果当前存储槽已经被清空（即从 0 变为非 0 再回到 0），退款会根据情况调整。
   > - 当存储槽的 **原始值和当前值相等** 并且新值为 0，可能会触发 **19900 gas** 的高额退款。
   > - Warm 和 cold 存储槽的退款不同，cold 访问的存储槽触发更高的退款。
   
   

## 总结

这一讲，我们介绍了EVM中的存储操作指令（`SSTORE`和`SLOAD`），并在极简版EVM中添加了对它们的支持。这些操作允许我们在EVM的存储中写入和读取值，为更复杂的合约逻辑提供基础。

课后习题: 写出`0x6002602055602054`对应的指令形式，并给出运行后的堆栈和存储的状态。

# 9. 控制流指令

在这一讲，我们将介绍EVM中用于控制流的5个指令，包括`STOP`，`JUMP`，`JUMPI`，`JUMPDEST`，和`PC`。我们将在用Python写的极简版EVM中添加对这些操作的支持。

## EVM中的控制流

我们在[第三讲](https://github.com/WTFAcademy/WTF-Opcodes/blob/main/03_StackOp/readme.md)介绍了程序计数器（Program Counter，PC），而EVM的控制流是由跳转指令（`JUMP`，`JUMPI`，`JUMPDEST`）控制PC指向新的指令位置而实现的，这允许合约进行条件执行和循环执行。

## STOP（停止）

`STOP`是EVM的停止指令，它的作用是停止当前上下文的执行，并成功退出。它的操作码是`0x00`，gas消耗为0。

将`STOP`操作作码设为`0x00`有一个好处：当一个调用被执行到一个没有代码的地址（EOA），并且EVM尝试读取代码数据时，系统会返回一个默认值0，这个默认值对应的就是`STOP`指令，程序就会停止执行。

下面，让我们在`run()`函数中添加对`STOP`指令的处理：

```python
def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()

        # ... 其他指令的处理 ...

        elif op == STOP: # 处理STOP指令
            print('Program has been stopped')
            break # 停止执行
```



现在，我们可以尝试运行一个包含`STOP`指令的字节码：

```python
# STOP
code = b"\x00"
evm = EVM(code)
evm.run()
# output: Program has been stopped
```



## JUMPDEST（跳转目标）

`JUMPDEST`指令标记一个有效的跳转目标位置，不然无法使用`JUMP`和`JUMPI`进行跳转。它的操作码是`0x5b`，gas消耗为1。

但是`0x5b`有时会作为`PUSH`的参数（详情可看[黄皮书](https://ethereum.github.io/yellowpaper/paper.pdf)中的9.4.3. Jump Destination Validity），所以需要在运行代码前，筛选字节码中有效的`JUMPDEST`指令，使用`ValidJumpDest` 来存储有效的`JUMPDEST`指令所在位置。

```python
def findValidJumpDestinations(self):
    pc = 0

    while pc < len(self.code):
        op = self.code[pc]
        if op == JUMPDEST:
            self.validJumpDest[pc] = True
        elif op >= PUSH1 and op <= PUSH32:
            pc += op - PUSH1 + 1
        pc += 1
```



```python
def jumpdest(self):
    pass
```



## JUMP（跳转）

`JUMP`指令用于无条件跳转到一个新的程序计数器位置。它从堆栈中弹出一个元素，将这个元素设定为新的程序计数器（`pc`）的值。操作码是`0x56`，gas消耗为8。

```python
def jump(self):
    if len(self.stack) < 1:
        raise Exception('Stack underflow')
    destination = self.stack.pop()
    if destination not in self.validJumpDest:
        raise Exception('Invalid jump destination')
    else:  self.pc = destination
```



我们在`run()`函数中添加对`JUMP`和`JUMPDEST`指令的处理：

```python
elif op == JUMP: 
    self.jump()
elif op == JUMPDEST: 
    self.jumpdest()
```



现在，我们可以尝试运行一个包含`JUMP`和`JUMPDEST`指令的字节码：`0x600456005B`（PUSH1 4 JUMP STOP JUMPDEST）。这段字节码将`4`推入堆栈，然后进行`JUMP`，跳转到`pc = 4`的位置，该位置正好是`JUMPDEST`指令，跳转成功，程序没有被`STOP`指令中断。

```python
# JUMP
code = b"\x60\x04\x56\x00\x5b"
evm = EVM(code)
evm.run()
print(evm.pc)  
# output: 5
```



## JUMPI（条件跳转）

`JUMPI`指令用于条件跳转，它从堆栈中弹出两个元素，如果第二个元素（条件，`condition`）不为0，那么将第一个元素（目标，`destination`）设定为新的`pc`的值。操作码是`0x57`，gas消耗为10。

```python
def jumpi(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    destination = self.stack.pop()
    condition = self.stack.pop()
    if condition != 0:
        if destination not in self.validJumpDest:
            raise Exception('Invalid jump destination')
        else:  self.pc = destination
```



我们在`run()`函数中添加对`JUMPI`指令的处理：

```python
elif op == JUMPI: 
    self.jumpi()
```



现在，我们可以尝试运行一个包含`JUMPI`和`JUMPDEST`指令的字节码：`0x6001600657005B`（PUSH1 01 PUSH1 6 JUMPI STOP JUMPDEST）。这个字节码将`1`和`6`推入堆栈，然后进行`JUMPI`，由于条件不为`0`，执行跳转到`pc = 6`的位置，该位置正好是`JUMPDEST`指令，跳转成功，程序没有被`STOP`指令中断。

```python
# JUMPI
code = b"\x60\x01\x60\x06\x57\x00\x5b"
evm = EVM(code)
evm.run()
print(evm.pc)  
# output: 7 程序没有被中断
```



## PC（程序计数器）

`PC`指令将当前的程序计数器（`pc`）的值压入堆栈。操作码为`0x58`，gas消耗为2。

```python
def pc(self):
    self.stack.append(self.pc)
```



## 总结

这一讲，我们介绍了EVM中的控制流程指令，并在极简版EVM中添加了对它们的支持。这些操作为合约提供了控制流程的能力，为编写更复杂的合约逻辑提供了可能。

课后习题: 写出`0x5F600557005B`对应的指令形式，并给出运行后的堆栈和程序计数器状态。

# 10. 区块信息指令

在这一讲，我们将介绍EVM中用于查询区块信息的9个指令，包括`BLOCKHASH`，`COINBASE`，`PREVRANDAO`等。我们将在用Python写的极简版EVM中添加对这些操作的支持。

## 区块信息

我们在写智能合约时经常会用到区块链信息，比如生成[伪随机数](https://github.com/AmazingAng/WTF-Solidity/blob/main/39_Random/Random.sol)时我们会使用`blockhash`，`block.number`，和`block.timestamp`:

```solidity
    /** 
    * 链上伪随机数生成
    * keccak256(abi.encodePacked())中填上一些链上的全局变量/自定义变量
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
```



EVM提供了一系列指令让智能合约访问当前或历史区块的信息，包括区块哈希、时间戳、coinbase等。

这些信息一般保存在区块头（`Header`）中，但我们可以为在极简EVM中添加`current_block`属性来模拟这些区块信息：

```python
def __init__(self, code):
    self.code = code
    self.pc = 0
    self.stack = []
    self.memory = bytearray()
    self.current_block = {
        "blockhash": 0x7527123fc877fe753b3122dc592671b4902ebf2b325dd2c7224a43c0cbeee3ca,
        "coinbase": 0x388C818CA8B9251b393131C08a736A67ccB19297,
        "timestamp": 1625900000,
        "number": 17871709,
        "prevrandao": 0xce124dee50136f3f93f19667fb4198c6b94eecbacfa300469e5280012757be94,
        "gaslimit": 30,
        "chainid": 1,
        "selfbalance": 100,
        "basefee": 30,
    }
```



## 区块信息指令

下面，我们介绍这些区块信息指令：

1. `BLOCKHASH`: 查询特定区块（最近的256个区块，不包括当前区块）的hash，它的操作码为`0x40`，gas消耗为20。它从堆栈中弹出一个值作为区块高度（block number），然后将该区块的hash压入堆栈，如果它不属于最近的256个区块，则返回0（你可以使用`NUMBER`指令查询当前区块高度）。但是为了简化，我们在这里只考虑当前块。

   ```python
   def blockhash(self):
       if len(self.stack) < 1:
           raise Exception('Stack underflow')
       number = self.stack.pop()
       # 在真实场景中, 你会需要访问历史的区块hash
       if number == self.current_block["number"]:
           self.stack.append(self.current_block["blockhash"])
       else:
           self.stack.append(0)  # 如果不是当前块，返回0
   ```

   

1. `COINBASE`: 将当前区块的coinbase（矿工/受益人）地址压入堆栈，它的操作码为`0x41`，gas消耗为2。

   ```python
   def coinbase(self):
       self.stack.append(self.current_block["coinbase"])
   ```

   

2. `TIMESTAMP`: 将当前区块的时间戳压入堆栈，它的操作码为`0x42`，gas消耗为2。

   ```python
   def timestamp(self):
       self.stack.append(self.current_block["timestamp"])
   ```

   

3. `NUMBER`: 将当前区块高度压入堆栈，它的操作码为`0x43`，gas消耗为2。

   ```python
   def number(self):
       self.stack.append(self.current_block["number"])
   ```

   

4. `PREVRANDAO`: 替代了原先的`DIFFICULTY`(0x44) 操作码，其返回值是beacon链随机性信标的输出。此变更允许智能合约在以太坊转向权益证明(PoS)后继续从原本的`DIFFICULTY`操作码处获得随机性。它的操作码为`0x44`，gas消耗为2。

   ```python
   def prevrandao(self):
       self.stack.append(self.current_block["prevrandao"])
   ```

   

5. `GASLIMIT`: 将当前区块的gas限制压入堆栈，它的操作码为`0x45`，gas消耗为2。

   ```python
   def gaslimit(self):
       self.stack.append(self.current_block["gaslimit"])
   ```

   

6. `CHAINID`: 将当前的[链ID](https://chainlist.org/)压入堆栈，它的操作码为`0x46`，gas消耗为2。

   ```python
   def chainid(self):
       self.stack.append(self.current_block["chainid"])
   ```

   

7. `SELFBALANCE`: 将合约的当前余额压入堆栈，它的操作码为`0x47`，gas消耗为5。

   ```python
   def selfbalance(self):
       self.stack.append(self.current_block["selfbalance"])
   ```

   

8. `BASEFEE`: 将当前区块的[基础费](https://ethereum.org/zh/developers/docs/gas/#base-fee)（base fee）压入堆栈，它的操作码`0x48`，gas消耗为2。

   ```python
   def basefee(self):
       self.stack.append(self.current_block["basefee"])
   ```

   

下面，我们在极简EVM中添加对这些操作码的支持：

```python
BLOCKHASH = 0x40
COINBASE = 0x41
TIMESTAMP = 0x42
NUMBER = 0x43
PREVRANDAO = 0x44
GASLIMIT = 0x45
CHAINID = 0x46
SELFBALANCE = 0x47
BASEFEE = 0x48

def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()

        # ... 其他指令的处理 ...

        elif op == BLOCKHASH:
            self.blockhash()
        elif op == COINBASE:
            self.coinbase()
        elif op == TIMESTAMP:
            self.timestamp()
        elif op == NUMBER:
            self.number()
        elif op == PREVRANDAO:
            self.prevrandao()
        elif op == GASLIMIT:
            self.gaslimit()
        elif op == CHAINID:
            self.chainid()
        elif op == SELFBALANCE:
            self.selfbalance()
        elif op == BASEFEE:
            self.basefee()        
```



## 总结

这一讲，我们介绍了EVM中与区块链信息相关的指令，这些指令允许智能合约访问与其所在区块链相关的信息。这些信息有很多用途，比如判断交易是否超时，或者检查合约的余额。

课后习题: 请尝试写出一段字节码，该字节码会先压入当前区块链的高度，然后获取它的区块哈希。



# 11. 堆栈指令2

之前，我们介绍了堆栈指令中的`PUSH`和`POP`，这一讲我们将介绍另外两个指令：`DUP`和`SWAP`。

## DUP

在EVM中，`DUP`是一系列的指令，总共有16个，从`DUP1`到`DUP16`，操作码范围为`0x80`到`0x8F`，gas消耗均为3。这些指令用于复制（Duplicate）堆栈上的指定元素（根据指令的序号）到堆栈顶部。例如，`DUP1`复制栈顶元素，`DUP2`复制距离栈顶的第二个元素，以此类推。

我们可以在极简EVM中增加对`DUP`指令的支持：

```python
DUP1 = 0x80
DUP16 = 0x8F

def dup(self, position):
    if len(self.stack) < position:
        raise Exception('Stack underflow')
    value = self.stack[-position]
    self.stack.append(value)

def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()

        # ... 其他指令的实现 ...

        elif DUP1 <= op <= DUP16: # 如果是DUP1-DUP16
            position = op - DUP1 + 1
            self.dup(position)
```



现在，我们可以尝试运行一个包含`DUP1`指令的字节码：`0x6001600280`（PUSH1 1 PUSH1 2 DUP1）。这个字节码将`1`和`2`推入堆栈，然后进行`DUP1`复制栈顶元素（2），堆栈最后会变为[1, 2, 2]。

```python
# DUP1
code = b"\x60\x01\x60\x02\x80"
evm = EVM(code)
evm.run()
print(evm.stack)  
# output: [1, 2, 2]
```



## SWAP

`SWAP`指令用于交换堆栈顶部的两个元素。与`DUP`类似，`SWAP`也是一系列的指令，从`SWAP1`到`SWAP16`共16个，操作码范围为`0x90`到`0x9F`，gas消耗均为3。`SWAP1`交换堆栈的顶部和次顶部的元素，`SWAP2`交换顶部和第三个元素，以此类推。

让我们在极简EVM中增加对`SWAP`指令的支持：

```python
SWAP1 = 0x90
SWAP16 = 0x9F

def swap(self, position):
    if len(self.stack) < position + 1:
        raise Exception('Stack underflow')
    idx1, idx2 = -1, -position - 1
    self.stack[idx1], self.stack[idx2] = self.stack[idx2], self.stack[idx1]

def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()

        # ... 其他指令的实现 ...

        elif SWAP1 <= op <= SWAP16: # 如果是SWAP1-SWAP16
            position = op - SWAP1 + 1
            self.swap(position)
```



现在，我们可以尝试运行一个包含`SWAP1`指令的字节码：`0x6001600290`（PUSH1 1 PUSH1 2 SWAP1）。这个字节码将`1`和`2`推入堆栈，然后进行`SWAP1`交换这两个元素，堆栈最后会变为[2, 1]。

```python
# SWAP1
code = b"\x60\x01\x60\x02\x90"
evm = EVM(code)
evm.run()
print(evm.stack)  
# output: [2, 1]
```



## 总结

这讲过后，我们已经介绍了EVM中最基础的四种堆栈操作：`PUSH`，`POP`，`DUP`，和`SWAP`，理解它们有助于更深入地理解EVM的工作原理。我们写的极简EVM也已经支持了111/144个操作码。

# 12. SHA3指令

这一讲，我们将介绍EVM唯一内置的密码学指令--`SHA3`，你可以用它计算`keccak-256`哈希。

## SHA3指令

在EVM中，计算数据的哈希是一个常见的[操作](https://github.com/AmazingAng/WTF-Solidity/tree/main/28_Hash)。以太坊使用Keccak算法（[SHA-3](https://en.wikipedia.org/wiki/SHA-3)）计算数据的哈希，并提供了一个专门的操作码`SHA3`，Solidity中的`keccak256()`函数就是建立在它之上的。

`SHA3(offset, size)`指令从堆栈中取出两个参数，起始位置`offset`和长度`size`（以字节为单位），然后它从内存中读取起始位置`offset`开始的`size`长度的数据，计算这段数据的Keccak-256哈希，并将结果（一个32字节的值）压入堆栈。它的操作码为`0x20`，gas消耗为`30 + 6*数据的字节长度 + 扩展内存成本`。

在Python中，我们可以使用`pysha3`库来实现`keccak-256`哈希计算。首先你需要安装这个库：

```bash
pip install pysha3
```



下面，让我们在极简EVM中支持SHA3指令：

```python
import sha3

SHA3 = 0x20

def sha3(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    
    offset = self.pop()
    size = self.pop()
    data = self.memory[offset:offset+size]  # 从内存中获取数据
    hash_value = int.from_bytes(sha3.keccak_256(data).digest(), 'big')  # 计算哈希值
    self.stack.append(hash_value)  # 将哈希值压入堆栈

def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()

        # ... 其他指令的实现 ...

            elif op == SHA3: # 如果为SHA3
                self.sha3()
```

> [!NOTE]
>
> `digest()` 会返回哈希计算的结果，结果是一个 32 字节（256 位）的 **字节序列**，也就是 Keccak-256 的输出。这是哈希函数的特性，输入的任何数据长度都被压缩为固定长度的输出。

我们可以尝试运行一个包含`SHA3`指令的字节码：`0x5F5F20`（PUSH0 PUSH0 SHA3）。这个字节码将两个`0`推入堆栈，然后使用`SHA3`指令计算`0`的哈希。

```python
# SHA3
code = b"\x5F\x5F\x20"
evm = EVM(code)
evm.run()
print(hex(evm.stack[-1]))  # 打印出0的keccak256 hash
# output: 0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470
```



我们可以在evm.codes上验证结果：



![img](https://www.wtf.academy/assets/images/12-1-c394cd816f2b8991991a3e8172269437.png)



## 总结

这一讲，我们介绍了EVM中重要的操作符`SHA3`，它为我们提供了计算数据哈希的功能，这在验证数据或身份时非常重要。目前，我们写的极简EVM已经支持了112/144个操作码，剩下的不多了！

# 13. 账户指令

在这一讲，我们将探索EVM中与账户（Account）相关的4个指令，包括`BALANCE`, `EXTCODESIZE`, `EXTCODE`, 以及 `EXTCODEHASH`。我们能利用这些指令获取以太坊账户的信息。

## 以太坊账户结构

以太坊上的账户分两类：外部账户（Externally Owned Accounts，EOA）和合约账户。EOA是用户在以太坊网络上的代表，它们可以拥有ETH、发送交易并与合约互动；而合约账户是存储和执行智能合约代码的实体，它们也可以拥有和发送ETH，但不能主动发起交易。



![img](https://www.wtf.academy/assets/images/13-1-a1e3580559e2048f52ef16079a3551d5.png)



以太坊上的账户结构非常简单，你可以它理解为地址到账户状态的映射。账户地址是20字节（160位）的数据，可以用40位的16进制表示，比如`0x9bbfed6889322e016e0a02ee459d306fc19545d8`。而账户的状态具有4种属性：

- **Balance**：这是账户持有的ETH数量，用Wei表示（1 ETH = 10^18 Wei）。
- **Nonce**：对于外部账户（EOA），这是该账户发送的交易数。对于合约账户，它是该账户创建的合约数量。
- **Storage**：每个合约账户都有与之关联的存储空间，其中包含状态变量的值。
- **Code**：合约账户的字节码。

也就是说，只有合约账户拥有`Storage`和`Code`，EOA没有。

为了让极简EVM支持账户相关的指令，我们利用`dict`做一个简单账户数据库：

```python
account_db = {
    '0x9bbfed6889322e016e0a02ee459d306fc19545d8': {
        'balance': 100, # wei
        'nonce': 1, 
        'storage': {},
        'code': b'\x60\x00\x60\x00'  # Sample bytecode (PUSH1 0x00 PUSH1 0x00)
    },
    # ... 其他账户数据 ...
}
```



下面，我们将介绍账户相关指令。

## BALANCE

`BALANCE` 指令用于返回某个账户的余额。它从堆栈中弹出一个地址，然后查询该地址的余额并压入堆栈。它的操作码是`0x31`，gas为2600（cold address）或100（warm address）。

```python
def balance(self):
    if len(self.stack) < 1:
        raise Exception('Stack underflow')
    addr_int = self.stack.pop()
    # 将stack中的int转换为bytes，然后再转换为十六进制字符串，用于在账户数据库中查询
    addr_str = '0x' + addr_int.to_bytes(20, byteorder='big').hex()
    self.stack.append(account_db.get(addr_str, {}).get('balance', 0))
```



我们可以尝试运行一个包含`BALANCE`指令的字节码：`739bbfed6889322e016e0a02ee459d306fc19545d831`（PUSH20 9bbfed6889322e016e0a02ee459d306fc19545d8 BALANCE）。这个字节码使用`PUSH20`将一个地址推入堆栈，然后使用`BALANCE`指令查询该地址的余额。

```python
# BALANCE
code = b"\x73\x9b\xbf\xed\x68\x89\x32\x2e\x01\x6e\x0a\x02\xee\x45\x9d\x30\x6f\xc1\x95\x45\xd8\x31"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: 100
```



## EXTCODESIZE

`EXTCODESIZE` 指令用于返回某个账户的代码长度（以字节为单位）。它从堆栈中弹出一个地址，然后查询该地址的代码长度并压入堆栈。如果账户不存在或没有代码，返回0。他的操作码为`0x3B`，gas为2600（cold address）或100（warm address）。

```python
def extcodesize(self):
    if len(self.stack) < 1:
        raise Exception('Stack underflow')
    addr_int = self.stack.pop()
    # 将stack中的int转换为bytes，然后再转换为十六进制字符串，用于在账户数据库中查询
    addr_str = '0x' + addr_int.to_bytes(20, byteorder='big').hex()
    self.stack.append(len(account_db.get(addr_str, {}).get('code', b'')))
```

> [!NOTE]
>
> `account_db.get(addr_str, {})`：尝试从账户数据库（`account_db`）中获取该地址对应的账户信息，如果该地址在数据库中不存在，返回一个空字典 `{}`。
>
> `.get('code', b'')`：从账户信息中获取 `code` 键值，如果账户没有代码（例如该地址不是智能合约），则返回空字节串 `b''`。
>
> `len(...)`：计算账户代码的字节长度。如果该地址是一个普通账户而不是合约账户，`code` 会是空的，长度为 0。
>
> `EXTCODESIZE` 用于检查目标地址上的合约代码大小。通过 `addr_int` 来获取合约地址，将其转换为标准的以太坊地址格式，然后在账户数据库中查找地址是否有代码。如果有代码，返回其字节长度，如果没有代码，返回 `0`。

我们可以尝试运行一个包含`EXTCODESIZE`指令的字节码：`739bbfed6889322e016e0a02ee459d306fc19545d83B`（PUSH20 9bbfed6889322e016e0a02ee459d306fc19545d8 EXTCODESIZE）。这个字节码使用`PUSH20`将一个地址推入堆栈，然后使用`EXTCODESIZE`指令查询该地址的代码长度。

```python
# EXTCODESIZE
code = b"\x73\x9b\xbf\xed\x68\x89\x32\x2e\x01\x6e\x0a\x02\xee\x45\x9d\x30\x6f\xc1\x95\x45\xd8\x3B"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: 4
```



## EXTCODE

`EXTCODE` 指令用于将某个账户的部分代码复制到EVM的内存中。它会从堆栈中弹出4个参数(addr, mem_offset, code_offset, length)，分别对应要查询的地址，写到内存的偏移量，读取代码的偏移量和长度。它的操作码是`0x3C`，gas由读取代码长度、内存扩展成本和地址是否为cold这三部分决定。

```python
def extcode(self):
    # 确保堆栈中有足够的数据
    if len(self.stack) < 4:
        raise Exception('Stack underflow')
    addr = self.stack.pop()
    mem_offset = self.stack.pop()
    code_offset = self.stack.pop()
    length = self.stack.pop()
    
    code = account_db.get(addr, {}).get('code', b'')[code_offset:code_offset+length]
    
    while len(self.memory) < mem_offset + length:
        self.memory.append(0)
        
    self.memory[mem_offset:mem_offset+length] = code
```



我们可以尝试运行一个包含`EXTCODE`指令的字节码：`60045F5F739bbfed6889322e016e0a02ee459d306fc19545d83C`（PUSH1 4 PUSH0 PUSH0 PUSH20 9bbfed6889322e016e0a02ee459d306fc19545d8 EXTCODE）。这个字节码将4（`length`）, 0（`code_offset`）, 0（`mem_offset`）, 地址（`addr`）分别推入堆栈，然后，然后使用`EXTCODE`指令将代码复制到内存中。

```python
# EXTCODE
code = b"\x60\x04\x5F\x5F\x73\x9b\xbf\xed\x68\x89\x32\x2e\x01\x6e\x0a\x02\xee\x45\x9d\x30\x6f\xc1\x95\x45\xd8\x3C"
evm = EVM(code)
evm.run()
print(evm.memory.hex())
# output: 60006000
```



## EXTCODEHASH

`EXTCODEHASH` 指令返回某个账户的代码的Keccak256哈希值。它从堆栈中弹出一个地址，然后查询该地址代码的哈希并压入堆栈。它的操作码是`0x3F`，gas为2600（cold address）或100（warm address）。

```python
import sha3

def extcodehash(self):
    if len(self.stack) < 1:
        raise Exception('Stack underflow')
    addr_int = self.stack.pop()
    # 将stack中的int转换为bytes，然后再转换为十六进制字符串，用于在账户数据库中查询
    addr_str = '0x' + addr_int.to_bytes(20, byteorder='big').hex()
    code = account_db.get(addr_str, {}).get('code', b'')        
    code_hash = int.from_bytes(sha3.keccak_256(code).digest(), 'big')  # 计算哈希值
    self.stack.append(code_hash)
```



我们可以尝试运行一个包含`EXTCODEHASH`指令的字节码：`739bbfed6889322e016e0a02ee459d306fc19545d83F`（PUSH20 9bbfed6889322e016e0a02ee459d306fc19545d8 EXTCODEHASH）。这个字节码使用`PUSH20`将一个地址推入堆栈，然后使用`EXTCODEHASH`指令查询该地址的代码哈希。

```python
# EXTCODEHASH
code = b"\x73\x9b\xbf\xed\x68\x89\x32\x2e\x01\x6e\x0a\x02\xee\x45\x9d\x30\x6f\xc1\x95\x45\xd8\x3F"
evm = EVM(code)
evm.run()
print(hex(evm.stack[-1]))
# output: 0x5e3ce470a8506d55e59815db7232a08774174ae0c7fdb2fbc81a49e4e242b0d6
```



## 总结

这一讲，我们简单介绍了以太坊账户结构，并学习了与账户相关的一系列指令。这些指令使得合约可以与以太坊上的其他账户交互并获取相关信息，为合约间的交互提供了基础。目前，我们已经学习了144个操作码中的116个！

# 14. 交易指令

在这一讲，我们将探索EVM中与交易（Transaction）上下文相关的4个指令，包括`ADDRESS`, `ORIGIN`, `CALLER`等。我们能利用这些指令访问当前交易或调用者的信息。

## 交易的基本结构



![img](https://www.wtf.academy/assets/images/14-1-7353ce0a85735858219ea3643f5837b5.png)



在深入学习这些指令之前，让我们先了解以太坊交易的基本结构。每一笔以太坊交易都包含以下属性：

- `nonce`：一个与发送者账户相关的数字，表示该账户已发送的交易数。

- `gasPrice`：交易发送者愿意支付的单位gas价格。

- `gasLimit`：交易发送者为这次交易分配的最大gas数量。

- `to`：交易的接收者地址。当交易为合约创建时，这一字段为空。

- `value`：以wei为单位的发送金额。

- ```
  data
  ```

  ：附带的数据，通常为合约调用的输入数据（calldata）或新合约的初始化代码（initcode）。

  ![img](https://www.wtf.academy/assets/images/14-2-a1f06f6ad751d606ca9c8175065916ed.png)

- `v, r, s`：与交易签名相关的三个值。

在此基础上，我们可以在极简EVM中添加一个交易类，除了上述的信息以外，我们还把一些交易上下文分信息包含其中，包含当前调用者`caller`，原始发送者`origin`（签名者），和执行合约地址，`thisAddr`（Solidity中的`address(this)`）:

```python
class Transaction:
    def __init__(self, to = '', value = 0, data = '', caller='0x00', origin='0x00', thisAddr='0x00', gasPrice=1, gasLimit=21000, nonce=0, v=0, r=0, s=0):
        self.nonce = nonce
        self.gasPrice = gasPrice
        self.gasLimit = gasLimit
        self.to = to
        self.value = value
        self.data = data
        self.caller = caller
        self.origin = origin
        self.thisAddr = thisAddr
        self.v = v
        self.r = r
        self.s = s
```



当初始化evm对象时，需要传入`Transaction`对象:

```python
class EVM:
    def __init__(self, code, txn = None):

        # 初始化其他变量...

        self.txn = txn

# 示例
code = b"\x73\x9b\xbf\xed\x68\x89\x32\x2e\x01\x6e\x0a\x02\xee\x45\x9d\x30\x6f\xc1\x95\x45\xd8\x31"
txn = Transaction(to='0x9bbfed6889322e016e0a02ee459d306fc19545d8', value=10, data='', caller='0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045', origin='0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045')
vm = EVM(code, txn)
```



## 交易指令

### 1. ADDRESS

- 操作码：`0x30`
- gas消耗: 2
- 功能：将当前执行合约的地址压入堆栈。
- 使用场景：当合约需要知道自己的地址时使用。

```python
def address(self):
    self.stack.append(self.txn.thisAddr)
```



### 2. ORIGIN

- 操作码：`0x32`
- gas消耗: 2
- 功能：将交易的原始发送者（即签名者）地址压入堆栈。
- 使用场景：区分合约调用者与交易发起者。

```python
def origin(self):
    self.stack.append(self.txn.origin)
```



### 3. CALLER

- 操作码：`0x33`
- gas消耗: 2
- 功能：将直接调用当前合约的地址压入堆栈。
- 使用场景：当合约需要知道是谁调用了它时使用。

```python
def caller(self):
    self.stack.append(self.txn.caller)
```



### 4. CALLVALUE

- 操作码：`0x34`
- gas消耗: 2
- 功能：将发送给合约的ether的数量（以wei为单位）压入堆栈。
- 使用场景：当合约需要知道有多少以太币被发送时使用。

```python
def callvalue(self):
    self.stack.append(self.txn.value)
```



### 5. CALLDATALOAD

- 操作码：`0x35`
- gas消耗: 3
- 功能：从交易或合约调用的`data`字段加载数据。它从堆栈中弹出calldata的偏移量（`offset`），然后从calldata的`offset`位置读取32字节的数据并压入堆栈。如果calldata剩余不足32字节，则补0。
- 使用场景：读取传入的数据。

```python
def calldataload(self):
    if len(self.stack) < 1:
        raise Exception('Stack underflow')
    offset = self.stack.pop()
    # 从字符形式转换为bytes数组
    calldata_bytes = bytes.fromhex(self.txn.data[2:])  # 假设由 '0x' 开头
    data = bytearray(32)
    # 复制calldata
    for i in range(32):
        if offset + i < len(calldata_bytes):
            data[i] = calldata_bytes[offset + i]
    self.stack.append(int.from_bytes(data, 'big'))
```



### 6. CALLDATASIZE

- 操作码：`0x36`
- gas消耗：2
- 功能：获取交易或合约调用的`data`字段的字节长度，并压入堆栈。
- 使用场景：在读取数据之前检查大小。

```python
def calldatasize(self):
    # Assuming calldata is a hex string with a '0x' prefix
    size = (len(self.transaction.data) - 2) // 2
    self.stack.append(size)
```

> [!NOTE]
>
> 每两个十六进制字符对应 1 个字节，所以需要将长度除以 2。



### 7. CALLDATA

- 操作码：`0x37`
- gas消耗：3 + 3 * 数据长度 + 内存扩展成本
- 功能：将`data`中的数据复制到内存中。它会从堆栈中弹出3个参数(mem_offset, calldata_offset, length)，分别对应写到内存的偏移量，读取calldata的偏移量和长度。
- 使用场景：将输入数据复制到内存。

```python
def calldata(self):
    # 确保堆栈中有足够的数据
    if len(self.stack) < 3:
        raise Exception('Stack underflow')
    mem_offset = self.stack.pop()
    calldata_offset = self.stack.pop()
    length = self.stack.pop()
        
    # 拓展内存
    if len(self.memory) < mem_offset + length:
        self.memory.extend([0] * (mem_offset + length - len(self.memory)))

    # 从字符形式转换为bytes数组.
    calldata_bytes = bytes.fromhex(self.txn.data[2:])  # Assuming it's prefixed with '0x'

    # 将calldata复制到内存
    for i in range(length):
        if calldata_offset + i < len(calldata_bytes):
            self.memory[mem_offset + i] = calldata_bytes[calldata_offset + i]
```

> [!NOTE]
>
> 这段代码的功能是将交易中的 `calldata`（传入数据）复制到 EVM 的内存中。具体的步骤如下：
>
> ### 1. **堆栈数据验证**
> ```python
> if len(self.stack) < 3:
>     raise Exception('Stack underflow')
> ```
> 这一步确保 EVM 的堆栈中至少有 3 个元素。这三个元素分别是：
> - `mem_offset`：内存的偏移量，表示将 `calldata` 复制到内存的起始位置。
> - `calldata_offset`：从 `calldata` 中读取数据的起始位置。
> - `length`：要从 `calldata` 中读取并复制到内存中的数据长度。
>
> ### 2. **弹出堆栈中的参数**
> ```python
> mem_offset = self.stack.pop()
> calldata_offset = self.stack.pop()
> length = self.stack.pop()
> ```
> 从堆栈中弹出上面提到的 3 个参数，分别用来控制数据复制的起始位置和数据长度。
>
> ### 3. **拓展内存**
> ```python
> if len(self.memory) < mem_offset + length:
>     self.memory.extend([0] * (mem_offset + length - len(self.memory)))
> ```
> 确保内存的大小足够容纳从 `calldata` 复制过来的数据。如果内存的长度不足以放下从 `mem_offset` 开始、长度为 `length` 的数据，就会将内存扩展到所需的大小。
>
> ### 4. **转换 `calldata` 为字节数组**
> ```python
> calldata_bytes = bytes.fromhex(self.txn.data[2:])  # Assuming it's prefixed with '0x'
> ```
> 这里假设 `self.txn.data` 是一个以 `'0x'` 为前缀的十六进制字符串，表示交易的 `calldata`。`[2:]` 是为了去掉前缀 `'0x'`。`bytes.fromhex()` 会将这个十六进制字符串转换为一个字节数组（`bytes` 对象），每两个十六进制字符对应一个字节。
>
> ### 5. **复制 `calldata` 到内存**
> ```python
> for i in range(length):
>     if calldata_offset + i < len(calldata_bytes):
>         self.memory[mem_offset + i] = calldata_bytes[calldata_offset + i]
> ```
> 这一步从 `calldata` 中按照 `calldata_offset` 偏移和 `length` 长度读取数据，并逐字节复制到内存中。
>
> - 使用 `for i in range(length)` 循环，遍历要复制的数据长度。
> - 检查 `calldata_offset + i` 是否在 `calldata_bytes` 的范围内（避免读取越界）。如果在范围内，将 `calldata_bytes` 的相应字节复制到 `self.memory` 中，从 `mem_offset` 开始填充。
>
> ### 总结
> 该函数的主要作用是将 `calldata` 的一部分复制到 EVM 的内存中。通过从堆栈中获取内存偏移量、`calldata` 偏移量和数据长度，函数在内存和 `calldata` 之间进行数据转移，并保证内存空间足够大。

> [!TIP]
>
> `calldata` 和 `calldataload` 两者都是操作 EVM 中交易的 `calldata` 数据，但它们的功能和用法有所不同：
>
> ### **1. `calldata` 函数：**
> - **主要功能**：从 `calldata` 中复制一个长度为 `length` 的数据段到 EVM 内存中，并且可以自由指定复制的偏移量和长度。
> - **操作步骤**：
>   - 从堆栈中获取 `mem_offset`、`calldata_offset` 和 `length`，分别对应内存中的偏移量、`calldata` 的偏移量，以及需要复制的数据长度。
>   - 将 `calldata` 中的数据逐字节复制到内存中。
> - **用法场景**：通常用于处理任意长度的 `calldata`，比如需要将多个字节从 `calldata` 复制到 EVM 内存以供后续使用。
>
> ### **2. `calldataload` 函数：**
> - **主要功能**：从 `calldata` 中加载一个固定长度的 32 字节（256 位）数据，并将其作为一个整型推入堆栈。
> - **操作步骤**：
>   - 从堆栈中获取一个偏移量 `offset`。
>   - 从 `calldata` 中，从 `offset` 开始，提取 32 字节。如果 `calldata` 的长度不够 32 字节，剩下的部分用 0 填充。
>   - 将提取出的 32 字节数据作为一个大整数推入堆栈。
> - **用法场景**：用于快速加载 32 字节的块数据，这是 EVM 中处理 `calldata` 时的常用操作。
>
> ### **核心区别**：
> 1. **复制范围和长度**：
>    - `calldata` 可以从 `calldata` 中任意偏移、任意长度地复制数据到 EVM 内存。
>    - `calldataload` 则是固定地从 `calldata` 的某个偏移量开始加载 **32 字节** 数据，并直接压入堆栈。
>
> 2. **操作目标**：
>    - `calldata` 将数据从 `calldata` 复制到 **内存**。
>    - `calldataload` 直接将数据从 `calldata` 加载到 **堆栈**。
>
> 3. **数据长度**：
>    - `calldata` 操作的长度由用户指定，可以是任意长度。
>    - `calldataload` 只能加载 **32 字节** 的数据。
>
> ### 示例对比：
> - 假设 `calldata` 包含 64 字节数据，而我们希望提取前 32 字节：
>   - **`calldata`**：我们可以设置 `length = 32`，将前 32 字节复制到内存。
>   - **`calldataload`**：直接从偏移 0 开始加载 32 字节到堆栈。
>
> ```python
> # calldata 函数操作示例（复制数据到内存）
> mem_offset = 0
> calldata_offset = 0
> length = 32
> calldata_bytes = bytes.fromhex(self.txn.data[2:])
> self.memory[mem_offset:mem_offset+length] = calldata_bytes[calldata_offset:calldata_offset+length]
> 
> # calldataload 函数操作示例（加载数据到堆栈）
> offset = 0
> data = calldata_bytes[offset:offset+32]
> self.stack.append(int.from_bytes(data, 'big'))
> ```
>
> 总体来说，`calldataload` 提供了更高效的固定长度数据读取，而 `calldata` 允许灵活的内存管理和更自由的数据操作。



### 8. CODESIZE

- 操作码：`0x38`
- gas消耗： 2
- 功能：获取当前合约代码的字节长度，然后压入堆栈。
- 使用场景：当合约需要访问自己的字节码时使用。

```python
def codesize(self):
    addr = self.txn.thisAddr
    self.stack.append(len(account_db.get(addr, {}).get('code', b'')))
```



### 9. CODE

- 操作码：`0x39`
- gas消耗：3 + 3 * 数据长度 + 内存扩展成本
- 功能：复制合约的代码到EVM的内存中。它从堆栈中弹出三个参数：目标内存的开始偏移量（`mem_offset`）、代码的开始偏移量（`code_offset`）、以及要复制的长度（`length`）。
- 使用场景：当合约需要读取自己的部分字节码时使用。

```python
def code(self):
    if len(self.stack) < 3:
        raise Exception('Stack underflow')

    mem_offset = self.stack.pop()
    code_offset = self.stack.pop()
    length = self.stack.pop()

    # 获取当前地址的code
    addr = self.txn.thisAddr
    code = account_db.get(addr, {}).get('code', b'')

    # 拓展内存
    if len(self.memory) < mem_offset + length:
        self.memory.extend([0] * (mem_offset + length - len(self.memory)))

    # 将代码复制到内存
    for i in range(length):
        if code_offset + i < len(code):
            self.memory[mem_offset + i] = code[code_offset + i]
```



### 10. GASPRICE

- 操作码：`0x3A`
- gas消耗：2
- 功能：获取交易的gas价格，并压入堆栈。
- 使用场景：当合约需要知道当前交易的gas价格时使用。

```python
def gasprice(self):
    self.stack.append(self.txn.gasPrice)
```



## 总结

在这一讲，我们详细介绍了EVM中与交易有关的10个指令。这些指令为智能合约提供了与其环境交互的能力，使其能够访问调用者，calldata，和代码等信息。目前，我们已经学习了144个操作码中的126个！

# 15. Log指令

这一讲，我们将介绍EVM中与日志（Log）相关的5个指令：：从`LOG0`到`LOG4`。日志是EVM中一个重要的概念，用于记录与合约交互的重要信息，是智能合约中事件（Event）的基础。这些记录永久保存在在区块链上，方便检索，但不会影响区块链的状态，是DApps和智能合约开发者的一个强大工具。

## EVM中的日志和事件

在Solidity中，我们常常使用`event`来定义和触发事件。当这些事件被触发时，它们会生成日志，将数据永久存储在区块链上。日志分为主题（`topic`）和数据（`data`）。第一个主题通常是事件签名的哈希值，后面的主题是由`indexed`修饰的事件参数。如果你对`event`不了解，推荐阅读WTF Solidity的[相应章节](https://github.com/AmazingAng/WTF-Solidity/tree/main/12_Event)。

EVM中的`LOG`指令用于创建这些日志。指令`LOG0`到`LOG4`的区别在于它们包含的主题数量。例如，`LOG0`没有主题，而`LOG4`有四个主题。

为了在我们的极简EVM中支持日志功能，我们首先需要定义一个`Log`类来表示一个日志条目，他会记录发出日志的合约地址`address`，数据部分`data`，和主体部分`topics`：

```python
class Log:
    def __init__(self, address, data, topics=[]):
        self.address = address
        self.data = data
        self.topics = topics

    def __str__(self):
        return f'Log(address={self.address}, data={self.data}, topics={self.topics})'
```



然后，我们需要在EVM的初始化函数中增加一个`logs`列表，记录这些日志：

```python
class EVM:
    def __init__(self, code, txn = None):
        
        # ... 初始化其他变量 ...

        self.logs = []
```



## LOG指令

EVM中有五个`Log`指令：`LOG0`、`LOG1`、`LOG2`、`LOG3`和`LOG4`。它们的主要区别在于携带的主题数（`topics`）：`LOG0`没有主题，而`LOG4`有四个。操作码从`A0`到`A4`，gas消耗由以下公式计算:

```python
gas = 375 + 375 * topic数量 + 内存扩展成本
```



`Log`指令从堆栈中弹出2 + n的元素。其中前两个参数是内存开始位置`mem_offset`和数据长度`length`，n是主题的数量（取决于具体的`LOG`指令）。所以对于`LOG1`，我们会从堆栈中弹出3个元素：内存开始位置，数据长度，和一个主题。需要`mem_offset`的原因是日志的数据（`data`）部分存储在内存中，gas消耗低，而主题（`topic`）部分直接存储在堆栈上。

接下来，我们实现`LOG`指令：

```python
def log(self, num_topics):
    if len(self.stack) < 2 + num_topics:
        raise Exception('Stack underflow')

    mem_offset = self.stack.pop()
    length = self.stack.pop()
    topics = [self.stack.pop() for _ in range(num_topics)]

    data = self.memory[mem_offset:mem_offset + length]
    log_entry = {
        "address": self.txn.thisAddr,
        "data": data.hex(),
        "topics": [f"0x{topic:064x}" for topic in topics]
    }
    self.logs.append(log_entry)
```

> [!NOTE]
>
> 这段代码 `f"0x{topic:064x}"` 是一个格式化字符串（f-string），用于将一个整数格式化为十六进制字符串，并添加前缀 `0x`。具体解释如下：
>
> ### 解释
>
> 1. **f-string**:
>    - 以 `f` 开头的字符串表示格式化字符串，允许在字符串中嵌入表达式。
>    - 例如，`{topic}` 会被替换为变量 `topic` 的值。
>
> 2. **`topic:064x`**:
>    - **`064`**：表示总宽度为 64 个字符，不足的部分用零填充。
>    - **`x`**：表示以小写字母形式格式化为十六进制。
>    - 所以，如果 `topic` 是一个整数，`064x` 会将它转换为一个 64 位的十六进制字符串，如果实际转换后的字符串长度不足 64 位，会在前面填充零。
>
> 3. **前缀 `0x`**:
>    - `0x` 是十六进制数的常见表示方式，用于指示数字是以十六进制表示。
>
> ### 举个例子
>
> 假设 `topic` 的值为 `255`，则：
> ```python
> topic = 255
> formatted_topic = f"0x{topic:064x}"
> print(formatted_topic)
> ```
> 输出结果将是：
> ```
> 0x00000000000000000000000000000000000000000000000000000000000000ff
> ```
> - 这里的 `ff` 是 `255` 的十六进制表示，前面填充了足够的零以确保总长度为 64 个字符。
>
> ### 结论
> `f"0x{topic:064x}"` 主要用于确保 `topic` 在被转换为十六进制字符串时，符合特定的格式和宽度要求，通常用于在区块链或 EVM 的上下文中记录地址或主题。

最后，我们需要在`run`方法中为不同的`LOG`指令添加支持：

```python
def run(self):
    while self.pc < len(self.code):
        op = self.next_instruction()
        
        # ... 其他指令的处理 ...
        
        elif op == LOG0:
            self.log(0)
        elif op == LOG1:
            self.log(1)
        elif op == LOG2:
            self.log(2)
        elif op == LOG3:
            self.log(3)
        elif op == LOG4:
            self.log(4)
```



## 测试

### 测试`LOG0`

我们运行一个包含`LOG0`指令的字节码：`60aa6000526001601fa0`（PUSH1 aa PUSH1 0 MSTORE PUSH1 1 PUSH1 1f LOG0）。这个字节码将`aa`存在内存中，然后使用`LOG0`指令将`aa`输出到日志的数据部分。

```python
# LOG0
code = b"\x60\xaa\x60\x00\x52\x60\x01\x60\x1f\xa0"
evm = EVM(code, txn)
evm.run()
print(evm.logs)
# output: [{'address': '0x9bbfed6889322e016e0a02ee459d306fc19545d8', 'data': 'aa', 'topics': []}]
```



### 测试`LOG1`

我们运行一个包含`LOG1`指令的字节码：`60aa60005260116001601fa1`（PUSH1 aa PUSH1 0 MSTORE PUSH 11 PUSH1 1 PUSH1 1f LOG1）。这个字节码将`aa`存在内存，然后将`11`压入堆栈，最后使用`LOG1`指令将`aa`输出到日志的数据部分，将`11`输出到日志的主题部分。

```python
# LOG1
code = b"\x60\xaa\x60\x00\x52\x60\x11\x60\x01\x60\x1f\xa1"
evm = EVM(code, txn)
evm.run()
print(evm.logs)
# output: [{'address': '0x9bbfed6889322e016e0a02ee459d306fc19545d8', 'data': 'aa', 'topics': ['0x0000000000000000000000000000000000000000000000000000000000000011']}]
```



## 总结

这一讲，我们学习了EVM中与日志和事件相关的5个指令。这些指令在智能合约开发中扮演着关键角色，允许开发者在区块链上永久记录重要信息，同时不会影响区块链的状态。目前，我们已经学习了144个操作码中的131个！

# 16. Return指令

这一讲，我们将介绍EVM中与返回数据（return）相关的3个指令: `RETURN`，`RETURNDATASIZE`，和`RETURNDATA`。它们是Solidity中`return`关键字的基础。

## 返回数据

EVM的返回数据，通常称为`returnData`，本质上是一个字节数组。它不遵循固定的数据结构，而是简单地表示为连续的字节。当合约函数需要返回复杂数据类型（如结构体或数组）时，这些数据将按照ABI规范被编码为字节，并存储在`returnData`中，供其他函数或合约访问。

为了支持这一特性，我们需要为我们的简化版EVM添加一个新属性以保存返回数据：

```python
class EVM:
    def __init__(self):
        # ... 其他属性 ...
        self.returnData = bytearray()
```



## 返回相关指令

### 1. RETURN

- **操作码**：`0xF3`
- **gas消耗**：内存扩展成本。
- **功能**：从指定的内存位置提取数据，存储到`returnData`中，并终止当前的操作。此指令需要从堆栈中取出两个参数：内存的起始位置`mem_offset`和数据的长度`length`。
- **使用场景**：当需要将数据返回给外部函数或交易时。

```python
def return_op(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')

    mem_offset = self.stack.pop()
    length = self.stack.pop()
    
    # 拓展内存
    if len(self.memory) < mem_offset + length:
        self.memory.extend([0] * (mem_offset + length - len(self.memory)))

    self.returnData = self.memory[offset:offset + length]      
```



### 2. RETURNDATASIZE

- **操作码**：`0x3D`
- **gas消耗**：2
- **功能**：将`returnData`的大小推入堆栈。
- **使用场景**：使用上一个调用返回的数据。

```python
def returndatasize(self):
    self.stack.append(len(self.returnData))
```



### 3. RETURNDATA

- 操作码：`0x3E`
- gas消耗： 3 + 3 * 数据长度 + 内存扩展成本
- **功能**：将`returnData`中的某段数据复制到内存中。此指令需要从堆栈中取出三个参数：内存的起始位置`mem_offset`，返回数据的起始位置`return_offset`，和数据的长度`length`。
- **使用场景**：使用上一个调用返回的部分数据。

```python
def returndata(self):
    if len(self.stack) < 3:
        raise Exception('Stack underflow')

    mem_offset = self.stack.pop()
    return_offset = self.stack.pop()
    length = self.stack.pop()

    if return_offset + length > len(self.returnData):
        raise Exception("Invalid returndata size")

    # 扩展内存
    if len(self.memory) < mem_offset + length:
        self.memory.extend([0] * (mem_offset + length - len(self.memory)))

    # 使用切片进行复制
    self.memory[mem_offset:mem_offset + length] = self.returnData[return_offset:return_offset + length]
```



## 测试

1. **RETURN**: 我们运行一个包含`RETURN`指令的字节码：`60a26000526001601ff3`（PUSH1 a2 PUSH1 0 MSTORE PUSH1 1 PUSH1 1f RETURN）。这个字节码将`a2`存在内存中，然后使用`RETURN`指令将`a2`复制到`returnData`中。

~~~text
```python
# RETURN
code = b"\x60\xa2\x60\x00\x52\x60\x01\x60\x1f\xf3"
evm = EVM(code)
evm.run()
print(evm.returnData.hex())
# output: a2
```
~~~



1. **RETURNDATASIZE**：我们将`returnData`设为`aaaa`，然后用`RETURNDATASIZE`将它的长度压入堆栈。

   ```python
   # RETURNDATASIZE
   code = b"\x3D"
   evm = EVM(code)
   evm.returnData = b"\xaa\xaa"
   evm.run()
   print(evm.stack)
   # output: 2
   ```

   

2. **RETURNDATA**：我们将`returnData`设为`aaaa`，然后运行一个包含`RETURNDATA`指令的字节码：`60025F5F3E`（PUSH1 2 PUSH0 PUSH0 RETURNDATA），将返回数据存入内存。

   ```python
   # RETURNDATA
   code = b"\x60\x02\x5F\x5F\x3E"
   evm = EVM(code)
   evm.returnData = b"\xaa\xaa"
   evm.run()
   print(evm.memory.hex())
   # output: aaaa
   ```

   

## 总结

这一讲，我们学习了EVM中与返回数据相关的3个指令：`RETURN`、`RETURNDATASIZE`，和`RETURNDATA`，并通过代码示例为极简EVM添加了对这些指令的支持。目前，我们已经学习了144个操作码中的134个（93%）！



# 17. Revert指令

这一讲，我们将介绍EVM中与异常处理相关的2个指令: `REVERT` 和 `INVALID`。当它们被触发时，交易会回滚。

## 交易状态

我们需要在咱们的极简`evm`中跟踪交易的状态`success`，默认为`True`，当交易失败回滚时变为`False`，只有当`success`为`True`时继续执行opcodes，否则结束交易:

```python
class EVM:
    def __init__(self):
        # ... 其他属性 ...
        self.success = True

    def run(self):
        while self.pc < len(self.code) and self.success:
            op = self.next_instruction()
        # ... 指令操作 ...
```



## REVERT

当合约运行出错，或者达到了某种条件需要终止执行并返回错误信息时，可以使用`REVERT`指令。`REVERT`指令会终止交易的执行，返回一个错误消息，并且所有状态更改（例如资金转移、存储值的更改等）都不会生效。它会从堆栈中弹出两个参数：内存中错误消息的起始位置`mem_offset`和错误消息的长度`length`。它的操作码为`0xFD`，gas消耗为内存扩展消耗。

```python
def revert(self):
    if len(self.stack) < 2:
        raise Exception('Stack underflow')
    mem_offset = self.stack.pop()
    length = self.stack.pop()

    # 拓展内存
    if len(self.memory) < mem_offset + length:
        self.memory.extend([0] * (mem_offset + length - len(self.memory)))

    self.returnData = self.memory[mem_offset:mem_offset+length]
    self.success = False
```



## INVALID

`INVALID`是EVM中用来表示无效操作的指令。当EVM遇到无法识别的操作码时，或者在故意触发异常的情境下，它会执行`INVALID`指令，导致所有状态更改都不会生效，并且消耗掉所有的gas。它确保了当合约试图执行未定义的操作时，不会无所作为或产生不可预测的行为，而是会安全地停止执行，对EVM的安全至关重要。它的操作码为`0xFE`，gas消耗为所有剩余的gas。

```python
def invalid(self):
    self.success = False
```



## 测试

1. **REVERT**: 我们运行一个包含`REVERT`指令的字节码：`60aa6000526001601ffd`（PUSH1 aa PUSH1 0 MSTORE PUSH1 1 PUSH1 1f REVERT）。这个字节码将`aa`存在内存中，然后使用`REVERT`指令将交易回滚，并将`aa`复制到`returnData`中。

~~~text
```python
# REVERT
code = b"\x60\xa2\x60\x00\x52\x60\x01\x60\x1f\xfd"
evm = EVM(code)
evm.run()
print(evm.returnData.hex())
# output: a2
```
~~~



## 总结

这一讲，我们学习了EVM中与异常处理相关的2个指令：`REVERT`和`INVALID`，并通过代码示例为极简EVM添加了对这些指令的支持。异常处理是任何程序或合约执行的重要部分，而这两个指令是Solidity中的`require`，`error`和`assert`关键字的基础。目前，我们已经学习了144个操作码中的136个（94%）！

# 18. Call指令

这一讲，我们介绍EVM中的`CALL`指令。`CALL`指令可以被视为以太坊的核心，它允许合约之间进行交互，让区块链上的合约不再孤立。如果你不了解`CALL`指令，请参考[WTF Solidity教程第22讲](https://github.com/AmazingAng/WTF-Solidity/blob/main/22_Call/readme.md)。



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410050938494.png)



## CALL 指令

`CALL`指令会创建一个子环境来执行其他合约的部分代码，发送`ETH`，并返回数据。返回数据可以使用`RETURNDATASIZE`和`RETURNDATA`获取。若执行成功，会将`1`压入堆栈；否则，则压入`0`。如果目标合约没有代码，仍将`1`压入堆栈（视为成功）。如果账户`ETH`余额小于要发送的`ETH`数量，调用失败，但当前交易不会回滚。

它从堆栈中弹出7个参数，依次为：

- `gas`：为这次调用分配的gas量。
- `to`：被调用合约的地址。
- `value`：要发送的以太币数量，单位为`wei`。
- `mem_in_start`：输入数据（calldata）在内存的起始位置。
- `mem_in_size`：输入数据的长度。
- `mem_out_start`：返回数据（returnData）在内存的起始位置。
- `mem_out_size`：返回数据的长度。

它的操作码为`0xF1`，gas消耗比较复杂，包含内存扩展和代码执行等成本。

下面，我们在极简EVM中支持`CALL`指令。由于`CALL`指令比较复杂，我们进行了一些简化，主要包括以下几个步骤：读取calldata，更新ETH余额，根据目标地址代码创建evm子环境，执行evm子环境代码，读取返回值。

```python
def call(self):
    if len(self.stack) < 7:
        raise Exception('Stack underflow')
        
    gas = self.stack.pop()
    to_addr = self.stack.pop()
    value = self.stack.pop()
    mem_in_start = self.stack.pop()
    mem_in_size = self.stack.pop()
    mem_out_start = self.stack.pop()
    mem_out_size = self.stack.pop()
    
    # 拓展内存
    if len(self.memory) < mem_in_start + mem_in_size:
        self.memory.extend([0] * (mem_in_start + mem_in_size - len(self.memory)))

    # 从内存中获取输入数据
    data = self.memory[mem_in_start: mem_in_start + mem_in_size]

    account_source = account_db[self.txn.caller]
    account_target = account_db[hex(to_addr)]
    
    # 检查caller的余额
    if account_source['balance'] < value:
        self.success = False
        print("Insufficient balance for the transaction!")
        self.stack.append(0) 
        return
    
    # 更新余额
    account_source['balance'] -= value
    account_target['balance'] += value
    
    # 使用txn构建上下文
    ctx = Transaction(to=hex(to_addr), 
                        data=data,
                        value=value,
                        caller=self.txn.thisAddr, 
                        origin=self.txn.origin, 
                        thisAddr=hex(to_addr), 
                        gasPrice=self.txn.gasPrice, 
                        gasLimit=self.txn.gasLimit, 
                        )
    
    # 创建evm子环境
    evm_call = EVM(account_target['code'], ctx)
    evm_call.run()
    
    # 拓展内存
    if len(self.memory) < mem_out_start + mem_out_size:
        self.memory.extend([0] * (mem_out_start + mem_out_size - len(self.memory)))
    
    self.memory[mem_out_start: mem_out_start + mem_out_size] = evm_call.returnData
    
    if evm_call.success:
        self.stack.append(1)  
    else:
        self.stack.append(0)  
```

> [!NOTE]
>
> 这段代码实现了 Ethereum 虚拟机（EVM）中的 `CALL` 操作。`CALL` 是一种用于向其他合约发送交易的指令，它包括多个参数，如 gas 限制、目标地址、转账金额等。下面是对这段代码的逐步解释：
>
> ### 代码解析
>
> 1. **检查堆栈中的元素数量**:
>    ```python
>    if len(self.stack) < 7:
>        raise Exception('Stack underflow')
>    ```
>    这行代码确保堆栈中有足够的元素（至少 7 个），以避免“堆栈下溢”的错误。如果堆栈元素不足，抛出异常。
>
> 2. **弹出堆栈中的参数**:
>    ```python
>    gas = self.stack.pop()
>    to_addr = self.stack.pop()
>    value = self.stack.pop()
>    mem_in_start = self.stack.pop()
>    mem_in_size = self.stack.pop()
>    mem_out_start = self.stack.pop()
>    mem_out_size = self.stack.pop()
>    ```
>    从堆栈中依次弹出参数：
>    - `gas`: 调用的 gas 限制
>    - `to_addr`: 目标合约地址
>    - `value`: 转账金额
>    - `mem_in_start`: 输入数据在内存中的起始位置
>    - `mem_in_size`: 输入数据的大小
>    - `mem_out_start`: 输出数据在内存中的起始位置
>    - `mem_out_size`: 输出数据的大小
>
> 3. **扩展内存**:
>    ```python
>    if len(self.memory) < mem_in_start + mem_in_size:
>        self.memory.extend([0] * (mem_in_start + mem_in_size - len(self.memory)))
>    ```
>    这部分代码确保内存足够大以容纳输入数据。如果内存长度小于输入数据的起始位置加上其大小，则扩展内存。
>
> 4. **获取输入数据**:
>    ```python
>    data = self.memory[mem_in_start: mem_in_start + mem_in_size]
>    ```
>    从内存中提取输入数据，存储在 `data` 变量中。
>
> 5. **检查余额**:
>    ```python
>    account_source = account_db[self.txn.caller]
>    account_target = account_db[hex(to_addr)]
>       
>    if account_source['balance'] < value:
>        self.success = False
>        print("Insufficient balance for the transaction!")
>        self.stack.append(0) 
>        return
>    ```
>    - 从账户数据库中获取发送方 (`account_source`) 和接收方 (`account_target`) 的信息。
>    - 检查发送方的余额是否足够支付 `value`（转账金额）。如果余额不足，记录失败并返回。
>
> 6. **更新余额**:
>    ```python
>    account_source['balance'] -= value
>    account_target['balance'] += value
>    ```
>    如果余额充足，更新发送方和接收方的余额。
>
> 7. **构建交易上下文**:
>    ```python
>    ctx = Transaction(to=hex(to_addr), 
>                      data=data,
>                      value=value,
>                      caller=self.txn.thisAddr, 
>                      origin=self.txn.origin, 
>                      thisAddr=hex(to_addr), 
>                      gasPrice=self.txn.gasPrice, 
>                      gasLimit=self.txn.gasLimit, 
>                      )
>    ```
>    创建一个 `Transaction` 对象，包含交易的详细信息（如目标地址、输入数据、转账金额等）。
>
> 8. **创建 EVM 子环境并运行**:
>    ```python
>    evm_call = EVM(account_target['code'], ctx)
>    evm_call.run()
>    ```
>    根据目标合约的代码和交易上下文创建一个新的 EVM 实例，然后运行这个实例。
>
> 9. **扩展内存以存储输出数据**:
>    ```python
>    if len(self.memory) < mem_out_start + mem_out_size:
>        self.memory.extend([0] * (mem_out_start + mem_out_size - len(self.memory)))
>    ```
>    确保内存足够大以存储输出数据。
>
> 10. **将输出数据存入内存**:
>     ```python
>     self.memory[mem_out_start: mem_out_start + mem_out_size] = evm_call.returnData
>     ```
>     将调用返回的数据存储到内存中指定的位置。
>
> 11. **更新堆栈中的成功状态**:
>     ```python
>     if evm_call.success:
>         self.stack.append(1)  
>     else:
>         self.stack.append(0)
>     ```
>     根据调用是否成功，向堆栈中压入 `1`（成功）或 `0`（失败）。
>
> ### 总结
>
> 这个 `call` 方法实现了 EVM 中合约间调用的基本逻辑。它处理输入和输出数据、检查账户余额、更新余额，并将结果存入内存和堆栈。通过这种方式，合约可以彼此交互，完成复杂的逻辑。



## 测试

测试用的以太坊账户状态：

```python
account_db = {
    '0x9bbfed6889322e016e0a02ee459d306fc19545d8': {
        'balance': 100, # wei
        'nonce': 1, 
        'storage': {},
        'code': b''
    },
    '0x1000000000000000000000000000000000000c42': {
        'balance': 0, # wei
        'nonce': 0, 
        'storage': {},
        'code': b'\x60\x42\x60\x00\x52\x60\x01\x60\x1f\xf3'  # PUSH1 0x42 PUSH1 0 MSTORE PUSH1 1 PUSH1 31 RETURN
    },

    # ... 其他账户数据 ...
}
```



在测试中，我们会使用第一个地址（`0x9bbf`起始）调用第二个地址（`0x1000`起始），运行上面的代码（`PUSH1 0x42 PUSH1 0 MSTORE PUSH1 1 PUSH1 31 RETURN`），成功的话会返回`0x42`。

测试字节码为`6001601f5f5f6001731000000000000000000000000000000000000c425ff15f51`（PUSH1 1 PUSH1 31 PUSH0 PUSH0 PUSH1 1 PUSH20 1000000000000000000000000000000000000c42 PUSH0 CALL PUSH0 MLOAD），它会调用第二个地址上的代码，并发送`1 wei`的以太坊，然后将内存中的返回值`0x42`压入堆栈。

```python
# Call
code = b"\x60\x01\x60\x1f\x5f\x5f\x60\x01\x73\x10\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x0c\x42\x5f\xf1\x5f\x51"
evm = EVM(code, txn)
evm.run()
print(hex(evm.stack[-2]))
# output: 0x1 (success)
print(hex(evm.stack[-1]))
# output: 0x42
```



## 总结

这一讲，我们探讨了`CALL`指令，它使得EVM上的合约可以调用其他合约，实现更复杂的功能。希望这一讲对您有所帮助！目前，我们已经学习了144个操作码中的137个（95%）！

# 19. Delegatecall指令

这一讲，我们介绍EVM中的`DELEGATECALL`指令和不再建议使用的`CALLCODE`指令。他们与`CALL`指令类似，但是调用的上下文不同。如果你不了解`DELEGATECALL`指令，请参考[WTF Solidity教程第23讲](https://github.com/AmazingAng/WTF-Solidity/blob/main/23_Delegatecall/readme.md)。



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410050938065.png)



## DELEGATECALL

`DELEGATECALL`指令与`CALL`有许多相似之处，但关键的区别在于调用的上下文不同，它在代理合约和可升级合约中被广泛应用。它的设计目的是允许一个合约借用其他合约的代码，但代码是在原始合约的上下文中执行。这使得一份代码可以被多个合约重复使用，而无需重新部署。使用`DELEGATECALL`时`msg.sender`和`msg.value`保持不变，修改的存储变量也是原始合约的。

它从堆栈中弹出6个参数，与`CALL`不同，它不包括`value`，因为ETH不会被发送：

- `gas`：为这次调用分配的gas量。
- `to`：被调用合约的地址。
- `mem_in_start`：输入数据（calldata）在内存的起始位置。
- `mem_in_size`：输入数据的长度。
- `mem_out_start`：返回数据（returnData）在内存的起始位置。
- `mem_out_size`：返回数据的长度。

```python
def delegatecall(self):
    if len(self.stack) < 6:
        raise Exception('Stack underflow')
    
    gas = self.stack.pop()
    to_addr = self.stack.pop()
    mem_in_start = self.stack.pop()
    mem_in_size = self.stack.pop()
    mem_out_start = self.stack.pop()
    mem_out_size = self.stack.pop()
    
    # 拓展内存
    if len(self.memory) < mem_in_start + mem_in_size:
        self.memory.extend([0] * (mem_in_start + mem_in_size - len(self.memory)))

    # 从内存中获取输入数据
    data = self.memory[mem_in_start: mem_in_start + mem_in_size]

    account_target = account_db[hex(to_addr)]
    
    # 创建evm子环境，注意，这里的上下文是原始的调用合约，而不是目标合约
    evm_delegate = EVM(account_target['code'], self.txn)
    evm_delegate.storage = self.storage
    # 运行代码
    evm_delegate.run()
    
    # 拓展内存
    if len(self.memory) < mem_out_start + mem_out_size:
        self.memory.extend([0] * (mem_out_start + mem_out_size - len(self.memory)))
    
    self.memory[mem_out_start: mem_out_start + mem_out_size] = evm_delegate.returnData
    
    if evm_delegate.success:
        self.stack.append(1)  
    else:
        self.stack.append(0)  
        print("Delegatecall execution failed!")
```



有两个关键点需要注意：

1. `DELEGATECALL`不会更改`msg.sender`和`msg.value`。
2. `DELEGATECALL`改变的存储（storage）是原始合约的存储。
3. 与`CALL`不同，`DELEGATECALL`不会传递ETH值，因此少一个`value`参数。

## CALLCODE

`CALLCODE`与`DELEGATECALL`非常相似，但当修改状态变量时，它会更改调用者的合约状态而不是被调用者的合约状态。由于这个原因，`CALLCODE`在某些情况下可能会引起意料之外的行为，目前被视为已弃用。建议大家使用`DELEGATECALL`，而不是`CALLCODE`。

我们根据[EIP-2488](https://eips.ethereum.org/EIPS/eip-2488)，将`CALLCODE`视为已弃用：每次调用在堆栈中压入`0`（视为调用失败）。

```python
def callcode(self):
    self.stack.append(0)  
    print("Callcode not support!")
```



## 测试

在测试中，我们会使用第一个地址（`0x9bbf`起始）调用第二个地址（`0x1000`起始），运行上面的代码（`PUSH1 0x42 PUSH1 0 MSTORE PUSH1 1 PUSH1 31 RETURN`），成功的话会返回`0x42`。

测试字节码为`6001601f5f5f731000000000000000000000000000000000000c425ff45f51`（PUSH1 1 PUSH1 31 PUSH0 PUSH0 PUSH20 1000000000000000000000000000000000000c42 PUSH0 DELEGATECALL PUSH0 MLOAD），它会调用第二个地址上的代码，然后将内存中的返回值`0x42`压入堆栈。

```python
# Delegatecall
code = b"\x60\x01\x60\x1f\x5f\x5f\x73\x10\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x0c\x42\x5f\xf4\x5f\x51"
evm = EVM(code, txn)
evm.run()
print(hex(evm.stack[-2]))
# output: 0x1 (success)
print(hex(evm.stack[-1]))
# output: 0x42
```



## 总结

这一讲，我们探讨了`DELEGATECALL`指令，它使得EVM上的合约在不更改上下文的情况下调用其他合约，增加代码的复用性。它在代理合约和可升级合约中被广泛应用。另外，我们还介绍了已被视为弃用的`CALLCODE`指令。目前，我们已经学习了144个操作码中的139个（96%）！

# 20. Staticcall指令

这一讲，我们介绍EVM中的`STATICCALL`指令，它和`CALL`指令类似，允许合约执行其他合约的代码，但是不能改变合约状态。它是Solidity中`pure`和`view`关键字的基础。

## STATICCALL 指令

`STATICCALL`指令会创建一个子环境来执行其他合约的部分代码，并返回数据。返回数据可以使用`RETURNDATASIZE`和`RETURNDATA`获取。若执行成功，会将`1`压入堆栈；否则，则压入`0`。如果目标合约没有代码，仍将`1`压入堆栈（视为成功）。

和`CALL`指令的不同，`STATICCALL`不能发送`ETH`，也不能改变合约的状态。它不允许子环境执行的代码中包含以下指令：

- `CREATE`, `CREATE2`, `SELFDESTRUCT`
- `LOG0` - `LOG4`
- `SSTORE`
- `value`不为0的`CALL`

它从堆栈中弹出6个参数，依次为：

- `gas`：为这次调用分配的gas量。
- `to`：被调用合约的地址。
- `mem_in_start`：输入数据（calldata）在内存的起始位置。
- `mem_in_size`：输入数据的长度。
- `mem_out_start`：返回数据（returnData）在内存的起始位置。
- `mem_out_size`：返回数据的长度。

它的操作码为`0xFA`，gas消耗为：内存扩展成本+地址操作成本。

下面，我们在极简evm中实现`STATICCALL`指令。首先，我们需要检查子环境的代码是否包含`STATICCALL`不支持的指令：

```python
def is_state_changing_opcode(self, opcode): # 检查static call不能包含的opcodes
    state_changing_opcodes = [
        0xF0, # CREATE
        0xF5, # CREATE2
        0xFF, # SELFDESTRUCT
        0xA0, # LOG0
        0xA1, # LOG1
        0xA2, # LOG2
        0xA3, # LOG3
        0xA4, # LOG4
        0x55  # SSTORE
    ]
    return opcode in state_changing_opcodes
```



然后在`init()`函数中初始化一个`is_static`状态，当它为`true`时，意味着执行的是`STATICCALL`，需要检查不支持的指令：

```python
class EVM:
    def __init__(self, code, is_static=False):
        # ... 其他初始化 ...
        self.is_static = is_static

    def run(self):
        while self.pc < len(self.code) and self.success:
            op = self.next_instruction()

            if self.is_static and self.is_state_changing_opcode(op):
                self.success = False
                raise Exception("State changing operation detected during STATICCALL!")
```



此外，对于不为0的value的CALL，我们需要稍作修改：

```python
def call(self):

    if self.is_static and value != 0:
        self.success = False
        raise Exception("State changing operation detected during STATICCALL!")

    # ... 其他代码 ...
```



最后，我们可以加入`staticcall`函数：

```python
def staticcall(self):
    if len(self.stack) < 6:
        raise Exception('Stack underflow')
        
    gas = self.stack.pop()
    to_addr = self.stack.pop()
    mem_in_start = self.stack.pop()
    mem_in_size = self.stack.pop()
    mem_out_start = self.stack.pop()
    mem_out_size = self.stack.pop()
    
    # 拓展内存
    if len(self.memory) < mem_in_start + mem_in_size:
        self.memory.extend([0] * (mem_in_start + mem_in_size - len(self.memory)))

    # 从内存中获取输入数据
    data = self.memory[mem_in_start: mem_in_start + mem_in_size]

    account_target = account_db[hex(to_addr)]
    
    # 使用txn构建上下文
    ctx = Transaction(to=hex(to_addr), 
                        data=data,
                        value=0,
                        caller=self.txn.thisAddr, 
                        origin=self.txn.origin, 
                        thisAddr=hex(to_addr), 
                        gasPrice=self.txn.gasPrice, 
                        gasLimit=self.txn.gasLimit, 
                        )
    
    # 创建evm子环境
    evm_staticcall = EVM(account_target['code'], ctx, is_static=True)
    # 运行代码
    evm_staticcall.run()
    
    # 拓展内存
    if len(self.memory) < mem_out_start + mem_out_size:
        self.memory.extend([0] * (mem_out_start + mem_out_size - len(self.memory)))
    
    self.memory[mem_out_start: mem_out_start + mem_out_size] = evm_staticcall.returnData
    
    if evm_staticcall.success:
        self.stack.append(1)  
    else:
        self.stack.append(0)
```



## 测试

在测试中，我们会使用第一个地址（`0x9bbf`起始）调用第二个地址（`0x1000`起始），运行上面的代码（`PUSH1 0x42 PUSH1 0 MSTORE PUSH1 1 PUSH1 31 RETURN`），成功的话会返回`0x42`。

测试字节码为`6001601f5f5f731000000000000000000000000000000000000c425ffA5f51`（PUSH1 1 PUSH1 31 PUSH0 PUSH0 PUSH20 1000000000000000000000000000000000000c42 PUSH0 STATICCALL PUSH0 MLOAD），它会调用第二个地址上的代码，然后将内存中的返回值`0x42`压入堆栈。

```python
# Staticcall
code = b"\x60\x01\x60\x1f\x5f\x5f\x73\x10\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x0c\x42\x5f\xfA\x5f\x51"
evm = EVM(code, txn)
evm.run()
print(hex(evm.stack[-2]))
# output: 0x1 (success)
print(hex(evm.stack[-1]))
# output: 0x42
```



## 总结

这一讲，我们探讨了`STATICCALL`指令，它提供了一种安全的方法来执行其他合约的代码，而不修改合约状态，是Solidity中`pure`和`view`关键字的基础。目前，我们已经学习了144个操作码中的140个（97%）！

# 21. Create指令

这一讲，我们介绍EVM中的`CREATE`指令，它可以让合约创建新的合约。

## initcode 初始代码

之前我们提到过，以太坊有两种交易，一种是合约调用，而另一种是合约创建。在合约创建的交易中，`to`字段设为空，而`data`字段应填写为合约的初始代码（`initcode`）。`initcode`也是字节码，但它只在合约创建时执行一次，目的是为新合约设置必要的状态和返回最终的合约字节码（`contract code`）。

下面，我们看一个简单的`initcode`：`63ffffffff6000526004601cf3`。它的指令形式为：

```text
PUSH4 ffffffff   ; 将 4 字节的值 0xffffffff 推入堆栈
PUSH1   00       ; 将 1 字节的值 0x00 推入堆栈
MSTORE           ; 将堆栈顶部的值存储到内存中，地址为 0xffffffff，值为 0x00
PUSH1   04       ; 将 1 字节的值 0x04 推入堆栈
PUSH1   1c       ; 将 1 字节的值 0x1c 推入堆栈
RETURN           ; 返回内存中从地址 0x04 开始的 0x1c 字节

```



它先用`MSTORE`指令把`ffffffff`拷贝到内存中，然后用`RETURN`指令将它拷贝到返回数据中。这段`initcode`会把新合约的字节码设置为`ffffffff`(???)。

## CREATE

在EVM中，当一个合约想要创建一个新的合约时，会使用`CREATE`指令。它的简化流程：

1. 从堆栈中弹出`value`（向新合约发送的ETH）、`mem_offset`和`length`（新合约的`initcode`在内存中的初始位置和长度）。

2. 计算新合约的地址，计算方法为:

   ```python
   address = keccak256(rlp([sender_address,sender_nonce]))[12:]
   ```

   > [!TIP]
   >
   > 这段代码的作用是生成以太坊合约的地址。让我们逐步解析这段代码中的每个部分：
   >
   > ### 1. RLP 编码
   >
   > ```python
   > rlp([sender_address, sender_nonce])
   > ```
   >
   > - **RLP (Recursive Length Prefix)** 是以太坊用来对任意数量和类型的数据进行编码的方式。它允许以太坊在区块链上高效存储数据。
   > - 在这个例子中，`rlp([sender_address, sender_nonce])` 表示将发送者的地址和 nonce 编码成一个 RLP 数据结构。
   >   - `sender_address` 是合约创建者的地址，通常是一个 20 字节的十六进制字符串。
   >   - `sender_nonce` 是合约创建者的 nonce，通常是一个表示交易计数的数字，用于防止重放攻击。
   >
   > ### 2. 计算 Keccak-256 哈希值
   >
   > ```python
   > keccak256(rlp([sender_address, sender_nonce]))
   > ```
   >
   > - `keccak256` 是一种加密哈希函数，它会将输入数据转换成一个 32 字节（256 位）的哈希值。
   > - 在这里，它对经过 RLP 编码的数据进行哈希计算。这一步是为了生成一个唯一的哈希值，以便作为合约地址的基础。
   >
   > ### 3. 提取地址部分
   >
   > ```python
   > address = keccak256(...)[12:]
   > ```
   >
   > - 生成的 32 字节哈希值是一个字节序列，但以太坊合约地址只使用哈希值的后 20 字节（160 位）。
   > - 通过 `keccak256(...)[12:]`，我们从生成的哈希值中提取后 20 字节。因为 Python 的索引从 0 开始，所以 `[12:]` 表示从第 12 字节开始提取，直到最后。
   >
   > ### 总结
   >
   > 这段代码的整体作用是通过 RLP 编码发送者的地址和 nonce，然后对编码结果进行 Keccak-256 哈希计算，最后提取哈希值的后 20 字节以生成新的合约地址。这是以太坊合约地址生成的一种标准方式，确保地址的唯一性和安全性。

   

3. 更新ETH余额。

4. 初始化新的EVM上下文`evm_create`，用于执行`initcode`。

5. 在`evm_create`中执行`initcode`。

6. 如果执行成功，则更新创建的账户状态：更新`balance`，将`nonce`初始化为`0`，将`code`字段设为`evm_create`的返回数据，将`storage`字段设置为`evm_create`的`storage`。

7. 如果成功，则将新合约地址推入堆栈；若失败，将`0`推入堆栈。

下面，我们在极简EVM中实现`CREATE`指令：

```python
def create(self):
    if len(self.stack) < 3:
        raise Exception('Stack underflow')

    # 弹出堆栈数据
    value = self.stack.pop()
    mem_offset = self.stack.pop()
    length = self.stack.pop()

    # 扩展内存
    if len(self.memory) < mem_offset + length:
        self.memory.extend([0] * (mem_offset + length - len(self.memory)))

    # 获取初始化代码
    init_code = self.memory[mem_offset: mem_offset + length]

    # 检查创建者的余额是否足够
    creator_account = account_db[self.txn.thisAddr]
    if creator_account['balance'] < value:
        raise Exception('Insufficient balance to create contract!')

    # 为创建者扣除指定的金额
    creator_account['balance'] -= value

    # 生成新的合约地址（参考geth中的方式，使用创建者的地址和nonce）
    creator_nonce = creator_account['nonce']
    new_contract_address_bytes = sha3.keccak_256(self.txn.thisAddr.encode() + str(creator_nonce).encode()).digest()
    new_contract_address = '0x' + new_contract_address_bytes[-20:].hex()  # 取后20字节作为地址

    # 使用txn构建上下文
    ctx = Transaction(to=new_contract_address,
                        data=init_code,
                        value=value,
                        caller=self.txn.thisAddr,
                        origin=self.txn.origin,
                        thisAddr=new_contract_address,
                        gasPrice=self.txn.gasPrice,
                        gasLimit=self.txn.gasLimit)

    # 创建并运行新的EVM实例
    evm_create = EVM(init_code, ctx)
    evm_create.run()

    # 如果EVM实例返回错误，压入0，表示创建失败
    if evm_create.success == False:
        self.stack.append(0)
        return

    # 更新创建者的nonce
    creator_account['nonce'] += 1

    # 存储合约的状态
    account_db[new_contract_address] = {
        'balance': value,
        'nonce': 0,  # 新合约的nonce从0开始
        'storage': evm_create.storage,
        'code': evm_create.returnData
    }
    
    # 压入新创建的合约地址
    self.stack.append(int(new_contract_address, 16))
```

> [!NOTE]
>
> 这段代码是一个用于在以太坊虚拟机 (EVM) 中创建合约的实现。以下是对该代码的逐步分析：
>
> ### 代码分析
>
> 1. **堆栈检查**：
>    ```python
>    if len(self.stack) < 3:
>        raise Exception('Stack underflow')
>    ```
>    - 确保堆栈上有足够的元素（至少3个），否则抛出异常。
>
> 2. **弹出堆栈数据**：
>    ```python
>    value = self.stack.pop()
>    mem_offset = self.stack.pop()
>    length = self.stack.pop()
>    ```
>    - 从堆栈中弹出三个元素：
>      - `value`：创建合约时转账的金额。
>      - `mem_offset`：合约初始化代码在内存中的起始地址。
>      - `length`：初始化代码的长度。
>
> 3. **扩展内存**：
>    ```python
>    if len(self.memory) < mem_offset + length:
>        self.memory.extend([0] * (mem_offset + length - len(self.memory)))
>    ```
>    - 确保内存足够存放初始化代码。如果当前内存不足，则扩展内存。
>
> 4. **获取初始化代码**：
>    ```python
>    init_code = self.memory[mem_offset: mem_offset + length]
>    ```
>    - 从内存中获取初始化代码。
>
> 5. **检查余额**：
>    ```python
>    creator_account = account_db[self.txn.thisAddr]
>    if creator_account['balance'] < value:
>        raise Exception('Insufficient balance to create contract!')
>    ```
>    - 检查合约创建者的余额是否足够。如果余额不足，抛出异常。
>
> 6. **扣除金额**：
>    ```python
>    creator_account['balance'] -= value
>    ```
>    - 从创建者的账户中扣除指定的金额。
>
> 7. **生成合约地址**：
>    ```python
>    creator_nonce = creator_account['nonce']
>    new_contract_address_bytes = sha3.keccak_256(self.txn.thisAddr.encode() + str(creator_nonce).encode()).digest()
>    new_contract_address = '0x' + new_contract_address_bytes[-20:].hex()
>    ```
>    - 使用创建者的地址和nonce生成新的合约地址。这里使用了Keccak-256哈希函数并取最后20个字节作为合约地址。
>
> 8. **构建上下文并运行新的EVM实例**：
>    ```python
>    ctx = Transaction(to=new_contract_address,
>                        data=init_code,
>                        value=value,
>                        caller=self.txn.thisAddr,
>                        origin=self.txn.origin,
>                        thisAddr=new_contract_address,
>                        gasPrice=self.txn.gasPrice,
>                        gasLimit=self.txn.gasLimit)
>       
>    evm_create = EVM(init_code, ctx)
>    evm_create.run()
>    ```
>    - 创建一个新的`Transaction`上下文，指定合约地址、初始化代码等，然后创建并运行一个新的EVM实例。
>
> 9. **处理EVM运行结果**：
>    ```python
>    if evm_create.success == False:
>        self.stack.append(0)
>        return
>    ```
>    - 如果EVM运行失败，则在堆栈中压入0，表示合约创建失败。
>
> 10. **更新nonce并存储合约状态**：
>     ```python
>     creator_account['nonce'] += 1
>         
>     account_db[new_contract_address] = {
>         'balance': value,
>         'nonce': 0,
>         'storage': evm_create.storage,
>         'code': evm_create.returnData
>     }
>     ```
>     - 更新创建者的nonce，并将新合约的状态（余额、nonce、存储和代码）存储到数据库中。
>
> 11. **压入新创建的合约地址**：
>     ```python
>     self.stack.append(int(new_contract_address, 16))
>     ```
>     - 将新创建的合约地址压入堆栈中，以便后续使用。
>
> ### 总结
>
> - 这段代码的功能是创建一个新的以太坊合约。它从堆栈中获取相关信息，检查余额，生成合约地址，运行合约的初始化代码，并更新创建者和新合约的状态。
> - 在执行合约创建的过程中，还涉及到对内存的管理以及对账户余额的处理。



## 测试

1. 部署一个新合约，发送`9` wei，不部署任何代码：

   ```python
   # CREATE (empty code, 9 wei balance)
   code = b"\x5f\x5f\x60\x09\xf0"
   evm = EVM(code, txn)
   evm.run()
   print(hex(evm.stack[-1]))
   # output: 0x260144093a2920f68e1ae2e26b3bd15ddd610dfe
   print(account_db[hex(evm.stack[-1])])
   # output: {'balance': 9, 'nonce': 0, 'storage': {}, 'code': bytearray(b'')}
   ```

   

2. 部署一个新合约，代码设置为`ffffffff`:

   ```python
   # CREATE (with 4x FF)
   code = b"\x6c\x63\xff\xff\xff\xff\x60\x00\x52\x60\x04\x60\x1c\xf3\x60\x00\x52\x60\x0d\x60\x13\x60\x00\xf0"
   # PUSH13 0x63ffffffff6000526004601cf3 PUSH1 0x00 MSTORE PUSH1 0x0d PUSH1 0x19 PUSH1 0x00 CREATE
   evm = EVM(code, txn)
   evm.run()
   print(hex(evm.stack[-1]))
   # output: 0x6dddd3288a19f0bf4eee7bfb9e168ad29e1395d0
   print(account_db[hex(evm.stack[-1])])
   # {'balance': 0, 'nonce': 0, 'storage': {}, 'code': bytearray(b'\xff\xff\xff\xff')}
   ```

   

## 总结

这一讲，我们介绍了`EVM`中创建合约的指令`CREATE`，通过它，合约可以创造其他合约，从而实现更为复杂的逻辑和功能。我们已经学习了144个操作码中的141个（98%）！

# 22. Create2指令

上一讲我们介绍了`CREATE`指令，使合约有能力创建其他合约。这一讲，我们将进一步探讨`CREATE2`指令，它提供了一种新的方式来确定新合约的地址。

## CREATE vs CREATE2

传统的`CREATE`指令通过调用者的地址和nonce来确定新合约的地址，而`CREATE2`则提供了一种新的计算方法，使我们可以在合约部署之前预知它的地址。

与`CREATE`不同，`CREATE2`使用调用者地址、盐（一个自定义的256位的值）以及`initcode`的哈希来确定新合约的地址，计算方法如下：

```python
address = keccak256( 0xff + sender_address + salt + keccak256(init_code))[12:]
```

> [!TIP]
>
> 这段代码是用来生成以太坊合约地址的另一种方式，涉及到合约的创建。让我们逐步解析这段代码的每个部分：
>
> ### 1. 组成输入数据
>
> ```python
> 0xff + sender_address + salt + keccak256(init_code)
> ```
>
> - **`0xff`**: 这是一个字节，通常用作合约地址生成过程中的前缀，表明这是一个由合约创建的地址。
>   
> - **`sender_address`**: 这是合约创建者的地址（20 字节）。它通常是一个 20 字节的十六进制字符串，代表发起创建合约的账户。
>
> - **`salt`**: 这是一个可选的字节序列，用于在合约创建时提供额外的随机性。可以理解为一个随机数或唯一标识符，避免相同输入数据生成相同的合约地址。可以是一个任意的字节串。
>
> - **`keccak256(init_code)`**: 这是合约的初始化代码的 Keccak-256 哈希值。`init_code` 通常是合约的字节码，生成的哈希值是 32 字节的。
>
> ### 2. 计算 Keccak-256 哈希值
>
> ```python
> keccak256(0xff + sender_address + salt + keccak256(init_code))
> ```
>
> - 在这一部分，首先将 `0xff`、`sender_address`、`salt` 和 `keccak256(init_code)` 连接成一个字节串。
> - 然后，对这个字节串进行 Keccak-256 哈希计算。这会生成一个 32 字节的哈希值。
>
> ### 3. 提取地址部分
>
> ```python
> address = keccak256(...)[12:]
> ```
>
> - 通过 `keccak256(...)[12:]`，我们从生成的哈希值中提取后 20 字节。这是以太坊合约地址的标准格式（160 位）。
>

这样的好处是，只要你知道`initcode`，盐值和发送者的地址，就可以预先知道新合约的地址，而不需要现在部署它。而`CREATE`计算的地址取决于部署账户的`nonce`，也就是说，在`nonce`不确定的情况下（合约还未部署，nonce可能会增加），没法确定新合约的地址。

对`CREATE2`的更多介绍可以参考[WTF Solidity教程第25讲](https://github.com/AmazingAng/WTF-Solidity/blob/main/25_Create2/readme.md)。

## CREATE2

在EVM中，`CREATE2`指令的简化流程如下：

1. 从堆栈中弹出`value`（向新合约发送的ETH）、`mem_offset`、`length`（新合约的`initcode`在内存中的初始位置和长度）以及`salt`。
2. 使用上面的公式计算新合约的地址。
3. 之后的步骤同`CREATE`指令：初始化新的EVM上下文、执行`initcode`、更新创建的账户状态、返回新合约地址或`0`（如果失败）。

下面，我们在极简EVM中实现`CREATE2`指令：

```python
def create2(self):
    if len(self.stack) < 4:
        raise Exception('Stack underflow')

    value = self.stack.pop()
    mem_offset = self.stack.pop()
    length = self.stack.pop()
    salt = self.stack.pop()

    # 扩展内存
    if len(self.memory) < mem_offset + length:
        self.memory.extend([0] * (mem_offset + length - len(self.memory)))

    # 获取初始化代码
    init_code = self.memory[mem_offset: mem_offset + length]

    # 检查创建者的余额是否足够
    creator_account = account_db[self.txn.thisAddr]
    if creator_account['balance'] < value:
        raise Exception('Insufficient balance to create contract!')

    # 为创建者扣除指定的金额
    creator_account['balance'] -= value

    # 生成新的合约地址（参考geth中的方式，使用盐和initcode的hash）
    init_code_hash = sha3.keccak_256(init_code).digest()
    data_to_hash = b'\xff' + self.txn.thisAddr.encode() + str(salt).encode() + init_code_hash
    new_contract_address_bytes = sha3.keccak_256(data_to_hash).digest()
    new_contract_address = '0x' + new_contract_address_bytes[-20:].hex()  # 取后20字节作为地址

    # 使用txn构建上下文并执行
    ctx = Transaction(to=new_contract_address,
                        data=init_code,
                        value=value,
                        caller=self.txn.thisAddr,
                        origin=self.txn.origin,
                        thisAddr=new_contract_address,
                        gasPrice=self.txn.gasPrice,
                        gasLimit=self.txn.gasLimit)
    evm_create2 = EVM(init_code, ctx)
    evm_create2.run()

    # 如果EVM实例返回错误，压入0，表示创建失败
    if evm_create2.success == False:
        self.stack.append(0)
        return

    # 更新创建者的nonce
    creator_account['nonce'] += 1

    # 存储合约的状态
    account_db[new_contract_address] = {
        'balance': value,
        'nonce': 0,
        'storage': evm_create2.storage,
        'code': evm_create2.returnData
    }

    # 压入新创建的合约地址
    self.stack.append(int(new_contract_address, 16))
```

> [!NOTE]
>
> 你的 `create2` 函数实现了以太坊的 `CREATE2` 操作码，允许用户在创建合约时指定一个盐值，从而使合约地址可以在合约部署之前就可预测。以下是对函数的详细解释：
>
> 1. **参数检查**：
>    ```python
>    if len(self.stack) < 4:
>        raise Exception('Stack underflow')
>    ```
>    检查堆栈中是否有足够的参数（至少 4 个）。这些参数分别是创建合约所需的 `value`、`mem_offset`、`length` 和 `salt`。
>
> 2. **弹出参数**：
>    ```python
>    value = self.stack.pop()
>    mem_offset = self.stack.pop()
>    length = self.stack.pop()
>    salt = self.stack.pop()
>    ```
>    从堆栈中获取创建合约所需的参数。
>
> 3. **扩展内存**：
>    ```python
>    if len(self.memory) < mem_offset + length:
>        self.memory.extend([0] * (mem_offset + length - len(self.memory)))
>    ```
>    确保内存足够大以存储初始化代码。
>
> 4. **获取初始化代码**：
>    ```python
>    init_code = self.memory[mem_offset: mem_offset + length]
>    ```
>
> 5. **检查余额**：
>    ```python
>    creator_account = account_db[self.txn.thisAddr]
>    if creator_account['balance'] < value:
>        raise Exception('Insufficient balance to create contract!')
>    ```
>    确保创建合约的账户有足够的余额。
>
> 6. **扣除余额**：
>    ```python
>    creator_account['balance'] -= value
>    ```
>
> 7. **生成新合约地址**：
>    ```python
>    init_code_hash = sha3.keccak_256(init_code).digest()
>    data_to_hash = b'\xff' + self.txn.thisAddr.encode() + str(salt).encode() + init_code_hash
>    new_contract_address_bytes = sha3.keccak_256(data_to_hash).digest()
>    new_contract_address = '0x' + new_contract_address_bytes[-20:].hex()  # 取后20字节作为地址
>    ```
>    - 使用 `keccak256` 哈希函数计算初始化代码的哈希值。
>    - 根据 `0xff`、发送者地址、盐值和初始化代码的哈希生成新的合约地址。
>
> 8. **创建并执行新的 EVM 实例**：
>    ```python
>    ctx = Transaction(to=new_contract_address,
>                      data=init_code,
>                      value=value,
>                      caller=self.txn.thisAddr,
>                      origin=self.txn.origin,
>                      thisAddr=new_contract_address,
>                      gasPrice=self.txn.gasPrice,
>                      gasLimit=self.txn.gasLimit)
>    evm_create2 = EVM(init_code, ctx)
>    evm_create2.run()
>    ```
>
> 9. **处理 EVM 执行结果**：
>    ```python
>    if evm_create2.success == False:
>        self.stack.append(0)
>        return
>    ```
>
> 10. **更新创建者的 nonce**：
>     ```python
>     creator_account['nonce'] += 1
>     ```
>
> 11. **存储合约状态**：
>     ```python
>     account_db[new_contract_address] = {
>         'balance': value,
>         'nonce': 0,
>         'storage': evm_create2.storage,
>         'code': evm_create2.returnData
>     }
>     ```
>
> 12. **压入新合约地址**：
>     ```python
>     self.stack.append(int(new_contract_address, 16))
>     ```
>
> ### 总结
> - `CREATE2` 允许在合约部署之前根据初始化代码和盐值预测新合约的地址，这样可以在合约创建的逻辑中进行更多的灵活性和安全性。
> - 该函数实现了合约的创建流程，包含对账户余额的检查、内存管理、合约地址计算及状态存储等步骤。



## 测试

1. 使用`CREATE2`指令部署一个新合约，发送`9` wei，但不部署任何代码：

   ```python
   # CREATE2 (empty code, 9 wei balance)
   code = b"\x5f\x5f\x5f\x60\x09\xf5"
   # PUSH0 PUSH0 PUSH0 PUSH1 0x09 CREATE2
   evm = EVM(code, txn)
   evm.run()
   print(hex(evm.stack[-1]))
   # output: 0x260144093a2920f68e1ae2e26b3bd15ddd610dfe
   print(account_db[hex(evm.stack[-1])])
   # output: {'balance': 9, 'nonce': 0, 'storage': {}, 'code': bytearray(b'')}
   ```

   

2. 使用`CREATE2`指令部署一个新合约，并将代码设置为`ffffffff`:

   ```python
   # CREATE2 (with 4x FF)
   code = b"\x6c\x63\xff\xff\xff\xff\x60\x00\x52\x60\x04\x60\x1c\xf3\x60\x00\x52\x60\x00\x60\x0d\x60\x13\x60\x00\xf5"
   # PUSH13 0x63ffffffff6000526004601cf3 PUSH1 0x00 MSTORE PUSH1 0x00 PUSH1 0x0d PUSH1 0x13 PUSH1 0x00 CREATE2
   evm = EVM(code, txn)
   evm.run()
   print(hex(evm.stack[-1]))
   # output: 0x6dddd3288a19f0bf4eee7bfb9e168ad29e1395d0
   print(account_db[hex(evm.stack[-1])])
   # {'balance': 0, 'nonce': 0, 'storage': {}, 'code': bytearray(b'\xff\xff\xff\xff')}
   ```

   

## 总结

这一讲，我们介绍了`EVM`中创建合约的另一个指令，`CREATE2`，通过它，合约不仅可以创造其他合约，而且可以预知新合约的地址。`Uniswap v2`中的LP地址就是用这个方法计算的。现在，我们已经学习了144个操作码中的142个（98.6%）！

# 23. Selfdestruct指令

这一讲，我们介绍EVM中的`SELFDESTRUCT`指令，它可以让合约自毁。这个指令可能在未来会被弃用，见[EIP-4758](https://eips.ethereum.org/EIPS/eip-4758)和[EIP-6049](https://eips.ethereum.org/EIPS/eip-6049)。

## 基本概念

EVM中的`SELFDESTRUCT`指令可以让合约自行销毁，并将账户中的ETH余额发送到指定地址。这个指令一些特殊的地方：

1. 使用`SELFDESTRUCT`指令时，当前合约会被标记为待销毁。但实际的销毁操作会在整个交易完成后进行。
2. 合约的`ETH`余额会被发送到指定的地址，并且这一过程保证会成功的。
3. 如果指定的地址是一个合约，那么该合约的代码不会被执行，即不会像平常的`ETH`转账执行目标地址的`fallback`方法。
4. 如果指定的地址不存在，则会为其创建一个新的账户，并存储这些ETH。
5. 一旦合约被销毁，其代码和数据都会永久地从链上删除，无法恢复。销毁合约可能会影响到与它互动的其他合约或服务。

`SELFDESTRUCT`指令的工作流程如下：

1. 从堆栈中弹出接收`ETH`的指定地址。
2. 将当前合约的余额转移到指定地址。
3. 销毁合约。

下面，我们在极简EVM中实现`SELFDESTRUCT`指令：

```python
def selfdestruct(self):
    if len(self.stack) < 1:
        raise Exception('Stack underflow')

    # 弹出接收ETH的指定地址
    raw_recipient = self.stack.pop()
    recipient = '0x' + format(raw_recipient, '040x')  # 转化为0x前缀的40个十六进制字符

    # 如果地址不存在，则创建它
    if recipient not in account_db:
        account_db[recipient] = {'balance': 0, 'nonce': 0, 'storage': {}, 'code': bytearray(b'')}

    # 将合约的余额转移到接收者账户
    account_db[recipient]['balance'] += account_db[self.txn.thisAddr]['balance']

    # 从数据库中删除合约
    del account_db[self.txn.thisAddr]
```

> [!TIP]
>
> 你的 `selfdestruct` 函数实现了以太坊中的 `SELFDESTRUCT` 操作码，允许合约将其余额发送到指定的地址并从区块链上删除自己。以下是对函数的逐步解释：
>
> 1. **参数检查**：
>    ```python
>    if len(self.stack) < 1:
>        raise Exception('Stack underflow')
>    ```
>    这里检查堆栈中是否有足够的参数（至少一个）。这个参数是接收 ETH 的地址。
>
> 2. **弹出接收地址**：
>    ```python
>    raw_recipient = self.stack.pop()
>    recipient = '0x' + format(raw_recipient, '040x')  # 转化为0x前缀的40个十六进制字符
>    ```
>    从堆栈中弹出地址，并将其格式化为以 `0x` 开头的 40 个十六进制字符（即以太坊地址的标准格式）。
>
> 3. **检查接收地址是否存在**：
>    ```python
>    if recipient not in account_db:
>        account_db[recipient] = {'balance': 0, 'nonce': 0, 'storage': {}, 'code': bytearray(b'')}
>    ```
>    如果接收地址不存在于账户数据库中，则创建一个新的账户，初始化其余额为 0、nonce 为 0、存储为空字典，代码为空字节数组。
>
> 4. **转移余额**：
>    ```python
>    account_db[recipient]['balance'] += account_db[self.txn.thisAddr]['balance']
>    ```
>    将合约当前的余额转移到接收地址的账户中。
>
> 5. **删除合约**：
>    ```python
>    del account_db[self.txn.thisAddr]
>    ```
>    从账户数据库中删除当前合约的记录，意味着合约被销毁。
>
> ### 总结
> - `SELFDESTRUCT` 指令用于合约自我销毁，并将其余额转移到指定地址。
> - 该函数实现了这一操作的主要逻辑，包括参数的处理、账户的创建和余额的转移。
> - 通过这种方式，合约可以在不再需要时主动释放其占用的资金，并清理状态。



## 测试

1. 自毁当前合约，并将余额转移到新地址。

```python
# Define Txn
addr = '0x1000000000000000000000000000000000000c42'
txn = Transaction(to=None, value=10, 
                  caller=addr, origin=addr, thisAddr=addr)

# SELFDESTRUCT 
# delete account: 0x1000000000000000000000000000000000000c42
print("自毁前: ", account_db)
# 自毁前:  {'0x9bbfed6889322e016e0a02ee459d306fc19545d8': {'balance': 100, 'nonce': 1, 'storage': {}, 'code': b''}, '0x1000000000000000000000000000000000000c42': {'balance': 10, 'nonce': 0, 'storage': {}, 'code': b'`B`\x00R`\x01`\x1f\xf3'}}

code = b"\x60\x20\xff"  # PUSH1 0x20 (destination address) SELFDESTRUCT
evm = EVM(code, txn)
evm.run()
print("自毁后: ", account_db)
# 自毁后:  {'0x9bbfed6889322e016e0a02ee459d306fc19545d8': {'balance': 100, 'nonce': 1, 'storage': {}, 'code': b''}, '0x0000000000000000000000000000000000000020': {'balance': 10, 'nonce': 0, 'storage': {}, 'code': bytearray(b'')}}
```



## 总结

这一讲，我们介绍了EVM中销毁合约的`SELFDESTRUCT`指令，它可以自毁合约并且将其剩余的`ETH`强行发送到另一个地址。该指令将会在未来被弃用，大家尽量不要使用。现在，我们已经学习了144个操作码中的143个（99%），仅剩一个了！

#  24. Gas指令

这一讲，我们介绍EVM中的`GAS`指令，并介绍以太坊的Gas机制。

## 什么是Gas

在EVM中，交易和执行智能合约需要消耗计算资源。为了防止用户恶意的滥用网络资源和补偿验证者所消耗的计算能源，以太坊引入了一种称为Gas的计费机制，使每一笔交易都有一个关联的成本。

在发起交易时，用户设定一个最大Gas数量（`gasLimit`）和每单位Gas的价格（`gasPrice`）。如果交易执行超出了`gasLimit`，交易会回滚，但已消耗的Gas不会退还。

## Gas规则

以太坊上的Gas用`gwei`衡量，它是`ETH`的子单位，`1 ETH = 10^9 gwei`。一笔交易的Gas成本等于每单位gas价格乘以交易的gas消耗，即`gasPrice * gasUsed`。gas价格会随着时间的推移而变化，具体取决于当前对区块空间的需求。gas消耗由很多因素决定，并且每个以太坊版本都会有所改动，下面总结下：

1. `calldata`大小：`calldata`中的每个字节都需要花费gas，交易数据的大小越大，gas消耗就越高。`calldata`每个零字节花费`4` Gas，每个非零字节花费`16` Gas（伊斯坦布尔硬分叉之前为 64 个）。
2. 内在gas：每笔交易的内在成本为21000 Gas。除了交易成本之外，创建合约还需要 32000 Gas。该成本是在任何操作码执行之前从交易中支付的。
3. `opcode`固定成本：每个操作码在执行时都有固定的成本，以Gas为单位。对于所有执行，该成本都是相同的。比如每个`ADD`指令消耗`3` Gas。
4. `opcode`动态成本：一些指令消耗更多的计算资源取决于其参数。因此，除了固定成本之外，这些指令还具有动态成本。比如`SHA3`指令消耗的Gas随参数长度增长。
5. 内存拓展成本：在EVM中，合约可以使用操作码访问内存。当首次访问特定偏移量的内存（读取或写入）时，内存可能会触发扩展，产生gas消耗。比如`MLOAD`或`RETURN`。
6. 访问集成本：对于每个外部交易，EVM会定义一个访问集，记录交易过程中访问过的合约地址和存储槽（slot）。访问成本根据数据是否已经被访问过（热）或是首次被访问（冷）而有所不同。
7. Gas退款：`SSTORE`的一些操作（比如清除存储）可以触发Gas退款。退款会在交易结束时执行，上限为总Gas消耗的20%（从伦敦硬分叉开始）。

更详细的Gas消耗信息可以参考[evm.codes](https://www.evm.codes/)。

## GAS指令

EVM中的`GAS`指令会将当前交易的剩余`Gas`压入堆栈。它的操作码为`0x5A`，gas消耗为`2`。

```python
def gas(self):
    self.stack.append(self.txn.gasLimit - self.gasUsed)
```



下面，我们在极简EVM中实现`GAS`。出于教学目的，目前我们仅实现部分`opcode`的固定成本，其他的未来实现。

首先，我们需要在`EVM`中添加一个`gasUsed`属性，用于记录已经消耗的Gas：

```python
class EVM:
    def __init__(self, ...):
        # ... 其他属性 ...
        self.gasUsed = 0
```



接下来，我们需要定义每个指令的固定成本：

```python
# 固定成本
GAS_COSTS = {
    'PUSH': 3,
    'POP': 2,
    'ADD': 3,
    'MUL': 5,
    'SUB': 3,
    # ... 其他操作码的固定成本 ...
}
```



在每一个操作码的实现中更新Gas消耗，比如`PUSH`指令：

```python
def push(self, size):
    data = self.code[self.pc:self.pc + size] # 按照size从code中获取数据
    value = int.from_bytes(data, 'big') # 将bytes转换为int
    self.stack.append(value) # 压入堆栈
    self.pc += size # pc增加size单位
    self.gasUsed += GAS_COSTS['PUSH'] # 更新Gas消耗
```



最后，在每个操作码执行后检查Gas是否被耗尽：

```python
def run(self):
    while self.pc < len(self.code) and self.success:
        op = self.next_instruction()
        # ... opcode执行逻辑 ...

        # 检查gas是否耗尽
        if self.gasUsed > self.txn.gasLimit:
            raise Exception('Out of gas!')
```



## 测试

```python
# Define Txn
addr = '0x1000000000000000000000000000000000000c42'
txn = Transaction(to=None, value=10, data='', 
                  caller=addr, origin=addr, thisAddr=addr, gasLimit=100, gasPrice=1)

# GAS 
code = b"\x60\x20\x5a"  # PUSH1 0x20 GAS
evm = EVM(code, txn)
evm.run()
print(evm.stack)
# output: [32, 97] 
# gasLimit=100，gasUsed=3
```

> [!TIP]
>
> 在这段代码中，首先定义了一个交易对象 `txn`，然后创建一个 EVM 实例并运行指定的字节码。下面是对每个步骤的详细解释：
>
> ### 1. 定义交易 (`Transaction`)
> ```python
> addr = '0x1000000000000000000000000000000000000c42'
> txn = Transaction(to=None, value=10, data='', 
>                   caller=addr, origin=addr, thisAddr=addr, gasLimit=100, gasPrice=1)
> ```
> - **`addr`**: 定义一个地址 `addr`，作为交易的调用者 (`caller`)、原始发起者 (`origin`) 和合约的地址 (`thisAddr`)。
> - **`txn`**: 创建一个 `Transaction` 对象，设置其 `to` 地址为 `None`（意味着没有目标地址）、转账的 `value` 为 10、`data` 为空字符串，同时指定 `gasLimit` 为 100 和 `gasPrice` 为 1。
>
> ### 2. 定义字节码
> ```python
> code = b"\x60\x20\x5a"  # PUSH1 0x20 GAS
> ```
> - 这段字节码包含三条指令：
>   - **`PUSH1 0x20`** (`\x60\x20`): 将值 `32`（即 `0x20` 的十进制值）推入堆栈。
>   - **`GAS`** (`\x5a`): 将剩余的可用气体（gas）数量推入堆栈。
>
> ### 3. 创建 EVM 实例并运行
> ```python
> evm = EVM(code, txn)
> evm.run()
> ```
> - 创建一个 EVM 实例，传入字节码和交易对象 `txn`。
> - 调用 `run` 方法执行 EVM。
>
> ### 4. 打印堆栈内容
> ```python
> print(evm.stack)
> ```
> - 输出堆栈的当前内容。
>
> ### 5. 输出分析
> - 在运行后，输出为 `[32, 97]`，表示：
>   - **`32`**: 这是 `PUSH1 0x20` 指令将值 `32` 推入堆栈的结果。
>   - **`97`**: 这是 `GAS` 指令推入的剩余气体数量，计算方法为 `gasLimit - gasUsed`。在这里，`gasUsed` 是 `3`（字节码的开销），因此剩余的气体为 `100 - 3 = 97`。
>
> ### 6. 结论
> - 通过这段代码，我们可以看到如何在 EVM 中使用字节码指令来操作堆栈和获取当前的气体信息。整个过程表明，EVM 能够成功执行给定的字节码，并维护堆栈的状态。



## 总结

这一讲，我们介绍了以太坊的Gas机制以及`GAS`操作码。Gas机制确保了以太坊网络的计算资源不被恶意代码滥用。通过`GAS`指令，智能合约可以实时地查询还剩下多少Gas，从而做出相应的决策。

至此，EVM中的144个操作码我们全部学习完了！相信你对EVM的理解一定有了质的飞跃，恭喜你！

#  25. 优化最小代理合约

这一讲，我们将综合应用之前所学的内容，用`PUSH0`指令优化[EIP-1167](https://eips.ethereum.org/EIPS/eip-1167)最小代理合约（Minimal Proxy Contract），减少合约长度并降低gas。



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410050940128.gif)



## 最小代理合约

当人们需要反复部署同一个合约时，比如每个用户都需要部署一遍抽象账户合约，[代理合约](https://github.com/AmazingAng/WTF-Solidity/tree/main/46_ProxyContract)是最好的解决办法。在这个模式下，复杂的逻辑合约可以被重复利用，用户只需要部署一个简单的代理合约，从而降低gas成本。



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410050940217.png)



由于代理合约会被用户重复部署，因此我们必须要优化它。在[WTF Solidity教程第46讲](https://github.com/AmazingAng/WTF-Solidity/tree/main/46_ProxyContract)我们用Solidity写了一个代理合约，在没有经过任何优化的情况下，它的合约`bytecode`有`573`字节。

```solidity
// SPDX-License-Identifier: MIT
// wtf.academy
pragma solidity ^0.8.4;

/**
 * @dev Proxy合约的所有调用都通过`delegatecall`操作码委托给另一个合约执行。后者被称为逻辑合约（Implementation）。
 *
 * 委托调用的返回值，会直接返回给Proxy的调用者
 */
contract Proxy {
    address public implementation; // 逻辑合约地址。implementation合约同一个位置的状态变量类型必须和Proxy合约的相同，不然会报错。

    /**
     * @dev 初始化逻辑合约地址
     */
    constructor(address implementation_){
        implementation = implementation_;
    }

    /**
     * @dev 回调函数，调用`_delegate()`函数将本合约的调用委托给 `implementation` 合约
     */
    fallback() external payable {
        _delegate();
    }

    /**
     * @dev 将调用委托给逻辑合约运行
     */
    function _delegate() internal {
        assembly {
            //  msg.data. We take full control of memory in this inline assembly
            // block because it will not return to Solidity code. We overwrite the
            // 读取位置为0的storage，也就是implementation地址。
            let _implementation := sload(0)

            calldata(0, 0, calldatasize())

            // 利用delegatecall调用implementation合约
            // delegatecall操作码的参数分别为：gas, 目标合约地址，input mem起始位置，input mem长度，output area mem起始位置，output area mem长度
            // output area起始位置和长度位置，所以设为0
            // delegatecall成功返回1，失败返回0
            let result := delegatecall(gas(), _implementation, 0, calldatasize(), 0, 0)

            // 将起始位置为0，长度为returndatasize()的returndata复制到mem位置0
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
}
```

> [!TIP]
>
> 这段 Solidity 代码定义了一个代理合约（Proxy），利用 `delegatecall` 操作码将调用委托给另一个合约（逻辑合约），即实现合约。以下是对代码的逐行解析：
>
> ### 1. 合约声明与导入
> ```solidity
> // SPDX-License-Identifier: MIT
> // wtf.academy
> pragma solidity ^0.8.4;
> ```
> - 这部分包含合约的许可证声明和 Solidity 版本。
>
> ### 2. Proxy 合约定义
> ```solidity
> contract Proxy {
>     address public implementation;
> ```
> - `Proxy` 合约声明，包含一个 `implementation` 状态变量，用于存储逻辑合约的地址。
>
> ### 3. 构造函数
> ```solidity
>     constructor(address implementation_){
>         implementation = implementation_;
>     }
> ```
> - 构造函数用于初始化 `implementation` 地址。合约部署时将逻辑合约的地址传递给构造函数。
>
> ### 4. 回调函数
> ```solidity
>     fallback() external payable {
>         _delegate();
>     }
> ```
> - `fallback` 函数在合约接收到调用时触发。它是一个默认的回调函数，当没有匹配的函数被调用时执行。此处，它调用 `_delegate()` 函数，将调用转发给逻辑合约。
>
> ### 5. 委托调用实现
> ```solidity
>     function _delegate() internal {
>         assembly {
>             let _implementation := sload(0)
> 
>             calldata(0, 0, calldatasize())
> ```
> - `_delegate` 函数使用内联汇编实现委托调用。首先，通过 `sload(0)` 加载 `implementation` 的地址（在代理合约的存储位置 0）。
> - `calldata(0, 0, calldatasize())` 将当前调用的输入数据（calldata）从位置 0 复制到内存。
>
> ### 6. delegatecall 调用
> ```solidity
>             let result := delegatecall(gas(), _implementation, 0, calldatasize(), 0, 0)
> ```
> - 使用 `delegatecall` 将调用委托给逻辑合约。参数包括：
>   - `gas()`: 发送给逻辑合约的剩余气体。
>   - `_implementation`: 目标逻辑合约的地址。
>   - `0`: 输入数据的起始内存位置。
>   - `calldatasize()`: 输入数据的长度。
>   - `0, 0`: 输出数据的内存位置和长度（0 表示不保存输出数据）。
> - `delegatecall` 返回值 `result`，指示调用是否成功。
>
> ### 7. 处理返回数据
> ```solidity
>             returndata(0, 0, returndatasize())
> 
>             switch result
>             case 0 {
>                 revert(0, returndatasize())
>             }
>             default {
>                 return(0, returndatasize())
>             }
>         }
>     }
> }
> ```
> - `returndata(0, 0, returndatasize())` 将返回数据复制到内存。
> - `switch` 语句根据 `result` 的值处理返回：
>   - 如果 `result` 为 0（调用失败），则使用 `revert()` 抛出错误，并返回相应的数据。
>   - 如果调用成功，则返回输出数据。
>
> ### 总结
> - 这个 `Proxy` 合约通过 `delegatecall` 实现了对逻辑合约的委托调用，使得逻辑合约的状态可以在代理合约的上下文中执行。这样，任何对代理合约的调用都将转发到指定的逻辑合约，且返回结果直接返回给调用者。
> - 代理合约的设计使得合约逻辑可以独立于存储，便于升级和维护，而不需要改变合约的地址或状态。

那么经过优化后的代理合约有多大呢？`EIP-1677`提出了最小代理合约，完全用字节码写成，合约长度仅有`55`字节，能节省超过90%的gas！😱，手撸字节码就是这么强大。

```text
363d3d373d3d3d363d73bebebebebebebebebebebebebebebebebebebebe5af43d82803e903d91602b57fd5bf3
```



我第一次见到这一串字节码就像见到了天书，不知所措，相信现在的你也能感同身受。但是，在我们学习完之前的章节之后，不单要看懂它，还要优化它！优化后的代理合约：

1. 使用了Shanghai升级后引入的新opcode：`PUSH0`。
2. 合约仅需`54`字节，部署时节省`200` gas，运行时节省`5` gas。

我们基于优化后的代理合约，提出一个新的[EIP-7511](https://eips.ethereum.org/EIPS/eip-7511): 使用`PUSH0`的最小代理合约。

## 从头搭建最小代理合约

代理合约中最重要的操作码是什么？对，是[DELEGATECALL](https://www.wtf.academy/docs/evm-opcodes-102/DelegatecallOp/)，它可以将用户对代理合约的调用委托给逻辑合约。



![img](https://www.wtf.academy/assets/images/25-3-f49e18de33692532b7b8aed640212fe3.png)



因此，最小代理合约的核心元素包括：

1. 使用`CALLDATA`复制交易的calldata。
2. 使用`DELEGATECALL`将calldata转发到逻辑合约。
3. 将`DELEGATECALL`返回的数据复制到内存。
4. 根据`DELEGATECALL`是否成功来返回结果或回滚交易。

### 第一步：复制Calldata

为了复制calldata，我们需要为`CALLDATA`操作码提供参数，这些参数是`[0, 0, cds]`，其中`cds`代表calldata的大小。

| pc   | op   | opcode       | stack   |
| ---- | ---- | ------------ | ------- |
| [00] | 36   | CALLDATASIZE | cds     |
| [01] | 5f   | PUSH0        | 0 cds   |
| [02] | 5f   | PUSH0        | 0 0 cds |
| [03] | 37   | CALLDATA     |         |

> [!TIP]
>
> CALLDATA将`data`中的数据复制到内存中。它会从堆栈中弹出3个参数(mem_offset, calldata_offset, length)，分别对应写到内存的偏移量，读取calldata的偏移量和长度。

### 第二步：Delegatecall

为了将calldata转发到委托调用，我们要在堆栈中准备`DELEGATECALL`操作码所需的参数，这些参数分别是`[gas 0xbebe. 0 cds 0 0]`，其中`gas`代表剩余的gas，`0xbebe.`代表逻辑合约的地址（20字节，实际使用时需要替换成你的逻辑合约地址），`suc`代表delegatecall是否成功。

| pc   | op      | opcode         | stack                 |
| ---- | ------- | -------------- | --------------------- |
| [04] | 5f      | PUSH0          | 0                     |
| [05] | 5f      | PUSH0          | 0 0                   |
| [06] | 36      | CALLDATASIZE   | cds 0 0               |
| [07] | 5f      | PUSH0          | 0 cds 0 0             |
| [08] | 73bebe. | PUSH20 0xbebe. | 0xbebe. 0 cds 0 0     |
| [1d] | 5a      | GAS            | gas 0xbebe. 0 cds 0 0 |
| [1e] | f4      | DELEGATECALL   | suc                   |

> [!TIP]
>
> DELEGATECALL从堆栈中弹出6个参数，与`CALL`不同，它不包括`value`，因为ETH不会被发送：
>
> - `gas`：为这次调用分配的gas量。
> - `to`：被调用合约的地址。
> - `mem_in_start`：输入数据（calldata）在内存的起始位置。
> - `mem_in_size`：输入数据的长度。
> - `mem_out_start`：返回数据（returnData）在内存的起始位置。
> - `mem_out_size`：返回数据的长度。



### 第三步：将`DELEGATECALL`返回的数据复制到内存

进行完`DELEGATECALL`之后，我们就可以处理返回的数据了。这一步，我们要使用``RETURNDATA`操作码将返回的数据复制到内存，它的参数是`[0, 0, rds]`，其中`rds`代表从`DELEGATECALL`返回的数据长度。

| pc   | op   | opcode         | stack       |
| ---- | ---- | -------------- | ----------- |
| [1f] | 3d   | RETURNDATASIZE | rds suc     |
| [20] | 5f   | PUSH0          | 0 rds suc   |
| [21] | 5f   | PUSH0          | 0 0 rds suc |
| [22] | 3e   | RETURNDATA     | suc         |

> [!TIP]
>
> RETURNDATA将`returnData`中的某段数据复制到内存中。此指令需要从堆栈中取出三个参数：内存的起始位置`mem_offset`，返回数据的起始位置`return_offset`，和数据的长度`length`。



### 第四步：返回数据或回滚交易

最后，我们需要根据`DELEGATECALL`是否成功（`suc`）选择返回数据或回滚交易。因为EVM操作码中没有`if/else`，我们需要使用`JUMPI`和`JUMPDEST`。`JUMPI`的参数是`[0x2a, suc]`，其中`0x2a`是条件跳转的目的地。

我们还需要在`JUMPI`之前为`REVERT`和`RETURN`操作码准备参数`[0, rds]`，否则我们就要在返回/回滚条件下重复准备两次。另外，我们不能避免使用`SWAP`操作交换`rds`和`suc`在堆栈中的位置，因为我们只能在`DELEGATECALL`之后获得返回数据的长度`rds`。

| pc   | op   | opcode         | stack          |
| ---- | ---- | -------------- | -------------- |
| [23] | 5f   | PUSH0          | 0 suc          |
| [24] | 3d   | RETURNDATASIZE | rds 0 suc      |
| [25] | 91   | SWAP2          | suc 0 rds      |
| [26] | 602a | PUSH1 0x2a     | 0x2a suc 0 rds |
| [27] | 57   | JUMPI          | 0 rds          |
| [29] | fd   | REVERT         |                |
| [2a] | 5b   | JUMPDEST       | 0 rds          |
| [2b] | f3   | RETURN         |                |

> [!TIP]
>
> `REVERT`指令会终止交易的执行，返回一个错误消息，并且所有状态更改（例如资金转移、存储值的更改等）都不会生效。它会从堆栈中弹出两个参数：内存中错误消息的起始位置`mem_offset`和错误消息的长度。
>
> `JUMPI`指令用于条件跳转，它从堆栈中弹出两个元素，如果第二个元素（条件，`condition`）不为0，那么将第一个元素（目标，`destination`）设定为新的`pc`的值（也就是执行跳转）。`JUMPI`如果成功，跳至[2a]行，随后执行`RETURN`指令；如果失败，不执行跳转，继续执行[29]行的`REVERT`指令。`JUMPI`是否成功要检查参数`suc`的值是否为1。
>
> `RETURN`从指定的内存位置提取数据，存储到`returnData`中，并终止当前的操作。此指令需要从堆栈中取出两个参数：内存的起始位置`mem_offset`和数据的长度

希望前面的步骤你都跟上了，如果没跟上的话，可以反复看几遍。其实逻辑很简单，就是为核心的指令准备参数，然后调用它。

最后，我们就得到了带有`PUSH0`的最小代理合约的运行时代码：

```text
365f5f375f5f365f73bebebebebebebebebebebebebebebebebebebebe5af43d5f5f3e5f3d91602a57fd5bf3
```



优化后的代码长度是`44`字节，比之前的最小代理合约少了`1`字节。此外，它用`PUSH0`替换了`RETURNDATASIZE`和`DUP`操作，节省了gas并提高了代码的可读性。总结一下，优化后的最小代理合约在部署时节省`200` gas，在运行时节省`5` gas，同时保持了与之前版本相同的功能。

你可以在[evm.codes](https://www.evm.codes/playground?fork=shanghai&unit=Wei&codeType=Bytecode&code='36z7z6y73~~~~~5af43dzey3d91602a57fd5bf3'~xxxxzyy3y5fxbexyz~_)中测试下它。



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410050940864.png)



## 部署最小代理合约

### 最小创建时代码

优化后的最小代理合约的创建时代码为：

```text
602c8060095f395ff3365f5f375f5f365f73bebebebebebebebebebebebebebebebebebebebe5af43d5f5f3e5f3d91602a57fd5bf3
```



总共`53`字节，其中前`9`字节为`initcode`，你可以结合[第21讲](https://github.com/WTFAcademy/WTF-EVM-Opcodes/blob/main/21_Create/readme.md)，思考它为什么长这样：

```text
602c8060095f395ff3
```



剩余部分是我们刚才建立的代理合约的运行时代码。

### 部署合约

我们可以用下面的`Solidity`合约来部署优化后的最小代理合约：

```solidity
// SPDX-License-Identifier: CC0-1.0
pragma solidity ^0.8.20;

// Note: this contract requires `PUSH0`, which is available in solidity > 0.8.20 and EVM version > Shanghai
contract Clone0Factory {
    error FailedCreateClone();

    receive() external payable {}

    /**
     * @dev Deploys and returns the address of a clone0 (Minimal Proxy Contract with `PUSH0`) that mimics the behaviour of `implementation`.
     *
     * This function uses the create opcode, which should never revert.
     */
    function clone0(address impl) public payable returns (address addr) {
        // first 18 bytes of the creation code 
        bytes memory data1 = hex"602c8060095f395ff3365f5f375f5f365f73";
        // last 15 bytes of the creation code
        bytes memory data2 = hex"5af43d5f5f3e5f3d91602a57fd5bf3";
        // complete the creation code of Clone0
        bytes memory _code = abi.encodePacked(data1, impl, data2);

        // deploy with create op
        assembly {
            // create(v, p, n)
            addr := create(callvalue(), add(_code, 0x20), mload(_code))
        }

        if (addr == address(0)) {
            revert FailedCreateClone();
        }
    }
}
```



## 总结

这一讲，我们结合了前面24讲学习的内容，从头构建了最小代理合约，并且使用`PUSH0`优化了它。优化后最小代理合约的代码长度减少了`1`字节，在部署时节省`200` gas，在运行时生生`5` gas，同时保持了与之前版本相同的功能。

相信你在学习完本教程后，对EVM，字节码，和最小代理合约的认识会有质的飞跃！如果你对本教程有疑问或建议，欢迎推特联系我们或者在GitHub上提issue。另外也欢迎你对[EIP-7511的草稿](https://ethereum-magicians.org/)给出改进建议，它是这门课程的结晶！

## 延伸阅读

1. Peter Murray (@yarrumretep), Nate Welch (@flygoing), Joe Messerman (@JAMesserman), "ERC-1167: Minimal Proxy Contract," Ethereum Improvement Proposals, no. 1167, June 2018. [Online serial]. Available: https://eips.ethereum.org/EIPS/eip-1167.
2. Alex Beregszaszi (@axic), Hugo De la cruz (@hugo-dc), Paweł Bylica (@chfast), "EIP-3855: PUSH0 instruction," Ethereum Improvement Proposals, no. 3855, February 2021. [Online serial]. Available: https://eips.ethereum.org/EIPS/eip-3855.
3. Martin Abbatemarco, Deep dive into the Minimal Proxy contract, https://blog.openzeppelin.com/deep-dive-into-the-minimal-proxy-contract
4. 0age, The More-Minimal Proxy, https://medium.com/@0age/the-more-minimal-proxy-5756ae08ee48