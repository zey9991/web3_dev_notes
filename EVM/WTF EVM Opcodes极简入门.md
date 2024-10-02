# Reference

[01. Hello Opcodes | WTF Academy](https://www.wtf.academy/docs/evm-opcodes-101/HelloOpcodes/)

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



字节码`0x60016001`（PUSH1 1 PUSH1 1）会将两个1压入堆栈，下面我们执行一下：

```python
code = b"\x60\x01\x60\x01"
evm = EVM(code)
evm.run()
print(evm.stack)
# output: [1, 1]
```



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

1. `BLOCKHASH`: 查询特定区块（最近的256个区块，不包括当前区块）的hash，它的操作码为`0x40`，gas消耗为20。。它从堆栈中弹出一个值作为区块高度（block number），然后将该区块的hash压入堆栈，如果它不属于最近的256个区块，则返回0（你可以使用`NUMBER`指令查询当前区块高度）。但是为了简化，我们在这里只考虑当前块。

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