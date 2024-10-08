# References

[1. HelloVitalik (6行代码) | WTF Academy](https://www.wtf.academy/docs/ethers-101/HelloVitalik/)

# 1. HelloVitalik (6行代码)

这一讲，我们会介绍`ethers.js`库，javascript在线编辑器`playcode`，并且我们会写第一个程序`HelloVitalik`：查询Vitalik的`ETH`余额，并输出在`console`中。

> 教程使用 ethers.js 最新的 v6 版本，与 v5 改动较大。v5 版本教程，见 [链接](https://github.com/WTFAcademy/WTF-Ethers/tree/wtf-ethers-v5)。

## ethers.js简述

`ethers.js`是一个完整而紧凑的开源库，用于与以太坊区块链及其生态系统进行交互。如果你要写Dapp的前端，你就需要用到`ethers.js`。

与更早出现的`web3.js`相比，它有以下优点：

1. 代码更加紧凑：`ethers.js`大小为116.5 kB，而`web3.js`为590.6 kB。
2. 更加安全：`Web3.js`认为用户会在本地部署以太坊节点，私钥和网络连接状态由这个节点管理（实际并不是这样）；`ethers.js`中，`Provider`提供器类管理网络连接状态，`Wallet`钱包类管理密钥，安全且灵活。
3. 原生支持`ENS`。



![ethers.js连接Dapp前端和区块链](https://www.wtf.academy/assets/images/1-1-62c0e785174f467af55b783aa4b549d8.png)



## 开发工具

### 1. VScode（推荐）

你可以使用本地`vscode`进行开发。你需要安装[Node.js](https://nodejs.org/zh-cn/download/)，然后利用包管理工具`npm`安装`ethers`库：

```shell
npm install ethers --save
```



### 2. playcode（不稳定）



![playcode](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071528792.png)



[playcode](https://playcode.io/)是一个在线编译`javascript`的平台，你不需要配置`Nodejs`就可以运行`.js`文件，非常方便。且要比更知名的`codesandbox`快一百倍。



![playcode](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071528540.png)



这一讲，我们将用`playcode`做演示。你需要在官网注册一个免费账号，然后点击`OPEN PLAYGROUND`以`Javascript`模版创建一个新项目，然后将代码写在自动生成的`script.js`中即可。很多时候，`playcode`并不能稳定的使用`ethers`，因此我们推荐使用VScode。

## HelloVitalik

现在，让我们用`ethers`编写第一个程序`HelloVitalik`：查询Vitalik的`ETH`余额，并输出在`console`中。整个程序只需要6行，非常简单！

**注意**：在`playcode`上第一次运行可能会提示`module not found`，这是因为`ethers`库还没有安装，只需要点击`install`按钮安装即可。



![Hello Vitalik](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071528214.png)



```javascript
import { ethers } from "ethers";
const provider = ethers.getDefaultProvider();
const main = async () => {
    const balance = await provider.getBalance(`vitalik.eth`);
    console.log(`ETH Balance of vitalik: ${ethers.formatEther(balance)} ETH`);
}
main()
```



我们逐行分析这个程序：

### 1. 导入`ethers`

第一行的作用是导入已经安装好的`ethers`库：

```javascript
import { ethers } from "ethers";
```



如果在`playcode`平台上，免费账号不能安装外部库。我们可以直接从`ethers`的CDN导入（出于安全考虑，仅用于教学）：

```javascript
import { ethers } from "https://cdnjs.cloudflare.com/ajax/libs/ethers/6.2.3/ethers.js";
```



### 2. 连接以太坊

在`ethers`中，`Provider`类是一个为以太坊网络连接提供抽象的类，它提供对区块链及其状态的只读访问。我们声明一个`provider`用于连接以太坊网络。`ethers`内置了一些公用`rpc`，方便用户连接以太坊：

```javascript
const provider = ethers.getDefaultProvider();
```



**注意:**`ethers`内置的`rpc`访问速度有限制，仅测试用，生产环境还是要申请个人`rpc`。比如:

```js
const ALCHEMY_MAINNET_URL = 'https://eth-mainnet.g.alchemy.com/v2/oKmOQKbneVkxgHZfibs-iFhIlIAl6HDN';
const provider = new ethers.JsonRpcProvider(ALCHEMY_MAINNET_URL)
```

> [!TIP]
>
> **RPC（Remote Procedure Call）** 是一种协议，允许程序调用远程服务器上的方法或函数，就像调用本地函数一样。RPC使得客户端和服务器能够在不同的网络位置上进行通信，隐藏了底层的网络传输细节。
>
> **API（Application Programming Interface）** 是一种定义应用程序如何彼此通信的接口。API通常包括一组公开的端点，允许客户端发送请求、接收响应。
>
> 两者的主要区别是：
> 1. **目的和抽象层**：API是一个更高层次的接口，它可以提供不同的协议实现（如HTTP、WebSocket），而RPC专注于方法调用，抽象掉了请求的过程。
> 2. **通信模式**：API通常是基于请求-响应模式，而RPC强调的是函数调用的概念，类似本地调用。
>
> 在`ethers`库中，`RPC`是用于与以太坊节点通信的协议，提供访问区块链数据的能力。通过定义`provider`，你可以使用RPC连接到区块链，查询链上数据或发送交易。



### 3. 声明`async`函数

由于和区块链交互不是实时的我们需要用到js的`async/await`语法糖。每次和链交互的调用需要用到`await`，再把这些用`async`函数包裹起来，最后再调用这个函数。

```javascript
const main = async () => {
    //...
}
main()
```



### 4. 获取Vitalik地址的`ETH`余额

我们可以利用`Provider`类的`getBalance()`函数来查询某个地址的`ETH`余额。由于`ethers`原生支持`ENS`域名，我们不需要知道具体地址，用`ENS`域名`vitalik.eth`就可以查询到以太坊创始人豚林-vitalik的余额。

```javascript
const balance = await provider.getBalance(`vitalik.eth`);
```



### 5. 转换单位后在`console`中输出

我们从链上获取的以太坊余额以`wei`为单位，而`1 ETH = 10^18 wei`。我们打印在`console`之前，需要进行单位转换。`ethers`提供了功能函数`formatEther`，我们可以利用它将`wei`转换为`ETH`。

```javascript
    console.log(`ETH Balance of vitalik: ${ethers.formatEther(balance)} ETH`);
```



如果你使用的是vscode开发工具的话，你需要在vscode控制台输入以下命令

```shell
node 01_HelloVitalik/HelloVitalik.js
```



这样，你就能在控制台中看到Vitalik的`ETH`余额了：`1951 ETH`。当然这不是Vitalik的全部持仓，他有多个钱包，`vitalik.eth`应该只是他用的比较频繁的一个热钱包。



![在控制台打印Vitalik余额](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071528948.png)



## 总结

这是WTF Ethers极简教程的第一讲，我们介绍了`ethers.js`，并完成了第一个使用`ethers`的程序`HelloVitalik`，查询Vitalik钱包的`ETH`余额。

**课后作业**：在图4和图5中，Vitalik的`ETH`余额并不一样。第一张余额为`2251 ETH`，而第二张变为了`1951 ETH`，减少`300 ETH`。其实，两张图片对应Vitalik在`2022.07.30`和`2022.07.31`的持仓。那么，这一天Vitalik用`300 ETH`干了什么？

ethers[v5]官方文档：https://docs.ethers.io/v5/ ethers[v6]官方文档：https://docs.ethers.io/v6/

# 2. Provider 提供器

这一讲，我们将介绍ethers.js的`Provider`类，然后利用它连接上Infura节点，读取链上的信息。

## `Provider`类

`Provider`类是对以太坊网络连接的抽象，为标准以太坊节点功能提供简洁、一致的接口。在`ethers`中，`Provider`不接触用户私钥，只能读取链上信息，不能写入，这一点比`web3.js`要安全。

除了[之前](https://github.com/WTFAcademy/WTF-Ethers)介绍的默认提供者`defaultProvider`以外，`ethers`中最常用的是`jsonRpcProvider`，可以让用户连接到特定节点服务商的节点。

## `jsonRpcProvider`

### 创建节点服务商的API Key

首先，你需要去节点服务商的网站注册并创建`API Key`。在`WTF Solidity极简教程`的工具篇，我们介绍了[Infura](https://github.com/AmazingAng/WTFSolidity/blob/main/Topics/Tools/TOOL02_Infura/readme.md)和[Alchemy](https://github.com/AmazingAng/WTFSolidity/blob/main/Topics/Tools/TOOL04_Alchemy/readme.md)两家公司`API Key`的创建方法，大家可以参考。



![Infura API Key](https://www.wtf.academy/assets/images/2-1-46293ad9ff18e73027a315921b339bc9.png)



你还可以在 [Chainlist](https://chainlist.org/) 网站找到各个链的公开节点。

### 连接公开节点

这里，我们用[Chainlist](https://chainlist.org/)上的公开节点作为例子。在找到合适的rpc之后，可以利用`ethers.JsonRpcProvider()`方法来创建`Provider`变量，该方法以节点服务的`url`链接作为参数。

在下面这个例子中，我们分别创建连接到`ETH`主网和`Sepolia`测试网的`provider`：

```javascript
// 利用公共rpc节点连接以太坊网络
// 可以在 https://chainlist.org 上找到
const ALCHEMY_MAINNET_URL = 'https://rpc.ankr.com/eth';
const ALCHEMY_SEPOLIA_URL = 'https://rpc.sepolia.org';
// 连接以太坊主网
const providerETH = new ethers.JsonRpcProvider(ALCHEMY_MAINNET_URL)
// 连接Sepolia测试网
const providerSepolia = new ethers.JsonRpcProvider(ALCHEMY_SEPOLIA_URL)
```



### 利用`Provider`读取链上数据

`Provider`类封装了一些方法，可以便捷的读取链上数据：

**1.** 利用`getBalance()`函数读取主网和测试网Vitalik的`ETH`余额（测试网目前不支持`ENS`域名，只能用钱包地址查询）：

```javascript
// 1. 查询vitalik在主网和Sepolia测试网的ETH余额
console.log("1. 查询vitalik在主网和Sepolia测试网的ETH余额");

// 查询以太坊主网余额（使用vitalik.eth ENS域名）
const balance = await providerETH.getBalance('vitalik.eth');

// 查询Sepolia测试网余额（使用vitalik的具体地址）
const balanceSepolia = await providerSepolia.getBalance('0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045');

// 输出主网ETH余额
console.log(`ETH Balance of vitalik: ${ethers.formatEther(balance)} ETH`);

// 输出Sepolia测试网ETH余额
console.log(`Sepolia ETH Balance of vitalik: ${ethers.formatEther(balanceSepolia)} ETH`);

```





![Vitalik余额](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071528168.png)



**2.** 利用`getNetwork()`查询`provider`连接到了哪条链，`homestead`代表`ETH`主网：

```javascript
    // 2. 查询provider连接到了哪条链
    console.log("\n2. 查询provider连接到了哪条链")
    const network = await providerETH.getNetwork();
    console.log(network.toJSON());
```



> ethers v6版本, 以上代码中`network`不能直接`console.log()`, 具体原因参考: [discussion-3977](https://github.com/ethers-io/ethers.js/discussions/3977)



![getNetwork](data:image/png;base64,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)



**3.** 利用`getBlockNumber()`查询当前区块高度：

```javascript
    // 3. 查询区块高度
    console.log("\n3. 查询区块高度")
    const blockNumber = await providerETH.getBlockNumber();
    console.log(blockNumber);
```





![getBlockNumber](https://www.wtf.academy/assets/images/2-4-bd6b9bdde2333475c1dab14f19e9820f.png)



**4.** 利用`getTransactionCount()`查询某个钱包的历史交易次数。

```javascript
    // 4. 查询 vitalik 钱包历史交易次数
    console.log("\n4. 查询 vitalik 钱包历史交易次数")
    const txCount = await providerETH.getTransactionCount("vitalik.eth");
    console.log(txCount);
```





![getGasPrice](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAeIAAAA/CAYAAAA8PsvmAAABSGlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf87AwsDKIMagzyCbmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsisx17ddnrM82cwxvlf9OnffwxTPQrgSkktTgbSf4A4PbmgqISBgTEFyFYuLykAsTuAbJEioKOA7DkgdjqEvQHEToKwj4DVhAQ5A9k3gGyB5IxEoBmML4BsnSQk8XQkNtReEOB1cfXxUQg1MjG09Agm4F6SQUlqRQmIds4vqCzKTM8oUXAEhlKqgmdesp6OgpGBkTEDAyjMIao/B4HDklFsH0IsfwkDg8U3BgbmiQixpCkMDNvbGBgkbiHEVOYxMPC3MDBsO1SQWJQIdwDjN5biNGMjCJvHnoGB9e7//581GBjYJzIw/J34///vxf///10MNP82A8OBSgAIgGBbU+rXzgAAAFZlWElmTU0AKgAAAAgAAYdpAAQAAAABAAAAGgAAAAAAA5KGAAcAAAASAAAARKACAAQAAAABAAAB4qADAAQAAAABAAAAPwAAAABBU0NJSQAAAFNjcmVlbnNob3S0BomeAAAB1WlUWHRYTUw6Y29tLmFkb2JlLnhtcAAAAAAAPHg6eG1wbWV0YSB4bWxuczp4PSJhZG9iZTpuczptZXRhLyIgeDp4bXB0az0iWE1QIENvcmUgNi4wLjAiPgogICA8cmRmOlJERiB4bWxuczpyZGY9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkvMDIvMjItcmRmLXN5bnRheC1ucyMiPgogICAgICA8cmRmOkRlc2NyaXB0aW9uIHJkZjphYm91dD0iIgogICAgICAgICAgICB4bWxuczpleGlmPSJodHRwOi8vbnMuYWRvYmUuY29tL2V4aWYvMS4wLyI+CiAgICAgICAgIDxleGlmOlBpeGVsWURpbWVuc2lvbj42MzwvZXhpZjpQaXhlbFlEaW1lbnNpb24+CiAgICAgICAgIDxleGlmOlBpeGVsWERpbWVuc2lvbj40ODI8L2V4aWY6UGl4ZWxYRGltZW5zaW9uPgogICAgICAgICA8ZXhpZjpVc2VyQ29tbWVudD5TY3JlZW5zaG90PC9leGlmOlVzZXJDb21tZW50PgogICAgICA8L3JkZjpEZXNjcmlwdGlvbj4KICAgPC9yZGY6UkRGPgo8L3g6eG1wbWV0YT4KIDCBFAAAFh1JREFUeAHtnQd0FUUbhicEQrEBFmwgithQQaxYUQQLdlAUu9hBxV5ARQU8gGBBsVc8gg1U7BV774odLCiKCipiICHJP8/kn8vczd6Sm+TGHN/vnGTLlN19d++8X5vdgjXXXLPCSISAEBACQkAICIF6QaBRvRxVBxUCQkAICAEhIAQcAiJiPQhCQAgIASEgBOoRARFxPYKvQwsBISAEhIAQEBHrGRACQkAICAEhUI8IiIjrEXwdWggIASEgBISAiFjPgBAQAkJACAiBekRARFyP4OvQQkAICAEhIARExHoGhIAQEAJCQAjUIwIi4noEX4cWAkJACAgBISAi1jMgBISAEBACQqAeERAR1yP4OrQQEAJCQAgIARGxngEhIASEgBAQAvWIgIi4HsHXoYWAEBACQkAING5IEBxwwAGmd+/eZsCAARlPe+211zbHHHOMufDCCxN1t9pqK3P66aebE0880fz555+J/Q1xZbnlljMrr7xy4tRnzpyZWM92ZdVVVzU///xzttWr1LvyyivNF198YW644YaksmHDhpny8nL3V1paakaNGpVUHm5suOGGhvrDhw83H3/8cViUcX3LLbfMWMdX+OGHHzJe6w477GCOPfZYc+SRR/pmWS+5HzfddJN5/PHHzcSJE7Nqx/3bY4890tadM2eOeeaZZ6rUWX/99R32YQE4FhYWJj3zYXm4zm/o3XffNSuuuKLp16+fOf744835559vbr/9drP88subiy++2Bx66KFhE60LASFQRwjUChFvs8027sf8+eefmxtvvLFWTnXw4MFmjTXWSOqrdevWZpllljFjxoxJ2s/GhAkTzKxZs5L2r7POOuaWW24xZ5xxhvnrr7/M/vvvbwoKCsw+++yTVI+NF1980Xz//fdV9tfGDgbm2bNnu4Eu2t8uu+xiZsyYkZEkou323Xdfs/feeyd2n3vuuebbb79NbIcrccdnIO7Vq5c5+eSTze+//x5Wz2q9ffv2ZvXVV3cKze67724WLVpkpk+f7to2bdrULSdNmmSGDBliDj/88JTkdMopp7i6Xbp0MfzFyXfffWdeeumlpCKeOZSqiorsvuLJ/b3++uuT+mjZsqVp1GipUwhS4tx5zkKZN29e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)



**5.** 利用`getFeeData()`查询当前建议的`gas`设置，返回的数据格式为`bigint`。

```javascript
    // 5. 查询当前建议的gas设置
    console.log("\n5. 查询当前建议的gas设置")
    const feeData = await providerETH.getFeeData();
    console.log(feeData);
```





![getFeeData](https://www.wtf.academy/assets/images/2-6-cd196adf6e9278a1b871a8a63e737ffa.png)



**6.** 利用`getBlock()`查询区块信息，参数为要查询的区块高度：

```javascript
    // 6. 查询区块信息
    console.log("\n6. 查询区块信息")
    const block = await providerETH.getBlock(0);
    console.log(block);
```





![getBlock](https://www.wtf.academy/assets/images/2-7-466069bb26d975ba43f4b930f1372aec.png)



**7.** 利用`getCode()`查询某个地址的合约`bytecode`，参数为合约地址，下面例子中用的主网`WETH`的合约地址：

```javascript
    // 7. 给定合约地址查询合约bytecode，例子用的WETH地址
    console.log("\n7. 给定合约地址查询合约bytecode，例子用的WETH地址")
    const code = await providerETH.getCode("0xc778417e063141139fce010982780140aa0cd5ab");
    console.log(code);
```





![getCode](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071528733.png)



## 总结

这一讲，我们介绍了ethers.js的`Provider`类，并用Infura的节点API Key创建了`jsonRpcProvider`，读取了`ETH`主网和`Sepolia`测试网的链上信息。

# 3. 读取合约信息

这一讲，我们将介绍`Contract`合约类，并利用它来读取链上的合约信息。

## `Contract`类

在`ethers`中，`Contract`类是部署在以太坊网络上的合约（`EVM`字节码）的抽象。通过它，开发者可以非常容易的对合约进行读取`call`和交易`transaction`，并可以获得交易的结果和事件。以太坊强大的地方正是合约，所以对于合约的操作要熟练掌握。

## 创建`Contract`变量

### 只读和可读写`Contract`

`Contract`对象分为两类，只读和可读写。只读`Contract`只能读取链上合约信息，执行`call`操作，即调用合约中`view`和`pure`的函数，而不能执行交易`transaction`。创建这两种`Contract`变量的方法有所不同：

- 只读`Contract`：参数分别是合约地址，合约`abi`和`provider`变量（只读）。

```javascript
const contract = new ethers.Contract(`address`, `abi`, `provider`);
```



- 可读写`Contract`：参数分别是合约地址，合约`abi`和`signer`变量。`Signer`签名者是`ethers`中的另一个类，用于签名交易，之后我们会讲到。

```javascript
const contract = new ethers.Contract(`address`, `abi`, `signer`);
```



**注意** `ethers`中的`call`指的是只读操作，与`solidity`中的`call`不同。

## 读取合约信息

### 1. 创建Provider

我们使用Infura节点的API Key创建`Provider`（见[第2讲：Provider](https://www.wtf.academy/docs/ethers-101/Provider/)）：

```javascript
import { ethers } from "ethers";
// 利用Infura的rpc节点连接以太坊网络
// 准备Infura API Key, 教程：https://github.com/AmazingAng/WTFSolidity/blob/main/Topics/Tools/TOOL02_Infura/readme.md
const INFURA_ID = ''
// 连接以太坊主网
const provider = new ethers.JsonRpcProvider(`https://mainnet.infura.io/v3/${INFURA_ID}`)
```

> [!TIP]
>
> 在这段代码中，使用了 `ethers.js` 库，并通过 Infura 的 RPC 节点连接到以太坊主网。以下是每个部分的详细解释：
>
> ### 1. 引入 `ethers` 库
> ```javascript
> import { ethers } from "ethers";
> ```
> 这行代码从 `ethers.js` 库中导入了 `ethers` 对象。`ethers.js` 是一个用于与以太坊网络交互的 JavaScript 库，它提供了许多工具来与智能合约和区块链进行操作。
>
> ### 2. 利用 Infura 的 RPC 节点连接以太坊网络
> ```javascript
> const INFURA_ID = ''
> ```
> - `INFURA_ID`: Infura 是一种提供以太坊节点服务的基础设施，用于连接和与区块链交互。这里 `INFURA_ID` 是你从 Infura 平台获得的 API Key，具体获取流程可以参考提供的教程链接。
>   
> ### 3. 通过 Infura 连接到以太坊主网
> ```javascript
> const provider = new ethers.JsonRpcProvider(`https://mainnet.infura.io/v3/${INFURA_ID}`)
> ```
> - `provider`: 这是 `ethers.js` 中的 `JsonRpcProvider`，它负责连接到以太坊网络并提供与区块链交互的功能。
> - `https://mainnet.infura.io/v3/${INFURA_ID}`: 通过这个 URL，`ethers.js` 使用 Infura 的 RPC 接口来连接到以太坊主网。`${INFURA_ID}` 将你的个人 API Key 插入到 URL 中，确保你有权限通过 Infura 与以太坊网络通信。
>
> ### 代码运行前的准备
> - **申请 Infura API Key**: 你需要前往 [Infura](https://infura.io/) 注册账号，创建一个项目，并获取相应的 API Key，将其填入到 `INFURA_ID` 中。
> - **安装 ethers.js**: 在运行这段代码之前，确保你的项目中已经安装了 `ethers.js` 库。你可以使用以下命令进行安装：
>
>   ```bash
>   npm install ethers
>   ```
>
> ### 总结
> 这段代码的主要目的是通过 Infura 提供的 RPC 服务连接到以太坊主网，然后通过 `ethers.js` 的 `JsonRpcProvider` 来与区块链进行交互。Infura 的服务让开发者不需要自己运行以太坊节点就可以连接到主网或其他测试网络，极大地简化了区块链开发。



### 2. 创建只读Contract实例

创建只读Contract实例需要填入`3`个参数，分别是合约地址，合约`abi`和`provider`变量。合约地址可以在网上查到，`provider`变量上一步我们已经创建了，那么`abi`怎么填？

`ABI` (Application Binary Interface) 是与以太坊智能合约交互的标准，更多内容见[WTF Solidity教程第27讲: ABI编码](https://github.com/AmazingAng/WTF-Solidity/blob/main/27_ABIEncode/readme.md)。`ethers`支持两种`abi`填法：

- **方法1.** 直接输入合约`abi`。你可以从`remix`的编译页面中复制，在本地编译合约时生成的`artifact`文件夹的`json`文件中得到，或者从`etherscan`开源合约的代码页面得到。我们用这个方法创建`WETH`的合约实例：

```javascript
// 第1种输入abi的方式: 复制abi全文
// WETH的abi可以在这里复制：https://etherscan.io/token/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2#code
const abiWETH = '[{"constant":true,"inputs":[],"name":"name","outputs":[{"name":"","type":"string"}],"payable":false,"stateMutability":"view",...太长后面省略...';
const addressWETH = '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2' // WETH Contract
const contractWETH = new ethers.Contract(addressWETH, abiWETH, provider)
```





![在Etherscan得到abi](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071529102.png)



- **方法2.** 由于`abi`可读性太差，`ethers`创新的引入了`Human-Readable Abi`（人类可读abi）。开发者可以通过`function signature`和`event signature`来写`abi`。我们用这个方法创建稳定币`DAI`的合约实例：

```javascript
// 第2种输入abi的方式：输入程序需要用到的函数，逗号分隔，ethers会自动帮你转换成相应的abi
// 人类可读abi，以ERC20合约为例
const abiERC20 = [
    "function name() view returns (string)",
    "function symbol() view returns (string)",
    "function totalSupply() view returns (uint256)",
    "function balanceOf(address) view returns (uint)",
];
const addressDAI = '0x6B175474E89094C44Da98b954EedeAC495271d0F' // DAI Contract
const contractDAI = new ethers.Contract(addressDAI, abiERC20, provider)
```



### 3. 读取`WETH`和`DAI`的链上信息

我们可以利用只读`Contract`实例调用合约的`view`和`pure`函数，获取链上信息：

```javascript
const main = async () => {
    // 1. 读取WETH合约的链上信息（WETH abi）
    const nameWETH = await contractWETH.name()
    const symbolWETH = await contractWETH.symbol()
    const totalSupplyWETH = await contractWETH.totalSupply()
    console.log("\n1. 读取WETH合约信息")
    console.log(`合约地址: ${addressWETH}`)
    console.log(`名称: ${nameWETH}`)
    console.log(`代号: ${symbolWETH}`)
    console.log(`总供给: ${ethers.formatEther(totalSupplyWETH)}`)
    const balanceWETH = await contractWETH.balanceOf('vitalik.eth')
    console.log(`Vitalik持仓: ${ethers.formatEther(balanceWETH)}\n`)

    // 2. 读取DAI合约的链上信息（IERC20接口合约）
    const nameDAI = await contractDAI.name()
    const symbolDAI = await contractDAI.symbol()
    const totalSupplDAI = await contractDAI.totalSupply()
    console.log("\n2. 读取DAI合约信息")
    console.log(`合约地址: ${addressDAI}`)
    console.log(`名称: ${nameDAI}`)
    console.log(`代号: ${symbolDAI}`)
    console.log(`总供给: ${ethers.formatEther(totalSupplDAI)}`)
    const balanceDAI = await contractDAI.balanceOf('vitalik.eth')
    console.log(`Vitalik持仓: ${ethers.formatEther(balanceDAI)}\n`)
}

main()
```

> [!TIP]
>
> `contractWETH.name()`: 调用 WETH 合约中的 `name()` 函数获取代币名称。
>
> `contractWETH.symbol()`: 获取代币的代号（符号）。
>
> `contractWETH.totalSupply()`: 获取代币的总供给量。
>
> `contractWETH.balanceOf('vitalik.eth')`: 获取账户 `vitalik.eth`（即 Vitalik）的 WETH 持仓。
>
> 类似地，这一部分是读取 `DAI` 合约的信息，方法与 `WETH` 合约相同。
>
> `contractDAI.name()`, `contractDAI.symbol()`, `contractDAI.totalSupply()`: 获取 DAI 合约的基本信息。
>
> `contractDAI.balanceOf('vitalik.eth')`: 获取 Vitalik 持有的 DAI 数量。

可以看到，用两种方法创建的合约实例都能成功与链上交互。Vitalik的钱包里有`0.05 WETH`及`555508 DAI`，见下图。



![成功读取VitalikWETH和DAI持仓](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071529266.png)



**说明** 我们可以通过[以太坊浏览器](https://etherscan.io/token/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2#readContract) 验证Vitalik钱包里的`WETH`余额, 是否与通过`Contract`读取的一致。 通过[ENS](https://app.ens.domains/name/vitalik.eth/details) 查到Vitalik钱包地址是`0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045`,然后通过合约方法`balanceOf`得到余额正好是`0.05 WETH`, 结论是一致！

![VitalikWETH余额](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071528241.png)



## 总结

这一讲，我们介绍了`ethers`中的`Contract`合约类，并创建了`WETH`和`DAI`的只读`Contract`实例，成功读取了Vitalik这两个币的持仓。

# 4. 发送ETH

这一讲，我们将介绍`Signer`签名者类和它派生的`Wallet`钱包类，并利用它来发送`ETH`。

## `Signer`签名者类

`Web3.js`认为用户会在本地部署以太坊节点，私钥和网络连接状态由这个节点管理（实际并不是这样）；而在`ethers.js`中，`Provider`提供器类管理网络连接状态，`Signer`签名者类或`Wallet`钱包类管理密钥，安全且灵活。

在`ethers`中，`Signer`签名者类是以太坊账户的抽象，可用于对消息和交易进行签名，并将签名的交易发送到以太坊网络，并更改区块链状态。`Signer`类是抽象类，不能直接实例化，我们需要使用它的子类：`Wallet`钱包类。

## `Wallet`钱包类

`Wallet`类继承了`Signer`类，并且开发者可以像包含私钥的外部拥有帐户（`EOA`）一样，用它对交易和消息进行签名。

下面我们介绍创建`Wallet`实例的几种办法：

### 方法1：创建随机的wallet对象

我们可以利用`ethers.Wallet.createRandom()`函数创建带有随机私钥的`Wallet`对象。该私钥由加密安全的熵源生成，如果当前环境没有安全的熵源，则会引发错误（没法在在线平台`playcode`使用此方法）。

```javascript
// 创建随机的wallet对象
const wallet1 = ethers.Wallet.createRandom()
```



### 方法2：用私钥创建wallet对象

我们已知私钥的情况下，可以利用`ethers.Wallet()`函数创建`Wallet`对象。

```javascript
// 利用私钥和provider创建wallet对象
const privateKey = '0x227dbb8586117d55284e26620bc76534dfbd2394be34cf4a09cb775d593b6f2b'
const wallet2 = new ethers.Wallet(privateKey, provider)
```

> [!TIP]
>
> **可以创建钱包**：不需要 `provider` 也可以成功创建 `Wallet` 对象。
>
> **有限的功能**：没有 `provider`，这个钱包的功能会受到限制，不能直接与以太坊网络交互。你可以后续将 `provider` 传递给钱包对象，但通常在创建时就提供会更方便。



### 方法3：从助记词创建wallet对象

我们已知助记词的情况下，可以利用`ethers.Wallet.fromPhrase()`函数创建`Wallet`对象。

```javascript
// 从助记词创建wallet对象
const wallet3 = ethers.Wallet.fromPhrase(mnemonic.phrase)
```



### 其他方法：通过JSON文件创建wallet对象

以上三种方法即可满足大部分需求，当然还可以通过`ethers.Wallet.fromEncryptedJson`解密一个`JSON`钱包文件创建钱包实例，`JSON`文件即`keystore`文件，通常来自`Geth`, `Parity`等钱包，通过`Geth`搭建过以太坊节点的个人对`keystore`文件不会陌生。

## 发送`ETH`

我们可以利用`Wallet`实例来发送`ETH`。首先，我们要构造一个交易请求，在里面声明接收地址`to`和发送的`ETH`数额`value`。交易请求`TransactionRequest`类型可以包含发送方`from`，nonce值`nounce`，请求数据`data`等信息，之后的教程里会更详细介绍。

```javascript
    // 创建交易请求，参数：to为接收地址，value为ETH数额
    const tx = {
        to: address1,
        value: ethers.parseEther("0.001")
    }
```



然后，我们就可以利用`Wallet`类的`sendTransaction`来发送交易，等待交易上链，并获得交易的收据，非常简单。

```javascript
    //发送交易，获得收据
    const txRes = await wallet2.sendTransaction(tx)
    const receipt = await txRes.wait() // 等待链上确认交易
    console.log(receipt) // 打印交易的收据
```



## 代码示例

### 1. 创建`Provider`实例

```javascript
// 利用Wallet类发送ETH
// 由于playcode不支持ethers.Wallet.createRandom()函数，我们只能用VScode运行这一讲代码
import { ethers } from "ethers";

// 利用Alchemy的rpc节点连接以太坊测试网络
// 准备 alchemy API 可以参考https://github.com/AmazingAng/WTFSolidity/blob/main/Topics/Tools/TOOL04_Alchemy/readme.md 
const ALCHEMY_GOERLI_URL = 'https://eth-goerli.alchemyapi.io/v2/GlaeWuylnNM3uuOo-SAwJxuwTdqHaY5l';
const provider = new ethers.JsonRpcProvider(ALCHEMY_GOERLI_URL);
```



### 2. 用三种不同方法创建`Wallet`实例

- 创建随机私钥的`Wallet`对象。这种方法创建的钱包是单机的，我们需要用`connect(provider)`函数，连接到以太坊节点。这种方法创建的钱包可以用`mnemonic`获取助记词。

```javascript
// 创建随机的wallet对象
const wallet1 = ethers.Wallet.createRandom()
const wallet1WithProvider = wallet1.connect(provider)
const mnemonic = wallet1.mnemonic // 获取助记词
```



- 利用私钥和`Provider`实例创建`Wallet`对象。这种方法创建的钱包不能获取助记词。

```javascript
// 利用私钥和provider创建wallet对象
const privateKey = '0x227dbb8586117d55284e26620bc76534dfbd2394be34cf4a09cb775d593b6f2b'
const wallet2 = new ethers.Wallet(privateKey, provider)
```



- 利用助记词创建`Wallet`对象。这里我们使用的是`wallet1`的助记词，因此创建出钱包的私钥和公钥都和`wallet1`相同。

```javascript
// 从助记词创建wallet对象
const wallet3 = ethers.Wallet.fromPhrase(mnemonic.phrase)
```



### 3. 获取钱包地址

利用`getAddress()`函数获取钱包地址。

```javascript
    const address1 = await wallet1.getAddress()
    const address2 = await wallet2.getAddress() 
    const address3 = await wallet3.getAddress() // 获取地址
    console.log(`1. 获取钱包地址`);
    console.log(`钱包1地址: ${address1}`);
    console.log(`钱包2地址: ${address2}`);
    console.log(`钱包3地址: ${address3}`);
    console.log(`钱包1和钱包3的地址是否相同: ${address1 === address3}`);
    
```





![获取钱包地址](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071529802.png)



### 4. 获取助记词

利用钱包对象的`mnemonic.phrase`成员获取助记词：

```javascript
console.log(`钱包1助记词: ${wallet1.mnemonic.phrase}`)
```





![获取助记词](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071529527.png)



### 5. 获取私钥

利用钱包对象的`privateKey`成员获取私钥：

```javascript
    console.log(`钱包2私钥: ${wallet2.privateKey}`)
```





![获取私钥](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071529362.png)



### 6. 获取钱包在链上的交互次数

利用`getTransactionCount()`函数获取钱包在链上的交互次数。

```javascript
    const txCount1 = await provider.getTransactionCount(wallet1WithProvider)
    const txCount2 = await provider.getTransactionCount(wallet2)
    console.log(`钱包1发送交易次数: ${txCount1}`)
    console.log(`钱包2发送交易次数: ${txCount2}`)
```





![获取钱包在链上的交互次数](https://www.wtf.academy/assets/images/4-4-4c35959c6e09da159b0e42211bbf0b1f.png)



### 7. 发送`ETH`

我们用`wallet2`给`wallet1`发送`0.001 ETH`，并打印交易前后的钱包余额。由于`wallet1`是新建的随机私钥钱包，因此交易前余额为`0`，而交易后余额为`0.001 ETH`。

```javascript
    // 5. 发送ETH
    // 如果这个钱包没goerli测试网ETH了，去水龙头领一些，钱包地址: 0xe16C1623c1AA7D919cd2241d8b36d9E79C1Be2A2
    // 1. chainlink水龙头: https://faucets.chain.link/goerli
    // 2. paradigm水龙头: https://faucet.paradigm.xyz/
    console.log(`\n5. 发送ETH（测试网）`);
    // i. 打印交易前余额
    console.log(`i. 发送前余额`)
    console.log(`钱包1: ${ethers.formatEther(await provider.getBalance(wallet1WithProvider))} ETH`)
    console.log(`钱包2: ${ethers.formatEther(await provider.getBalance(wallet2))} ETH`)
    // ii. 构造交易请求，参数：to为接收地址，value为ETH数额
    const tx = {
        to: address1,
        value: ethers.parseEther("0.001")
    }
    // iii. 发送交易，获得收据
    console.log(`\nii. 等待交易在区块链确认（需要几分钟）`)
    const receipt = await wallet2.sendTransaction(tx)
    await receipt.wait() // 等待链上确认交易
    console.log(receipt) // 打印交易详情
    // iv. 打印交易后余额
    console.log(`\niii. 发送后余额`)
    console.log(`钱包1: ${ethers.formatEther(await provider.getBalance(wallet1WithProvider))} ETH`)
    console.log(`钱包2: ${ethers.formatEther(await provider.getBalance(wallet2))} ETH`)
```





![发送ETH](https://www.wtf.academy/assets/images/4-5-e48692533c5ccbb9350ace798b32e49f.png)



## 总结

这一讲，我们介绍了`Signer`签名者类和`Wallet`钱包类，使用钱包实例获取了地址、助记词、私钥、链上交互次数，并发送`ETH`。

# 5. 合约交互

这一讲，我们将介绍如何声明可写的`Contract`合约变量，并利用它与测试网的`WETH`合约交互。

## 创建可写`Contract`变量

声明可写的`Contract`变量的规则：

```js
const contract = new ethers.Contract(address, abi, signer)
```



其中`address`为合约地址，`abi`是合约的`abi`接口，`signer`是`wallet`对象。注意，这里你需要提供`signer`，而在声明可读合约时你只需要提供`provider`。

你也可以利用下面的方法，将可读合约转换为可写合约：

```js
const contract2 = contract.connect(signer)
```



## 合约交互

我们在[第三讲](https://github.com/WTFAcademy/WTFEthers/blob/main/03_ReadContract/readme.md)介绍了读取合约信息。它不需要`gas`。这里我们介绍写入合约信息，你需要构建交易，并且支付`gas`。该交易将由整个网络上的每个节点以及矿工验证，并改变区块链状态。

你可以用下面的方法进行合约交互：

```js
// 发送交易
const tx = await contract.METHOD_NAME(args [, overrides])
// 等待链上确认交易
await tx.wait() 
```



其中`METHOD_NAME`为调用的函数名，`args`为函数参数，`[, overrides]`是可以选择传入的数据，包括：

- gasPrice：gas价格
- gasLimit：gas上限
- value：调用时传入的ether（单位是wei）
- nonce：nonce

**注意：** 此方法不能获取合约运行的返回值，如有需要，要使用`Solidity`事件记录，然后利用交易收据去查询。

## 例子：与测试网`WETH`合约交互

`WETH` (Wrapped ETH)是`ETH`的带包装版本，将以太坊原生代币用智能合约包装成了符合`ERC20`的代币。对`WETH`合约更详细的内容可以参考WTF Solidity极简合约的[第41讲 WETH](https://github.com/AmazingAng/WTFSolidity/blob/main/41_WETH/readme.md)。

1. 创建`provider`，`wallet`变量。

   ```js
   import { ethers } from "ethers";
   
   // 利用Alchemy的rpc节点连接以太坊网络
   const ALCHEMY_GOERLI_URL = 'https://eth-goerli.alchemyapi.io/v2/GlaeWuylnNM3uuOo-SAwJxuwTdqHaY5l';
   const provider = new ethers.JsonRpcProvider(ALCHEMY_GOERLI_URL);
   
   // 利用私钥和provider创建wallet对象
   const privateKey = '0x227dbb8586117d55284e26620bc76534dfbd2394be34cf4a09cb775d593b6f2b'
   const wallet = new ethers.Wallet(privateKey, provider)
   ```

   

2. 创建可写`WETH`合约变量，我们在`ABI`中加入了4个我们要调用的函数：

   - `balanceOf(address)`：查询地址的`WETH`余额。
   - `deposit()`：将转入合约的`ETH`转为`WETH`。
   - `transfer(address, uint256)`：转账。
   - `withdraw(uint256)`：取款。

   ```js
   // WETH的ABI
   const abiWETH = [
       "function balanceOf(address) public view returns(uint)",
       "function deposit() public payable",
       "function transfer(address, uint) public returns (bool)",
       "function withdraw(uint) public",
   ];
   // WETH合约地址（Goerli测试网）
   const addressWETH = '0xb4fbf271143f4fbf7b91a5ded31805e42b2208d6' // WETH Contract
   
   // 声明可写合约
   const contractWETH = new ethers.Contract(addressWETH, abiWETH, wallet)
   // 也可以声明一个只读合约，再用connect(wallet)函数转换成可写合约。
   // const contractWETH = new ethers.Contract(addressWETH, abiWETH, provider)
   // contractWETH.connect(wallet)
   ```

   

3. 读取账户`WETH`余额，可以看到余额为`1.001997`。

   ```js
   const address = await wallet.getAddress()
   // 读取WETH合约的链上信息（WETH abi）
   console.log("\n1. 读取WETH余额")
   const balanceWETH = await contractWETH.balanceOf(address)
   console.log(`存款前WETH持仓: ${ethers.formatEther(balanceWETH)}\n`)
   ```

   

   ![读取WETH余额](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071529139.png)

   

4. 调用`WETH`合约的`deposit()`函数，将`0.001 ETH`转换为`0.001 WETH`，打印交易详情和余额。`deposit()`函数没有参数，可以看到余额变为`1.002997`。

   ```js
       console.log("\n2. 调用desposit()函数，存入0.001 ETH")
       // 发起交易
       const tx = await contractWETH.deposit({value: ethers.parseEther("0.001")})
       // 等待交易上链
       await tx.wait()
       console.log(`交易详情：`)
       console.log(tx)
       const balanceWETH_deposit = await contractWETH.balanceOf(address)
       console.log(`存款后WETH持仓: ${ethers.formatEther(balanceWETH_deposit)}\n`)
   ```

   

   

   ![调用deposit](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071529031.png)

   

2. 调用`WETH`合约的`transfer()`函数，给Vitalik转账`0.001 WETH`，并打印余额。可以看到余额变为`1.001997`。

   ```js
       console.log("\n3. 调用transfer()函数，给vitalik转账0.001 WETH")
       // 发起交易
       const tx2 = await contractWETH.transfer("vitalik.eth", ethers.parseEther("0.001"))
       // 等待交易上链
       await tx2.wait()
       const balanceWETH_transfer = await contractWETH.balanceOf(address)
       console.log(`转账后WETH持仓: ${ethers.formatEther(balanceWETH_transfer)}\n`)
   ```

   

   

   ![给Vitalik转WETH](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071529297.png)

   

**注意**：观察`deposit()`函数和`balanceOf()`函数，为什么他们的返回值不一样？为什么前者返回一堆数据，而后者只返回确定的值？这是因为对于钱包的余额，它是一个只读操作，读到什么就是什么。而对于一次函数的调用，并不知道数据何时上链，所以只会返回这次交易的信息。总结来说，就是对于非`pure`/`view`函数的调用，会返回交易的信息。如果想知道函数执行过程中合约变量的变化，可以在合约中使用`emit`输出事件，并在返回的`transaction`信息中读取事件信息来获取相应的值。

## 总结

这一讲，我们介绍了如何声明可写的`Contract`合约变量，并利用它与测试网的`WETH`合约交互。我们不仅调用`WETH`的`deposit()`函数，将`0.001 ETH`转换为`WETH`，并转账给了Vitalik。

# 6. 部署合约

提示：本教程基于ethers.js 6.3.0 ，如果你使用的是v5，可以参考[ethers.js v5文档](https://docs.ethers.io/v5/)。

这一讲，我们将介绍`ethers.js`中的合约工厂`ContractFactory`类型，并利用它部署合约。

具体可参考[ethers.js文档](https://docs.ethers.io/v5/api/contract/contract-factory)。

## 部署智能合约

在以太坊上，智能合约的部署是一种特殊的交易：将编译智能合约得到的字节码发送到0地址。如果这个合约的构造函数有参数的话，需要利用`abi.encode`将参数编码为字节码，然后附在在合约字节码的尾部一起发送。对于ABI编码的介绍见WTF Solidity极简教程[第27讲 ABI编码](https://github.com/AmazingAng/WTFSolidity/blob/main/27_ABIEncode/readme.md)。

> [!NOTE]
>
> 在以太坊上，部署智能合约的过程是一种特殊的交易，因为它不是将代币或数据发送给某个已存在的账户，而是将合约代码发送到一个新生成的合约地址。以下是部署合约的一些关键点：
>
> ### 1. 合约部署的交易
> 在以太坊上，所有的合约都是通过交易部署的，部署合约的交易与普通的交易有所不同，因为它的接收者是**0地址**（即`0x0000000000000000000000000000000000000000`），该地址代表“无地址”，标志这是一笔合约创建交易。
>
> ### 2. 编译合约的字节码
> 部署合约时，首先需要编译智能合约。智能合约是用高级语言（如Solidity）编写的，编译后生成的字节码才是部署到以太坊网络的内容。编译的结果不仅包括合约的逻辑代码，还包括初始化数据和一些运行时信息。
>
> ### 3. 构造函数和参数编码
> 如果智能合约的构造函数需要接收参数，这些参数不能直接以人类可读的形式附在交易数据中。相反，需要将这些参数用一种标准化的方式进行编码，这就是**ABI编码**。
>
> ABI（Application Binary Interface）是一种定义以太坊上智能合约与外部通信的标准，它用于编码和解码函数调用、参数和返回值。在部署合约时，构造函数的参数需要用`abi.encode`函数进行编码，将这些参数转换成字节码，附加在合约代码的末尾。
>
> #### 例子
> 假设我们有一个合约的构造函数是这样的：
>
> ```solidity
> contract MyContract {
>     uint public value;
> 
>     constructor(uint _value) {
>         value = _value;
>     }
> }
> ```
>
> 要部署这个合约，并且传递一个`_value`参数为`100`，我们需要将合约的字节码与`100`这个参数的ABI编码值拼接在一起。
>
> ```javascript
> const bytecode = "0x608060405234801561001057600080fd5b5060405161010038038061010083398101604081905261001f9161003d565b6000819055506100cb565b6100bb8061002f6000396000f3fe60806040526004361060485760003560e01c80636d4ce63c14604d575b600080fd5b6053606d565b60408051918252519081900360200190f35b60006001905090565b600081905091905056fea26469706673582212203b5df0768174df11ac4bfb13213d1b0d9eb2dbfc996bd08c0f118c81267d301a64736f6c63430007060033"; // 合约字节码
> const abiEncodedParameter = ethers.utils.defaultAbiCoder.encode(["uint256"], [100]); // 参数ABI编码
> const fullBytecode = bytecode + abiEncodedParameter.slice(2); // 将参数附加到字节码后面
> ```
>
> ### 4. 合约部署的交易发送
> 在构造了包含参数的完整字节码之后，我们将其发送到区块链上，创建新合约：
>
> ```javascript
> const tx = await wallet.sendTransaction({
>     data: fullBytecode, // 合约的完整字节码
>     gasLimit: 1000000   // 设置gas限制
> });
> ```
>
> ### 5. 部署过程中的细节
> - **构造函数**：合约的构造函数在部署时会被调用，它在合约部署完成前只运行一次。
> - **字节码和初始化代码**：发送的交易数据中包含两个部分：合约字节码（即合约的逻辑）和初始化数据（如构造函数参数）。
> - **交易的结果**：部署成功后，新的合约地址将被生成，这个地址是基于发起交易者的地址和交易的nonce计算出来的。
>
> ### 总结
> 在以太坊上，合约部署是一种特殊交易，通过将合约的编译字节码发送到`0`地址完成。如果合约的构造函数有参数，则需要使用ABI编码工具将参数编码，并将其附加在字节码的尾部发送。这种标准化的编码方式确保了合约能够正确解析和接收构造函数的参数。



## 合约工厂

`ethers.js`创造了合约工厂`ContractFactory`类型，方便开发者部署合约。你可以利用合约`abi`，编译得到的字节码`bytecode`和签名者变量`signer`来创建合约工厂实例，为部署合约做准备。

```js
const contractFactory = new ethers.ContractFactory(abi, bytecode, signer);
```



**注意**：如果合约的构造函数有参数，那么在`abi`中必须包含构造函数。

在创建好合约工厂实例之后，可以调用它的`deploy`函数并传入合约构造函数的参数`args`来部署并获得合约实例：

```js
const contract = await contractFactory.deploy(args)
```



你可以利用下面两种命令，等待合约部署在链上确认，然后再进行交互。

```js
await contractERC20.waitForDeployment();
```



## 例子：部署ERC20代币合约

`ERC20`标准代币合约的介绍见WTF Solidity极简教程[第31讲 ERC20](https://github.com/AmazingAng/WTFSolidity/blob/main/31_ERC20/readme.md)。

1. 创建`provider`和`wallet`变量。

   ```js
   import { ethers } from "ethers";
   
   // 利用Alchemy的rpc节点连接以太坊网络
   // 连接goerli测试网
   const ALCHEMY_GOERLI_URL = 'https://eth-goerli.alchemyapi.io/v2/GlaeWuylnNM3uuOo-SAwJxuwTdqHaY5l';
   const provider = new ethers.JsonRpcProvider(ALCHEMY_GOERLI_URL);
   
   // 利用私钥和provider创建wallet对象
   const privateKey = '0x227dbb8586117d55284e26620bc76534dfbd2394be34cf4a09cb775d593b6f2b'
   const wallet = new ethers.Wallet(privateKey, provider)
   ```

   

2. 准备ERC20合约的字节码和ABI。因为ERC20的构造函数含有参数，因此我们必须把它包含在ABI中。合约的字节码可以从`remix`的编译面板中点击`Bytecode`按钮，把它复制下来，其中"object"字段对应的数据就是字节码。如果部署在链上的合约，你可以在etherscan的Contract页面的`Contract Creation Code`中找到。

   ```js
   // ERC20的人类可读abi
   const abiERC20 = [
       "constructor(string memory name_, string memory symbol_)",
       "function name() view returns (string)",
       "function symbol() view returns (string)",
       "function totalSupply() view returns (uint256)",
       "function balanceOf(address) view returns (uint)",
       "function transfer(address to, uint256 amount) external returns (bool)",
       "function mint(uint amount) external",
   ];
   // 填入合约字节码，在remix中，你可以在两个地方找到Bytecode
   // 1. 编译面板的Bytecode按钮
   // 2. 文件面板artifact文件夹下与合约同名的json文件中
   // 里面"bytecode"属性下的"object"字段对应的数据就是Bytecode，挺长的，608060起始
   // "object": "608060405260646000553480156100...
   const bytecodeERC20 = "60806040526012600560006101000a81548160ff021916908360ff1602179055503480156200002d57600080fd5b5060405162001166380380620011668339818101604052810190620000539190620001bb565b81600390805190602001906200006b9291906200008d565b508060049080519060200190620000849291906200008d565b505050620003c4565b8280546200009b90620002d5565b90600052602060002090601f016020900481019282620000bf57600085556200010b565b82601f10620000da57805160ff19168380011785556200010b565b828001600101855582156200010b579182015b828111156200010a578251825591602001919060010190620000ed565b5b5090506200011a91906200011e565b5090565b5b80821115620001395760008160009055506001016200011f565b5090565b6000620001546200014e8462000269565b62000240565b905082815260208101848484011115620001735762000172620003a4565b5b620001808482856200029f565b509392505050565b600082601f830112620001a0576200019f6200039f565b5b8151620001b28482602086016200013d565b91505092915050565b60008060408385031215620001d557620001d4620003ae565b5b600083015167ffffffffffffffff811115620001f657620001f5620003a9565b5b620002048582860162000188565b925050602083015167ffffffffffffffff811115620002285762000227620003a9565b5b620002368582860162000188565b9150509250929050565b60006200024c6200025f565b90506200025a82826200030b565b919050565b6000604051905090565b600067ffffffffffffffff82111562000287576200028662000370565b5b6200029282620003b3565b9050602081019050919050565b60005b83811015620002bf578082015181840152602081019050620002a2565b83811115620002cf576000848401525b50505050565b60006002820490506001821680620002ee57607f821691505b6020821081141562000305576200030462000341565b5b50919050565b6200031682620003b3565b810181811067ffffffffffffffff8211171562000338576200033762000370565b5b80604052505050565b7f4e487b7100000000000000000000000000000000000000000000000000000000600052602260045260246000fd5b7f4e487b7100000000000000000000000000000000000000000000000000000000600052604160045260246000fd5b600080fd5b600080fd5b600080fd5b600080fd5b6000601f19601f8301169050919050565b610d9280620003d46000396000f3fe608060405234801561001057600080fd5b50600436106100a95760003560e01c806342966c681161007157806342966c681461016857806370a082311461018457806395d89b41146101b4578063a0712d68146101d2578063a9059cbb146101ee578063dd62ed3e1461021e576100a9565b806306fdde03146100ae578063095ea7b3146100cc57806318160ddd146100fc57806323b872dd1461011a578063313ce5671461014a575b600080fd5b6100b661024e565b6040516100c39190610b02565b60405180910390f35b6100e660048036038101906100e19190610a14565b6102dc565b6040516100f39190610ae7565b60405180910390f35b6101046103ce565b6040516101119190610b24565b60405180910390f35b610134600480360381019061012f91906109c1565b6103d4565b6040516101419190610ae7565b60405180910390f35b610152610583565b60405161015f9190610b3f565b60405180910390f35b610182600480360381019061017d9190610a54565b610596565b005b61019e60048036038101906101999190610954565b61066d565b6040516101ab9190610b24565b60405180910390f35b6101bc610685565b6040516101c99190610b02565b60405180910390f35b6101ec60048036038101906101e79190610a54565b610713565b005b61020860048036038101906102039190610a14565b6107ea565b6040516102159190610ae7565b60405180910390f35b61023860048036038101906102339190610981565b610905565b6040516102459190610b24565b60405180910390f35b6003805461025b90610c88565b80601f016020809104026020016040519081016040528092919081815260200182805461028790610c88565b80156102d45780601f106102a9576101008083540402835291602001916102d4565b820191906000526020600020905b8154815290600101906020018083116102b757829003601f168201915b505050505081565b600081600160003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508273ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff167f8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925846040516103bc9190610b24565b60405180910390a36001905092915050565b60025481565b600081600160008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008282546104629190610bcc565b92505081905550816000808673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008282546104b79190610bcc565b92505081905550816000808573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020600082825461050c9190610b76565b925050819055508273ffffffffffffffffffffffffffffffffffffffff168473ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef846040516105709190610b24565b60405180910390a3600190509392505050565b600560009054906101000a900460ff1681565b806000803373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008282546105e49190610bcc565b9250508190555080600260008282546105fd9190610bcc565b92505081905550600073ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef836040516106629190610b24565b60405180910390a350565b60006020528060005260406000206000915090505481565b6004805461069290610c88565b80601f01602080910402602001604051908101604052809291908181526020018280546106be90610c88565b801561070b5780601f106106e05761010080835404028352916020019161070b565b820191906000526020600020905b8154815290600101906020018083116106ee57829003601f168201915b505050505081565b806000803373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008282546107619190610b76565b92505081905550806002600082825461077a9190610b76565b925050819055503373ffffffffffffffffffffffffffffffffffffffff16600073ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef836040516107df9190610b24565b60405180910390a350565b6000816000803373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020600082825461083a9190610bcc565b92505081905550816000808573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020600082825461088f9190610b76565b925050819055508273ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef846040516108f39190610b24565b60405180910390a36001905092915050565b6001602052816000526040600020602052806000526040600020600091509150505481565b60008135905061093981610d2e565b92915050565b60008135905061094e81610d45565b92915050565b60006020828403121561096a57610969610d18565b5b60006109788482850161092a565b91505092915050565b6000806040838503121561099857610997610d18565b5b60006109a68582860161092a565b92505060206109b78582860161092a565b9150509250929050565b6000806000606084860312156109da576109d9610d18565b5b60006109e88682870161092a565b93505060206109f98682870161092a565b9250506040610a0a8682870161093f565b9150509250925092565b60008060408385031215610a2b57610a2a610d18565b5b6000610a398582860161092a565b9250506020610a4a8582860161093f565b9150509250929050565b600060208284031215610a6a57610a69610d18565b5b6000610a788482850161093f565b91505092915050565b610a8a81610c12565b82525050565b6000610a9b82610b5a565b610aa58185610b65565b9350610ab5818560208601610c55565b610abe81610d1d565b840191505092915050565b610ad281610c3e565b82525050565b610ae181610c48565b82525050565b6000602082019050610afc6000830184610a81565b92915050565b60006020820190508181036000830152610b1c8184610a90565b905092915050565b6000602082019050610b396000830184610ac9565b92915050565b6000602082019050610b546000830184610ad8565b92915050565b600081519050919050565b600082825260208201905092915050565b6000610b8182610c3e565b9150610b8c83610c3e565b9250827fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff03821115610bc157610bc0610cba565b5b828201905092915050565b6000610bd782610c3e565b9150610be283610c3e565b925082821015610bf557610bf4610cba565b5b828203905092915050565b6000610c0b82610c1e565b9050919050565b60008115159050919050565b600073ffffffffffffffffffffffffffffffffffffffff82169050919050565b6000819050919050565b600060ff82169050919050565b60005b83811015610c73578082015181840152602081019050610c58565b83811115610c82576000848401525b50505050565b60006002820490506001821680610ca057607f821691505b60208210811415610cb457610cb3610ce9565b5b50919050565b7f4e487b7100000000000000000000000000000000000000000000000000000000600052601160045260246000fd5b7f4e487b7100000000000000000000000000000000000000000000000000000000600052602260045260246000fd5b600080fd5b6000601f19601f8301169050919050565b610d3781610c00565b8114610d4257600080fd5b50565b610d4e81610c3e565b8114610d5957600080fd5b5056fea2646970667358221220f87d0662c51e3b4b5e034fe8e1e7a10185cda3c246a5ba78e0bafe683d67789764736f6c63430008070033";
   ```

   

   

   ![Remix中获取字节码](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071529811.png)

   ![json](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071529905.jpeg)

   ![object](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071529435.jpeg)

   

3. 创建合约工厂`ContractFactory`实例。

   ```js
   const factoryERC20 = new ethers.ContractFactory(abiERC20, bytecodeERC20, wallet);
   ```

   

4. 调用工厂合约的`deploy()`函数并填入构造函数的参数（代币名称和代号），部署`ERC20`代币合约并获得合约实例。你可以利用：

   - `contract.target`获取合约地址，
   - `contract.deployTransaction`获取部署详情，
   - `contractERC20.waitForDeployment()`等待合约部署在链上确认。

   ```js
   // 1. 利用contractFactory部署ERC20代币合约
   console.log("\n1. 利用contractFactory部署ERC20代币合约")
   // 部署合约，填入constructor的参数
   const contractERC20 = await factoryERC20.deploy("WTF Token", "WTF")
   console.log(`合约地址: ${contractERC20.target}`);
   console.log("部署合约的交易详情")
   console.log(contractERC20.deploymentTransaction())
   console.log("\n等待合约部署上链")
   await contractERC20.waitForDeployment()
   // 也可以用 contractERC20.deployTransaction.wait()
   console.log("合约已上链")
   ```

   

   

   ![部署合约](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071529939.png)

   

5. 在合约上链后，调用`name()`和`symbol()`函数打印代币名称和代号，然后调用`mint()`函数给自己铸造`10,000`枚代币。

   ```js
   // 打印合约的name()和symbol()，然后调用mint()函数，给自己地址mint 10,000代币
   console.log("\n2. 调用mint()函数，给自己地址mint 10,000代币")
   console.log(`合约名称: ${await contractERC20.name()}`)
   console.log(`合约代号: ${await contractERC20.symbol()}`)
   let tx = await contractERC20.mint("10000")
   console.log("等待交易上链")
   await tx.wait()
   console.log(`mint后地址中代币余额: ${await contractERC20.balanceOf(wallet)}`)
   console.log(`代币总供给: ${await contractERC20.totalSupply()}`)
   ```

   

   

   ![铸造代币](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071529212.png)

   

6. 调用`transfer()`函数，给Vitalik转账`1,000`枚代币。

   ```js
   // 3. 调用transfer()函数，给Vitalik转账1000代币
   console.log("\n3. 调用transfer()函数，给Vitalik转账1,000代币")
   tx = await contractERC20.transfer("vitalik.eth", "1000")
   console.log("等待交易上链")
   await tx.wait()
   console.log(`Vitalik钱包中的代币余额: ${await contractERC20.balanceOf("vitalik.eth")}`)
   ```

   

   

   ![转账](https://www.wtf.academy/assets/images/6-4-e9c1732090db6a461529db190021aaac.png)

   

## 总结

这一讲我们介绍了ethers.js中的合约工厂`ContractFactory`类型，利用它部署了一个`ERC20`代币合约，并给Vitalik转账了`1,000`枚代币。

# 7. 检索事件

提示：本教程基于ethers.js 6.3.0 ，如果你使用的是v5，可以参考[ethers.js v5文档](https://docs.ethers.io/v5/)。

这一讲，我们将介绍如何使用`ethers.js`读取智能合约释放的事件。如果你不了解`Solidity`的事件，可以阅读WTF Solidity极简教程中[第12讲：事件](https://github.com/AmazingAng/WTFSolidity/blob/main/12_Event/readme.md)。

具体可参考[ethers.js文档](https://docs.ethers.org/v6/api/contract/#ContractEvent)。

## 事件 Event

智能合约释放出的事件存储于以太坊虚拟机的日志中。日志分为两个主题`topics`和数据`data`部分，其中事件哈希和`indexed`变量存储在`topics`中，作为索引方便以后搜索；没有`indexed`变量存储在`data`中，不能被直接检索，但可以存储更复杂的数据结构。

以ERC20代币中的`Transfer`转账事件为例，在合约中它是这样声明的：

```solidity
event Transfer(address indexed from, address indexed to, uint256 amount);
```



它共记录了3个变量`from`，`to`和`amount`，分别对应代币的发出地址，接收地址和转账数量，其中`from`和`to`前面带有`indexed`关键字。转账时，`Transfer`事件会被记录，可以在`etherscan`中[查到](https://rinkeby.etherscan.io/tx/0x8cf87215b23055896d93004112bbd8ab754f081b4491cb48c37592ca8f8a36c7)。



![Transfer事件](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071529891.png)



从上图中可以看到，`Transfer`事件被记录到了EVM的日志中，其中`Topics`包含3个数据，分别对应事件哈希，发出地址`from`，和接收地址`to`；而`Data`中包含一个数据，对应转账数额`amount`。

## 检索事件

我们可以利用`Ethers`中合约类型的`queryFilter()`函数读取合约释放的事件。

```js
const transferEvents = await contract.queryFilter('事件名', 起始区块, 结束区块)
```



`queryFilter()`包含3个参数，分别是事件名（必填），起始区块（选填），和结束区块（选填）。检索结果会以数组的方式返回。

**注意**：要检索的事件必须包含在合约的`abi`中。

## 例子：检索`WETH`合约中的`Transfer`事件

1. 创建`provider`。

   ```js
   import { ethers } from "ethers";
   // 利用Alchemy的rpc节点连接以太坊网络
   // 准备 alchemy API 可以参考https://github.com/AmazingAng/WTFSolidity/blob/main/Topics/Tools/TOOL04_Alchemy/readme.md 
   const ALCHEMY_GOERLI_URL = 'https://eth-goerli.alchemyapi.io/v2/GlaeWuylnNM3uuOo-SAwJxuwTdqHaY5l';
   const provider = new ethers.JsonRpcProvider(ALCHEMY_GOERLI_URL);
   ```

   

2. 创建包含检索事件的`abi`。

   ```js
   // WETH ABI，只包含我们关心的Transfer事件
   const abiWETH = [
       "event Transfer(address indexed from, address indexed to, uint amount)"
   ];
   ```

   

3. 声明`WETH`合约实例。

   ```js
   // 测试网WETH地址
   const addressWETH = '0xb4fbf271143f4fbf7b91a5ded31805e42b2208d6'
   // 声明合约实例
   const contract = new ethers.Contract(addressWETH, abiWETH, provider)
   ```

   

4. 获取过去10个区块内的`Transfer`事件，并打印出1个。我们可以看到，`topics`中有3个数据，对应事件哈希，`from`，和`to`；而`data`中只有一个数据`amount`。另外，`ethers`还会根据`ABI`自动解析事件，结果显示在`args`成员中。

   ```js
   // 获取当前的区块高度
   const block = await provider.getBlockNumber();
   console.log(`当前区块高度: ${block}`);
   
   // 获取过去 10 个区块内的 Transfer 事件
   const transferEvents = await contract.queryFilter('Transfer', block - 10, block);
   
   // 打印第一个 Transfer 事件
   console.log(`打印事件详情:`);
   console.log(transferEvents[0]);
   
   ```

   

   

   ![打印事件](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071530452.png)

   

5. 读取事件的解析结果。

   ```js
   /* 解析Transfer事件的数据（变量在args中）*/
   
   console.log("\n2. 解析事件：")
   const amount = ethers.formatUnits(ethers.getBigInt(transferEvents[0].args["amount"]), "ether");
   console.log(`地址 ${transferEvents[0].args["from"]} 转账${amount} WETH 到地址 ${transferEvents[0].args["to"]}`)
   ```
   
   > [!NOTE]
   >
   > 这一行代码用于提取和格式化 `Transfer` 事件中代表转账金额的 `amount`，并将其转换为人类可读的形式（以以太单位展示）。这里的代码分为几个步骤，逐步解释如下：
   >
   > ### 1. `transferEvents[0].args["amount"]`
   > - `transferEvents[0]` 是通过 `queryFilter` 获取的第一个 `Transfer` 事件对象。
   > - `args` 是事件对象的参数集合，它存储了 `Transfer` 事件的三个参数：`from`（发送者地址）、`to`（接收者地址）和 `amount`（转账金额）。
   > - `args["amount"]` 直接提取了转账的金额，这是一个大整数（BigInt），表示以最小单位（wei）为单位的金额。
   >
   > ### 2. `ethers.getBigInt(transferEvents[0].args["amount"])`
   > - `ethers.getBigInt()` 将传入的值转换为 `BigInt` 类型，确保它可以被正确处理。因为以太坊上的金额通常以 `wei`（最小单位）表示，`BigInt` 是处理大数的常用类型。
   >
   > ### 3. `ethers.formatUnits(..., "ether")`
   > - `ethers.formatUnits` 用于将 `BigInt` 格式的数值转换为人类可读的单位。在以太坊中，1 `ether` = \(10^{18}\) `wei`。
   > - 第二个参数 `"ether"` 表示将该金额从 `wei` 单位转换为 `ether`，即以太坊的主要单位。这样可以使金额显示为浮点数形式，而不是一个超大整数。
   >
   > ### 代码含义总结
   > ```js
   > const amount = ethers.formatUnits(ethers.getBigInt(transferEvents[0].args["amount"]), "ether");
   > ```
   > 这行代码的作用是：
   > 1. 从 `Transfer` 事件中提取转账金额（以 `wei` 为单位）。
   > 2. 将其转换为 `BigInt` 类型，确保可以处理大数。
   > 3. 使用 `formatUnits` 函数，将金额从 `wei` 转换为 `ether` 单位。
   > 4. 最终得到一个格式化后的转账金额，并以以太（ether）单位展示。
   >
   > ### 举例
   > 如果 `amount` 是 `1000000000000000000` `wei`，即 1 `ether`，该代码将会把它转换为 `1.0` `ether` 并返回。
   
   
   
   ![解析事件](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071529325.png)
   
   

## 总结

这一讲，我们回顾了`Solidity`中的事件，并介绍如何用`ethers`检索智能合约释放的事件。要注意的一点：要检索的事件必须包含在合约`abi`中。

# 8. 监听合约事件

提示：本教程基于ethers.js 6.3.0 ，如果你使用的是v5，可以参考[ethers.js v5文档](https://docs.ethers.io/v5/)。

这一讲，我们将介绍如何监听合约，并实现监听USDT合约的`Transfer`事件。

具体可参考[ethers.js文档](https://docs.ethers.org/v6/api/contract/#ContractEvent)。

## 监听合约事件

### `contract.on`

在`ethersjs`中，合约对象有一个`contract.on`的监听方法，让我们持续监听合约的事件：

```js
contract.on("eventName", function)
```



`contract.on`有两个参数，一个是要监听的事件名称`"eventName"`，需要包含在合约`abi`中；另一个是我们在事件发生时调用的函数。

### `contract.once`

合约对象有一个`contract.once`的监听方法，让我们只监听一次合约释放事件，它的参数与`contract.on`一样：

```js
contract.once("eventName", function)
```



## 监听`USDT`合约

1. 声明`provider`：Alchemy是一个免费的ETH节点提供商。需要先申请一个，后续会用到。你可以参考这篇攻略来申请Alchemy API[Solidity极简入门-工具篇4：Alchemy](https://github.com/AmazingAng/WTFSolidity/blob/main/Topics/Tools/TOOL04_Alchemy/readme.md)

   ```js
   import { ethers } from "ethers";
   // 准备 alchemy API  
   // 可以参考https://github.com/AmazingAng/WTFSolidity/blob/main/Topics/Tools/TOOL04_Alchemy/readme.md 
   const ALCHEMY_MAINNET_URL = 'https://eth-mainnet.g.alchemy.com/v2/oKmOQKbneVkxgHZfibs-iFhIlIAl6HDN';
   // 连接主网 provider
   const provider = new ethers.JsonRpcProvider(ALCHEMY_MAINNET_URL);
   ```

   

2. 声明合约变量：我们只关心`USDT`合约的`Transfer`事件，把它填入到`abi`中就可以。如果你关心其他函数和事件的话，可以在[etherscan](https://etherscan.io/address/0xdac17f958d2ee523a2206206994597c13d831ec7#code)上找到。

   ```js
   // USDT的合约地址
   const contractAddress = '0xdac17f958d2ee523a2206206994597c13d831ec7'
   // 构建USDT的Transfer的ABI
   const abi = [
     "event Transfer(address indexed from, address indexed to, uint value)"
   ];
   // 生成USDT合约对象
   const contractUSDT = new ethers.Contract(contractAddress, abi, provider);
   ```

   

3. 利用`contract.once()`函数，监听一次`Transfer`事件，并打印结果。

   ```js
     // 只监听一次
     console.log("\n1. 利用contract.once()，监听一次Transfer事件");
     contractUSDT.once('Transfer', (from, to, value)=>{
       // 打印结果
       console.log(
         `${from} -> ${to} ${ethers.formatUnits(ethers.getBigInt(value),6)}`
       )
     })
   ```

   

   

   ![只监听一次](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071530174.png)

   

4. 利用`contract.on()`函数，持续监听`Transfer`事件，并打印结果。

   ```js
     // 持续监听USDT合约
     console.log("\n2. 利用contract.on()，持续监听Transfer事件");
     contractUSDT.on('Transfer', (from, to, value)=>{
       console.log(
        // 打印结果
        `${from} -> ${to} ${ethers.formatUnits(ethers.getBigInt(value),6)}`
       )
     })
   ```

   

   

   ![持续监听](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071530903.png)

   > [!TIP]
   >
   > ### 1. 利用 `contract.once()` 函数监听一次 `Transfer` 事件
   >
   > `contract.once()` 函数用于监听特定事件，但只在事件第一次发生时触发回调函数，之后监听会自动取消。下面的代码展示了如何使用 `contract.once()` 监听一次 `Transfer` 事件并打印相关数据。
   >
   > ```js
   > // 只监听一次
   > console.log("\n1. 利用 contract.once()，监听一次 Transfer 事件");
   > contractUSDT.once('Transfer', (from, to, value) => {
   >     // 打印结果
   >     console.log(
   >         `${from} -> ${to} ${ethers.formatUnits(ethers.getBigInt(value), 6)}`
   >     );
   > });
   > ```
   >
   > - **解释**：
   >   - `contractUSDT.once('Transfer', ...)`：监听 `USDT` 合约的 `Transfer` 事件，只触发一次。
   >   - `(from, to, value)`：这三个参数分别代表发送者地址 (`from`)、接收者地址 (`to`) 和转账金额 (`value`)。
   >   - `ethers.formatUnits(ethers.getBigInt(value), 6)`：将 `value` 从 `BigInt` 转换为带有 6 位小数的单位格式（USDT 通常为 6 位小数）。
   >   - 当事件发生时，会输出类似 `"0xSenderAddress -> 0xReceiverAddress 100.0"` 的结果。
   >
   > ![监听一次](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071530174.png)
   >
   > ### 2. 利用 `contract.on()` 函数持续监听 `Transfer` 事件
   >
   > `contract.on()` 函数用于持续监听特定事件，每当事件触发时都会执行回调函数。
   >
   > ```js
   > // 持续监听 USDT 合约
   > console.log("\n2. 利用 contract.on()，持续监听 Transfer 事件");
   > contractUSDT.on('Transfer', (from, to, value) => {
   >     console.log(
   >         `${from} -> ${to} ${ethers.formatUnits(ethers.getBigInt(value), 6)}`
   >     );
   > });
   > ```
   >
   > - **解释**：
   >   - `contractUSDT.on('Transfer', ...)`：监听 `Transfer` 事件，并在每次事件触发时执行回调函数。
   >   - 该监听器不会自动取消，因此可以持续获取和处理每次 `Transfer` 事件的数据。
   >
   > 这两种方式分别适用于只监听一次事件和需要持续监听的场景，能够帮助你根据不同需求获取实时的链上转账事件。
   
   

## 总结

这一讲，我们介绍了`ethers`中最简单的链上监听功能，`contract.on()`和`contract.once()`。通过上述方法，可以你可以监听指定合约的指定事件。

# 9. 事件过滤

在上一讲 [Ethers极简入门: 8. 合约监听](https://github.com/WTFAcademy/WTFEthers/tree/main/08_ContractListener) 的基础上，我们拓展一下，在监听的过程中增加过滤器，监听指定地址的转入转出。

具体可参考[ethers.js文档](https://docs.ethers.io/v5/concepts/events)。

## 过滤器

当合约创建日志（释放事件）时，它最多可以包含[4]条数据作为索引（`indexed`）。索引数据经过哈希处理并包含在[布隆过滤器](https://en.wikipedia.org/wiki/Bloom_filter)中，这是一种允许有效过滤的数据结构。因此，一个事件过滤器最多包含`4`个主题集，每个主题集是个条件，用于筛选目标事件。规则：

- 如果一个主题集为`null`，则该位置的日志主题不会被过滤，任何值都匹配。
- 如果主题集是单个值，则该位置的日志主题必须与该值匹配。
- 如果主题集是数组，则该位置的日志主题至少与数组中其中一个匹配。



![过滤器规则](https://www.wtf.academy/assets/images/9-1-4273780b5cd8a46c30cc3fa2b0d174d5.png)

> [!NOTE]
>
> 布隆过滤器（Bloom Filter）是一种**空间高效的概率性数据结构**，用于判断某个元素是否存在于一个集合中。布隆过滤器可以确定某个元素"可能存在"或"一定不存在"，但它**不会产生假阴性**，也就是说，如果它判断元素不存在，那一定是真的不存在；但它可能产生假阳性，即某些情况下可能会错误地判断元素存在。
>
> ### 布隆过滤器的工作原理
> 布隆过滤器的核心是一个**位数组**和一组**哈希函数**：
>
> 1. **位数组**：这是一个长度为 `m` 的位数组，初始时，数组中的每个元素都是 0。
>
> 2. **哈希函数**：有 `k` 个独立的哈希函数，每个函数会把输入映射到位数组的某个位置。
>
> #### 元素插入
> 要将一个元素插入布隆过滤器时，使用 `k` 个哈希函数分别计算该元素的哈希值，并将哈希值对应的数组位置置为 1。每个哈希函数会映射到位数组中的某个索引位置，多个哈希函数可能会映射到同一个索引。
>
> #### 元素查询
> 要检查一个元素是否存在于布隆过滤器时，再次使用同样的 `k` 个哈希函数计算这个元素的哈希值，然后检查这些位置上的值。如果所有的哈希值对应的位都是 1，则判断该元素"可能存在"；如果至少有一个位为 0，则该元素"一定不存在"。
>
> ### 布隆过滤器的特点
> - **空间效率高**：布隆过滤器的空间复杂度远小于传统的哈希表或集合，因此在存储大量数据时非常节省内存。
> - **快速查询**：插入和查询操作的时间复杂度都是常数（`O(k)`，`k` 是哈希函数的个数），因此布隆过滤器适合高效查询操作。
> - **无误报的不存在判断**：如果布隆过滤器告诉你某个元素不存在，那是确定的；如果告诉你某个元素存在，则有可能是错误的（假阳性）。
>
> ### 布隆过滤器的应用场景
> 由于它的高效性和概率性特点，布隆过滤器常用于以下场景：
>
> 1. **网页缓存**：可以用布隆过滤器快速判断网页是否已经缓存，减少不必要的磁盘读取或网络请求。
>    
> 2. **垃圾邮件检测**：用来判断某个邮件地址或域名是否在黑名单中，从而加快垃圾邮件过滤的速度。
>
> 3. **区块链**：例如在以太坊的事件过滤中，使用布隆过滤器来高效筛选事件日志，通过哈希匹配过滤出目标事件。
>
> 4. **数据库查询优化**：布隆过滤器可以用于快速判断数据是否在某个数据库中，以避免执行昂贵的数据库查询操作。
>
> ### 布隆过滤器的局限
> - **假阳性**：它可能会告诉你某个元素存在于集合中，但实际上这个元素并不存在。
> - **无法删除元素**：一旦元素被插入布隆过滤器，就无法将其删除，因为多个元素可能会共享同一个哈希位置，删除会导致其他元素的错误判断。
>
> 总结来说，布隆过滤器是一种空间和时间效率非常高的结构，适用于对内存和计算资源要求较高的场景，尤其适合大量数据的存在性查询。



## 构建过滤器

`ethers.js`中的合约类提供了`contract.filters`来简化过滤器的创建：

```js
const filter = contract.filters.EVENT_NAME( ...args ) 
```



其中`EVENT_NAME`为要过滤的事件名，`..args`为主题集/条件。前面的规则有一点抽象，下面举几个例子。

1. 过滤来自`myAddress`地址的`Transfer`事件

   ```js
   contract.filters.Transfer(myAddress)
   ```

   

2. 过滤所有发给 `myAddress`地址的`Transfer`事件

   ```js
   contract.filters.Transfer(null, myAddress)
   ```

   

3. 过滤所有从 `myAddress`发给`otherAddress`的`Transfer`事件

   ```js
   contract.filters.Transfer(myAddress, otherAddress)
   ```

   

4. 过滤所有发给`myAddress`或`otherAddress`的`Transfer`事件

   ```js
   contract.filters.Transfer(null, [ myAddress, otherAddress ])
   ```

   

## 监听交易所的USDT转账

1. 从币安交易所转出USDT的交易

   监听USDT合约之前，我们需要先看懂交易日志`Logs`，包括事件的`topics`和`data`。我们先找到一笔从币安交易所转出USDT的交易，然后通过hash在etherscan查它的详情：

   交易哈希：[0xab1f7b575600c4517a2e479e46e3af98a95ee84dd3f46824e02ff4618523fff5](https://etherscan.io/tx/0xab1f7b575600c4517a2e479e46e3af98a95ee84dd3f46824e02ff4618523fff5)

   

   ![etherscan 示意图](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071530632.png)

   

   该交易做了一件事：从 `binance14` （币安热钱包）向地址`0x354de44bedba213d612e92d3248b899de17b0c58` 转账`2983.98`USDT。

   查看该事件日志`Logs`信息：

   

   ![etherscan logs示意图](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071530735.png)

   

- `address`：USDT合约地址
- `topics[0]`：事件哈希，`keccak256("Transfer(address,address,uint256)")`
- `topics[1]`：转出地址（币安交易所热钱包）。
- `topics[2]` 转入地址。
- `data`：转账数量。

1. 创建`provider`，`abi`，和`USDT`合约变量：

   ```js
   const provider = new ethers.JsonRpcProvider(ALCHEMY_MAINNET_URL);
   // 合约地址
   const addressUSDT = '0xdac17f958d2ee523a2206206994597c13d831ec7'
   // 交易所地址
   const accountBinance = '0x28C6c06298d514Db089934071355E5743bf21d60'
   // 构建ABI
   const abi = [
     "event Transfer(address indexed from, address indexed to, uint value)",
     "function balanceOf(address) public view returns(uint)",
   ];
   // 构建合约对象
   const contractUSDT = new ethers.Contract(addressUSDT, abi, provider);
   ```

   

2. 读取币安热钱包USDT余额。可以看到，当前币安热钱包有8亿多枚USDT

   ```js
   const balanceUSDT = await contractUSDT.balanceOf(accountBinance)
   console.log(`USDT余额: ${ethers.formatUnits(balanceUSDT,6)}\n`)
   ```

   

   

   ![币安热钱包USDT余额](data:image/png;base64,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)

   

3. 创建过滤器，监听`USDT`转入币安的事件。

   ```js
   // 2. 创建过滤器，监听转移USDT进交易所
   console.log("\n2. 创建过滤器，监听USDT转进交易所")
   let filterBinanceIn = contractUSDT.filters.Transfer(null, accountBinance);
   console.log("过滤器详情：")
   console.log(filterBinanceIn);
   contractUSDT.on(filterBinanceIn, (res) => {
     console.log('---------监听USDT进入交易所--------');
     console.log(
       `${res.args[0]} -> ${res.args[1]} ${ethers.formatUnits(res.args[2],6)}`
     )
   })
   ```

   > [!TIP]
   >
   > `let filterBinanceIn = contractUSDT.filters.Transfer(null, accountBinance);`这个过滤器专门用于监听USDT转入指定交易所（`accountBinance`）的事件。
   >
   > `contractUSDT.on(filterBinanceIn, callback)`：持续监听满足过滤器条件的事件。每当有符合条件的`Transfer`事件发生时，回调函数会被调用。
   >
   > 回调函数中的参数`res`是事件的结果，其中：
   >
   > - `res.args[0]`：发送方地址（`from`）。
   > - `res.args[1]`：接收方地址（`to`），应该是`accountBinance`。
   > - `res.args[2]`：转账的数量。
   >
   > `ethers.formatUnits(res.args[2], 6)`：将USDT的数量格式化为带有6位小数的字符串，因为USDT的最小单位是`10^6`。

   

   ![监听转入币安的USDT交易](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071530085.png)

   

2. 创建过滤器，监听`USDT`转出币安的交易。

   ```js
     // 3. 创建过滤器，监听交易所转出USDT
     let filterToBinanceOut = contractUSDT.filters.Transfer(accountBinance);
     console.log("\n3. 创建过滤器，监听USDT转出交易所")
     console.log("过滤器详情：")
     console.log(filterToBinanceOut);
     contractUSDT.on(filterToBinanceOut, (res) => {
       console.log('---------监听USDT转出交易所--------');
       console.log(
         `${res.args[0]} -> ${res.args[1]} ${ethers.formatUnits(res.args[2],6)}`
       )
     }
     );
   ```

   

   

   ![监听转出币安的USDT交易](https://www.wtf.academy/assets/images/9-6-a874f8824417a31f75a34a0458703c4a.png)

   

## 总结

这一讲，我们介绍了事件过滤器，并用它监听了与币安交易所热钱包相关的`USDT`交易。你可以用它监听任何你感兴趣的交易，发现`smart money`做了哪些新交易，`NFT`大佬冲了哪些新项目，等等。

# 10. BigInt和单位转换

提示：本教程基于ethers.js 6.3.0 ，如果你使用的是v5，可以参考[ethers.js v5文档](https://docs.ethers.io/v5/)。

这一讲，我们介绍`BigInt`类和单位转换。

## `BigInt`

以太坊中，许多计算都对超出`JavaScript`整数的安全值（js中最大安全整数为`9007199254740991`）。因此，`ethers.js`使用 JavaScript ES2020 版本原生的 `BigInt` 类 安全地对任何数量级的数字进行数学运算。在`ethers.js`中，大多数需要返回值的操作将返回 `BigInt`，而接受值的参数也会接受它们。

### 创建`BigInt`实例

你可以利用`ethers.getBigInt()`函数将`string`，`number`等类型转换为`BigInt`。

**注意**，超过js最大安全整数的数值将不能转换。

```js
const oneGwei = ethers.getBigInt("1000000000"); // 从十进制字符串生成
console.log(oneGwei)
console.log(ethers.getBigInt("0x3b9aca00")) // 从hex字符串生成
console.log(ethers.getBigInt(1000000000)) // 从数字生成
// 不能从js最大的安全整数之外的数字生成BigNumber，下面代码会报错
// ethers.getBigInt(Number.MAX_SAFE_INTEGER);
console.log("js中最大安全整数：", Number.MAX_SAFE_INTEGER)
```

> [!TIP]
>
> 这段代码展示了如何使用 `ethers.getBigInt` 方法生成 `BigInt` 对象，这在以太坊开发中非常有用，特别是在处理大数值时，比如 wei、gwei 等。下面对代码中的每个部分进行详细解释：
>
> ### 1. 从十进制字符串生成
>
> ```javascript
> const oneGwei = ethers.getBigInt("1000000000"); // 从十进制字符串生成
> console.log(oneGwei);
> ```
>
> - **解释**：
>   - 这里使用 `ethers.getBigInt("1000000000")` 从字符串 `"1000000000"` 创建了一个 `BigInt` 对象，表示 1 Gwei（即 10^9 wei）。
>   - 输出结果为 `1000000000n`，其中 `n` 表示这是一个 `BigInt` 类型。
>
> ### 2. 从十六进制字符串生成
>
> ```javascript
> console.log(ethers.getBigInt("0x3b9aca00")); // 从hex字符串生成
> ```
>
> - **解释**：
>   - `ethers.getBigInt("0x3b9aca00")` 从十六进制字符串生成了一个 `BigInt`。`0x3b9aca00` 等于十进制的 `1000000000`。
>   - 输出结果同样为 `1000000000n`。
>
> ### 3. 从数字生成
>
> ```javascript
> console.log(ethers.getBigInt(1000000000)); // 从数字生成
> ```
>
> - **解释**：
>   - `ethers.getBigInt(1000000000)` 直接从数字 `1000000000` 创建了一个 `BigInt` 对象。
>   - 输出结果仍为 `1000000000n`。
>
> ### 4. 最大安全整数
>
> ```javascript
> // 不能从js最大的安全整数之外的数字生成BigNumber，下面代码会报错
> // ethers.getBigInt(Number.MAX_SAFE_INTEGER);
> console.log("js中最大安全整数：", Number.MAX_SAFE_INTEGER);
> ```
>
> - **解释**：
>   - `Number.MAX_SAFE_INTEGER` 是 JavaScript 中能够安全使用的最大整数值（`2^53 - 1`，即 `9007199254740991`）。超出这个范围的整数在计算时可能会出现精度丢失。
>   - 注释的代码行 `ethers.getBigInt(Number.MAX_SAFE_INTEGER)` 如果取消注释，将会抛出错误，因为它尝试从超出 JavaScript 最大安全整数范围的值生成 `BigInt`。
>
> ### 总结
> - `ethers.getBigInt` 是处理以太坊数值（特别是 wei 和 gwei）的重要工具，可以从字符串、十六进制和数字生成 `BigInt`。
> - 需要注意的是，使用超出 JavaScript 最大安全整数范围的数值时，会导致错误，因此在处理较大的数值时要特别小心。



![BigNumber](https://www.wtf.academy/assets/images/10-1-79a176b4005ae95d15b14d9283691130.png)



### `BigInt`运算

`BigInt`支持很多运算，例如加减乘除、取模`mod`，幂运算`pow`，绝对值`abs`等运算:

> 注意：数值带后缀`n`会自动转换成`BigInt`

```js
// 运算
console.log("加法：", oneGwei + 1n)
console.log("减法：", oneGwei - 1n)
console.log("乘法：", oneGwei * 2n)
console.log("除法：", oneGwei / 2n)
// 比较
console.log("是否相等：", oneGwei == 1000000000n)
```

![BigNumber运算](https://www.wtf.academy/assets/images/10-2-639632e68b961a56f26f6b4bcec92f44.png)



## 单位转换

在以太坊中，`1 ether`等于`10^18 wei`。下面列出了一些常用的单位：



![常用单位](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071530500.png)



在应用中，我们经常将数值在用户可读的字符串（以`ether`为单位）和机器可读的数值（以`wei`为单位）之间转换。例如，钱包可以为用户界面指定余额（以`ether`为单位）和`gas`价格（以`gwei`为单位），但是在发送交易时，两者都必须转换成以`wei`为单位的数值。`ethers.js`提供了一些功能函数，方便这类转换。

- `formatUnits(变量, 单位)`：格式化，小单位转大单位，比如`wei` -> `ether`，在显示余额时很有用。参数中，单位填位数（数字）或指定的单位（字符串）。

  ```js
  //代码参考：https://docs.ethers.org/v6/api/utils/#about-units
  console.group('\n2. 格式化：小单位转大单位，formatUnits');
  console.log(ethers.formatUnits(oneGwei, 0));
  // '1000000000'
  console.log(ethers.formatUnits(oneGwei, "gwei"));
  // '1.0'
  console.log(ethers.formatUnits(oneGwei, 9));
  // '1.0'
  console.log(ethers.formatUnits(oneGwei, "ether"));
  // `0.000000001`
  console.log(ethers.formatUnits(1000000000, "gwei"));
  // '1.0'
  console.log(ethers.formatEther(oneGwei));
  // `0.000000001` 等同于formatUnits(value, "ether")
  console.groupEnd();
  ```

  > [!NOTE]
  >
  > `console.log(ethers.formatUnits(oneGwei, 0))`：当你使用 `0` 作为第二个参数时，表示你希望结果为整数，且不保留任何小数位。

  

  ![formatUnits](https://www.wtf.academy/assets/images/10-4-3bb9285d14f5174b1a4665ea72994f95.png)

  

- `parseUnits`：解析，大单位转小单位，比如`ether` -> `wei`，在将用户输入的值转为`wei`为单位的数值很有用。参数中，单位填位数（数字）或指定的单位（字符串）。

  ```js
  // 3. 解析：大单位转小单位
  // 例如将ether转换为wei：parseUnits(变量, 单位),parseUnits默认单位是 ether
  // 代码参考：https://docs.ethers.org/v6/api/utils/#about-units
  console.group('\n3. 解析：大单位转小单位，parseUnits');
  console.log(ethers.parseUnits("1.0").toString());
  // { BigNumber: "1000000000000000000" }
  console.log(ethers.parseUnits("1.0", "ether").toString());
  // { BigNumber: "1000000000000000000" }
  console.log(ethers.parseUnits("1.0", 18).toString());
  // { BigNumber: "1000000000000000000" }
  console.log(ethers.parseUnits("1.0", "gwei").toString());
  // { BigNumber: "1000000000" }
  console.log(ethers.parseUnits("1.0", 9).toString());
  // { BigNumber: "1000000000" }
  console.log(ethers.parseEther("1.0").toString());
  // { BigNumber: "1000000000000000000" } 等同于parseUnits(value, "ether")
  console.groupEnd();
  ```

  

  

  ![parseUnits](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071530264.png)

  

## 总结

这一讲，我们介绍了`BigNumber`类，以太坊中的常用单位，以及单位转换。

# 11. StaticCall

这一讲，我们介绍合约类的`staticCall`方法，在发送交易之前检查交易是否会失败，节省大量gas。

`staticCall`方法是属于`ethers.Contract`类的编写方法分析，同类的还有`populateTransaction`和`estimateGas`方法。

## 可能失败的交易

在以太坊上发交易需要付昂贵的`gas`，并且有失败的风险，发送失败的交易并不会把`gas`返还给你。因此，在发送交易前知道哪些交易可能会失败非常重要。如果你用过`metamask`小狐狸钱包，那对下图不会陌生。



![你的交易可能失败！](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071531009.png)



如果你的交易将失败，小狐狸会告诉你`this transaction may fail`，翻译过来就是“这笔交易可能失败”。当用户看到这个红字提示，就知道要取消这笔交易了，除非他想尝尝失败的滋味。

它是怎么做到的呢？这是因为以太坊节点有一个`eth_call`方法，让用户可以模拟一笔交易，并返回可能的交易结果，但不真正在区块链上执行它（交易不上链）。

## `staticCall`

在 ethers.js 中，你可以使用 `contract.函数名.staticCall()` 方法来模拟执行一个可能会改变状态的函数，但不实际向区块链提交这个状态改变。这相当于调用以太坊节点的 `eth_call`。这通常用于模拟状态改变函数的结果。如果函数调用成功，它将返回函数本身的返回值；如果函数调用失败，它将抛出异常。

请注意，这种调用适用于任何函数，无论它在智能合约中是标记为 view/pure 还是普通的状态改变函数。它使你能够安全地预测状态改变操作的结果，而不实际执行这些操作。

```js
    const tx = await contract.函数名.staticCall( 参数, {override})
    console.log(`交易会成功吗？：`, tx)
```



- 函数名：为模拟调用的函数名。
- 参数：调用函数的参数。
- {override}：选填，可包含以下参数：
  - `from`：执行时的`msg.sender`，也就是你可以模拟任何一个人的调用，比如Vitalik。
  - `value`：执行时的`msg.value`。
  - `blockTag`：执行时的区块高度。
  - `gasPrice`
  - `gasLimit`
  - `nonce`

## 用`staticCall`模拟`DAI`转账

1. 创建`provider`和`wallet`对象。

   ```js
   import { ethers } from "ethers";
   
   //准备 alchemy API 可以参考https://github.com/AmazingAng/WTFSolidity/blob/main/Topics/Tools/TOOL04_Alchemy/readme.md 
   const ALCHEMY_MAINNET_URL = 'https://eth-mainnet.g.alchemy.com/v2/oKmOQKbneVkxgHZfibs-iFhIlIAl6HDN';
   const provider = new ethers.JsonRpcProvider(ALCHEMY_MAINNET_URL);
   
   // 利用私钥和provider创建wallet对象
   const privateKey = '0x227dbb8586117d55284e26620bc76534dfbd2394be34cf4a09cb775d593b6f2b'
   const wallet = new ethers.Wallet(privateKey, provider)
   ```

   

2. 创建`DAI`合约对象，注意，这里生成合约时要用`provider`而不是`wallet`，不然则不能更改`staticCall`方法中的`from`参数（可能是bug，也可能是feature）。

   ```js
   // DAI的ABI
   const abiDAI = [
       "function balanceOf(address) public view returns(uint)",
       "function transfer(address, uint) public returns (bool)",
   ];
   // DAI合约地址（主网）
   const addressDAI = '0x6B175474E89094C44Da98b954EedeAC495271d0F' // DAI Contract
   // 创建DAI合约实例
   const contractDAI = new ethers.Contract(addressDAI, abiDAI, provider)
   ```

   

3. 查看钱包中`DAI`余额，为0。

   ```js
   const address = await wallet.getAddress()
   console.log("\n1. 读取测试钱包的DAI余额")
   const balanceDAI = await contractDAI.balanceOf(address)
   console.log(`DAI持仓: ${ethers.formatEther(balanceDAI)}\n`)
   ```

   

   

   ![钱包DAI余额](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA1MAAAA8CAYAAACD8uCOAAABQ2lDQ1BJQ0MgUHJvZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8bAycAMFNRnkE1MLi5wDAjwAfIYYDQq+HaNgRFEX9YFmWX8fZrZzpXLOv8kWWStvjN3LqZ6FMCVklqcDKT/AHFackFRCQMDYwqQrVxeUgBidwDZIkVARwHZc0DsdAh7A4idBGEfAasJCXIGsm8A2QLJGYlAMxhfANk6SUji6UhsqL0gwBPg4aNgZG7mauHmRcC5pIOS1IoSEO2cX1BZlJmeUaLgCAylVAXPvGQ9HQUjAyMjBgZQmENUf74BDktGMQ6EWDMQW68HCpYjxPzdGRi2TgN6ox8hptLPwMC3i4HhoHpBYlEi3AGM31iK04yNIGzu7QwMrNP+//8czsDArsnA8Pf6//+/t////3cZAwPzLQaGA98AVkRgn2S00RsAAABWZVhJZk1NACoAAAAIAAGHaQAEAAAAAQAAABoAAAAAAAOShgAHAAAAEgAAAESgAgAEAAAAAQAAA1OgAwAEAAAAAQAAADwAAAAAQVNDSUkAAABTY3JlZW5zaG90PqLsRgAAAdVpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IlhNUCBDb3JlIDYuMC4wIj4KICAgPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4KICAgICAgPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIKICAgICAgICAgICAgeG1sbnM6ZXhpZj0iaHR0cDovL25zLmFkb2JlLmNvbS9leGlmLzEuMC8iPgogICAgICAgICA8ZXhpZjpQaXhlbFlEaW1lbnNpb24+NjA8L2V4aWY6UGl4ZWxZRGltZW5zaW9uPgogICAgICAgICA8ZXhpZjpQaXhlbFhEaW1lbnNpb24+ODUxPC9leGlmOlBpeGVsWERpbWVuc2lvbj4KICAgICAgICAgPGV4aWY6VXNlckNvbW1lbnQ+U2NyZWVuc2hvdDwvZXhpZjpVc2VyQ29tbWVudD4KICAgICAgPC9yZGY6RGVzY3JpcHRpb24+CiAgIDwvcmRmOlJERj4KPC94OnhtcG1ldGE+Cpx4/R0AABpVSURBVHgB7Z15vE3V+8cXzSNJqIQkqZAMRUlJJCUllAZTRFRCpWi4SEVmlSEyJClTJSkSpQyFlwYZooSSkhCVsd99P6/W+e27nXPvuZP7ve7neb2Oe84+a6299nufP/bH51nPylW4cOF/nUIEREAEREAEREAEREAEREAERCBVBHKnqrUai4AIiIAIiIAIiIAIiIAIiIAIGAGJKf0QREAEREAEREAEREAEREAERCANBCSm0gBNXURABERABERABERABERABERAYkq/AREQAREQAREQAREQAREQARFIAwGJqTRAUxcREAEREAEREAEREAEREAERkJjSb0AEREAEREAEREAEREAEREAE0kBAYioN0NRFBERABERABERABERABERABCSm9BsQAREQAREQAREQAREQAREQgTQQkJhKAzR1EQEREAEREAEREAEREAEREAGJKf0GREAEREAEREAEREAEREAERCANBCSm0gBNXURABERABERABERABERABERAYkq/AREQAREQAREQAREQAREQARFIA4HDUkwdeeSRaUCRM7vkzn1Y/gRy5s3UVYuACIiACIiACIiACBxSAkecfPLJCYf0jBlwsjPPPNN17NjRLVq0yO3bty/JiGeddZYbOnSo++CDD9yePXuSfMeHAgUKuBtuuMGVLl36oFehQoXcDz/8cFCf4AGEWps2bdw333xj5y5fvrwrXLiwY07+tWnTpkiXF154wf31119u3bp1kWNnn32269Spk/vss8/c/v37I8f9m3bt2rnbb7/d3XLLLfb9d99957+K/O3fv79jnMWLF0eO8SYhIcFVq1bNXXHFFa5KlSp2jiQNAh8uuOACN2jQILdy5Ur366+/Br5J+W3i78a98sor7quvvnJbt261Drly5XLjxo2zz8HrTXm0zG1x/PHHu+eee87dddddjnuzcePGFE943HHHuTFjxrjt27dHfhP8ZipXruzOO++8JC/uf0q/mxRPqAYiIAIiIAIiIAIiIALZjkCmWThHHXWUa9SokStbtqxbtmyZe/311zMMDmOfe+65bvDgwe7hhx92lSpVci1atLDxeaDn9fLLL7t///3XjiEYFixYYO/POOMMV7t2bccD9q5du9yBAwccD85HHHGE27lzp7vqqqusXfAf5v7tt9/aIUQEIgURhaB75JFHTPAwDnH00Ue7e+65x3Xp0sX16tXL5cmTx51wwgn2XfCf4sWLuwEDBtgY//zzT/Arh2DjGqdMmeKaNWvmVqxYkeRhvVixYo7r4EGfa6H/3LlzbYxjjjnG/jLnrl27moB49dVXk4zvP9x3333G6uKLL3blypXzh5P8/fHHH928efOSHOPDZZddZszWrl0b+Q4mzPvrr7+OHAu/yZs3r3vyySftMPNG2Hz88cdu+fLl4abu/vvvN8EIh08//TTyfatWrdz5558f+ezfIOSWLl3qP9pffiecD9G6evVq16FDB/fRRx+5YcOGJWnnP3B/27dv7z8aP66V4PdRpkwZe889Razv3bvX/f3332727Nl2XP+IgAiIgAiIgAiIgAjkHAKZIqbq1q3rbr31VnuwBmU0hyg9iHE9EDK9e/e2B+XHH3/c+Yd63CFEAk7Ejh077DRBpwhhx8N1nz59rB2uUefOnc2xmjBhgo2LSPntt9+sb8mSJR3ixYspXBge8vv16+eaN29ubbp37+7OOeccN2fOHDd69Gg7Rh9EWrTAxXj00Ufds88+a2IMdycYRYoUcSeeeKI79thj3U8//eQKFiyYREzhWhElSpSwF3y9mPLj4DbNmjXLxkBcemHpv8e5OvXUU00gXHnllf5wkr/MHxZhMcX5L7/8chMSCBsYImRwxDjPzTffnGQc5oEoIxAh3COE1O7du00s0Q+xO3DgwEg/RBnnYO716tVLIqYQrLwQqvz9448/zCUMpnfSHyeqVq1a5kYhbhE9N954o7vjjjvchRde6HD3wo7SSSedZI4lomzz5s3ul19+sWuqWLGi3XccPIT4qFGjTKyuX78+Mme9EQEREAEREAEREAERyFkEMkVM8T/5iA7SpHBuMiN4qEU04cQgqrwjg8NEIHi8W8SDOilp4UAo4U7hlhBffPGFPTx///335nohJhBHXkj5/jgUbdu2NTGAS0U0adLEffnll75Jin83bNhgwo0HfFIBg2uXEAV8Js2PuPTSS93ChQvtPeIBd4RzPfPMM3aMf66++mpLQSPNESHh3SiE1sSJE922bdsibRFrzJ9UxR49ekSOh99w72gbDsQy80askvYGp8mTJzsEBwLpkksuiXRB8GzZsiUipvwXS5YssRRD+vbs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)

   

4. 用`staticCall`调用`transfer()`函数，将`from`参数填为Vitalik地址，模拟Vitalik转账`10000 DAI`。这笔交易将成功，因为Vitalik钱包有充足的`DAI`。

   ```js
   console.log("\n2.  用staticCall尝试调用transfer转账1 DAI，msg.sender为Vitalik地址")
   // 发起交易
   const tx = await contractDAI.transfer.staticCall("vitalik.eth", ethers.parseEther("1"), {from:  await provider.resolveName("vitalik.eth")})
   console.log(`交易会成功吗？：`, tx)
   ```

   

   

   ![模拟Vitalik转账](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071531446.png)

   

5. 用`staticCall`调用`transfer()`函数，将`from`参数填为测试钱包地址，模拟转账`10000 DAI`。这笔交易将失败，报错，并返回原因`Dai/insufficient-balance`。

   ```js
   console.log("\n3.  用staticCall尝试调用transfer转账10000 DAI，msg.sender为测试钱包地址")
   const tx2 = await contractDAI.transfer.staticCall("vitalik.eth", ethers.parseEther("10000"), {from: address})
   console.log(`交易会成功吗？：`, tx2)
   ```

   

   

   ![模拟测试钱包转账](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071531103.png)

   

## 总结

`ethers.js`将`eth_call`封装在`staticCall`方法中，方便开发者模拟交易的结果，并避免发送可能失败的交易。我们利用`staticCall`模拟了Vitalik和测试钱包的转账。当然，这个方法还有更多用处，比如计算土狗币的交易滑点。开动你的想象力，你会将`staticCall`用在什么地方呢？

> [!TIP]
>
> `staticCall` 的主要优势在于它能够模拟交易，而无需实际在链上发送交易，也不需要支付 gas 费用。这可以用在多个场景中，帮助开发者在确保安全性和交易成功率的情况下设计应用。以下是一些可能的用法：
>
> ### 1. **预估代币兑换交易是否成功**
> 在去中心化交易所（如 Uniswap 或 Sushiswap）上进行代币兑换时，用户可能面临滑点问题。如果滑点过高，交易将会失败。通过 `staticCall` 可以在发送实际交易前，预估代币兑换操作是否会成功，并调整滑点容忍度。
>
> ```js
> const amountOut = await uniswapRouter.swapExactTokensForTokens.staticCall(
>   amountIn, 
>   minAmountOut, 
>   [tokenIn, tokenOut], 
>   userAddress, 
>   deadline
> );
> if (amountOut > minAmountOut) {
>   console.log("交易成功，滑点在容忍范围内");
> } else {
>   console.log("交易滑点过大，可能会失败");
> }
> ```
>
> ### 2. **模拟复杂的合约调用**
> 在 DeFi 协议中，合约调用通常涉及复杂的逻辑。通过 `staticCall` 可以在不提交交易的情况下，预先模拟复杂的调用操作。例如，在借贷平台上，可以模拟用户是否有足够的抵押品来借款，或者用户的清算风险有多高。
>
> ```js
> const canBorrow = await lendingPlatform.borrow.staticCall(
>   amountToBorrow, 
>   userCollateral, 
>   userAddress
> );
> if (canBorrow) {
>   console.log("用户可以借款");
> } else {
>   console.log("抵押品不足，借款将失败");
> }
> ```
>
> ### 3. **检测预言机报价或外部数据源是否可用**
> 通过 `staticCall` 预先检查预言机或其他外部数据是否能正确返回结果，避免出现因为预言机报价缺失或更新不及时而导致的交易失败。
>
> ```js
> const oraclePrice = await priceOracle.getPrice.staticCall(tokenAddress);
> if (oraclePrice > 0) {
>   console.log("价格已更新，可以继续交易");
> } else {
>   console.log("价格未更新，交易失败");
> }
> ```
>
> ### 4. **模拟质押（Staking）与收益计算**
> 在质押平台上，用户可能需要确认他们的质押是否会产生预期的收益。可以通过 `staticCall` 模拟质押收益的计算，帮助用户在决定前预估收益。
>
> ```js
> const rewards = await stakingContract.calculateRewards.staticCall(userAddress);
> console.log(`预期收益: ${ethers.formatEther(rewards)} tokens`);
> ```
>
> ### 5. **模拟分配机制或空投**
> 对于空投、NFT minting 或其他代币分配，`staticCall` 可以帮助确认用户是否符合条件或空投的逻辑是否正确。例如，模拟空投分发给某个用户之前，可以预估是否符合资格。
>
> ```js
> const isEligible = await airdropContract.checkEligibility.staticCall(userAddress);
> if (isEligible) {
>   console.log("用户符合空投资格");
> } else {
>   console.log("用户不符合空投资格");
> }
> ```
>
> ### 6. **合约安全性检查**
> 在与复杂的合约进行交互之前，开发者可以通过 `staticCall` 预先检测合约逻辑是否正常，比如合约是否会拒绝特定调用。这有助于规避潜在的安全风险，尤其是与未经审计的合约交互时。
>
> ### 总结：
> 通过 `staticCall`，我们可以在不冒实际损失的情况下模拟交易行为，测试各类交互逻辑和合约状态。无论是预估成功率、避免滑点失败，还是优化质押收益，`staticCall` 为 DApp 开发者提供了极大的灵活性和安全保障。你可以在涉及任何会产生状态变更或 gas 费用的地方，首先通过 `staticCall` 进行模拟，确保交易成功后再发送正式交易。



# 12. 识别ERC721合约

这一讲，我们介绍如何用`ether.js`识别一个合约是否为`ERC721`标准。

## `ERC721`

`ERC721`是以太坊上流行的非同质化代币（NFT）标准，如果对这个标准不熟悉，可以阅读[WTF Solidity第34讲 ERC721](https://github.com/AmazingAng/WTFSolidity/blob/main/34_ERC721/readme.md)。在做NFT相关产品时，我们需要筛选出符合`ERC721`标准的合约。例如Opensea，他会自动识别`ERC721`，并爬下它的名称、代号、metadata等数据用于展示。要识别`ERC721`，我们先要理解`ERC165`。

## `ERC165`

通过[ERC165标准](https://eips.ethereum.org/EIPS/eip-165)，智能合约可以声明它支持的接口，供其他合约检查。因此，我们可以通过`ERC165`来检查一个智能合约是不是支持了`ERC721`的接口。

`IERC165`接口合约只声明了一个`supportsInterface`函数，输入要查询的`interfaceId`接口id（类型为`bytes4`），若合约实现了该接口id，则返回`true`；反之，则返回`false`：

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



`ERC721`合约中会实现`IERC165`接口合约的`supportsInterface`函数，并且当查询`0x80ac58cd`（`ERC721`接口id）时返回`true`。

```solidity
   function supportsInterface(bytes4 interfaceId)
        external
        pure
        override
        returns (bool)
    {
        return
            interfaceId == type(IERC721).interfaceId 
    }
```



## 识别`ERC721`

1. 创建`provider`，连接以太坊主网。

   ```js
   //准备 alchemy API 可以参考https://github.com/AmazingAng/WTFSolidity/blob/main/Topics/Tools/TOOL04_Alchemy/readme.md 
   const ALCHEMY_MAINNET_URL = 'https://eth-mainnet.g.alchemy.com/v2/oKmOQKbneVkxgHZfibs-iFhIlIAl6HDN';
   const provider = new ethers.JsonRpcProvider(ALCHEMY_MAINNET_URL);
   ```

   

2. 创建`ERC721`合约实例，在`abi`接口中，我们声明要使用的`name()`，`symbol()`，和`supportsInterface()`函数即可。这里我们用的BAYC的合约地址。

   ```js
   // 合约abi
   const abiERC721 = [
       "function name() view returns (string)",
       "function symbol() view returns (string)",
       "function supportsInterface(bytes4) public view returns(bool)",
   ];
   // ERC721的合约地址，这里用的BAYC
   const addressBAYC = "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d"
   // 创建ERC721合约实例
   const contractERC721 = new ethers.Contract(addressBAYC, abiERC721, provider)
   ```

   

3. 读取合约的链上信息：名称和代号。

   ```js
   // 1. 读取ERC721合约的链上信息
   const nameERC721 = await contractERC721.name()
   const symbolERC721 = await contractERC721.symbol()
   console.log("\n1. 读取ERC721合约信息")
   console.log(`合约地址: ${addressBAYC}`)
   console.log(`名称: ${nameERC721}`)
   console.log(`代号: ${symbolERC721}`)
   ```

   

   

   ![读取合约名称和代好](https://www.wtf.academy/assets/images/12-1-3cfbe60e396afcce328e0c2dfc3457b4.png)

   

4. 利用`ERC165`的`supportsInterface()`函数，识别合约是否为ERC721标准。如果是，则返回`true`；反之，则报错或返回`false`。

   注意此处的代码中的`selectorERC721`常量被提取出main函数

   ```js
   // 2. 利用ERC165的supportsInterface，确定合约是否为ERC721标准
   // ERC721接口的ERC165 identifier
   const selectorERC721 = "0x80ac58cd"
   const isERC721 = await contractERC721.supportsInterface(selectorERC721)
   console.log("\n2. 利用ERC165的supportsInterface，确定合约是否为ERC721标准")
   console.log(`合约是否为ERC721标准: ${isERC721}`)
   ```

   

   

   ![识别ERC721](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071531209.png)

   

## 总结

这一讲，我们介绍如何`ethers.js`来识别一个合约是否为`ERC721`。由于利用了`ERC165`标准，因此只有支持`ERC165`标准的合约才能用这个方法识别，包括`ERC721`，`ERC1155`等。但是像`ERC20`这种不支持`ERC165`的标准，就要用别的方法识别了。你知道怎么检查一个合约是否为`ERC20`吗？

> [!TIP]
>
> 识别一个合约是否为 `ERC20` 通常不涉及 `ERC165` 标准，因为 `ERC20` 标准并没有规定这种检测机制。相反，我们可以通过检查合约是否实现了 `ERC20` 标准的核心函数来判断它是否为 `ERC20`。这些函数包括：
>
> - `totalSupply()`: 返回代币的总供应量。
> - `balanceOf(address owner)`: 返回某个地址的代币余额。
> - `transfer(address to, uint256 amount)`: 代币转账。
> - `approve(address spender, uint256 amount)`: 授权某个地址消费代币。
> - `transferFrom(address from, address to, uint256 amount)`: 从授权的地址转账。
> - `allowance(address owner, address spender)`: 查看授权额度。
>
> 我们可以通过以下步骤来检测合约是否符合 `ERC20` 标准：
>
> ### 1. **检查合约是否实现了 `ERC20` 的核心函数**
>
> 我们可以利用 `ethers.js` 中的 `callStatic` 或 `staticCall` 方法检查合约是否支持上述 `ERC20` 的函数，而无需实际调用这些函数。如果函数存在且返回有效值，则表明该合约支持 `ERC20` 标准。
>
> ```js
> import { ethers } from "ethers";
> 
> const provider = new ethers.JsonRpcProvider('<RPC_URL>');
> const contractAddress = "<ERC20_CONTRACT_ADDRESS>";
> const abiERC20 = [
>     "function totalSupply() view returns (uint256)",
>     "function balanceOf(address account) view returns (uint256)",
>     "function transfer(address to, uint256 amount) returns (bool)",
>     "function approve(address spender, uint256 amount) returns (bool)",
>     "function transferFrom(address from, address to, uint256 amount) returns (bool)",
>     "function allowance(address owner, address spender) view returns (uint256)"
> ];
> 
> // 创建 ERC20 合约实例
> const contract = new ethers.Contract(contractAddress, abiERC20, provider);
> 
> // 检查合约是否为 ERC20
> async function checkERC20() {
>     try {
>         // 测试 totalSupply 函数
>         const totalSupply = await contract.callStatic.totalSupply();
>         console.log("totalSupply: ", ethers.formatUnits(totalSupply, 18));
> 
>         // 测试 balanceOf 函数
>         const balance = await contract.callStatic.balanceOf("0x0000000000000000000000000000000000000000");
>         console.log("balanceOf: ", ethers.formatUnits(balance, 18));
> 
>         console.log("该合约符合 ERC20 标准");
>     } catch (error) {
>         console.log("该合约不符合 ERC20 标准");
>     }
> }
> 
> checkERC20();
> ```
>
> ### 2. **捕获合约函数调用错误**
>
> 如果某个合约不是 `ERC20`，调用这些函数可能会失败并抛出错误。我们可以通过捕获这些错误来判断它是否支持 `ERC20`。上面的代码中，`try-catch` 语句用来捕获调用 `ERC20` 函数时可能产生的错误。
>
> ### 3. **检查事件日志**
>
> 此外，`ERC20` 合约通常还会触发 `Transfer` 和 `Approval` 事件。我们可以进一步检查这些事件是否存在，来确认合约是否符合 `ERC20` 标准：
>
> ```js
> const abiERC20Events = [
>     "event Transfer(address indexed from, address indexed to, uint256 value)",
>     "event Approval(address indexed owner, address indexed spender, uint256 value)"
> ];
> 
> const contractWithEvents = new ethers.Contract(contractAddress, abiERC20Events, provider);
> 
> async function checkERC20Events() {
>     try {
>         const filter = contractWithEvents.filters.Transfer();
>         const logs = await provider.getLogs({
>             fromBlock: 0,
>             toBlock: "latest",
>             address: contractAddress,
>             topics: filter.topics,
>         });
>         if (logs.length > 0) {
>             console.log("该合约符合 ERC20 标准（有 Transfer 事件）");
>         } else {
>             console.log("该合约不符合 ERC20 标准（无 Transfer 事件）");
>         }
>     } catch (error) {
>         console.log("检查 ERC20 事件时出错：", error);
>     }
> }
> 
> checkERC20Events();
> ```
>
> ### 总结
>
> 虽然 `ERC165` 标准可以用于检测一些支持的接口（如 `ERC721`、`ERC1155`），但由于 `ERC20` 并不支持 `ERC165`，我们需要通过检查其是否实现了核心函数（如 `totalSupply`、`balanceOf`、`transfer` 等）以及事件日志来识别 `ERC20` 合约。
>
> 通过这种方法，开发者可以有效地判断合约是否符合 `ERC20` 标准。



# 13. 编码calldata

这一讲，我们将介绍`ethers.js`中的接口类，并利用它编码`calldata`。

> [!IMPORTANT]
>
> 在与智能合约交互时，**编码和解码**是必不可少的步骤，原因主要在于区块链的底层结构和合约的执行机制。智能合约通过发送交易与外部进行交互，而每次交互都必须以严格的二进制格式（称为 `calldata`）传递数据。`ethers.js` 的 `Interface` 类帮助开发者简化了这一过程，自动处理编码和解码工作。这里是一些核心原因：
>
> ### 1. **智能合约只能接收和发送二进制数据**
>    以太坊虚拟机（EVM）和智能合约的执行环境不能理解人类可读的参数，比如普通的字符串、地址或数字。为了与合约交互，所有的输入参数和返回值必须转换成 EVM 可识别的二进制格式。这个过程称为**编码**。
>
>    例如，如果你想调用 `WETH` 合约中的 `deposit()` 函数，函数签名和参数需要被转换为特定的 `calldata` 形式，才能通过交易发送到区块链。
>
>    **编码的好处**：
>    - 将人类可读的高层信息（函数名、参数）转换为 EVM 机器可读的格式。
>    - 保证数据以标准化格式传递，不会因为传输差异导致执行错误。
>
>    示例：
>    ```js
>    const calldata = iface.encodeFunctionData("deposit", [amount]);
>    ```
>
> ### 2. **代理合约和复杂合约需要自定义编码**
>    在与代理合约或某些特殊合约（如多签合约或 DeFi 协议）交互时，函数调用往往需要通过间接的方式来实现。这时，直接调用合约可能不够，需要自己手动编码 `calldata`，并将这些数据通过合约的低层调用方法传递。
>
>    例如，对于代理合约，用户可能要先通过一个合约调用另一个目标合约，手动构造调用数据来确保交易正确传递和执行。
>
>    **代理合约示例**：
>    ```js
>    const data = iface.encodeFunctionData("transfer", [recipient, amount]);
>    // 在代理合约中通过低层次方法调用
>    const tx = await proxyContract.execute(targetContractAddress, data);
>    ```
>
> ### 3. **解码返回值**
>    当合约执行完毕并返回数据时，返回的数据同样是二进制的，需要通过解码将其转换回可读格式。例如，当你调用合约的 `view` 函数时，返回的结果是经过编码的数据，`ethers.js` 可以帮你解码它以供查看。
>
>    **解码的好处**：
>    - 将二进制格式转换回原始的人类可读值（如地址、数字、字符串等）。
>    - 方便开发者查看、使用智能合约的返回数据。
>
>    示例：
>    ```js
>    const result = iface.decodeFunctionResult("transfer", returnedData);
>    console.log(result); // 人类可读的解码后的返回值
>    ```
>
> ### 总结
> 通过 `ethers.js` 中的接口类进行编码和解码是与智能合约安全、正确交互的关键步骤。编码保证我们能够按照 EVM 需要的格式传递数据，而解码则帮助我们从智能合约的返回值中提取有用的信息。特别是在代理合约和复杂合约场景下，编码解码使得开发者可以精确控制合约交互。



## 接口类 Interface

`ethers.js`的接口类抽象了与以太坊网络上的合约交互所需的`ABI`编码和解码。`ABI`（Application Binary Interface）与`API`类似，是一格式，用于对合约可以处理的各种类型的数据进行编码，以便它们可以交互。更多内容见[WTF Solidity教程第27讲 ABI编码](https://github.com/AmazingAng/WTFSolidity/tree/main/27_ABIEncode)。

我们可以利用`abi`生成或者直接从合约中获取`interface`变量：

```js
// 利用abi生成
const interface = ethers.Interface(abi)
// 直接从contract中获取
const interface2 = contract.interface
```

> [!TIP]
>
> 在 `ethers.js` 中，`Interface` 是用来解析和格式化合约的 ABI（Application Binary Interface）。它允许开发者更轻松地与合约交互，解析事件、编码和解码函数参数等。`Interface` 对象可以通过两种方式生成：
>
> 1. **利用 ABI 生成 `Interface`**  
>    如果你已经有合约的 ABI，可以直接用它生成一个 `Interface` 实例。
>
>    ```js
>    const abi = [
>        "function transfer(address to, uint amount) external returns (bool)",
>        "event Transfer(address indexed from, address indexed to, uint amount)"
>    ];
>       
>    const iface = new ethers.Interface(abi);
>    console.log(iface);
>    ```
>
>    这种方法直接使用 ABI 数据（通常是 JSON 格式的数组）来创建 `Interface` 实例，随后可以通过它调用合约方法或者解析事件。
>
> 2. **从合约实例中获取 `interface`**  
>    当你使用 `ethers.Contract` 创建一个合约实例时，该实例自带一个 `interface` 属性，方便你获取合约的 `Interface`。
>
>    ```js
>    const contractAddress = "<CONTRACT_ADDRESS>";
>    const contract = new ethers.Contract(contractAddress, abi, provider);
>       
>    // 直接从合约实例中获取 interface
>    const iface2 = contract.interface;
>    console.log(iface2);
>    ```
>
>    这种方式是通过 `contract.interface` 获取该合约的 `Interface`，从而可以解码、编码合约方法，或处理事件。
>
> ### `Interface` 的常见用途
>
> - **编码函数调用**
>   
>    通过 `Interface` 可以将函数名称和参数编码成适用于发送交易的 `data` 字段。
>
>    ```js
>    const data = iface.encodeFunctionData("transfer", ["0xRecipientAddress", ethers.parseUnits("1", 18)]);
>    console.log(data); // 编码后的数据
>    ```
>
> - **解码返回数据**
>   
>    如果你通过 `callStatic` 模拟交易，可以利用 `Interface` 解码返回值。
>
>    ```js
>    const result = iface.decodeFunctionResult("transfer", returnData);
>    console.log(result);
>    ```
>
> - **解析事件日志**
>   
>    通过 `Interface` 可以解析事件日志，得到更易读的结果。
>
>    ```js
>    const log = {
>        topics: [/* 事件的 topics */],
>        data: "0x" // 事件的日志数据
>    };
>       
>    const parsedLog = iface.parseLog(log);
>    console.log(parsedLog);
>    ```
>
> 无论是通过 ABI 创建还是从合约实例中获取，`Interface` 都是与合约交互的核心工具之一，可以方便地管理合约调用、解析事件以及处理数据。

接口类封装了一些编码解码的方法。与一些特殊的合约交互时（比如代理合约），你需要编码参数、解码返回值：

**注意**：相关函数必须包含在`abi`中。

- `getSighash()`：获取函数选择器（function selector），参数为函数名或函数签名。

  ```js
  interface.getSighash("balanceOf");
  // '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef'
  ```

  

- `encodeDeploy()`：编码构造器的参数，然后可以附在合约字节码的后面。

  ```js
  interface.encodeDeploy("Wrapped ETH", "WETH");
  ```

  

- `encodeFunctionData()`：编码函数的`calldata`。

  ```js
  interface.encodeFunctionData("balanceOf", ["0xc778417e063141139fce010982780140aa0cd5ab"]);
  ```

  

- `decodeFunctionResult()`：解码函数的返回值。

  ```js
  interface.decodeFunctionResult("balanceOf", resultData)
  ```

  

## 例子：与测试网`WETH`合约交互

这里，我们利用接口类编码`calldata`的方法，重复[第5讲](https://github.com/WTFAcademy/WTFEthers/blob/main/05_WriteContract/readme.md)中与测试网`WETH`合约交互的例子。

1. 创建`provider`，`wallet`变量。

   ```js
   //准备 alchemy API 可以参考https://github.com/AmazingAng/WTFSolidity/blob/main/Topics/Tools/TOOL04_Alchemy/readme.md 
   const ALCHEMY_GOERLI_URL = 'https://eth-rinkeby.alchemyapi.io/v2/GlaeWuylnNM3uuOo-SAwJxuwTdqHaY5l';
   const provider = new ethers.JsonRpcProvider(ALCHEMY_GOERLI_URL);
   
   // 利用私钥和provider创建wallet对象
   const privateKey = '0x227dbb8586117d55284e26620bc76534dfbd2394be34cf4a09cb775d593b6f2b'
   const wallet = new ethers.Wallet(privateKey, provider)
   ```

   

2. 创建`WETH`合约实例

   ```js
   // WETH的ABI
   const abiWETH = [
       "function balanceOf(address) public view returns(uint)",
       "function deposit() public payable",
   ];
   // WETH合约地址（Goerli测试网）
   const addressWETH = '0xb4fbf271143f4fbf7b91a5ded31805e42b2208d6'
   // 声明WETH合约
   const contractWETH = new ethers.Contract(addressWETH, abiWETH, wallet)
   ```

   

3. 调用`balanceOf()`函数，读取钱包地址`address`的`WETH`余额。

   ```js
   const address = await wallet.getAddress()
   // 1. 读取WETH合约的链上信息（WETH abi）
   console.log("\n1. 读取WETH余额")
   // 编码calldata
   const param1 = contractWETH.interface.encodeFunctionData(
       "balanceOf",
       [address]
     );
   console.log(`编码结果： ${param1}`)
   // 创建交易
   const tx1 = {
       to: addressWETH,
       data: param1
   }
   // 发起交易，可读操作（view/pure）可以用 provider.call(tx)
   const balanceWETH = await provider.call(tx1)
   console.log(`存款前WETH持仓: ${ethers.formatEther(balanceWETH)}\n`)
   ```

   

   

   ![查看WETH余额](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071531384.png)

   

4. 调用`deposit()`函数，将`0.001 ETH`转换为`0.001 WETH`，打印交易详情和余额。可以看到余额变化。

   ```js
   // 编码calldata
   const param2 = contractWETH.interface.encodeFunctionData(
       "deposit"          
       );
   console.log(`编码结果： ${param2}`)
   // 创建交易
   const tx2 = {
       to: addressWETH,
       data: param2,
       value: ethers.parseEther("0.001")}
   // 发起交易，写入操作需要 wallet.sendTransaction(tx)
   const receipt1 = await wallet.sendTransaction(tx2)
   // 等待交易上链
   await receipt1.wait()
   console.log(`交易详情：`)
   console.log(receipt1)
   const balanceWETH_deposit = await contractWETH.balanceOf(address)
   console.log(`存款后WETH持仓: ${ethers.formatEther(balanceWETH_deposit)}\n`)
   ```

   

   

   ![调用deposit()函数](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071531187.png)

   

## 总结

这一讲，我们介绍了`ethers.js`中的接口类，并利用它编码`calldata`与`WETH`合约交互。与一些特殊的合约交互时（比如代理合约），你需要用这类方法编码参数，然后解码返回值。

# 14. 批量生成钱包

这一讲，我们将介绍HD钱包，并写一个批量生成钱包的脚本。

## HD钱包

HD钱包（Hierarchical Deterministic Wallet，多层确定性钱包）是一种数字钱包 ，通常用于存储比特币和以太坊等加密货币持有者的数字密钥。通过它，用户可以从一个随机种子创建一系列密钥对，更加便利、安全、隐私。要理解HD钱包，我们需要简单了解比特币的[BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki)，[BIP44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki)，和[BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki)。

### BIP32

在`BIP32`推出之前，用户需要记录一堆的私钥才能管理很多钱包。`BIP32`提出可以用一个随机种子衍生多个私钥，更方便的管理多个钱包。钱包的地址由衍生路径决定，例如`“m/0/0/1”`。



![BIP32](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071532940.png)



### BIP44

`BIP44`为`BIP32`的衍生路径提供了一套通用规范，适配比特币、以太坊等多链。这一套规范包含六级，每级之间用"/"分割：

```text
m / purpose' / coin_type' / account' / change / address_index
```



其中：

- m: 固定为"m"
- purpose：固定为"44"
- coin_type：代币类型，比特币主网为0，比特币测试网为1，以太坊主网为60
- account：账户索引，从0开始。
- change：是否为外部链，0为外部链，1为内部链，一般填0.
- address_index：地址索引，从0开始，想生成新地址就把这里改为1，2，3。

举个例子，以太坊的默认衍生路径为`"m/44'/60'/0'/0/0"`。

### BIP39

`BIP39`让用户能以一些人类可记忆的助记词的方式保管私钥，而不是一串16进制的数字：

```text
//私钥
0x813f8f0a4df26f6455814fdd07dd2ab2d0e2d13f4d2f3c66e7fd9e3856060f89
//助记词
air organ twist rule prison symptom jazz cheap rather dizzy verb glare jeans orbit weapon universe require tired sing casino business anxiety seminar hunt
```



## 批量生成钱包

`ethers.js`提供了[HDNodeWallet类](https://docs.ethers.org/v6-beta/api/wallet/#HDNodeWallet)，方便开发者使用HD钱包。下面我们利用它从一个助记词批量生成20个钱包。

1. 创建`baseWallet`钱包变量，可以看到助记词为`'air organ twist rule prison symptom jazz cheap rather dizzy verb glare jeans orbit weapon universe require tired sing casino business anxiety seminar hunt'`

   ```js
   // 生成随机助记词
   const mnemonic = ethers.Mnemonic.entropyToPhrase(ethers.randomBytes(32))
   // 创建HD基钱包
   // 基路径："m / purpose' / coin_type' / account' / change"
   const basePath = "44'/60'/0'/0"
   const baseWallet = ethers.HDNodeWallet.fromPhrase(mnemonic, basePath)
   console.log(baseWallet);
   ```

   > [!NOTE]
   >
   > `ethers.randomBytes(32)`：生成32字节的随机数（256位），这相当于一个随机的私钥。
   >
   > `ethers.Mnemonic.entropyToPhrase()`：使用BIP39标准将这个随机数（熵）转换为助记词（mnemonic）。助记词是基于熵生成的一组可以记忆的单词，用来代表私钥。
   >
   > `ethers.HDNodeWallet.fromPhrase()`：这是`ethers.js`中用于从助记词创建HD钱包的方法。它会基于助记词和指定的路径（`basePath`）创建一个HD钱包节点。这个HD钱包可以通过不同的路径派生出多个子钱包。
   >
   > `basePath`：用来定义生成钱包的路径，即我们根据这个路径来生成钱包。如果不提供 `basePath` 参数，默认情况下 `ethers.HDNodeWallet.fromPhrase()` 将使用BIP44标准中的默认路径。这通常是 `"m/44'/60'/0'/0/0"`，其中`44'`代表BIP44协议，`60'`代表以太坊币种ID，`0'`表示账户索引，最后的`0/0`代表外部的第一个地址。

   

   ![baseWallet](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071532605.png)

   

2. 通过HD钱包派生20个钱包。

   ```js
   const numWallet = 20
   // 派生路径：基路径 + "/ address_index"
   // 我们只需要提供最后一位address_index的字符串格式，就可以从baseWallet派生出新钱包。V6中不需要重复提供基路径！
   let wallets = [];
   for (let i = 0; i < numWallet; i++) {
       let baseWalletNew = baseWallet.derivePath(i.toString());
       console.log(`第${i+1}个钱包地址： ${baseWalletNew.address}`)
       wallets.push(baseWalletNew);
   }
   ```

   > [!NOTE]
   >
   > 这里的`derivePath(i.toString())`函数是关键。它从`baseWallet`派生出一个新的钱包：
   >
   > - `i.toString()`将数字`i`（从0到19）转换为字符串，并将它添加到基路径的末尾，作为`address_index`。例如，当`i=0`时，路径为`m/44'/60'/0'/0/0`；当`i=1`时，路径为`m/44'/60'/0'/0/1`，以此类推。
   > - `derivePath`方法会基于这个新的路径派生出一个新的HD钱包。
   >
   > 由于`V6`版本的`ethers.js`优化了HD钱包的派生机制，我们只需要提供最后的`address_index`，而不需要重复传入整个路径。

   

   ![批量生成钱包](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071532204.png)

   

3. 保存钱包为加密json：

   ```js
   const wallet = ethers.Wallet.fromPhrase(mnemonic)
   console.log("通过助记词创建钱包：")
   console.log(wallet)
   // 加密json用的密码，可以更改成别的
   const pwd = "password"
   const json = await wallet.encrypt(pwd)
   console.log("钱包的加密json：")
   console.log(json)
   ```

   

   

   ![保存钱包](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071532357.png)

   

4. 从加密json中读取钱包：

   ```js
   const wallet2 = await ethers.Wallet.fromEncryptedJson(json, pwd);
   console.log("\n4. 从加密json读取钱包：")
   console.log(wallet2)
   ```

   

   

   ![读取钱包](https://www.wtf.academy/assets/images/14-5-bc2607f5d24856fa5cf234ce2dac033a.png)

   

## 总结

这一讲我们介绍了HD钱包（BIP32，BIP44，BIP39），并利用它使用`ethers.js`批量生成了20个钱包。

# 15. 批量转账

这一讲，我们将介绍用`ethers.js`进行批量转账。通过调用[WTF Solidity极简入门第33讲：空投](https://github.com/AmazingAng/WTF-Solidity/blob/main/33_Airdrop/readme.md)中的`Airdrop`合约，可以在一笔交易中实现批量转账，节省gas费。

## Airdrop合约

这里简单介绍下`Airdrop`合约，细节可以去Solidity教程中看。我们会用到`2`个函数：

- ```
  multiTransferETH()：批量发送ETH，包含2个参数：
  ```

  - `_addresses`：接收空投的用户地址数组（`address[]`类型）
  - `_amounts`：空投数量数组，对应`_addresses`里每个地址的数量（`uint[]`类型）
  
- ```
  multiTransferToken()函数：批量发送ERC20代币，包含3个参数：
  ```

  - `_token`：代币合约地址（`address`类型）
  - `_addresses`：接收空投的用户地址数组（`address[]`类型）
  - `_amounts`：空投数量数组，对应`_addresses`里每个地址的数量（`uint[]`类型）

我们在`Goerli`测试网部署了一个`Airdrop`合约，地址为：

```text
0x71C2aD976210264ff0468d43b198FD69772A25fa
```



## 批量转账

下面我们写一个脚本，调用`Airdrop`合约将`ETH`（原生代币）和`WETH`（ERC20代币）转账给`20`个地址。

1. 创建HD钱包，用于批量生成地址。

   ```js
   console.log("\n1. 创建HD钱包")
   // 通过助记词生成HD钱包
   const mnemonic = `air organ twist rule prison symptom jazz cheap rather dizzy verb glare jeans orbit weapon universe require tired sing casino business anxiety seminar hunt`
   const hdNode = ethers.HDNodeWallet.fromPhrase(mnemonic)
   console.log(hdNode);
   ```

   

   

   ![HD钱包](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071532908.png)

   

2. 利用HD钱包，生成20个钱包地址。

   ```js
   console.log("\n2. 通过HD钱包派生20个钱包")
   const numWallet = 20
   // 派生路径：m / purpose' / coin_type' / account' / change / address_index
   // 我们只需要切换最后一位address_index，就可以从hdNode派生出新钱包
   let basePath = "m/44'/60'/0'/0";
   let addresses = [];
   for (let i = 0; i < numWallet; i++) {
       let hdNodeNew = hdNode.derivePath(basePath + "/" + i);
       let walletNew = new ethers.Wallet(hdNodeNew.privateKey);
       addresses.push(walletNew.address);
   }
   console.log(addresses)
   const amounts = Array(20).fill(ethers.parseEther("0.0001"))
   console.log(`发送数额：${amounts}`)
   ```

   > [!TIP]
   >
   > `derivePath(basePath + "/" + i)`：这个方法从基础路径派生出子路径。通过切换 `address_index`（即`i`），我们可以派生出一系列独立的子钱包，每个钱包都有自己的地址。
   >
   > `new ethers.Wallet(hdNodeNew.privateKey)`：使用 `ethers.js` 的 `Wallet` 类，通过派生出的 `privateKey` 创建一个新钱包实例。
   >
   > `addresses.push(walletNew.address)`：将派生的新钱包的地址添加到 `addresses` 数组中。

   

   ![生成20个地址](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071532977.png)

   

3. 创建provider和wallet，发送代币用。

   ```js
   //准备 alchemy API 可以参考https://github.com/AmazingAng/WTF-Solidity/blob/main/Topics/Tools/TOOL04_Alchemy/readme.md 
   const ALCHEMY_GOERLI_URL = 'https://eth-goerli.alchemyapi.io/v2/GlaeWuylnNM3uuOo-SAwJxuwTdqHaY5l';
   const provider = new ethers.JsonRpcProvider(ALCHEMY_GOERLI_URL);
   
   // 利用私钥和provider创建wallet对象
   // 如果这个钱包没goerli测试网ETH了
   // 请使用自己的小号钱包测试，钱包地址: 0x338f8891D6BdC58eEB4754352459cC461EfD2a5E ,请不要给此地址发送任何ETH
   // 注意不要把自己的私钥上传到github上
   const privateKey = '0x21ac72b6ce19661adf31ef0d2bf8c3fcad003deee3dc1a1a64f5fa3d6b049c06'
   const wallet = new ethers.Wallet(privateKey, provider)
   ```

   

4. 创建Airdrop合约。

   ```js
   // Airdrop的ABI
   const abiAirdrop = [
       "function multiTransferToken(address,address[],uint256[]) external",
       "function multiTransferETH(address[],uint256[]) public payable",
   ];
   // Airdrop合约地址（Goerli测试网）
   const addressAirdrop = '0x71C2aD976210264ff0468d43b198FD69772A25fa' // Airdrop Contract
   // 声明Airdrop合约
   const contractAirdrop = new ethers.Contract(addressAirdrop, abiAirdrop, wallet)
   ```

   

5. 创建WETH合约。

   ```js
   // WETH的ABI
   const abiWETH = [
       "function balanceOf(address) public view returns(uint)",
       "function transfer(address, uint) public returns (bool)",
       "function approve(address, uint256) public returns (bool)"
   ];
   // WETH合约地址（Goerli测试网）
   const addressWETH = '0xB4FBF271143F4FBf7B91A5ded31805e42b2208d6' // WETH Contract
   // 声明WETH合约
   const contractWETH = new ethers.Contract(addressWETH, abiWETH, wallet)
   ```

   

6. 读取一个地址的ETH和WETH余额。

   ```js
   console.log("\n3. 读取一个地址的ETH和WETH余额")
   //读取WETH余额
   const balanceWETH = await contractWETH.balanceOf(addresses[10])
   console.log(`WETH持仓: ${ethers.formatEther(balanceWETH)}\n`)
   //读取ETH余额
   const balanceETH = await provider.getBalance(addresses[10])
   console.log(`ETH持仓: ${ethers.formatEther(balanceETH)}\n`)
   ```

   

   

   ![读取WETH和ETH持仓](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071532204.png)

   

1. 调用`multiTransferETH()`函数，给每个钱包转`0.0001 ETH`，可以看到发送后余额发生变化。

   ```js
   console.log("\n4. 调用multiTransferETH()函数，给每个钱包转 0.0001 ETH")
   // 发起交易
   const tx = await contractAirdrop.multiTransferETH(addresses, amounts, {value: ethers.parseEther("0.002")}) //总共发送 0.002 ETH，每个地址将得到 0.0001 ETH
   // 等待交易上链
   await tx.wait()
   // console.log(`交易详情：`)
   // console.log(tx)
   const balanceETH2 = await provider.getBalance(addresses[10])
   console.log(`发送后该钱包ETH持仓: ${ethers.formatEther(balanceETH2)}\n`)
   ```

   

   

   ![批量发送ETH](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071532215.png)

   

2. 调用multiTransferToken()函数，给每个钱包转 `0.0001 WETH`，可以看到发送后余额发生变化。

   ```js
   console.log("\n5. 调用multiTransferToken()函数，给每个钱包转 0.0001 WETH")
   // 先approve WETH给Airdrop合约
   const txApprove = await contractWETH.approve(addressAirdrop, ethers.parseEther("1"))
   await txApprove.wait()
   // 发起交易
   const tx2 = await contractAirdrop.multiTransferToken(addressWETH, addresses, amounts)
   // 等待交易上链
   await tx2.wait()
   // console.log(`交易详情：`)
   // console.log(tx2)
   // 读取WETH余额
   const balanceWETH2 = await contractWETH.balanceOf(addresses[10])
   console.log(`发送后该钱包WETH持仓: ${ethers.formatEther(balanceWETH2)}\n`)
   ```

   

   ![批量发送WETH](https://www.wtf.academy/assets/images/15-5-b26e4a4bd5dffa7d0813755ead8f71c3.png)

   > [!TIP]
   >
   > 这个代码展示了如何通过合约中的 `multiTransferToken()` 函数，给多个钱包发送 `WETH`（Wrapped Ether）。步骤包括先批准合约使用指定数量的 WETH，然后执行多地址转账。让我们详细解释每一步：
   >
   > 1. 批准合约使用 WETH
   >
   > ```js
   > const txApprove = await contractWETH.approve(addressAirdrop, ethers.parseEther("1"));
   > await txApprove.wait();
   > ```
   > - `contractWETH.approve(addressAirdrop, ethers.parseEther("1"))`：调用 WETH 合约的 `approve` 函数，允许空投合约 `addressAirdrop` 代替用户使用最多 `1 WETH`。WETH 作为 ERC20 代币，任何外部合约在转移代币之前需要先被持有人授权。
   > - `txApprove.wait()`：等待批准交易上链并完成。
   >
   > 2. 调用 `multiTransferToken()` 函数发送 WETH
   >
   > ```js
   > const tx2 = await contractAirdrop.multiTransferToken(addressWETH, addresses, amounts);
   > await tx2.wait();
   > ```
   > - `contractAirdrop.multiTransferToken(addressWETH, addresses, amounts)`：调用空投合约的 `multiTransferToken()` 函数。这个函数将按指定的金额（`amounts` 数组）把 WETH 转移到多个地址（`addresses`）。
   >   - `addressWETH`：WETH 合约的地址，表示这是转账的代币类型。
   >   - `addresses`：之前生成的钱包地址列表，每个地址都会收到 WETH。
   >   - `amounts`：一个包含20个 `0.0001 WETH` 数量的数组。
   >   
   >
   > 3. 等待交易上链
   >
   > ```js
   > await tx2.wait();
   > ```
   > - `tx2.wait()`：等待代币转账交易完成并上链。
   >
   > 4. 读取其中一个钱包的 WETH 余额
   >
   > ```js
   > const balanceWETH2 = await contractWETH.balanceOf(addresses[10]);
   > console.log(`发送后该钱包WETH持仓: ${ethers.formatEther(balanceWETH2)}\n`);
   > ```
   > - `contractWETH.balanceOf(addresses[10])`：调用 WETH 合约的 `balanceOf` 函数，查询第11个地址的 WETH 余额（索引从0开始，`addresses[10]` 是第11个地址）。
   > - `ethers.formatEther(balanceWETH2)`：将余额从最小单位 `Wei` 转换为 `Ether`（WETH 使用与 ETH 相同的单位）。
   >
   > 总结
   >
   > 该代码通过 `multiTransferToken()` 函数，批量向多个地址发送 `WETH`，并在此之前批准了空投合约使用一定数量的 WETH。之后，代码检查了其中一个钱包在交易后的 WETH 余额。这种方法能够高效进行批量代币空投。
   
   

## 总结

这一讲，我们介绍了如何利用`ethers.js`调用`Airdrop`合约进行批量转账。在例子中，我们将`ETH`和`WETH`发送给了`20`个不同地址，省事且省钱（gas费）。

# 16. 批量归集

这一讲，我们介绍如何使用`ethers.js`将多个钱包的`ETH`和代币归集到一个钱包中。

## 批量归集

在链上交互、撸毛之后，就需要将多个钱包的资产进行归集管理。你可以用[HD钱包](https://github.com/WTFAcademy/WTF-Ethers/blob/main/14_HDwallet/readme.md)或者保存多份密钥的方式操作多个钱包，然后用`ethers.js`脚本完成归集。下面我们分别示范归集`ETH`（原生代币）和`WETH`（ERC20代币）。

1. 创建`provider`和`wallet`，其中`wallet`是接收资产的钱包。

   ```js
   // 准备 alchemy API 可以参考https://github.com/AmazingAng/WTF-Solidity/blob/main/Topics/Tools/TOOL04_Alchemy/readme.md 
   const ALCHEMY_GOERLI_URL = 'https://eth-goerli.alchemyapi.io/v2/GlaeWuylnNM3uuOo-SAwJxuwTdqHaY5l';
   const provider = new ethers.JsonRpcProvider(ALCHEMY_GOERLI_URL);
   // 利用私钥和provider创建wallet对象
   const privateKey = '0x21ac72b6ce19661adf31ef0d2bf8c3fcad003deee3dc1a1a64f5fa3d6b049c06'
   const wallet = new ethers.Wallet(privateKey, provider)
   ```

   

2. 声明WETH合约。

   ```js
   // WETH的ABI
   const abiWETH = [
       "function balanceOf(address) public view returns(uint)",
       "function transfer(address, uint) public returns (bool)",
   ];
   // WETH合约地址（Goerli测试网）
   const addressWETH = '0xB4FBF271143F4FBf7B91A5ded31805e42b2208d6' // WETH Contract
   // 声明WETH合约
   const contractWETH = new ethers.Contract(addressWETH, abiWETH, wallet)
   ```

   

3. 创建`HD`钱包，用于管理多个钱包。

   ```js
   console.log("\n1. 创建HD钱包")
   // 通过助记词生成HD钱包
   const mnemonic = `air organ twist rule prison symptom jazz cheap rather dizzy verb glare jeans orbit weapon universe require tired sing casino business anxiety seminar hunt`
   const hdNode = ethers.HDNodeWallet.fromPhrase(mnemonic)
   console.log(hdNode);
   ```

   

   

   ![HD钱包](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071532020.png)

   

4. 通过`HD`钱包衍生`20`个钱包，这些钱包上需要有资产。

   ```js
   const numWallet = 20
   // 派生路径：m / purpose' / coin_type' / account' / change / address_index
   // 我们只需要切换最后一位address_index，就可以从hdNode派生出新钱包
   let basePath = "m/44'/60'/0'/0";
   let wallets = [];
   for (let i = 0; i < numWallet; i++) {
       let hdNodeNew = hdNode.derivePath(basePath + "/" + i);
       let walletNew = new ethers.Wallet(hdNodeNew.privateKey);
       wallets.push(walletNew);
       console.log(walletNew.address)
   }
   // 定义发送数额
   const amount = ethers.parseEther("0.0001")
   console.log(`发送数额：${amount}`)
   ```

   

   

   ![生成20个地址](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071532345.png)

   

5. 读取一个地址的ETH和WETH余额。

   ```js
   console.log("\n3. 读取一个地址的ETH和WETH余额")
   //读取WETH余额
   const balanceWETH = await contractWETH.balanceOf(wallets[19])
   console.log(`WETH持仓: ${ethers.formatEther(balanceWETH)}`)
   //读取ETH余额
   const balanceETH = await provider.getBalance(wallets[19])
   console.log(`ETH持仓: ${ethers.formatEther(balanceETH)}\n`)
   ```

   

   

   ![读取余额](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071532202.png)

   

6. 利用钱包类的`sendTransaction()`发送交易，归集每个钱包中的`ETH`。

   ```js
   // 批量归集钱包的ETH
   const txSendETH = {
       to: wallet.address, // 归集到的目标地址
       value: amount // 转账的金额
   }
   for (let i = 0; i < numWallet; i++) {
       // 将钱包连接到provider
       let walletiWithProvider = wallets[i].connect(provider);
       var tx = await walletiWithProvider.sendTransaction(txSendETH);
       console.log(`第 ${i+1} 个钱包 ${walletiWithProvider.address} ETH 归集开始`);
   }
   await tx.wait();
   console.log(`ETH 归集结束`);
   
   ```

   > [!TIP]
   >
   > **资产类型**：处理的是原生 `ETH`，直接调用钱包类的 `sendTransaction()` 方法将 `ETH` 发送到目标钱包。
   >
   > **交易结构**：通过 `txSendETH` 创建一个包含目标地址和转账金额的交易对象，然后通过每个钱包发送这笔交易。
   >
   > **`sendTransaction()`**：这是一个针对原生 `ETH` 的标准交易发送方法，它通过签署交易并提交到区块链来发送 `ETH`。

   

   ![归集ETH](https://www.wtf.academy/assets/images/16-4-630e21a2b4683cf02ae1b2be4cfd5565.png)

   

7. 将`WETH`合约连接到新的钱包，然后调用`transfer()`方法归集每个钱包的`WETH`。

   ```js
   for (let i = 0; i < numWallet; i++) {
       // 将钱包连接到provider
       let walletiWithProvider = wallets[i].connect(provider);
       // 将WETH合约连接到新的钱包
       let contractConnected = contractWETH.connect(walletiWithProvider);
       var tx = await contractConnected.transfer(wallet.address, amount);
       console.log(`第 ${i+1} 个钱包 ${wallets[i].address} WETH 归集开始`);
   }
   await tx.wait();
   console.log(`WETH 归集结束`);
   
   ```

   > [!TIP]
   >
   > **资产类型**：处理的是 `WETH`（一个 ERC-20 代币），这里需要调用 `WETH` 合约的 `transfer()` 方法将代币从各个钱包发送到目标钱包。
   >
   > **交易结构**：使用 `WETH` 合约的 `transfer()` 方法将代币从每个钱包转移到指定的目标钱包。
   >
   > **`transfer()`**：这是一个针对 ERC-20 代币的标准方法，用于从一个地址向另一个地址转移代币。

   > [!NOTE]
   >
   > 归集ETH和WETH区别总结：
   >
   > 1. **资产类型**：第一段代码处理的是原生 `ETH`，而第二段代码处理的是 `WETH`（ERC-20 代币）。`ETH` 不需要合约，直接通过钱包类发送，而 `WETH` 必须通过合约方法来转账。
   > 2. **交易方法**：`ETH` 通过 `sendTransaction()` 方法直接发送，`WETH` 通过 `WETH` 合约的 `transfer()` 方法转账。
   > 3. **实现细节**：`WETH` 的归集需要将合约连接到每个钱包，而 `ETH` 的归集只需直接操作钱包实例。

   ![归集WETH](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071532713.png)

   

8. 读取一个地址在归集后的ETH和WETH余额，可以看到`ETH`和`WETH`余额减少，归集成功！

   ```js
   console.log("\n6. 读取一个地址在归集后的ETH和WETH余额")
   // 读取WETH余额
   const balanceWETHAfter = await contractWETH.balanceOf(wallets[19])
   console.log(`归集后WETH持仓: ${ethersfromPhrase.formatEther(balanceWETHAfter)}`)
   // 读取ETH余额
   const balanceETHAfter = await provider.getBalance(wallets[19])
   console.log(`归集后ETH持仓: ${ethersfromPhrase.formatEther(balanceETHAfter)}\n`)
   ```

   

   

   ![归集后余额变动](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071532078.png)

   

## 总结

这一讲，我们介绍了批量归集，并用`ethers.js`脚本将`20`个钱包的`ETH`和`WETH`归集到一个钱包中。

# 17. MerkleTree脚本

这一讲我们写一个利用`Merkle Tree`白名单铸造`NFT`的脚本，如果你对`Merkle Tree`合约不熟悉，请看[WTF Solidity极简教程第37讲：Merkle Tree](https://github.com/AmazingAng/WTF-Solidity/blob/main/36_MerkleTree/readme.md)。

## Merkle Tree

`Merkle Tree`，也叫默克尔树或哈希树，是区块链的底层加密技术，被比特币和以太坊区块链广泛采用。`Merkle Tree`是一种自下而上构建的加密树，每个叶子是对应数据的哈希，而每个非叶子为它的`2`个子节点的哈希。



![Merkle Tree](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071533460.png)



`Merkle Tree`允许对大型数据结构的内容进行有效和安全的验证（`Merkle Proof`）。对于有`N`个叶子结点的`Merkle Tree`，在已知`root`根值的情况下，验证某个数据是否有效（属于`Merkle Tree`叶子结点）只需要`log(N)`个数据（也叫`proof`），非常高效。如果数据有误，或者给的`proof`错误，则无法还原出`root`根植。下面的例子中，叶子`L1`的`Merkle proof`为`Hash 0-1`和`Hash 1`：知道这两个值，就能验证`L1`的值是不是在`Merkle Tree`的叶子中。



![Merkle Proof](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071533429.png)



## `Merkle Tree`合约简述

[WTF Solidity极简教程第36讲：Merkle Tree](https://github.com/AmazingAng/WTF-Solidity/blob/main/36_MerkleTree/readme.md)中的`MerkleTree`合约利用`Merkle Tree`验证白名单铸造`NFT`。我们简单讲下这里用到的两个函数：

1. 构造函数：初始化NFT的名称，代号，和`Merkle Tree`的`root`。
2. `mint()`：利用`Merkle Proof`验证白名单地址并铸造。参数为白名单地址`account`，铸造的`tokenId`，和`proof`。

## `MerkleTree.js`

`MerkleTree.js`是构建`Merkle Tree`和`Merkle Proof`的Javascript包（[Github连接](https://github.com/miguelmota/merkletreejs)）。你可以用`npm`安装他：

```shell
npm install merkletreejs
```



这里，我们演示如何生成叶子数据包含`4`个白名单地址的`Merkle Tree`。

1. 创建白名单地址数组。

   ```js
   import { MerkleTree } from "merkletreejs";
   // 白名单地址
   const tokens = [
       "0x5B38Da6a701c568545dCfcB03FcB875f56beddC4", 
       "0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2",
       "0x4B20993Bc481177ec7E8f571ceCaE8A9e22C02db",
       "0x78731D3Ca6b7E34aC0F824c42a7cC18A495cabaB"
   ];
   ```

   

2. 将数据进行`keccak256`哈希（与solidity使用的哈希函数匹配），创建叶子结点。

   ```js
   const leaf = tokens.map(x => ethers.keccak256(x))
   ```

   

3. 创建`Merkle Tree`，哈希函数仍然选择`keccak256`，可选参数`sortPairs: true`（[constructor函数文档](https://github.com/miguelmota/merkletreejs/blob/master/docs/classes/_src_merkletree_.merkletree.md#constructor)），与`Merkle Tree`合约处理方式保持一致。

   ```js
   const merkletree = new MerkleTree(leaf, ethers.keccak256, { sortPairs: true });
   ```

   > [!TIP]
   >
   > 使用 `merkletreejs` 库创建一个 `Merkle Tree`。这里的关键点是指定哈希函数为 `keccak256`，并设置 `sortPairs: true`，这意味着 `Merkle Tree` 的每一对节点在哈希时会自动排序，以确保树的结构与 Solidity 中的合约一致。

   

4. 获得`Merkle Tree`的`root`。

   ```js
   const root = merkletree.getHexRoot()
   ```

   

5. 获得第`0`个叶子节点的`proof`。

   ```js
   const proof = merkletree.getHexProof(leaf[0]);
   ```

   > [!TIP]
   >
   > `proof` 是一个用于验证某个地址是否在 `Merkle Tree` 中的证明。通过给定的叶子节点和 `proof`，合约可以使用 `Merkle Root` 验证这个地址是否在白名单内。
   
   

## `Merkle Tree`白名单铸造`NFT`

这里，我们举个例子，利用`MerkleTree.js`和`ethers.js`验证白名单并铸造`NFT`。

1. 生成`Merkle Tree`。

   ```js
   // 1. 生成merkle tree
   console.log("\n1. 生成merkle tree")
   // 白名单地址
   const tokens = [
       "0x5B38Da6a701c568545dCfcB03FcB875f56beddC4", 
       "0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2",
       "0x4B20993Bc481177ec7E8f571ceCaE8A9e22C02db",
       "0x78731D3Ca6b7E34aC0F824c42a7cC18A495cabaB"
   ];
   // leaf, merkletree, proof
   const leaf       = tokens.map(x => ethers.keccak256(x))
   const merkletree = new MerkleTree(leaf, ethers.keccak256, { sortPairs: true });
   const proof      = merkletree.getHexProof(leaf[0]);
   const root = merkletree.getHexRoot()
   console.log("Leaf:")
   console.log(leaf)
   console.log("\nMerkleTree:")
   console.log(merkletree.toString())
   console.log("\nProof:")
   console.log(proof)
   console.log("\nRoot:")
   console.log(root)
   ```

   

   

   ![生成Merkle Tree](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071532365.png)

   

2. 创建provider和wallet

   ```js
   // 准备 alchemy API 可以参考https://github.com/AmazingAng/WTF-Solidity/blob/main/Topics/Tools/TOOL04_Alchemy/readme.md 
   const ALCHEMY_GOERLI_URL = 'https://eth-goerli.alchemyapi.io/v2/GlaeWuylnNM3uuOo-SAwJxuwTdqHaY5l';
   const provider = new ethers.JsonRpcProvider(ALCHEMY_GOERLI_URL);
   // 利用私钥和provider创建wallet对象
   const privateKey = '0x227dbb8586117d55284e26620bc76534dfbd2394be34cf4a09cb775d593b6f2b'
   const wallet = new ethers.Wallet(privateKey, provider)
   ```

   

3. 创建合约工厂，为部署合约做准备。

   ```js
   // 3. 创建合约工厂
   // NFT的abi
   const abiNFT = [
       "constructor(string memory name, string memory symbol, bytes32 merkleroot)",
       "function name() view returns (string)",
       "function symbol() view returns (string)",
       "function mint(address account, uint256 tokenId, bytes32[] calldata proof) external",
       "function ownerOf(uint256) view returns (address)",
       "function balanceOf(address) view returns (uint256)",
   ];
   // 合约字节码，在remix中，你可以在两个地方找到Bytecode
   // i. 部署面板的Bytecode按钮
   // ii. 文件面板artifact文件夹下与合约同名的json文件中
   // 里面"object"字段对应的数据就是Bytecode，挺长的，608060起始
   // "object": "608060405260646000553480156100...
   const bytecodeNFT = contractJson.default.object;
   const factoryNFT = new ethers.ContractFactory(abiNFT, bytecodeNFT, wallet);
   ```

   > [!NOTE]
   >
   > ### 2. **`bytecodeNFT`**
   >
   > `bytecodeNFT` 是合约的字节码，也就是合约在 EVM 上执行的机器码。通常，字节码是在编译 Solidity 合约后生成的，可以从 Remix IDE 或编译器的生成文件中找到。
   >
   > - 你提到的 `bytecodeNFT` 是从 JSON 文件中读取的 `object` 字段，它包含合约的实际字节码。字节码是一个非常长的 16 进制字符串，通常以 `608060` 开头。
   >
   > ### 3. **`ethers.ContractFactory`**
   >
   > `ContractFactory` 是 `ethers.js` 中用于创建和部署智能合约的类。
   >
   > - **参数1**：`abiNFT`。这个参数是合约的 ABI，用于定义合约的接口和交互方式。
   > - **参数2**：`bytecodeNFT`。这是合约的字节码，表示合约的实际代码，它会被部署到以太坊网络。
   > - **参数3**：`wallet`。这是一个 `ethers.Wallet` 实例，表示用哪个钱包签署和发送交易（合约部署交易）。这个钱包通常包含用于支付部署费用的 ETH。

   

4. 利用contractFactory部署NFT合约

   ```js
   console.log("\n2. 利用contractFactory部署NFT合约")
   // 部署合约，填入constructor的参数
   const contractNFT = await factoryNFT.deploy("WTF Merkle Tree", "WTF", root)
   console.log(`合约地址: ${contractNFT.target}`);
   console.log("等待合约部署上链")
   await contractNFT.waitForDeployment()
   console.log("合约已上链")
   ```

   

   

   ![部署Merkle Tree合约](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071532967.png)

   

5. 调用`mint()`函数，利用`merkle tree`验证白名单，并给第`0`个地址铸造`NFT`。在`mint`成功后可以看到`NFT`余额变为`1`。

   ```js
   console.log("\n3. 调用mint()函数，利用merkle tree验证白名单，给第一个地址铸造NFT")
   console.log(`NFT名称: ${await contractNFT.name()}`)
   console.log(`NFT代号: ${await contractNFT.symbol()}`)
   let tx = await contractNFT.mint(tokens[0], "0", proof)
   console.log("铸造中，等待交易上链")
   await tx.wait()
   console.log(`mint成功，地址${tokens[0]} 的NFT余额: ${await contractNFT.balanceOf(tokens[0])}\n`)
   ```

   

   

   ![白名单铸造](https://www.wtf.academy/assets/images/17-5-92ccfd103926480eba8eb30929d8f4f8.png)

   

## 用于生产环境

在生产环境使用`Merkle Tree`验证白名单发行`NFT`主要有以下步骤：

1. 确定白名单列表。
2. 在后端生成白名单列表的`Merkle Tree`。
3. 部署`NFT`合约，并将`Merkle Tree`的`root`保存在合约中。
4. 用户铸造时，向后端请求地址对应的`proof`。
5. 用户调用`mint()`函数进行铸造`NFT`。

## 总结

这一讲，我们简单介绍了`Merkle Tree`，并利用`MerkleTree.js`和`ethers.js`创建、验证白名单，铸造`NFT`。

# 18. 数字签名脚本

这一讲，我们介绍一个利用链下签名作为白名单发放`NFT`的方法。如果你对`ECDSA`合约不熟悉，请看[WTF Solidity极简教程第37讲：数字签名](https://github.com/AmazingAng/WTF-Solidity/blob/main/37_Signature/readme.md)。

## 数字签名

如果你用过`opensea`交易`NFT`，对签名就不会陌生。下图是小狐狸（`metamask`）钱包进行签名时弹出的窗口，它可以证明你拥有私钥的同时不需要对外公布私钥。



![metamask签名](https://www.wtf.academy/assets/images/18-1-6c4059d562d3a3c6eeb7a39bf69dceef.png)



以太坊使用的数字签名算法叫双椭圆曲线数字签名算法（`ECDSA`），基于双椭圆曲线“私钥-公钥”对的数字签名算法。它主要起到了[三个作用](https://en.wikipedia.org/wiki/Digital_signature)：

1. **身份认证**：证明签名方是私钥的持有人。
2. **不可否认**：发送方不能否认发送过这个消息。
3. **完整性**：消息在传输过程中无法被修改。

## 数字签名合约简述

[WTF Solidity极简教程第37讲：数字签名](https://github.com/AmazingAng/WTF-Solidity/blob/main/37_Signature/readme.md)中的`SignatureNFT`合约利用`ECDSA`验证白名单铸造`NFT`。我们讲下两个重要的函数：

1. 构造函数：初始化NFT的名称，代号，和签名公钥`signer`。
2. `mint()`：利用`ECDSA`验证白名单地址并铸造。参数为白名单地址`account`，铸造的`tokenId`，和签名`signature`。

## 生成数字签名

1. 打包消息：在以太坊的`ECDSA`标准中，被签名的`消息`是一组数据的`keccak256`哈希，为`bytes32`类型。我们可以利用`ethers.js`提供的`solidityPackedKeccak256()`函数，把任何想要签名的内容打包并计算哈希。等效于`solidity`中的`keccak256(abi.encodePacked())`。

   在下面的代码中，我们将一个`address`类型变量和一个`uint256`类型变量打包后哈希，得到`消息`：

   ```js
   // 创建消息
   const account = "0x5B38Da6a701c568545dCfcB03FcB875f56beddC4"
   const tokenId = "0"
   // 等效于Solidity中的keccak256(abi.encodePacked(account, tokenId))
   const msgHash = ethers.solidityPackedKeccak256(
       ['address', 'uint256'],
       [account, tokenId])
   console.log(`msgHash：${msgHash}`)
   // msgHash：0x1bf2c0ce4546651a1a2feb457b39d891a6b83931cc2454434f39961345ac378c
   ```

   

2. 签名：为了避免用户误签了恶意交易，`EIP191`提倡在`消息`前加上`"\x19Ethereum Signed Message:\n32"`字符，再做一次`keccak256`哈希得到`以太坊签名消息`，然后再签名。`ethers.js`的钱包类提供了`signMessage()`函数进行符合`EIP191`标准的签名。注意，如果`消息`为`string`类型，则需要利用`arrayify()`函数处理下。例子：

   ```js
   // 签名
   const messageHashBytes = ethers.getBytes(msgHash)
   const signature = await wallet.signMessage(messageHashBytes);
   console.log(`签名：${signature}`)
   // 签名：0x390d704d7ab732ce034203599ee93dd5d3cb0d4d1d7c600ac11726659489773d559b12d220f99f41d17651b0c1c6a669d346a397f8541760d6b32a5725378b241c
   ```

   

## 链下签名白名单铸造`NFT`

1. 创建`provider`和`wallet`，其中`wallet`是用于签名的钱包。

   ```js
   // 准备 alchemy API 可以参考https://github.com/AmazingAng/WTF-Solidity/blob/main/Topics/Tools/TOOL04_Alchemy/readme.md 
   const ALCHEMY_GOERLI_URL = 'https://eth-goerli.alchemyapi.io/v2/GlaeWuylnNM3uuOo-SAwJxuwTdqHaY5l';
   const provider = new ethers.JsonRpcProvider(ALCHEMY_GOERLI_URL);
   // 利用私钥和provider创建wallet对象
   const privateKey = '0x227dbb8586117d55284e26620bc76534dfbd2394be34cf4a09cb775d593b6f2b'
   const wallet = new ethers.Wallet(privateKey, provider)
   ```

   

2. 根据白名单地址和他们能铸造的`tokenId`生成`消息`并签名。

   ```js
   // 创建消息
   const account = "0x5B38Da6a701c568545dCfcB03FcB875f56beddC4"
   const tokenId = "0"
   // 等效于Solidity中的keccak256(abi.encodePacked(account, tokenId))
   const msgHash = ethers.solidityPackedKeccak256(
       ['address', 'uint256'],
       [account, tokenId])
   console.log(`msgHash：${msgHash}`)
   // 签名
   const messageHashBytes = ethers.getBytes(msgHash)
   const signature = await wallet.signMessage(messageHashBytes);
   console.log(`签名：${signature}`)
   ```

   

   

   ![创建签名](https://www.wtf.academy/assets/images/18-2-3e710b694092c8ba288677f88ffdfa8c.png)

   

3. 创建合约工厂，为部署`NFT`合约做准备。

   ```js
   // NFT的人类可读abi
   const abiNFT = [
       "constructor(string memory _name, string memory _symbol, address _signer)",
       "function name() view returns (string)",
       "function symbol() view returns (string)",
       "function mint(address _account, uint256 _tokenId, bytes memory _signature) external",
       "function ownerOf(uint256) view returns (address)",
       "function balanceOf(address) view returns (uint256)",
   ];
   // 合约字节码，在remix中，你可以在两个地方找到Bytecode
   // i. 部署面板的Bytecode按钮
   // ii. 文件面板artifact文件夹下与合约同名的json文件中
   // 里面"object"字段对应的数据就是Bytecode，挺长的，608060起始
   // "object": "608060405260646000553480156100...
   const bytecodeNFT = contractJson.default.object;
   const factoryNFT = new ethers.ContractFactory(abiNFT, bytecodeNFT, wallet);
   ```

   

4. 利用合约工厂部署NFT合约。

   ```js
   // 部署合约，填入constructor的参数
   const contractNFT = await factoryNFT.deploy("WTF Signature", "WTF", wallet.address)
   console.log(`合约地址: ${contractNFT.target}`);
   console.log("等待合约部署上链")
   await contractNFT.waitForDeployment()
   // 也可以用 contractNFT.deployTransaction.wait()
   console.log("合约已上链")
   ```

   

   

   ![部署NFT合约](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071533307.png)

   

5. 调用`NFT`合约的`mint()`函数，利用链下签名验证白名单，为`account`地址铸造`NFT`。

   ```js
   console.log(`NFT名称: ${await contractNFT.name()}`)
   console.log(`NFT代号: ${await contractNFT.symbol()}`)
   let tx = await contractNFT.mint(account, tokenId, signature)
   console.log("铸造中，等待交易上链")
   await tx.wait()
   console.log(`mint成功，地址${account} 的NFT余额: ${await contractNFT.balanceOf(account)}\n`)
   ```

   

   

   ![验证签名并铸造NFT](https://www.wtf.academy/assets/images/18-4-7f3e6546ce9608a8fea6b867b011aa4c.png)

   

## 用于生产环境

在生产环境使用数字签名验证白名单发行`NFT`主要有以下步骤：

1. 确定白名单列表。
2. 在后端维护一个签名钱包，生成每个白名单对应的`消息`和`签名`。
3. 部署`NFT`合约，并将签名钱包的公钥`signer`保存在合约中。
4. 用户铸造时，向后端请求地址对应的`签名`。
5. 用户调用`mint()`函数进行铸造`NFT`。

## 总结

这一讲，我们介使用`ethers.js`配合智能合约，以链下数字签名的方式验证白名单并发行`NFT`。`Merkle Tree`和链下数字签名是目前最主流也最经济的发放白名单方式。如果合约部署的时候已经确定好白名单列表，那么建议用`Merkle Tree`；如果在合约部署之后要不断添加白名单，例如Galaxy Project的`OAT`，那么建议用链下签名的方式，不然就要不断更新合约中`Merkle Tree`的`root`，耗费更多的gas。

# 19. 监听Mempool

这一讲，我们将介绍如何读取`mempool`（交易内存池）中的交易。

## MEV

`MEV`（Maximal Extractable Value，最大可提取价值）是个令人着迷的话题。大部分人对它很陌生，因为在支持智能合约的区块链被发明之前它并不存在。它是科学家的盛宴，矿场的友人，散户的噩梦。

在区块链中，矿工可以通过打包、排除或重新排序他们产生的区块中的交易来获得一定的利润，而`MEV`是衡量这种利润的指标。

## Mempool

在用户的交易被矿工打包进以太坊区块链之前，所有交易会汇集到Mempool（交易内存池）中。矿工也是在这里寻找费用高的交易优先打包，实现利益最大化。通常来说，gas price越高的交易，越容易被打包。

同时，一些`MEV`机器人也会搜索`mempool`中有利可图的交易。比如，一笔滑点设置过高的`swap`交易可能会被三明治攻击：通过调整gas，机器人会在这笔交易之前插一个买单，之后发送一个卖单，等效于把把代币以高价卖给用户（抢跑）。



![Mempool](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071533684.png)



## 监听mempool

你可以利用`ethers.js`的`Provider`类提供的方法，监听`mempool`中的`pending`（未决，待打包）交易：

```js
provider.on("pending", listener)
```



## 监听mempool脚本

下面，我们写一个监听`mempool`脚本。

1. 创建`provider`和`wallet`。这次我们用的`provider`是WebSocket Provider，更持久的监听交易。因此，我们需要将`url`换成`wss`的。

   ```js
   console.log("\n1. 连接 wss RPC")
   // 准备 alchemy API 可以参考https://github.com/AmazingAng/WTF-Solidity/blob/main/Topics/Tools/TOOL04_Alchemy/readme.md 
   const ALCHEMY_MAINNET_WSSURL = 'wss://eth-mainnet.g.alchemy.com/v2/oKmOQKbneVkxgHZfibs-iFhIlIAl6HDN';
   const provider = new ethers.WebSocketProvider(ALCHEMY_MAINNET_WSSURL);
   ```

   

2. 因为`mempool`中的未决交易很多，每秒上百个，很容易达到免费`rpc`节点的请求上限，因此我们需要用`throttle`限制请求频率。

   ```js
   function throttle(fn, delay) {
       let timer;
       return function(){
           if(!timer) {
               fn.apply(this, arguments)
               timer = setTimeout(()=>{
                   clearTimeout(timer)
                   timer = null
               },delay)
           }
       }
   }
   ```

   

3. 监听`mempool`的未决交易，并打印交易哈希。

   ```js
   let i = 0
   provider.on("pending", async (txHash) => {
       if (txHash && i < 100) {
           // 打印txHash
           console.log(`[${(new Date).toLocaleTimeString()}] 监听Pending交易 ${i}: ${txHash} \r`);
           i++
           }
   });
   ```

   

   

   ![获取pending交易哈希](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071533453.png)

   

4. 通过未决交易的哈希，获取交易详情。我们看到交易还未上链，它的`blockHash`，`blockNumber`，和`transactionIndex`都为空。但是我们可以获取到交易的发送者地址`from`，燃料费`gasPrice`，目标地址`to`，发送的以太数额`value`，发送数据`data`等等信息。机器人就是利用这些信息进行`MEV`挖掘的。

   ```js
   let j = 0
   provider.on("pending", throttle(async (txHash) => {
       if (txHash && j <= 100) {
           // 获取tx详情
           let tx = await provider.getTransaction(txHash);
           console.log(`\n[${(new Date).toLocaleTimeString()}] 监听Pending交易 ${j}: ${txHash} \r`);
           console.log(tx);
           j++
           }
   }, 1000));
   ```

   

   

   ![获取交易详情](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071533897.png)

   

## 总结

这一讲，我们简单介绍了`MEV`和`mempool`，并写了个脚本监听`mempool`的未决交易。

# 20. 解码交易详情

这一讲，我们以未决交易（Pending Transaction）为例，介绍如何解码交易详情。

## 未决交易

未决交易是用户发出但没被矿工打包上链的交易，在mempool（交易内存池）中出现。对于`mempool`的更多介绍可以看[WTF Ethers极简教程第19讲：监听Mempool](https://github.com/WTFAcademy/WTF-Ethers/blob/main/19_Mempool/readme.md)

下面是一个转账`ERC20`代币的未决交易，你可以在[etherscan](https://etherscan.io/tx/0xbe5af8b8885ea9d6ae8a2f3f44315554ff62daebf3f99b42eae9d4cda880208e)上查看交易详情：



![ERC20未决交易](https://www.wtf.academy/assets/images/20-1-52fbf68f5fbfdf0a4308de635c3b6322.png)



红框中是这个交易的`input data`，看似杂乱无章的十六进制数据，实际上编码了这笔交易的内容：包括调用的函数，以及输入的参数。我们在etherscan点击**Decode Input Data**按钮，就可以解码这段数据：



![Decode Input Data](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071534012.png)



解码之后，我们可以看到这笔交易调用的函数以及输入的参数。

## Interface类

`ethers.js`提供了`Interface`类方便解码交易数据。声明`Interface`类型和声明`abi`的方法差不多，例如：

```js
const iface = ethers.Interface([
    "function balanceOf(address) public view returns(uint)",
    "function transfer(address, uint) public returns (bool)",
    "function approve(address, uint256) public returns (bool)"
]);
```



## 解码交易数据

下面我们写一个解码未决交易数据的脚本。

1. 创建`provider`和`wallet`，监听交易时候推荐用`wss`连接而不是`http`。

   ```js
   // 准备 alchemy API 可以参考https://github.com/AmazingAng/WTF-Solidity/blob/main/Topics/Tools/TOOL04_Alchemy/readme.md 
   const ALCHEMY_MAINNET_WSSURL = 'wss://eth-mainnet.g.alchemy.com/v2/oKmOQKbneVkxgHZfibs-iFhIlIAl6HDN';
   const provider = new ethers.WebSocketProvider(ALCHEMY_MAINNET_WSSURL);
   let network = provider.getNetwork()
   network.then(res => console.log(`[${(new Date).toLocaleTimeString()}] 连接到 chain ID ${res.chainId}`));
   ```

   

2. 创建`Interface`对象，用于解码交易详情。

   ```js
   const iface = new ethers.Interface([
   "function transfer(address, uint) public returns (bool)",
   ])
   ```

   

3. 获取函数选择器。

   ```js
   const selector = iface.getFunction("transfer").selector
   console.log(`函数选择器是${selector}`)
   ```

   

4. 监听`pending`的`ERC20` 转账交易，获取交易详情并解码：

   ```js
   // 处理bigInt
   function handleBigInt(key, value) {
       if (typeof value === "bigint") {
           return value.toString() + "n"; // or simply return value.toString();
       }
   return value;
   }
   
   provider.on('pending', async (txHash) => {
   if (txHash) {
       const tx = await provider.getTransaction(txHash)
       j++
       if (tx !== null && tx.data.indexOf(selector) !== -1) {
           console.log(`[${(new Date).toLocaleTimeString()}]监听到第${j + 1}个pending交易:${txHash}`)
           console.log(`打印解码交易详情:${JSON.stringify(iface.parseTransaction(tx), handleBigInt, 2)}`)
           console.log(`转账目标地址:${iface.parseTransaction(tx).args[0]}`)
           console.log(`转账金额:${ethers.formatEther(iface.parseTransaction(tx).args[1])}`)
           provider.removeListener('pending', this)
       }
   }})
   ```

   

   

   ![监听并解码交易](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071534045.png)

   

5. 交易参数解码：

   

   ![交易参数解码](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAbMAAAAlCAYAAADIpQdtAAABYWlDQ1BJQ0MgUHJvZmlsZQAAKJFtkD9LA0EQxd/FSDSmSFCsUqSTSJR4ESSNEKP4hxRHVDR2l714US9xuZyInZ3YWIl+A7GzTJPCWiwEQcFKUPADCFdE4zmbU5Ooswzz4zFvd3YAT0Dl3PACKJUtMzs7FVnNrUV8L+iFF/0II6qyCk8pSoZa8F07w76DJOrtiLir/rTgP6r3MM9HKBy8Prz4298Rfq1QYVTfKWXGTQuQ4sTKrsUF7xMPmDQU8bFg3eVzwXmXa82epWya+IY4yIqqRvxIHMu36Xobl4wd9jWDmD5QKC8vUh2kDGMaM8jQiUCBjAmMIYk52tH/nvGmJ41tcOzBxAZ0FGGRO0UKh4EC8TzKYBhFjFhGnDIhdv17hy1NOwASw/SUv6VtPgO1UyB01dKGtug7k8Bljqum+rNZyfZW1hOyy31VoPvEcV5XAF8UaNw7zlvVcRpnQNcDee1P6uRiqrCQi5kAAABWZVhJZk1NACoAAAAIAAGHaQAEAAAAAQAAABoAAAAAAAOShgAHAAAAEgAAAESgAgAEAAAAAQAAAbOgAwAEAAAAAQAAACUAAAAAQVNDSUkAAABTY3JlZW5zaG90PKfb8wAAAdVpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IlhNUCBDb3JlIDYuMC4wIj4KICAgPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4KICAgICAgPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIKICAgICAgICAgICAgeG1sbnM6ZXhpZj0iaHR0cDovL25zLmFkb2JlLmNvbS9leGlmLzEuMC8iPgogICAgICAgICA8ZXhpZjpQaXhlbFlEaW1lbnNpb24+Mzc8L2V4aWY6UGl4ZWxZRGltZW5zaW9uPgogICAgICAgICA8ZXhpZjpQaXhlbFhEaW1lbnNpb24+NDM1PC9leGlmOlBpeGVsWERpbWVuc2lvbj4KICAgICAgICAgPGV4aWY6VXNlckNvbW1lbnQ+U2NyZWVuc2hvdDwvZXhpZjpVc2VyQ29tbWVudD4KICAgICAgPC9yZGY6RGVzY3JpcHRpb24+CiAgIDwvcmRmOlJERj4KPC94OnhtcG1ldGE+CoJBHXsAABsRSURBVHgB7Z0FtB01E4BTWqC4uxUv7tpDKS3uTilW3J3i0OLursWluDstDgd3d3eXYvnnm3b25O7dzd53+947/yvJOfdmNzLJTmQykqSTF+dGuq+++soNGzbMbbHFFu6HH35wY489tkWN9n6AhtH+W9MHJgwkDCQMjG4Y6BJ+0Omnn+6eeuoph/9fIWSJiIU9ID0nDCQMJAx0TAx0CjmzjvkJ9bVOBKoeJykkYSBhIGFgdMZADWfWUT40EauO0lKpngkDCQMJA+2DgTHap5jWKyURstbDZYKUMJAwkDAwumCgjph98803Lk8wfv75Z/fdd9+16Jt//PFH99tvv7UoT1XisF4//fST+/vvv6uy1MX/9ddfdWG//vqrGrzURQQBGMTkHfX55JNP8sHpPWEgYSBhIGGgnTFQozODOEw22WTu008/deOPP35WlRNPPNF9+OGH7owzzsjC7OH7779322yzjb2qf9JJJzl+8803n9tuu+2UOJKXdOOOO26WFiJ5wAEHZO9FD0cddZSbcMIJ66KWXnppd+qpp7rFF1/c3XLLLe6tt96qSdO1a1e366671oR98MEHbvnll3fvvPOOhkOMOnXq5M455xz35ptvKryaDCNfvv32WzfzzDM7CGjoPv74Y7fEEku4zz77LAyuWwzUROZeIIZTTDFFuxnctHd5uc9t+JW2eeONN7TfzTTTTG6uueZqOG9VwnvvvdfNPvvs2qZVaavisQCeZJJJ3JhjjlmT1BY6U045Zbu1bU0Fgpe2rksRPmPtV4YzqhyLawZm1bc3A5N6fvnll27iiSducdu2xfiL4Yy6/ldcxpldeOGFbq211nLDhw93W221ldtoo43cJZdc4jbccEN37rnnqsk+z/yeffbZDD9//PGHe+6559y+++6rPxoZAhe6ww8/3F133XWuS5daFR2c26WXXup69epV91t22WXdlVde6X755ZcQVOEzE0nRrzDxyEA68TjjjBNLokSJdPxw9hz6EMPw3dJGAUskhHD++ed3c845p06G559/flUW9/777ysOwWP423zzzbO8gwcPdpNPPrnbeeedszAeYuVNMMEEGbzpp5/eDRw40P377781+Q855BAlKLR33hXFrb/++hlMq+tHH32UZWWBgMXsMccck4XZA2WzENpkk03cFVdc4R588EGNqoJp+av8ww47zD3yyCNVydxqq61W9w3WTlj99unTx3Xr1s1NNNFEDpjmHnroIQ2fZZZZdMI79NBDLSrqx8pr5Ntp8379+tWUEatLGcxG+llYSB6fZe0Xw1ksjrKagRn79mZhPvzww46F9GyzzeYmnXRSXaD/888/io5Y+8XGH5nLxi1xZWOlDGcs2m3MwZQstthi7vrrrweUulg9LU2H9GXyVSerYL/OOuv4/v37+6uvvtrff//9njB8WYF4mVT0mXdBrmXzwpX4ueee2wvB80cffbRfZZVVvBA3v8suu3jhzvy2227ru3fv7mX1kOWxhy+++MILJ+iloxb+pplmGi8rmZo4YAsR8NJYXjqUHzRoUE18GSzKuu222/x0003nhRj733//3Y811lheOqI/88wz/QorrOD33ntvv/DCC3sZzBpO3KuvvuqHDBnihfD5u+++28uE7GXS8C+//LKXTuOpI+liP8r+888/a9Kst956np8sHvxNN93kO3fu7IX7rUmThymcsxcxcPb7+uuv/bzzzuuFc/ayMPDCdfqpp57aC7fot99++xpYsfKEi/UyuStcWcBAub0M2iw/z0J4/JNPPpmFWd3K4nr06KF4o93tR/0tnwxeL1y6l4GWhVnc0KFDFa95nFXBtPxV/pJLLukpvyrdiiuu6A8++GAvkorsJ4srzTfHHHP4PfbYQ/F+5513Ks5ee+01LyJrP9VUU/ndd9/di2jaP/DAA9p3RHowSuVVfTt1pB2feeaZrJyqupTBjPWzIpzl8VnWfmU4A2YsjvihJX2iLF/VtzcDkzzMZTvuuKPOH8wBjAvmFeJi/aVs/FWNW+CWjZWybxfJk/bHt99+W+cv5mXmy7vuuquynpTXUX9wFeogArLK9MJB6YRO4IEHHug322wzRcyWW27phWPT3+WXXz4ik/yHxExEgjXEbM8999T8Ip7L0ocPTPJMnMLdFP6IyxMz6smkT+MwUQyVTs7kXfQ75ZRTsoaRFbUSXQjYIoss4l9//XUte/XVV1eiBmE8+eSTvXAm/t13383yQaRXWmklrd8aa6yhHZfB++ijjyoxY0KGuPGT1VeWzzoERIK6br311lkcHZh6yMpKw/hGFgzUl7hFF11UFwfAEC7XC5eSDRiDi0/nZDEAfiFssipXf7fddqshZrHygMMk+PTTT2tdRKfohbNTQkSciIK9cBheuOus/laHWBz4NJiWPvRZOAETPIR4oyyIgXDaXkS7+mORQd4YTPoSbUl7iNjW095WHm01zzzz6HeecMIJPpx8IbRySIAuAkSU6UVkluVjcjr++OOzd4MHkRXxeU29aYc77rhDF0osTFjwWXqRZihx472Z8sgX+3biRTKi/dTKxGfRFqtLFUyDFfYzwmL4LGu/GM5icZTXDMyqb28GJnVh8XrNNddkbQsckWrpe1l/iY2/2Lg1/BeNlRjOjJgxLxgMUfEoseW9rJ6WtqP6mZjx8ccfV3EZoh9ESbLKVJ0CxhHopRZYYAEViyEakwaNcqFCDJysClREKBOMk8HghLtRMRkZhaDpj2d0dIK8wl9ZOei40O8J9+FmmGEGd8QRR+gP9h/9hb1TtjkhJk5WUA4x2hNPPOGEA9MoIVRuwIABbtVVV3WymnbjjTeesuiWTzhLJ8Rbw2+++WZNR/3NyWThpp12Wv0J0bLgzCctdcWwxtznn3/upDM64apULyQrZI1CDAf+99lnH7fffvs5maAdIjyZ3LVcy28+3ymES+uGyIN64uddrDxL+8ILLzjhMNxOO+2korHevXtr1FlnnaUiSpmo3XLLLVcjrojFyaTthBBofWgj2t8c/Qs9S9++fZ0QFnf77bdblLvhhhucLKK0nW688UbHz3SfMZiI/xDl0EZCsJysnjPdKHrZGWec0fENwk3rwQDWhojAwTN1QMwukomsLjygP37++eezH3WnzemDtDtOFlXa15daainVf9KfQ5Hqe++9l+lWmimPMmLfjnESqgC+k7pedNFFZKmsSwymAhj5F/YzgmL4LGu/GM5icZTXDEz00LF2aAYmddlhhx10TJ522mmOOUUkPDVjs6i/xMZfbNxSXtlYqcIZeUPHPIddgLmielpch/VlUKsTYqacy6yzzqqrYkSHcF2ij9HVqVgnevtZHnzjzGRwe+PMEM3IBOZZ6bKSYVWMGA8xXSgGZDXdUjEjqxxgyuTkRfbrZQLyiHBYcV9wwQUeDpJnRHf5FQYcFyspwqWDZWJGmZQ93Azh1BtRHs+IW/iJHtCL7Dl7hws0zoy6WLoyH9Eo4imLRxQE54GIju+HQ4GLlYk0S7P22mt7mRy9GL8op2h5zUfcK7ourauFmW+cmb1XlQdnBl7EKEK5VSHsylnApcHlIAqUwa+U6LB8LA4RjwwIv/HGG3tZOKgoeIwxxlARGHW69dZbVazEMyKQlVdeOftuwmhP+o7VH78K5oILLuhlEs/yIPqRwavtTNmIAIEjk4OXBY+/+OKL9Z3vIByRIGmoN5wyYaxg4fTgVO334osvahzx/Oj/QtS8TG5ZuOh7Vfx79tln+0033VRhCpHV+GbKq/p2ITYekSH1ueyyy5RDs/qV1aUKpuXP9zPGTQyf5CtqP4OHX4Qziy+LawZm2bdbWc3ApF8x7hgXQlA84xRcArOsv1SNP6tPftwSXjVWSJPHmXFmzNcGGymWLNSj9bS0HdXPWAlWlaIfUo5MRIuZkcdLL73kBKHu2GOP1ZUOJvcYeGDJEzpBqHJZhK277rpq6o4SXwavg1PDurHIodzEsqzIsXIMndBOd9VVV6mxiOi1lHsZOnSog0NAqWkOww4hZm7NNde0oDofIwkcMM0XgqLfhkLfwjWy5K+RNGSFmw0dqzHwAjcookUnBNjBAYZcFVacsghQTglrvrw78sgjdZWYb4d8Ot4bKU9EJ8qtithDcYlBDxwS73DWQiyUc8H4RyYBR53K4nr27KlWiHDWMvGpAhquD24MOPQnWZQ4+hkrRBTZGPqEFrR53MKxYlFbBpO+a9w23yy6WzwHx0l/EP2CvsM90y/N3XPPPe6ggw5S2IZ/WXBZtBrDiJgzew8fMJYSXYhj7GB8YQ7uEG6GPggniFTD+mez5ZV9OwZEHD83WAx/ilxZXTBcKoNJG5nL9zPaK4ZPy5dvPwsvwxnxsTjiWwqz7NuBZa4lMOnvG2ywgVo9w5UxP2EdDbfNeMVhPJXvL3DpVePd6pP3q8ZKEc6Kvom6I+ExV1RPi+uofiZmFE5ERYNYAIF8LLUYJIgtIF4QHQas6BfqCBkfLzooFWvkEcFgv/baa0v3hDEZI/4p+kFUcDSONRBEDHEgDgtGLC9l9ehgo80JF+juu+8+e63JT6cSIwf3yiuv1MQzuMV4QsVoPOcd5Qsn5ZiMcFaffLr8OxMjxABib45yhBvSCQ+xFrCYdCEQPPNDjAExw6KTvBaOL1yhEgCIbxgePlOWvVeVZ/UiPUSeASociBIi4ggzWDxDeCBSZXEMHMRwDDTLR1siDgMfiPToF6IbVAKJaBi8WloFLH/2jh+DSTyiTETjlgfixmQDgZKVs/Zp4ujnJm7hHRyymCDtY489ZkUrHHsxmHmfrSb0JwhJGAdRPu6443QBJ1yeY2sLrtnyYt9OvyEeESl9iv4ELhkb4LqsLjGY9i1F/awKn+Q1Z3BCvwxnpInFNQOz7NutPi2FCa7pP8Jta1a2XaDKYDEGTHMG3/yq8WfpDIa9NzJWinBm9cA3WKhY2N5iZYRxlqaj+xlnhp4GvYNY+6nOCCRBIOCyaIyFFlpI9R6Y4YeOlTKTNQSEVSIrUiZhc6wGQCKTMoQw75D92qrZ4gzhrMbt2eKoZ7jvDLisyOHuzNxaRKU6sOEqbRXOwBQxpEN+zYp5mWWWMZBORGy6/w0Td3QPdE5W65RNWrgWJkQIp1hPZvnsIV9HC8enEzFx0+mBhWOigWuEgMOdQCTFMsqJolfjeWcBAEHhe9GLsbXBHKtA6oJeIHTofnAQGyZZ3iHMtEGsPPKwKZ5VN/pEcArXiH5RjARUR4AJPQsbVrvgKBYHcWKrB/oEuDvaBQ5arP+cGIU49hfyDbQvDiIEnuhruCJ8xmCSh7563nnnOTHuUeIPJyTiHe1b7BHEfFzE34pHto/gKIeFGhMUhJa+a+H6IH/oOtF5mYOY0//gWERsroTZJAjU0fqmiGqUsNDne/XqpdmbLS/27fT9sH7oglgssGCzRVlRXWIw7VuL+hmLhjJ8Wr6i9iMuhrNYHHmbgUm+om8nHNdSmOi46StIU1hQs7BmXIa6+bL+Eht/ZeMWzjk2VspwNuLrnPYLFpTMO2Khni3EiS+rp+XtkL40qDp0OrISUFNOGSAW7DHvRIciH+dFEa9pskh5kMb1MmA9Ogvp/GqJh17LLPywxBElvuqGpPHrdGbojjDjL/qhrwgt3SjLfuit0Mdgjs5WAuS86MrQmfGMtRnvPPMbLKbYslpWE2vesQbCypDtBzLxZz+sDtlSYGHoVkTE6oUwql4FazdMYmXDtuonZKWqFnCE52EBA6tJZOxYmxlMfBE/qZkv+gf0UOhXCAd3WJlh2ci7dGjVm8k+EX3nm0kvE1gNPPR8tFH+JwRD05WVRxnozCwf+k1R8KvVHXHoiNBPEk9daSfCq+LQj6IPJB+6BWCSB18GfwaDMCxowSNtwrvpMngOf2UwSUPfEhGQlieLLy8DPcuL3gcrVeoihMWLQZPq18gn0gftB9SR7Qz0CXBOHDoQw4v5bOOQCUKtWy3MfHRXVl9Z9KglJro4C2u2PPLFvj2ET39le0wYVlaXGMyyfgbcGD6JL2q/GM5icfYdLYVp+cq+vZl6kgfLRfoS/QQLZKy9hcuN9hfylY2/2LiNjRV0v7JYqeuf9EE5QCILZ2wzn6PzNpyU9WuL76h+zQkgMijrdGaE4ZDdsrLea6+9nExoIwLlnxU4HB1cBpaJcBeiFFXLOjgE5MdwJqyMEVEAwxwrWrgoIToWVOPvv//+qsczqzGLFBrqsADkBBAxVFEujNUvnAwiHU4dgcugPOT7OPLknRBhtZaDO8SRBo4DnRAcSd4hMsKCsswhTwdm3gHXVsn5OOnkDnGFEO58VJu8N1seomfwGeq1rIJlcYhJsDDk+6wdLE+zfhVMxGf0QxODWjkyQJVTNM7JwvGxGKONqGOsrcI8o/LcbHlV395MnZqFGcNnM/XoaHno10iskLK0xDU7/lpSxn81bR0xY6AxaRdN5sThkM2bQ5TEgMCknYmANMQjtgmNE2DPmWDCSZ18EKBQ4Wxw8dF7ILpEaY8DvjlM/zG3NlEVR01BlKwelq5RP4TdaJ6ULmEgYSBhIGHg/wMDdcSsmWo1QwgazdNIukbS2He1JK3lKfJbC04R7BSWMJAwkDCQMNAyDGQGIC3JNqoTeVX+qnjq2lpp7LsbgWdpk58wkDCQMJAw8P+FgTpihpULOodQHIhFDSdWEN7opM9+NOTJoS6oKi+iSFxe3xGizGCYxR5WWeYszt6L/EbSFOWzsFHNb3CSnzCQMJAwkDDQehioETOKlZ8SLIwnQkW/XQHDvrO8w7SZDb+hI72cc6jHNWGMgW5MrMD0+JeQuFkeCARm9JzizTOmpJjBhs6ICHWEuMpJB3qaOibI6MrY1I0pa+jYK9df9t004gx+I2mL0oAzzLZNh1eUJoUlDCQMJAwkDLQNBjLODKtEiAj7EtjDBGfGKQqc3MDeMiy9uBYGx+kQ7OfBYfBBPPsYcOyLgsAZccBn/w7n1xVZAhJP3oGyc17M07VciBrn+snBvgoz/GNTN1eD2KkYchSSWi6ySRpjFM40ZI8R+8jCHe8Gw+pl76HPdTRYUGKVGBLuWB6MZdiwyl4f0kHI2aOXXMJAwkDCQMJA+2EgI2ZM/hAuOU9PN6CyIRczdTZJQlzgrDBFxbFpMnRwW+yOZ+NtaPqMKBACxoblYcOGOdkfFWZTAsddT3BubPQ04sPGXAgWR2CxeZkN2TiIBUSVODbwssmWQ5Axh2fTMdsHONkD8SYbZuHWiggR5tuYmcPREY8IFVjkxYqTsKJ8YeUtHsKOxaVcj6KbaMEfBJbN58klDCQMJAwkDLQPBrLjrDiFAwIBV8O+L0R0iPLgVjCzh7PiXER+EL0iZxO8xcG1wLkx0YenVZCOEy44FkY2P2fHZ8Ft8YN4sSueM+04A42L5Qw25+CxNw3dHkdocfQSt1hDzDgNgToj4kTkiLl+6IDBCRcQY/bKGUyILvWDw4Q4El71Ay5cLPvr2HvH9gG4VcSzEGNcFYwUX43nhKOEo9QHUh9opA9knFnZFTByqkV2BYzO0PLHEVYxZ1fAsA+Mo17kpAGd2LnxtFu3bpqVjdRwMHBycGBUluNz4JLs1l7C5FT1mn1tcHDEQzTYuMm1L1xNgviR8//kpA+9/sO4QGCEjnf0bhBDi8OIRE5OCJPps8XXRYwMsKsd2LgNntgsjmMTcVXekSCSlzCQMJAwkDDQChjIiBkWhGw45uBVJmP0RuihOFcPMWNoSBGKEq0O4eTNRmi4JnbJw7kg0oMAQmyMmCHig4Ai8jMHZwQc7uUyhwUlujuDj2EI4kROHSEdxIyz9ogPf+S3POYTxv1ZnL0YntQfxpMG10gYukFEmnC0cgGjcnuEwckW5R8BOf0nDCQMJAwkDLQ2BjJi1pIrYNCNhad7UCm7AoZJnCOtmNDDK2AwjMg7xI+c5GEOIwrM8+HkzCFShIMzB6Hkska4MU4I4WBVCJTcXaSEEuIYWhSGRMWezVLS3oFtz3nfyg19SwORhjvEAATRLIcGc7klnJ6lCfOl54SBhIGEgYSBtsFARswgIhCT8AoYJmm4JXOcOo4Jep6QEQ8nZqe+W3p8u+oDYww7lopwJnssGDkHkckfAxREiogZ5XBQ5Qo5x8wsA404YJTCCdTovuAYcVgwIvLDkAQuycSg5LF8mlD+SMO9WrEbs8vywamG+ThzkKO7+A70f+RDd2fPVmbyEwYSBhIGEgbaFgMZMSu6AkZOV1ZiFF4Bw+WMoYNwYBBCWqz6uKjOroBhcmfC7969uxqOcMVKnriwuZpr3iFmRkTwOUQYUWc+Pec4QkzZJsAPwkcZGH9gcIIuDfEl15tT73x+xJ59+/ZV0eWQIUOyT7FrQTAGgaDaO7BxZumJyBPjFRwiRq5K4QocrBi5DwuLSIhtvlzNkP4SBhIGEgYSBtoEAxkx424crADhsBCXMeHjuGSQk+65bBHxXriZmng4OszrMc/nh5gN7o7JHC4F7olLPdk8jSgQoxDLh36pd+/ebsCAAXpaP7cPY/3IBmpEkNybhaEG4rzwRBLyc8Ei5v52cSV3kmEmD8GE2FBPu2coJCzcrUZceFEdVo/5g5W5wwxxpd1VBUEmH34ID6MVDD+wwoTzRJwKAQzT6Aenv4SBhIGEgYSBNsNARsww/ihyTPJYEGJ0gXEIhhN2BQwTNtaDEEBut8VYA+MKNkFz4SJcDlfAQFTYb4bJOhdN4shjxIa9Y3atPHFy/5mTO8Bcz549edV8eT0XRE7usFLze27B5tZiRJJwmIgS+/Xrp5foYTaPM+KCWT6iUoijhVEWHGLoLM588mHQEuYjPZwphJetABAxu0YkhJWeEwYSBhIGEgbaFgM1x1lRFKdoMNljeJF3cE049EQ2yYdXwBBHGjia8AoY0sLBFZ25aHDIGz7n38M4ODq4IDglCBn1gauDmJpjDxhlQlzMhTBiYY3EWRr8IrhhfHpOGEgYSBhIGGhbDNQQs0Yn5bJ0ReFhWPjMZ4Xvbf1saAzLydfB0pifT2vheb/RdPl86T1hIGEgYSBhoHUwkIkZG52QG01H9cK0Zc+NpCvL29LwfFlF74SZC+FbWN5vJE0+T3pPGEgYSBhIGGhdDHRBv5Q3rigrIjZx5+PC99Z4roJRFW/fFKYjLP9els7CzS/LZ/HJTxhIGEgYSBhoPwx07jrcD+rRp5eW2ChRy1cvP7GH780+F+VrJoy6FuWzbwjjYmEWh1+UJ4xPzwkDCQMJAwkD7YuB/wGuPS5lEzO3DgAAAABJRU5ErkJggg==)

   

## 总结

这一讲，我们介绍了`ethers.js`的`Interface`类，并利用它解码了`mempool`中的`transfer`交易。

# 21. 靓号生成器

这一讲，我们介绍如何利用`ethers.js`生成靓号地址，这是一个价值$1.6亿的教程（并不）。

## 靓号地址

现实生活中，有人追求车牌号“888888”，而在区块链中，大家也追求“靓号地址”。靓号地址（Vanity Address）是个性化的地址，易于识别，并且具有与其它地址一样的安全性。比如以`7`个`0`开头的地址：

```solidity
0x0000000fe6a514a32abdcdfcc076c85243de899b
```



是的，这也是知名做市商`Wintermute`被盗$1.6亿的靓号地址（[报道](https://www.blocktempo.com/head-market-maker-wintermute-hacked-loses-160-million-magnesium/)）。刚才我们说了，靓号和普通地址具有一样的安全性，那么这里为什么被攻击了呢？

问题出在生成靓号工具存在漏洞。`Wintermute`使用了一个叫`Profinity`的靓号生成器来生成地址，但这个生成器的随机种子有问题。本来随机种子应该有2的256次方可能性，但是`Profinity`使用的种子只有2的32次方的长度，可以被暴力破解。

## 靓号生成器

利用`ethers.js`，我们可以用`10`行代码就可以写出一个靓号生成器，它可能没有其它的工具快，但安全有保障。

### 生成随机钱包

我们可以利用下面的代码安全并随机的生成钱包：

```js
const wallet = ethers.Wallet.createRandom() // 随机生成钱包，安全
```



### 正则表达式

我们需要用正则表达式来筛选出目标靓号地址。这里简单的讲一下正则表达式：

```text
- 开头几位字符匹配，我们用`^`符号，例如`^0x000`就会匹配以`0x000`开头的地址。
- 最后几位字符匹配，我们用`$`符号，例如`000$`就会匹配以`000`结尾的地址。
- 中间几位我们不关心，可以利用`.*`通配符，例如`^0x000.*000$`就会匹配任何以`0x000`开头并以`000`结尾的地址。
```



在`js`中，我们可以用下面的表达式筛选靓号地址：

```js
const regex = /^0x000.*$/ // 表达式，匹配以0x000开头的地址
isValid = regex.test(wallet.address) // 检验正则表达式
```



### 靓号生成脚本

靓号生成器的逻辑非常简单，不断生成随机钱包，直到匹配到我们想要的靓号才结束。作为测试，以`0x000`开头的靓号仅需几秒就可以生成，每多一个`0`，耗时多16倍。

```js
import { ethers } from "ethers";
var wallet // 钱包
const regex = /^0x000.*$/ // 表达式
var isValid = false
while(!isValid){
    wallet = ethers.Wallet.createRandom() // 随机生成钱包，安全
    isValid = regex.test(wallet.address) // 检验正则表达式
}
// 打印靓号地址与私钥
console.log(`靓号地址：${wallet.address}`)
console.log(`靓号私钥：${wallet.privateKey}`)
```





![靓号生成](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071534802.png)



## 扩展——顺序地址生成

我们基于靓号生成器，扩充部分代码，批量生成指定开头的地址（比如001，002，…，999），以便在各种场景（空投交互）中进行简单的标识，方便自己进行管理。

```shell
0x0017c58B5F7199198C490E7b602Dd559aC22EDcA:0x087922c19c90b41b2786968ee04300a34d99e8e556e71057ab7a30e9b8e34f4e
0x0023F31fdc08FCD3296870F67e1eEC5d71bf2633:0x39f66b17c6ad3e8cc919f4d767fad2f8dd82a341b4431f4eb18365f52be7d0cd
0x003a605E6E59B569bC37bb1287514357E311da34:0x2c4c787d155ef78e6d1ca364c808ec33a68937bead8bc7fd4eac360f6626d206
```



如果现在需要生成001、002、…、100，共计`100个`地址。那我们手动更改正则表达式工作量就太大了，因此使用循环进行处理，简单增加一个for循环和`padStart()`（填充补0，比如001，002）。

```js
import { ethers } from "ethers";

var wallet // 钱包
for (let i = 1; i <= 101; i += 1) {
    // 填充3位数字，比如001，002，003，...，999
    const paddedIndex = (i).toString().padStart(3, '0');
    const regex = new RegExp(`^0x${paddedIndex}.*$`);  // 表达式
    var isValid = false
    while(!isValid){
        wallet = ethers.Wallet.createRandom() // 随机生成钱包
        isValid = regex.test(wallet.address) // 检验正则表达式
    }
    // 打印地址与私钥
    console.log(`钱包地址：${wallet.address}`)
    console.log(`钱包私钥：${wallet.privateKey}`)
}
```



### 时间问题

但上述脚本实际使用时，耗费的时间是极其巨大的，因为上段中所用的脚本做了很多的重复工作，举个例子

有一个小游戏，面前的盒子中有编号1-10000的玻璃珠（编号会重复），需要从中找到编号1-100的玻璃珠，我们抓起一把，其中的编号是：`[1545,2,5,8544,6,44858,1112]`这其中`[2,5,6]`是符合条件的，那我们就需要把这三颗玻璃珠挑出，并且不再要这三个编号的珠子。

但是上段中的代码仅进行了简单的挑选，先挑选编号为`[1]`的玻璃珠，即使这把玻璃珠内恰好有`[2,3,…,99,100]`，也会将其丢弃，然后继续挑选步骤，这显然是不符合要求的，也是耗费时间过长的原因。

要解决这个问题，首先增加一个创建存有所有需要的正则表达式的数组。

```js
// 生成正则匹配表达式，并返回数组
function CreateRegex(total) {
    const regexList = [];
    for (let index = 0; index < total; index++) {
        // 填充3位数字，比如001，002，003，...，999
        const paddedIndex = (index + 1).toString().padStart(3, '0');
        const regex = new RegExp(`^0x${paddedIndex}.*$`);
        regexList.push(regex);
    }
    return regexList;
}
```



接着在生成钱包的函数中传入该数组并进行匹配，如匹配到则从数组中删除对应regex

```js
async function CreateWallet(regexList) {
    let wallet;
    var isValid = false;

    //从21讲的代码扩充
    //https://github.com/WTFAcademy/WTFEthers/blob/main/21_VanityAddress/readme.md
    while (!isValid && regexList.length > 0) {
        wallet = ethers.Wallet.createRandom();
        const index = regexList.findIndex(regex => regex.test(wallet.address));
        // 移除匹配的正则表达式
        if (index !== -1) {
            isValid = true;
            regexList.splice(index, 1);
        }
    }
    const data = `${wallet.address}:${wallet.privateKey}`
    console.log(data);
    return data
}
```



此时时间缩短至可接受范围，测试生成100个顺序地址耗费时间大概为2分钟。

## 总结

这一讲，我们利用`ethers.js`写了一个10行代码不到的靓号生成器，并省了$1.6亿。

另外扩展了该代码，编写了一个顺序地址生成器并进行优化，方便在空投交互等场景中对地址进行简单的标识。

# 22. 读取任意数据

以太坊所有数据都是公开的，因此 `private` 变量并不私密。这一讲，我们将介绍如何读取智能合约的任意数据。

## 智能合约存储布局

以太坊智能合约的存储是一个 `uint256 -> uint256` 的映射。`uint256` 大小为 `32 bytes`，这个固定大小的存储空间被称为 `slot` （插槽）。智能合约的数据就被存在一个个的 `slot` 中，从 `slot 0` 开始依次存储。每个基本数据类型占一个`slot`，例如`uint`，`address`，等等；而数组和映射这类复杂结构则会更复杂，详见[网址](https://docs.soliditylang.org/en/v0.8.17/internals/layout_in_storage.html?highlight=Layout of State Variables in Storage)。



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071534586.png)



因此，即使是没有 `getter` 函数的 `private` 变量，你依然可以通过 `slot` 索引来读取它的值。

## `getStorageAt`

`ethersjs` 提供了 `getStorageAt()` 方便开发者读取特定 `slot` 的值：

```js
const value = await provider.getStorageAt(contractAddress, slot)
```



`getStorageAt()` 有两个参数，分别是合约地址 `contractAddress` 和 想读取变量的 `slot` 索引。

## 读取任意数据脚本

下面，我们写一个脚本，利用 `getStorageAt()` 函数来读取 `Arbitrum` 跨链桥的合约所有者。该跨链桥为可升级代理合约，将 `owner` 存在了特定的 `slot` 避免发生变量碰撞，并且没有读取它的函数。这里，我们就可以利用`getStorageAt()` 来读取它。

```solidity
合约地址: 0x8315177aB297bA92A06054cE80a67Ed4DBd7ed3a
slot索引: 0xb53127684a568b3173ae13b9f8a6016e243e63b6e8ee1178d6a717850b5d6103
```



运行结果：



![img](https://www.wtf.academy/assets/images/22-2-a6c6f11ec58641a13cbc0c66fed10773.png)



代码：

```js
import { ethers } from "ethers";

//准备 alchemy API 可以参考https://github.com/AmazingAng/WTFSolidity/blob/main/Topics/Tools/TOOL04_Alchemy/readme.md 
const ALCHEMY_MAINNET_URL = 'https://eth-mainnet.g.alchemy.com/v2/oKmOQKbneVkxgHZfibs-iFhIlIAl6HDN';
const provider = new ethers.JsonRpcProvider(ALCHEMY_MAINNET_URL);

// 目标合约地址: Arbitrum ERC20 bridge（主网）
const addressBridge = '0x8315177aB297bA92A06054cE80a67Ed4DBd7ed3a' // DAI Contract
// 合约所有者 slot
const slot = `0xb53127684a568b3173ae13b9f8a6016e243e63b6e8ee1178d6a717850b5d6103`

const main = async () => {
    console.log("开始读取特定slot的数据")
    const privateData = await provider.getStorage(addressBridge, slot)
    console.log("读出的数据（owner地址）: ", ethers.getAddress(ethers.dataSlice(privateData, 12)))    
}

main()
```



## 总结

这一讲，我们介绍了如何读取智能合约中的任意数据，包括私密数据。由于以太坊是公开透明的，大家不要将秘密存在智能合约中！

# 23. 抢先交易脚本

这一讲，我们将介绍抢先交易（Front-running，抢跑）的脚本。据统计，以太坊上的套利者通过三明治攻击（sandwich attack）[共获利12亿美元](https://dune.com/chorus_one/ethereum-mev-data)。在学习之前，请先阅读[WTF Solidity教程 合约安全S11: 抢先交易](https://github.com/AmazingAng/WTFSolidity/blob/main/S11_Frontrun/readme.md)。



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071534005.png)



## Freemint NFT合约

我们要抢跑的目标合约是一个ERC721标准的NFT合约`Frontrun.sol`，它拥有一个`mint()`函数进行免费铸造。

```solidity
// SPDX-License-Identifier: MIT
// By 0xAA
pragma solidity ^0.8.4;
import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

// 我们尝试frontrun一笔Free mint交易
contract FreeMint is ERC721 {
    uint256 public totalSupply;

    // 构造函数，初始化NFT合集的名称、代号
    constructor() ERC721("Free Mint NFT", "FreeMint"){}

    // 铸造函数
    function mint() external {
        totalSupply++;
        _mint(msg.sender, totalSupply); // mint
    }
}
```



为了简化测试环境，我们将上述合约部署在foundry本地测试网，然后监听在`mempool`中的未决交易，筛选出符合标准的交易进行抢跑。

如果你不了解 `foundry`，可以阅读WTF Solidity中的[Foundry教程](https://github.com/AmazingAng/WTF-Solidity/blob/main/Topics/Tools/TOOL07_Foundry/readme.md)。安装好 foundry 后，在命令行输入以下命令就可以启动本地测试网:

```shell
anvil
```



## 抢跑脚本

下面，我们详解一下抢跑脚本`frontrun.js`，这个脚本会监听链上的`mint()`交易，并发送一个gas更高的相同交易，进行抢跑。

1. 创建连接到foundry本地测试网的`provider`对象，用于监听和发送交易。foundry本地测试网默认url：`"http://127.0.0.1:8545"`。

   ```js
   //1.连接到foundry本地网络
   
   import { ethers } from "ethers";
   const provider = new ethers.providers.JsonRpcProvider('<http://127.0.0.1:8545>')
   let network = provider.getNetwork()
   network.then(res => console.log(`[${(new Date).toLocaleTimeString()}]链接到网络${res.chainId}`))
   ```

   

2. 创建合约实例，用于查看mint结果，确认是否抢跑成功。

   ```js
   //2.构建contract实例
   const contractABI = [
       "function mint() public",
       "function ownerOf(uint256) public view returns (address) ",
       "function totalSupply() view returns (uint256)"
   ]
   
   const contractAddress = '0xC76A71C4492c11bbaDC841342C4Cb470b5d12193'//合约地址
   const contractFM = new ethers.Contract(contractAddress, contractABI, provider)
   ```

   

3. 创建一个包含我们感兴趣的`mint()`函数的`interface`对象，用于在监听过程中使用。如果你不了解它，可以阅读[WTF Ethers极简教程第20讲：解码交易](https://github.com/WTFAcademy/WTFEthers/blob/main/20_DecodeTx/readme.md)。

   ```js
   //3.创建Interface对象，用于检索mint函数。
   //V6版本 const iface = new ethers.Interface(contractABI)
   const iface = new ethers.utils.Interface(contractABI)
   function getSignature(fn) {
   // V6版本 return iface.getFunction("mint").selector
       return iface.getSighash(fn)
   }
   ```

   

4. 创建测试钱包，用于发送抢跑交易，私钥是foundry测试网提供的，里面有10000 ETH测试币。

   ```js
   //4. 创建测试钱包，用于发送抢跑交易，私钥是foundry测试网提供
   const privateKey = '0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80'
   const wallet = new ethers.Wallet(privateKey, provider)
   ```

   

5. 我们先看一下正常的mint结果是怎样的。我们利用`provider.on`方法监听mempool中的未决交易，当交易出现时，我们会利用交易哈希`txHash`来读取交易详情`tx`，并筛选出调用了`mint()`函数的交易，查看交易结果，获取mint的nft编码及对应的owner，比对交易发起地址与owner是否一致。确认，mint按预期执行。

   ```js
   //5. 构建正常mint函数，检验mint结果，显示正常。
   const normaltx = async () => {
   provider.on('pending', async (txHash) => {
       provider.getTransaction(txHash).then(
           async (tx) => {
               if (tx.data.indexOf(getSignature("mint")) !== -1) {
                   console.log(`[${(new Date).toLocaleTimeString()}]监听到交易:${txHash}`)
                   console.log(`铸造发起的地址是:${tx.from}`)//打印交易发起地址
                   await tx.wait()
                   const tokenId = await contractFM.totalSupply()
                   console.log(`mint的NFT编号:${tokenId}`)
                   console.log(`编号${tokenId}NFT的持有者是${await contractFM.ownerOf(tokenId)}`)//打印nft持有者地址
                   console.log(`铸造发起的地址是不是对应NFT的持有者:${tx.from === await contractFM.ownerOf(tokenId)}`)//比较二者是否一致
               }
           }
       )
   })
   }
   ```

   

   

   ![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071534365.png)

   

6. 进行抢跑mint。我们依旧利用`provider.on`方法监听mempool中的未决交易，当有调用了mint()函数的交易出现且发送方不是自己钱包地址的交易（如果不筛选，会自己抢跑自己的交易，陷入死循环）时，构建抢跑交易，发送交易进行抢跑。等待交易结束后，查看抢跑结果。预期将要被mint的nft并未被原交易发起地址mint，而是由抢跑地址mint。同时查看区块内数据，抢跑交易在原始交易前被打包进区块，抢跑成功！

   ```js
   const frontRun = async () => {
   provider.on('pending', async (txHash) => {
       const tx = await provider.getTransaction(txHash)
       if (tx.data.indexOf(getSignature("mint")) !== -1 && tx.from !== wallet.address) {
           console.log(`[${(new Date).toLocaleTimeString()}]监听到交易:${txHash}\n准备抢先交易`)
           const frontRunTx = {
               to: tx.to,
               value: tx.value,
   // V6版本 maxPriorityFeePerGas: tx.maxPriorityFeePerGas * 2n， 其他运算同理。参考https://docs.ethers.org/v6/migrating/#migrate-bigint
               maxPriorityFeePerGas: tx.maxPriorityFeePerGas.mul(2),
               maxFeePerGas: tx.maxFeePerGas.mul(2),
               gasLimit: tx.gasLimit.mul(2),
               data: tx.data
           }
           const aimTokenId = (await contractFM.totalSupply()).add(1)
           console.log(`即将被mint的NFT编号是:${aimTokenId}`)//打印应该被mint的nft编号
           const sentFR = await wallet.sendTransaction(frontRunTx)
           console.log(`正在frontrun交易`)
           const receipt = await sentFR.wait()
           console.log(`frontrun 交易成功,交易hash是:${receipt.transactionHash}`)
           console.log(`铸造发起的地址是:${tx.from}`)
           console.log(`编号${aimTokenId}NFT的持有者是${await contractFM.ownerOf(aimTokenId)}`)//刚刚mint的nft持有者并不是tx.from
           console.log(`编号${aimTokenId.add(1)}的NFT的持有者是:${await contractFM.ownerOf(aimTokenId.add(1))}`)//tx.from被wallet.address抢跑，mint了下一个nft
           console.log(`铸造发起的地址是不是对应NFT的持有者:${tx.from === await contractFM.ownerOf(aimTokenId)}`)//比对地址，tx.from被抢跑
           //检验区块内数据结果
           const block = await provider.getBlock(tx.blockNumber)
           console.log(`区块内交易数据明细:${block.transactions}`)//在区块内，后发交易排在先发交易前，抢跑成功。
       }
   })
   }
   ```

   

   

   ![img](https://www.wtf.academy/assets/images/23-3-0faed4c3c30e870bf6ff1efb519da2fd.png)

   

## 总结

这一讲，我们介绍了一个简单的抢先交易脚本。你可以在这个脚本的基础上加入你想要的功能，开启币圈科学家之路！

# 24. 识别ERC20合约

这一讲，我们介绍如何用`ethers.js`识别一个合约是否为`ERC20`标准，你会在链上分析，识别貔貅，抢开盘等场景用到它。

## `ERC20`

`ERC20` 是以太坊上最常用的代币标准，如果对这个标准不熟悉，可以阅读[WTF Solidity第31讲 ERC20](https://github.com/AmazingAng/WTF-Solidity/blob/main/31_ERC20/readme.md)。`ERC20` 标准包含以下函数和事件:

```solidity
interface IERC20 {
    event Transfer(address indexed from, address indexed to, uint256 value);

    event Approval(address indexed owner, address indexed spender, uint256 value);

    function totalSupply() external view returns (uint256);

    function balanceOf(address account) external view returns (uint256);

    function transfer(address to, uint256 amount) external returns (bool);

    function allowance(address owner, address spender) external view returns (uint256);

    function approve(address spender, uint256 amount) external returns (bool);

    function transferFrom(address from, address to, uint256 amount) external returns (bool);
}
```



## 识别 `ERC20` 合约

在之前的[教程](https://github.com/WTFAcademy/WTF-Ethers/blob/main/12_ERC721Check/readme.md)中，我们讲了如何基于 `ERC165` 识别 `ERC721` 合约。但是由于 `ERC20` 的发布早于 `ERC165`（20 < 165），因此我们没法用相同的办法识别 `ERC20` 合约，只能另找办法。

区块链是公开的，我们能获取任意合约地址上的代码（bytecode）。因此，我们可以先获取合约代码，然后对比其是否包含 `ERC20` 标准中的函数就可以了。

首先，我们用 `provider` 的 `getCode()` 函数来取得对应地址的 `bytecode`：

```js
let code = await provider.getCode(contractAddress)
```



接下来我们要检查合约 `bytecode` 是否包含 `ERC20` 标准中的函数。合约 `bytecode` 中存储了相应的[函数选择器]：如果合约包含 `transfer(address, uint256)` 函数，那么 `bytecode` 就会包含 `a9059cbb`；如果合约包含 `totalSupply()`，那么 `bytecode` 就会包含 `18160ddd`。如果你不了解函数选择器，可以阅读 WTF Solidity的[相应章节](https://github.com/AmazingAng/WTF-Solidity/blob/main/29_Selector/readme.md)。如果想更深入的了解 `bytecode`，可以阅读[深入EVM](https://github.com/AmazingAng/WTFSolidity/blob/main/Topics/Translation/DiveEVM2017)。

这里，我们仅需检测 `transfer(address, uint256)` 和 `totalSupply()` 两个函数，而不用检查全部6个，这是因为：

1. `ERC20`标准中只有 `transfer(address, uint256)` 不包含在 `ERC721`标准、`ERC1155`和`ERC777`标准中。因此如果一个合约包含 `transfer(address, uint256)` 的选择器，就能确定它是 `ERC20` 代币合约，而不是其他。
2. 额外检测 `totalSupply()` 是为了防止[选择器碰撞](https://github.com/AmazingAng/WTFSolidity/blob/main/S01_ReentrancyAttack/readme.md)：一串随机的字节码可能和 `transfer(address, uint256)` 的选择器（4字节）相同。

代码如下

```js
async function erc20Checker(addr){
    // 获取合约bytecode
    let code = await provider.getCode(addr)
    // 非合约地址的bytecode是0x
    if(code != "0x"){
        // 检查bytecode中是否包含transfer函数和totalSupply函数的selector
        if(code.includes("a9059cbb") && code.includes("18160ddd")){
            // 如果有，则是ERC20
            return true
        }else{
            // 如果没有，则不是ERC20
            return false
        }
    }else{
        return null;
    }
}
```



## 测试脚本

下面，我们利用 `DAI`（ERC20）和 `BAYC`（ERC721）合约来测试脚本是否能正确识别 `ERC20` 合约。

```js
// DAI address (mainnet)
const daiAddr = "0x6b175474e89094c44da98b954eedeac495271d0f"
// BAYC address (mainnet)
const baycAddr = "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d"

const main = async () => {
    // 检查DAI合约是否为ERC20
    let isDaiERC20 = await erc20Checker(daiAddr)
    console.log(`1. Is DAI a ERC20 contract: ${isDaiERC20}`)

    // 检查BAYC合约是否为ERC20
    let isBaycERC20 = await erc20Checker(baycAddr)
    console.log(`2. Is BAYC a ERC20 contract: ${isBaycERC20}`)
}

main()
```



输出如下：



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071535062.png)



脚本成功检测出 `DAI` 合约是 `ERC20` 合约，而 `BAYC` 合约不是 `ERC20` 合约。

## 总结

这一讲，我们介绍了如何通过合约地址获取合约 `bytecode`，并且利用函数选择器来检测合约是否为 `ERC20` 合约。脚本能成功检测出 `DAI` 合约是 `ERC20` 合约，而 `BAYC` 合约不是 `ERC20` 合约。你会将它用在什么场景呢？

# 25. Flashbots

> 目前 Flashbots Bundle 仅支持 ethers.js v5 版本。

在以太坊转为 POS 之后，有超过 60% 的区块都是 flashbots 产出的，非常惊人，但是很多人并不了解它。这一讲，我们将介绍 Flashbots，包括:

1. 什么是 Flashbots?
2. 普通用户如何连接 Flashbots 节点发送隐私交易。
3. 开发者如何使用 Flashbots Bundle 打包多笔交易。

## Flashbots

Flashbots 是致力于减轻 MEV（最大可提取价值）对区块链造成危害的研究组织。目前有以下几款产品:

1. Flashbots RPC: 保护以太坊用户受到有害 MEV（三明治攻击）的侵害。
2. Flashbots Bundle: 帮助 MEV 搜索者（Searcher）在以太坊上提取 MEV。
3. mev-boost: 帮助以太坊 POS 节点通过 MEV 获取更多的 ETH 奖励。

本教程中，我们主要介绍前两个产品。

## Flashbots RPC

Flashbots RPC 是一款面向以太坊普通用户的免费产品，你只需要在加密的钱包中将 RPC（网络节点）设置为Flashbots RPC，就可以将交易发送到Flashbots的私有交易缓存池（mempool）而非公开的，从而免受抢先交易/三明治攻击的损害。如果你不了解mempool或抢先交易，可以阅读之前的 [mempool](https://github.com/WTFAcademy/WTFEthers/blob/main/19_Mempool/readme.md) 和 [抢先交易](https://github.com/WTFAcademy/WTFEthers/blob/main/23_Frontrun/readme.md) 教程

下面我们演示一下如何用 Metamask 钱包连接 Flashbots RPC。

1. 点击 Metamask 顶部的网络按钮（默认显示 `Ethereum Mainnet`），然后点击底部的 `Add network` 按钮添加网络节点（新版 Metamask 还需要在下一个页面点击 `Add a network manually` 按钮）。



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071535547.png)



1. 依次输入网络参数:

```text
Network name: Flashbots RPC
New RPC URL: https://rpc.flashbots.net
Chain ID: 1
Currency Symbol: ETH
Block Explorer URL: https://etherscan.io
```





![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071535067.png)



完成这两步，你的加密钱包就成功的连接到了 Flashbots RPC，之后你只需要像往常一样操作钱包就可以避免三明治攻击了！

## Flashbots Bundle

在区块链上搜索 MEV 机会的开发者被称为`搜索者`。Flashbots Bundle（交易包）是一款帮助搜索者提取以太坊交易中 MEV 的工具。搜索者可以利用它将多笔交易组合在一起，按照指定的顺序执行。

举个例子，搜索者在公共`mempool`发现一笔在 `Uniswap` 买入PEOPLE代币的交易有被三明治攻击的机会，他可以在这币交易前后各插入一笔买入和卖出的交易，组成交易 Bundle 发送给 Flashbots。这些交易将在指定的区块执行，不会改变顺序，且不用担心被别的MEV机器人攻击。



![MEV Steps by 0xBeans.eth](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071535487.jpeg)



## Flashbots Bundle 脚本

Flashbots 提供了 [ethers-provider-flashbots-bundle](https://github.com/flashbots/ethers-provider-flashbots-bundle)，一个建立在 `ethers.js` 之上帮助搜索者连接 flashbots provider 并发送 flashbots bundle 的 JavaScript 库。你可以通过 `npm` 命令安装它。

```shell
npm install --save @flashbots/ethers-provider-bundle
```



下面，我们利用它写一个脚本，给大家演示如何在 Sepolia 测试网发送 Flashbots Bundle。代码开源在 [WTF-Ethers repo](https://github.com/WTFAcademy/WTF-Ethers)。

1. 创建一个连接到非Flashbots RPC的普通provider，这里我们使用 Alchemy 提供的 Sepolia 测试网节点。

   ```js
   // 1. 普通rpc （非flashbots rpc）
   const ALCHEMY_GOERLI_URL = 'https://eth-sepolia.g.alchemy.com/v2/424OtGw_2L1A2wH6wrbPVPvyukI-sCoK';
   const provider = new ethers.JsonRpcProvider(ALCHEMY_GOERLI_URL);
   ```

   

2. 创建 Flashbots `声誉私钥`，用于建立“声誉”，[详情](https://docs.flashbots.net/flashbots-auction/searchers/advanced/reputation)

   > 注意: 这个账户不要储存资金，它不是flashbots主私钥。
   >
   > ```js
   > const authKey = '0x227dbb8586117d55284e26620bc76534dfbd2394be34cf4a09cb775d593b6f2c'
   > const authSigner = new ethers.Wallet(authKey, provider)
   > ```
   >
   > 

3. 创建 Flashbots RPC (测试网），用于发送交易，这里用到了普通provider和声誉私钥。

   ```js
   const flashbotsProvider = await FlashbotsBundleProvider.create(
       provider,
       authSigner,
       // 使用主网 Flashbots，需要把下面两行删去
       'https://relay-sepolia.flashbots.net'', 
       'sepolia'
       );
   ```

   

4. 创建一笔符合 `EIP1559` 标准的交易，交易内容: 发送 0.001 ETH 测试币到 WTF Academy 地址。这里用到了钱包私钥（含资产）以及普通provider

   ```js
   const privateKey = '0x227dbb8586117d55284e26620bc76534dfbd2394be34cf4a09cb775d593b6f2c'
   const wallet = new ethers.Wallet(privateKey, provider)
   // EIP 1559 transaction
   const transaction0 = {
   chainId: CHAIN_ID,
   type: 2,
   to: "0x25df6DA2f4e5C178DdFF45038378C0b08E0Bce54",
   value: ethers.parseEther("0.001"),
   maxFeePerGas: GWEI * 100n,
   maxPriorityFeePerGas: GWEI * 50n
   }
   ```

   

5. 创建交易Bundle，这里我们只打包了一笔交易，实际使用中可以打包多笔签名过或未签名的交易。

   ```js
   const transactionBundle = [
       {
           signer: wallet, // ethers signer
           transaction: transaction0 // ethers populated transaction object
       }
       // 也可以加入mempool中签名好的交易（可以是任何人发送的）
       // ,{
       //     signedTransaction: SIGNED_ORACLE_UPDATE_FROM_PENDING_POOL // serialized signed transaction hex
       // }
   ]
   ```

   

6. 模拟交易并打印交易详情。bundle 要模拟成功后才能被执行。这里用到了flashbots provider的 `signBundle()` 和 `simulate()` 方法。注意，`simulate()` 方法需要指定交易执行的目标区块高度，这里用的下一个区块。

   

   ![img](https://www.wtf.academy/assets/images/25-4-b8e1ad038e3b5474d55c1413c3b27809.png)

   

   ```js
   // 签名交易
   const signedTransactions = await flashbotsProvider.signBundle(transactionBundle)
   // 设置交易的目标执行区块（在哪个区块执行）
   const targetBlockNumber = (await provider.getBlockNumber()) + 1
   // 模拟
   const simulation = await flashbotsProvider.simulate(signedTransactions, targetBlockNumber)
   // 检查模拟是否成功
   if ("error" in simulation) {
       console.log(`模拟交易出错: ${simulation.error.message}`);
   } else {
       console.log(`模拟交易成功`);
       console.log(JSON.stringify(simulation, (key, value) => 
           typeof value === 'bigint' 
               ? value.toString() 
               : value, // return everything else unchanged
           2
       ));
   }
   ```

   

7. 发送交易 Bundle 上链。由于 Flashbots Bundle 需要指定执行的区块高度，且测试网Flashbots的节点很少，需要尝试很多次才能成功上链，所以我们用了一个循环，让 bundle 在未来的 100 个区块内依次尝试执行。我们用到了 flashbots provider 的 `sendRawBundle()` 方法发送 bundle。交易结果有三种状态：

   - `BundleIncluded`: bundle 成功上链。
   - `BlockPassedWithoutInclusion`: bunddle 未成功上链，需要继续尝试。
   - `AccountNonceTooHigh`: Nonce 设置有错。

   从下图可以看到，我们提交的 bundle 在5次尝试后成功上链。

   ![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410071535042.png)

   

   ```js
   for (let i = 1; i <= 100; i++) {
       let targetBlockNumberNew = targetBlockNumber + i - 1;
       // 发送交易
       const res = await flashbotsProvider.sendRawBundle(signedTransactions, targetBlockNumberNew);
       if ("error" in res) {
       throw new Error(res.error.message);
       }
       // 检查交易是否上链
       const bundleResolution = await res.wait();
       // 交易有三个状态: 成功上链/没有上链/Nonce过高。
       if (bundleResolution === FlashbotsBundleResolution.BundleIncluded) {
       console.log(`恭喜, 交易成功上链，区块: ${targetBlockNumberNew}`);
       console.log(JSON.stringify(res, null, 2));
       process.exit(0);
       } else if (
       bundleResolution === FlashbotsBundleResolution.BlockPassedWithoutInclusion
       ) {
       console.log(`请重试, 交易没有被纳入区块: ${targetBlockNumberNew}`);
       } else if (
       bundleResolution === FlashbotsBundleResolution.AccountNonceTooHigh
       ) {
       console.log("Nonce 太高，请重新设置");
       process.exit(1);
       }
   }
   ```

   

## 总结

这一讲，我们介绍了 Flashbots 的几款产品，并着重介绍了保护普通用户免受恶意 MEV 侵害的的 Flashbots RPC网络节点和面向开发者的 Flashbots Bundle，最后写了一个发送 Flashbots Bundle 的脚本。希望这篇教程让你更加了解 MEV 和 Flashbots。你会用他们做些什么呢？

# 26. EIP712 签名脚本

在本教程中，我们将介绍如何使用 Ethers.js 写 EIP712 签名脚本。请结合 [WTF Solidity 第52讲：EIP712](https://github.com/AmazingAng/WTFSolidity/blob/main/52_EIP712/readme.md) 一起阅读。

## EIP712

[EIP712 类型化数据签名](https://eips.ethereum.org/EIPS/eip-712)提供了一种更高级、更安全的签名方法。当支持 EIP712 的 Dapp 请求签名时，钱包会展示签名消息的原始数据，用户可以在验证数据符合预期之后签名。此外，你也可以使用脚本生成 EIP712 签名。

## EIP712 签名脚本

1. 创建 `provider` 和 `wallet` 对象。在本例中，我们使用 Remix 测试钱包的私钥。

   ```js
   // 使用 Alchemy 的 RPC 节点连接以太坊网络
   // 准备 Alchemy API 可以参考 https://github.com/AmazingAng/WTFSolidity/blob/main/Topics/Tools/TOOL04_Alchemy/readme.md 
   const ALCHEMY_GOERLI_URL = 'https://eth-goerli.alchemyapi.io/v2/GlaeWuylnNM3uuOo-SAwJxuwTdqHaY5l';
   const provider = new ethers.JsonRpcProvider(ALCHEMY_GOERLI_URL);
   
   // 使用私钥和 provider 创建 wallet 对象
   const privateKey = '0x503f38a9c967ed597e47fe25643985f032b072db8075426a92110f82df48dfcb'
   const wallet = new ethers.Wallet(privateKey, provider)
   ```

   

2. 创建 EIP712 Domain，它包含了合约的 `name`、`version`（通常约定为 “1”）、`chainId` 以及 `verifyingContract`（验证签名的合约地址）。

   ```js
   // 创建 EIP712 Domain
   let contractName = "EIP712Storage"
   let version = "1"
   let chainId = "1"
   let contractAddress = "0xf8e81D47203A594245E36C48e151709F0C19fBe8"
   
   const domain = {
       name: contractName,
       version: version,
       chainId: chainId,
       verifyingContract: contractAddress,
   };
   ```

   

3. 创建签名消息的类型化数据，其中 `types` 声明类型，而 `message` 包含数据。

   ```js
   // 创建类型化数据，Storage
   let spender = "0x5B38Da6a701c568545dCfcB03FcB875f56beddC4"
   let number = "100"
   
   const types = {
       Storage: [
           { name: "spender", type: "address" },
           { name: "number", type: "uint256" },
       ],
   };
   
   const message = {
       spender: spender,
       number: number,
   };
   ```

   

4. 调用 wallet 对象的 `signTypedData()` 签名方法，参数为之前创建的 `domain`、`types` 和 `message` 变量：

   ```js
   // EIP712 签名
   const signature = await wallet.signTypedData(domain, types, message);
   console.log("Signature:", signature);
   // Signature: 0xdca07f0c1dc70a4f9746a7b4be145c3bb8c8503368e94e3523ea2e8da6eba7b61f260887524f015c82dd77ebd3c8938831c60836f905098bf71b3e6a4a09b7311b
   ```

   

5. 你可以使用 `verifyTypedData()` 方法复原出签名的 `signer` 地址并验证签名的有效性。通常，这一步会在智能合约中执行。

   ```js
   // 验证 EIP712 签名，从签名和消息复原出 signer 地址
   let eip712Signer = ethers.verifyTypedData(domain, types, message, signature)
   console.log("EIP712 Signer: ", eip712Signer)
   //EIP712 Signer: 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4
   ```

   

## 总结

在本教程中，我们介绍了如何使用 Ethers.js 编写 EIP712 签名脚本。