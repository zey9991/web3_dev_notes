

# 1. 成为链上数据分析师

## TL；DR

- 链上数据的丰富源于区块链技术的成熟和项目的创新
- 掌握链上数据视角有助于减少信息差，在黑暗森林里前行多一层保护
- 链上数据真实地反应了价值的流动，因此分析后的洞见更有价值
- 数据分析提供一个可量化的视角最终去支撑决策，分析只是过程而不是目的
- 好的数据分析来源于数据思维，需要加深行业理解，培养抽象事物的能力

## 什么是链上数据

大部分人刚接触区块链时都会得到这样的概念：区块链是个公开的、不可篡改的记账本，一切的转账、交易记录是透明可信的。然而这一功能并不是区块链的全部，只是最初我们从“点对点的电子现金系统”，也就是“记账本”这个角度出发的。随着智能合约的发展，区块链实际上正在成为一个大型的数据库，下图从架构对比了传统web2和web3应用的区别：智能合约代替了后端，区块链也承担起一部分数据库的功能。越来越多的链上项目涌现，我们在链上的交互越来越频繁，比如在DeFi协议里添加了多少流动性，mint了哪些NFT，甚至关注哪个社交账号记录都能上链，我们一切与区块链的交互都将被记录在这个数据库中，这些记录就属于链上数据。



![img](https://www.wtf.academy/assets/images/01-78854e68381bb1f0880914b9b9d8059a.jpg)



**链上数据大致分为三类：**

1. 交易数据 如收发地址，转账金额，地址余额等
2. 区块数据 例如时间戳，矿工费，矿工奖励等
3. 智能合约代码 即区块链上的编码业务逻辑

链上数据分析就是从这三类数据中提取想要的信息进行解读。 从数据栈角度来看，区块链数据产品可以分为数据源、数据开发工具和数据app三类。



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051315730.jpeg)



灵活运用各类数据产品，会为我们在crypto世界提供崭新的视角。

虽然我们一直在说链上数据是公开透明的，但是我们很难直接读取那些数据，因为一笔简单的swap交易在链上看起来可能是这样的：



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051315835.jpeg)



我们能在区块链浏览器里看到一些原始链上数据，但是我的问题是想知道今天UniswapV3成交量是多少，这不解决我问题阿！我想看到的是下面这张图：



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051315312.jpeg)



链上原始数据并不能给我们答案，我们需要通过索引 (indexing)，处理 (processing)，存储 (storage) 等等一系列数据摄取 (ingestion) 的处理过程，再根据所提问题来聚合运算对应的数据，才能得到问题的答案。



![img](https://www.wtf.academy/assets/images/data-process-8af437d780bf3ac98433e3b10f3d3b10.png)



要从头做起，我们可能需要自己搭节点来接区块链数据，再作处理，但是这明显是非常耗时耗力的。还好，有许多数据平台，如Dune，Flipside，Footprint，他们将索引得到的原始链上数据，经过一系列处理后，存入由平台负责更新和管理的数据仓库，也就是说整个区块链数据被他们做成了好多张关系型数据表格，我们要做的就是从表格里选一些我们想要的数据构建我们的分析数据。更进一步地，有Nansen，Messari，DeBank这些数据类产品，不光整理好数据，还按照需求分门别类地封装起来，方便用户直接使用。

| 分类     | 应用示例                    |
| -------- | --------------------------- |
| 数据应用 | Nansen，Messari，DeBank..   |
| 数据平台 | Dune，FLipside，Footprint.. |
| 数据节点 | Infura，Quick Node..        |

## 链上数据的重要性

随着链上生态的繁荣，丰富的交互行为带来了海量数据。这些链上数据对应着链上价值的流动，对这些数据的分析和根据分析而得出的洞察和见解变得极为有价值。通过链上透明且不会说谎的数据，我们可以推断交易者，甚至市场整体的心理状态和心理预期，从而帮助自身做更有利的决策，也可以在黑暗森林前行中时为自己提起一盏明灯，照亮前方保护自己。

以大家熟悉的DeFi协议流动性挖矿为例：你添加流动性收获了奖励，池子增加了深度，用户享受了更低的滑点，大家都有光明的未来，你安心地将钱锁在合约里。可是某一天，黑天鹅悄然而至，聪明钱消息灵通立马撤退，而你只是个普通投资者，等你看到负面新闻再想到去提款时，手里的奖励几乎分文不值，猛烈的无常损失让你保本都难，直呼区块链骗局。



![image](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051315373.png)



但如果你有个链上数据的视角，你可能会发现：协议TVL陡然下降，奖励的代币在Uniswap上抛量激增，换句话说，有聪明人得到消息或者发现不对，池子里的流动性变差钱在逃跑，大家都看跌代币疯狂出售，请问现在应该离场吗？

当然这只是个抽象且简单的举例，但是我想传递给大家的是：**普通投资者在Crypto这片黑暗丛林中，始终处于信息不对称的劣势地位。** 但是链上数据是透明且真实的。为什么大家很执着于追踪Nansen的Smart Money？因为有内幕的人不会把消息告诉你，但是信息会映射到链上行为，被真实地记录下来，我们所要做的就是细心地观察这个数据世界，通过捕捉链上细节，在一定程度上弥补信息差。

DeFi summer之后，我们开始关心协议的锁仓量；Axie爆火，我们研究日增用户数；NFT崛起，我们研究mint数；以太坊上Gas飙升，我们观察是哪个项目这么火热。发现了吗？我们对链上数据与日俱增的了解和敏感度实则上来源于链上活动的繁荣发展，换句话说，**链上数据的重要性来源于区块链技术的成熟和应用的蓬勃。** 越来越多的链上项目给了我们足够丰富的交互空间，同时随着SBT、OAT的成熟和广泛应用，万物上链变为可能，这意味着日后的数据将多到足以支撑每一个用户丰满的链上肖像，届时我们能讲出关于DID，SocialFi更好的故事。

## 链上数据分析谁来做

对于大部分用户来说，成熟的数据产品已经够用，灵活组合多个数据工具就能取到不错的效果。比如使用Nansen帮助用户追踪巨鲸的实时动向；用Token Terminal查看各协议的收入；NFT类的数据监控平台更是五花八门。这些“成品”类数据产品虽然门槛低，使用方便，却也有无法满足高定制化要求的瓶颈。



![image](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051315995.jpeg)



举个例子， 你通过https://ultrasound.money/ 发现以太坊上Gas消耗突然上涨，是由这个没有听说过的XEN推动的，你敏锐地意识到，这可能是个早期机会！通过推特搜索，你了解了XEN采用PoP（Proof of Participation）挖矿机制，XEN挖矿参与者拥有挖出的XEN代币的所有权，随参与人数增加，挖矿难度加大，供应量降低。你想了解大家的参与情况，光靠个gas消耗可不够，你还想知道参与的人数，趋势，参与者都选择锁仓多久？同时你还发现，他好像没有防女巫？付个gas就能参与，冲进来的科学家多吗？我还有利润吗？分析到这你急需数据来支撑你“冲不冲”的决策，可是正因为早期，数据app中还没有对它的分析，同时数据app也很可能不会对每一个协议都进行监控分析。这就是为什么已经有很多数据产品的情况下，我们仍然需要自己会写一些数据分析：现成的产品难以满足定制化的需求。



![image](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051315172.png)



通过自己分析数据：https://dune.com/sixdegree/xen-crypto-overview， 我得知了大部分人都选择的是短期质押，且接近百分70的都是新钱包，说明被大家撸坏了，那我就明白了短期抛售压力会非常大，所以我如果想选择参与，就选质押最短的时间，尽快卖出，比谁跑得快。 至此，你已经完成了链上数据分析的整个流程：发现项目，研究项目机制，抽象出评估项目的标准，最后才是动手做数据处理、可视化，辅助决策。

## 如何做链上数据分析

尽管Dune这类的数据分析平台已经为我们做了很多整理工作，我们只要用SQL类的语法从数据表中抽取我们需要的部分进行构建就可以了。大部分人的学习路径我相信都是直奔《3日速成SQL》，拿下之后又开始迷茫，还是不知道如何从毛线团中找到哪根线头。怎么会这样？学习数据分析最重要的是培养数据思维，熟练使用编程语言是次要的。

**数据分析提供一个可量化的视角最终去支撑决策，分析只是过程而不是目的。简单的步骤是厘清三个问题，构建数据思维：**

**1. 我的目的是什么？**

是判断一个币现在是否是买入的好时机？决定是否为AAVE添加流动性赚取收益？还是想知道现在入场Stepn是否为时已晚？

**2. 我的策略是什么？**

买币的策略就是紧跟Smart money，买啥跟啥，他进我进他出我出；观察如果协议运作情况良好，存款利率满意，就把暂时不动的币存进去吃利息；Stepn最近大火，如果势头仍然向上，那我就参与其中。

**3. 我需要什么数据帮我做决策？**

需要监控Smart money地址的持仓动向，甚至考量代币的交易量和持仓分布；要查一下协议的TVL，未偿债务数额，资金利用率，APR等；考虑每日新增用户数，增长趋势，每日活跃用户数，交易笔数，玩家出入金情况，NFT市场里道具的销售情况。



![image](https://www.wtf.academy/assets/images/10-67f3fba3706e8a6bccde0a27c3198642.jpg)



这三个问题的难度逐渐增加，一二还容易回答，想明白第三个问题需要大量的学习和理解，这也是区分数据分析师们水平高低的小门槛。一名优秀的分析师应该具备以下三种特点：

**1. 对赛道或者协议有理解与认识**

即分析的是什么赛道？这个项目的运行机制是什么？会产生哪些数据，分别代表什么含义？

**2. 抽象事物的能力**

将一个模糊的概念变成可量化的指标，即

> “这个DEX协议好不好” =>“流动性”+“成交量”+“活跃用户量”+“资本利用率”+“协议产生的收益”

再回到上一点，通过你对协议的了解找到对应的数据。

**3. 处理数据的能力**

这里包含取数据（链上数据从哪来），处理数据（怎么筛选想要的滤除无关的），以及数据可视化的能力。



![image](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051315902.jpeg)



总的来说，数据分析只是支撑研究的工具，不要为了分析而分析。这个过程首先是出于你想对某个项目、概念、赛道进行研究、投资，然后学习、了解项目的运行机制，抽象出对定性概念的定量分析，最后才是找数据，做可视化。

数据分析最重要的始终是数据思维，至于最后动手做这一步，无非是熟练功，可以分为两部分：

- 对区块链数据结构的了解。比如在EVM链中，只有EOA账户能发起交易，但是智能合约在被调用时可以转账ETH，这些内部调用就是通过traces 表来记录的，所以查表时查transactions会遗漏内部调用的交易。
- 掌握Python、SQL等语言。掌握基本的数据库语言，无论是自己接数据或者用数据平台，都可以比较得心应手。

## 最后

网上有关链上数据分析的资料或者教程不少，但是都比较零散，质量也参差不齐。Web3是一所开放的大学，但是很多精力花费在寻找合适的教材上是比较痛苦的，同时大部分高质量的内容都是英文书写，对国内的用户构成一定语言障碍。

因此，Sixdegree团队将推出《成为链上数据分析师》的系列教程，以实际应用为导向，结合区块链数据结构和SQL语法，为大家提供一套上手教材，帮助更多的人掌握链上数据分析技能，最大化利用区块链数据的特性，一定程度上消除信息差。熊市多Build，成为链上数据分析师就从这里开始吧！

## 关于我们

SixdegreeLab是专业的链上数据团队，我们的使命是为用户提供准确的链上数据图表、分析以及洞见，并致力于普及链上数据分析。通过建立社区、编写教程等方式，培养链上数据分析师，输出有价值的分析内容，推动社区构建区块链的数据层，为未来广阔的区块链数据应用培养人才，欢迎大家加入社区交流！

## 参考资料

1. [The Capital Efficiency Era of DeFi](https://blog.hashflow.com/the-capital-efficiency-era-of-defi-d8b3427feae4)
2. [Using On-Chain Data for Policy Research: Part 1](https://policy.paradigm.xyz/writing/using-on-chain-data-for-policy-research-part-1)
3. [IOSG：解析链上数据分析平台现状与前景](https://foresightnews.pro/article/detail/8473)
4. [An Introduction to «On-chain» Analysis](https://www.blockstar.ch/post/an-introduction-to-on-chain-analysis)
5. [The Architecture of a Web 3.0 application](https://www.preethikasireddy.com/post/the-architecture-of-a-web-3-0-application)
6. [Sixdegree Dune Dashborads](https://dune.com/sixdegree)

# 2. Dune平台介绍

前文提到从数据栈角度来看，区块链数据产品可以分为`数据源`、`数据开发工具`和`数据app`三类，直接接入数据源成本太高，难度也更大，而数据app又是固定好的，我们要想分析数据， 需要一个开发工作量不大，又能接获取各种数据的平台，这类数据开发工具中，最便捷的便是Dune平台。

[Dune](https://dune.com/)是一个链上的数据分析平台，用户可以在平台上面书写SQL语句，从Dune解析的区块链数据库中筛选出自己需要的数据，并生成对应的图表，组成仪表盘。

本教程的全部查询示例和引用的相关查询（完整的数据看板和第三方账号的查询除外）全部使用Dune SQL查询引擎测试通过。Dune已经宣布2023年内全面过渡到Dune SQL引擎，所以大家直接学习Dune SQL的语法即可。

## Dune SQL

**Trino** 是一个开源的分布式 SQL 查询引擎，最初名为 Presto。它允许用户在大规模数据集上执行交互式分析查询，可以从多个数据源（如关系型数据库、Hadoop、NoSQL 数据库等）中提取数据，进行统一查询。Trino 具有以下特点：

1. **分布式架构**：能够处理大量数据并支持并行查询，以提高查询性能。
2. **多数据源支持**：可以连接到多种数据源，包括传统的数据库、数据仓库和大数据存储。
3. **交互式查询**：专为快速、交互式数据分析而设计，适合数据分析和业务智能应用。
4. **SQL 兼容性**：支持标准 SQL，使用户可以轻松上手。

### Dune SQL

**Dune Analytics** 是一个基于 Trino 的区块链数据分析平台，特别关注于以太坊及其生态系统。Dune SQL 是 Dune 提供的 SQL 查询语言，用于从区块链数据中提取信息和生成分析报告。用户可以使用 Dune SQL 来：

1. **查询链上数据**：从以太坊区块链获取交易、智能合约、事件等数据。
2. **可视化数据**：创建图表和仪表板，方便分析和展示数据。
3. **分享和协作**：与其他用户共享查询和数据分析结果。

### Trino 与 Dune SQL 的关系

- **基础架构**：Dune Analytics 是基于 Trino 构建的，利用 Trino 的强大查询能力来处理区块链数据。
- **数据访问**：Dune SQL 用户通过 Trino 的接口查询链上数据，享受分布式查询的优势。
- **目标用户**：Dune SQL 专注于区块链分析，提供与区块链相关的查询，而 Trino 是一个更通用的数据查询引擎，可以用于多种数据源和类型。

### 总结

Trino 是一个通用的分布式 SQL 查询引擎，支持多种数据源的查询，而 Dune SQL 则是基于 Trino 的平台，专注于区块链数据分析和可视化。Dune SQL 允许用户以简单的 SQL 语言从以太坊区块链中提取和分析数据，利用了 Trino 的强大功能。

## 页面介绍

在注册完Dune平台后，平台的主界面如下，具体的各项功能：

- Discover : 展示平台的各个方面趋势

  - **Dashboard**：显示当前关注量最多的dashboard，在这个界面，可以左上角的搜索/右侧的搜索框搜索自己感兴趣的关键词，这也是最重要的一个部分，可以点击一个dashboard，查看别人制作的dashboard
  - Queries：显示的是当前关注量最多的query，在这个界面，可以左上角的搜索/右侧的搜索框搜索自己感兴趣的关键词；
  - Wizards：平台中收藏量最高的用户排名；
  - Teams：平台中收藏量最高的团队排名；
  
- Favorites：

  - Dashboard：自己收藏的dashboard，可以在右侧搜索框搜索
  - Queries：自己收藏的query，可以在右侧搜索框搜索

- My Creations :

  - Dashboard：自己创建的dashboard，可以在右侧搜索框搜索，如果你有团队，仪表盘可以在不同的团队中
  - Queries：自己创建的query，可以在右侧搜索框搜索
  - Contracts：自己提交解析的合约，可以在右侧搜索框搜索
  
- **New Query**：新建一个查询

- 其它

  - Docs：链接到帮助文档
  - Discord：链接到社区讨论组



![img](https://www.wtf.academy/assets/images/main-page-04badcc725e99b07a4597de4e11665d4.png)



## 核心功能

### 查询Query

在点击`New Query` 之后，会进入一个新的界面，界面包含三个主要部分：

- 数据表目录：在左侧有一个`数据搜索框`和`数据列表`，展开数据列表后可以看到具体的每一张表。（注：在第一次进入显示的是v1版本的，已弃用，请在上面选择`Dune Engine v2(SparkSQL)`）
  - Raw：记录了各个区块链的原始数据表，主要为区块信息blocks、交易信息transactions、事件日志信息logs和traces表等；目前支持的链有：Ethereum、Polygon、Arbitrum、Solana、Optimism、Gnosis Chain、Avalanche
  - Decoded projects：各个项目/合约的直接解析表，解析出来的表会更加清晰易懂，如果分析具体项目用这里的表会更加合适
  - Spells：是从raw和Decoded projects中提取的综合数据表，比如Dex，NFT，ERC20等等
  - Community：社区用户贡献的数据表
- 代码编辑器：位于右上方的黑色区域，用于写自己的SQL语句，写完可以点击右下角的`Run`执行
- 结果&图表可视化：位于右下方，查询结果会显示在`Query results`，可以依次在后面新建新的子可视化页面



![query-page](https://www.wtf.academy/assets/images/query-page-4bd9b3753f6cd87c3ed2cf2468f22b2b.png)



平台的query可以通过分支fork的方式，将别人的query复制到自己的账户下，进行修改和编辑。

**spellbook**

spellbook是Dune平台非常重要的一个数据表，它是由社区用户贡献的一系列加工后的数据表，可以在github页面[duneanalytics/spellbook](https://github.com/duneanalytics/spellbook)贡献自己定义的数据表，dune平台会通过该定义，在后台生成相应的数据，在上图的前端页面中可以直接使用这些定义好的数据表，这些数据表的定义和字段意义可以到这里查看：https://spellbook-docs.dune.com/#!/overview

目前spellbook中已经由社区用户贡献了几百张各种各样的表，比如nft.trades, dex.trades, tokens.erc20等等



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051315563.png)



**参数**

在query中还可以设置一个可变的输入参数，改变查询条件，比如可以设置不同的用户地址，或者设置不同的时间范围，参数设置是以`'{{参数名称}}'`形式嵌入到查询语句中的。



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051315571.png)



### 图表可视化Visualization

在图表可视化中，Dune平台提供了散点图、柱状图、折线图、饼状图、面积图和计数器以及二维数据表。在执行完查询，得到结果之后，可以选择`New visualization` 创建一个新可视化图，在图中可以选择想要显示的数据字段，可以立刻得到对应的可视化图，图中支持显示多个维度的数据，在图表下方是设置图表样式的区域，包括名称、坐标轴格式、颜色等信息。



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051315323.png)



### 仪表盘Dashboard

上一小节的单个图表可视化，可以在仪表盘中灵活的组合，形成一个数据指标的聚合看板，并附带解释说明，这样可以从一个更加全面的角度去说明。在`Discover`中找到`New Dashboard`可以新建一个仪表盘，在仪表盘中可以添加所有query中生成的图表，并且可以添加markdown格式的文本信息，每个可视化的控件都可以拖拽并调整大小。



![img](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051315398.png)



### Dune相关资料

- 官方资料
  - [Dune官方文档（包括中文文档）](https://dune.com/docs/)
  - [Discord](https://discord.com/invite/ErrzwBz)
  - [Youtube](https://www.youtube.com/channel/UCPrm9d2hLd_YxSExH7oRyAg)
  - [Github Spellbook](https://github.com/duneanalytics/spellbook)
- 社区教程
  - [Dune 数据看板零基础极简入门指南](https://twitter.com/gm365/status/1525013340459716608)
  - [Dune入门指南——以Pooly为例，做一个NFT看板](https://mirror.xyz/0xa741296A1E9DDc3D6Cf431B73C6225cFb5F6693a/iVzr5bGcGKKCzuvl902P05xo7fxc2qWfqfIHwmCXDI4)
  - [从0到1构建你的Dune V1 Analytics看板（基础篇）](https://mirror.xyz/0xbi.eth/6cbedGOx0GwZdvuxHeyTAgn333jaT34y-2qryvh8Fio)
  - [从0到1构建你的Dune V1 Analytics看板（实战篇）](https://mirror.xyz/0xbi.eth/603BIaKXn7s2_7A84oayY_Fn5XUPh6zDsv2OlQTdzCg)
  - [从0到1构建你的Dune V1 Analytics看板（常用表结构）](https://mirror.xyz/0xbi.eth/uSr336PzXtqMuE_LPBewbJ1CHN2oUs40-TDET2rnkqU)

# 3. 数据分析新手上路

## 写在前面

我们的教程偏重实战，结合日常链上数据分析的场景与需求来编写。本文将为大家讲解开始创建数据看板之前需要熟悉的相关SQL基础知识。本教程为入门级，主要面向希望学习数据分析的新手用户。我们假定您之前并无编写SQL查询的经验，有SQL经验但不熟悉Dune平台的用户也可快速浏览本教程。本篇教程主要包括Dune平台简介、SQL查询快速入门等内容。在下一篇教程中，我们将一起编写查询并创建可视化图表、使用查询图表创建数据看板。我们相信，只要你有信心并跟随我们的教程动手实践，你也可以做出高质量的数据看板，迈出成为链上数据分析师的第一步。

## Dune 平台简介

[Dune](https://dune.com/)是一个强大的区块链数据分析平台，以SQL数据库的方式提供原始区块链数据和已解析的数据。通过使用SQL查询，我们可以从Dune的数据库中快速搜索和提取各种区块链信息，然后将其转换为直观的可视化图表。以此来获得信息和见解。数据看板（Dashboard）是Dune上内容的载体，由各种小部件（Widget）组成。这些小部件可以是从Query查询结果生成的可视化图表或文本框，你还可以在文本框中嵌入图像、链接等。查询（Query）是Dune数据面板的主要数据来源。我们通过编写SQL语句，执行查询并在结果集上生成可视化图表，再将图表添加到对应的数据看板中。

使用Dune处理数据的一般过程可以概括为：编写SQL查询显示数据 ->可视化查询结果 ->在数据看板中组装可视化图表 ->调整美化数据看板。关于Dune平台的使用，可以查看其[官方文档](https://dune.com/docs/)。Dune最新文档的中文版本目前正在翻译整理中，你可以在这里找到V1版本的[Dune中文文档](https://docs.dune.com/v/chinese/)。

## 数据库基础知识

在开始编写我们的数据看板所需的第一个SQL查询之前，我们需要先了解一些必备的SQL查询基础知识。

### 数据库的基本概念介绍

**数据库（Database）**：数据库是结构化信息或数据的有序集合，是按照数据结构来组织、存储和管理数据的仓库。Dune平台目前提供了多个数据库，分别支持来自不同区块链的数据。本教程使用Dune平台的“v2 Dune SQL”数据库查询引擎。所有示例查询和引用的例子链接（第三方的query除外）均以更新到Dune SQL。

**模式（Schema）**：同一个数据库中，可以定义多个模式。我们暂时可以将模式简单理解为数据表的拥有者（Owner）。不同的模式下可以存在相同名称的数据表。

**数据表（Table）**：数据表是由表名、表中的字段和表的记录三个部分组成的。数据表是我们编写SQL查询访问的主要对象。Dune将来自不同区块链的数据分别存贮到不同模式下的多个数据表中供我们查询使用。使用数据表编写查询时，我们用`schema_name.table_name`的格式来指定查询要使用的数据表名称。例如`ethereum.transactions`表示`ethereum`模式下的`transactions`表，即以太坊的交易表。同一个模式下的数据表名称必须唯一，但是相同名称的数据表可以同时存在于多个不同的模式下。例如V2中同时存在`ethereum.transactions`和`bnb.transactions`表。

**数据列（Column）**：数据列也称为字段（Field），有时也简称为“列”，是数据表存贮数据的基本单位。每一个数据表都包含一个或多个列，分别存贮不同类型的数据。编写查询时，我们可以返回全部列或者只返回需要的数据列。通常，只返回需要的最少数据可以提升查询的效率。

**数据行（Row）**：数据行也称为记录（Record）。每一个记录包括数据表定义的多个列的数据。SQL查询执行得到的结果就是一个或多个记录。查询输出的记录集通常也被称为结果集（Results）。

### 本教程使用的数据表

在本节的SQL查询示例中，我们使用ERC20代币表`tokens.erc20`做例子。ERC20代币表是由Dune社区用户通过魔法书（Spellbook）方式生成的抽象数据表（Spells，也称为Abstractions）。除了生成方式不同，这种类型的数据表的使用方式跟其他表完全一样。ERC20代币表保存了Dune支持检索的不同区块链上面的兼容ERC20标准的主流代币的信息。对于每种代币，分别记录了其归属的区块链、代币合约地址、代币支持的小数位数和代币符号信息。

ERC20代币表`tokens.erc20`的结构如下：

| **列名**         | **数据类型** | **说明**             |
| ---------------- | ------------ | -------------------- |
| blockchain       | string       | 代币归属的区块链名称 |
| contract_address | string       | 代币的合约地址       |
| decimals         | integer      | 代币支持的小数位数   |
| symbol           | string       | 代币的符号           |

## SQL查询快速入门

广义的SQL查询语句类型包括新增（Insert）、删除（Delete）、修改（Update）、查找（Select）等多个类型。狭义的SQL查询主要指使用Select语句进行数据检索。链上数据分析绝大多数时候只需使用Select语句就能完成工作，所以我们这里只介绍Select查询语句。后续内容中我们会交替使用查询、Query、Select等词汇，如无特别说明，都是指使用Select语句编写Query进行数据检索。

### 编写第一个查询

下面的SQL可以查询所有的ERC20代币信息：

```sql
select * from tokens.erc20
limit 10
```



### Select 查询语句基本语法介绍

一个典型的SQL查询语句的结构如下所示：

```sql
select 字段列表
from 数据表
where 筛选条件
order by 排序字段
limit 返回记录数量
```



**字段列表**可以逐个列出查询需要返回的字段（数据列），多个字段之间用英文逗号分隔，比如可以这样指定查询返回的字段列表`contract_address, decimals, symbol`。也可以使用通配符`*`来表示返回数据表的全部字段。如果查询用到了多个表并且某个字段同时存在于这些表中，我们就需要用`table_name.field_name`的形式指定需要返回的字段属于哪一个表。

**数据表**以`schema_name.table_name`的格式来指定，例如`tokens.erc20`。我们可以用`as alias_name`的语法给表指定一个别名，例如：`from tokens.erc20 as t`。这样就可以同一个查询中用别名`t`来访问表`tokens.erc20`和其中的字段。

**筛选条件**用于按指定的条件筛选返回的数据。对于不同数据类型的字段，适用的筛选条件语法各有不同。字符串（`varchar`）类型的字段，可以用`=`，`like`等条件做筛选。日期时间（`datetime`）类型的字段可以用`>=`，`<=`，`between ... and ...`等条件做筛选。使用`like`条件时，可以用通配符`%`匹配一个或多个任意字符。多个筛选条件可以用`and`（表示必须同时满足）或`or`（表示满足任意一个条件即可）连接起来。

**排序字段**用于指定对查询结果集进行排序的判断依据，这里是一个或多个字段名称，加上可选的排序方向指示（`asc`表示升序，`desc`表示降序）。多个排序字段之间用英文逗号分隔。Order By排序子句还支持按照字段在Select子句中出现的位置来指定排序字段，比如`order by 1`表示按照Select子句中出现的第一个字段进行排序（默认升序）。

**返回记录数量**用于指定（限制）查询最多返回多少条满足条件的记录。区块链保存的是海量数据，通常我们需要添加返回记录数量限制来提高查询的效率。

下面我们举例说明如何使用查询的相关部分。注意，在SQL语句中，我们可以`--`添加单行注释说明。还可以使用`/*`开头和`*/`结尾将多行内容标记为注释说明。注释内容不会被执行。

**指定返回的字段列表：**

```sql
select blockchain, contract_address, decimals, symbol   -- 逐个指定需要返回的列
from tokens.erc20
limit 10
```



**添加筛选条件：**

```sql
select blockchain, contract_address, decimals, symbol
from tokens.erc20
where blockchain = 'ethereum'   -- 只返回以太坊区块链的ERC20代币信息
limit 10
```



**使用多个筛选条件：**

```sql
select blockchain, contract_address, decimals, symbol
from tokens.erc20
where blockchain = 'ethereum'   -- 返回以太坊区块链的ERC20代币信息
    and symbol like 'E%'    -- 代币符号以字母E开头
```



**指定排序字段：**

```sql
select blockchain, contract_address, decimals, symbol
from tokens.erc20
where blockchain = 'ethereum'   -- 返回以太坊区块链的ERC20代币信息
    and symbol like 'E%'    -- 代币符号以字母E开头
order by symbol asc -- 按代币符号升序排列
```



**指定多个排序字段：**

```sql
select blockchain, contract_address, decimals, symbol
from tokens.erc20
where blockchain = 'ethereum'   -- 返回以太坊区块链的ERC20代币信息
    and symbol like 'E%'    -- 代币符号以字母E开头
order by decimals desc, symbol asc  -- 先按代币支持的小数位数降序排列，再按代币符号升序排列
```



**使用Limit子句限制返回的最大记录数量：**

```sql
select *
from tokens.erc20
limit 10
```



### Select查询常用的一些函数和关键词

#### As定义别名

可以通过使用“as”子句给表、字段定义别名。别名对于表名（或字段名）较长、包含特殊字符或关键字等情况，或者需要对输出字段名称做格式化时，非常实用。别名经常用于计算字段、多表关联、子查询等场景中。

```sql
select t.contract_address as "代币合约地址",
    t.decimals as "代币小数位数",
    t.symbol as "代币符号"
from tokens.erc20 as t
limit 10
```



实际上为了书写更加简洁，定义别名时`as`关键词可以省略，可以直接将别名跟在表名或字段名后，用一个空格分隔。下面的查询，功能和上一个查询完全相同。

```sql
-- 定义别名时，as 关键词可以省略
select t.contract_address "代币合约地址",
    t.decimals "代币小数位数",
    t.symbol "代币符号"
from tokens.erc20 t
limit 10
```



#### Distinct筛选唯一值

通过使用`distinct`关键词，我们可以筛选出出现在Select子句列表中的字段的唯一值。当Select子句包含多个字段时，返回的是这些字段的唯一值当组合。

```sql
select distinct blockchain
from tokens.erc20
```



#### Now 获取当前系统日期时间

使用`now()`可以获得当前系统的日期时间值。我们还可以使用`current_date`来得到当前系统日期，注意这里不需要加括号。

```sql
select now(), current_date
```



#### Date_Trunc 截取日期

区块链中的日期时间字段通常是以“年-月-日 时:分:秒”的格式保存的。如果要按天、按周、按月等进行汇总统计，可以使用`date_trunc()`函数对日期先进行转换。例如：`date_trunc('day', block_time)`将block_time的值转换为以“天”表示的日期值，`date_trunc('month', block_time)`将block_time的值转换为以“月”表示的日期值。

```sql
select now(),
    date_trunc('day', now()) as today,
    date_trunc('month', now()) as current_month
```



#### Interval获取时间间隔

使用`interval '2 days'`这样的语法，我们可以指定一个时间间隔。支持多种不同的时间间隔表示方式，比如：`'12 hours'`，`'7 days'`，`'3 months'`, `'1 year'`等。时间间隔通常用来在某个日期时间值的基础上增加或减少指定的间隔以得到某个日期区间。

```sql
select now() as right_now, 
    (now() - interval '2' hour) as two_hours_ago, 
    (now() - interval '2' day) as two_days_ago,
    (current_date - interval '1' year) as one_year_ago
```



#### Concat连接字符串

我们可以使用`concat()`函数将多个字符串连接到一起的到一个新的值。还可以使用更简洁的连接操作符`||`。

```sql
select concat('Hello ', 'world!') as hello_world,
    'Hello' || ' ' || 'world' || '!' as hello_world_again
```



#### Cast转换字段数据类型

SQL查询种的某些操作要求相关的字段的数据类型一致，比如concat()函数就需要参数都是字符串`varchar`类型。如果需要将不同类型的数据连接起来，我们可以用`cast()`函数强制转换为需要的数据类型，比如：`cast(25 as string)`将数字25转换为字符串“25”。还可以使用`data_type 'value string'`操作符方式完成类型转换，比如：`integer '123'`将字符串转换为数值类型。

```sql
select (cast(25 as varchar) || ' users') as user_counts,
    integer '123' as intval,
    timestamp '2023-04-28 20:00:00' as dt_time
```



#### Power求幂

区块链上的ERC20代币通常都支持很多位的小数位。以太坊的官方代币ETH支持18位小数，因为相关编程语言的限制，代币金额通常是以整数形式存贮的，使用时必须结合支持的小数位数进行换算才能得到正确的金额。使用`power()`函数，或者`pow()`可以进行求幂操作实现换算。在Dune V2中，可以用简洁的形式表示10的N次幂，例如`1e18`等价于`power(10, 18)`。

```sql
select 1.23 * power(10, 18) as raw_amount,
    1230000000000000000 / pow(10, 18) as original_amount,
    7890000 / 1e6 as usd_amount
```



### Select查询进阶

#### Group By分组与常用汇总函数

SQL中有一些常用的汇总函数，`count()`计数，`sum()`求和，`avg()`求平均值，`min()`求最小值，`max()`求最大值等。除了对表中所有数据汇总的情况外，汇总函数通常需要结合分组语句`group by`来使用，按照某个条件进行分组汇总统计。Group By分组子句的语法为`group by field_name`，还可以指定多个分组字段`group by field_name1, field_name2`。与Order By子句相似，也可以按字段在Select子句中出现的位置来指定分组字段，这样可以让我们的SQL更加简洁。例如`group by 1`表示按第一个字段分组，`group by 1, 2`表示同时按第一个和第二个字段分组。我们通过一些例子来说明常用汇总函数的用法。

**统计目前支持的各个区块链的ERC20代币类型数量：**

```sql
select blockchain, count(*) as token_count
from tokens.erc20
group by blockchain
```



**统计支持的所有区块链的代币类型总数量、平均值、最小值、最大值：**

```sql
-- 这里为了演示相关函数，使用了子查询
select count(*) as blockchain_count,
    sum(token_count) as total_token_count,
    avg(token_count) as average_token_count,
    min(token_count) as min_token_count,
    max(token_count) as max_token_count
from (
    select blockchain, count(*) as token_count
    from tokens.erc20
    group by blockchain
)
```



#### 子查询（Sub Query）

子查询（Sub Query）是嵌套在一个Query中的Query，子查询会返回一个完整的数据集供外层查询（也叫父查询、主查询）进一步查询使用。当我们需要必须从原始数据开始通过多个步骤的查询、关联、汇总操作才能得到理想的输出结果时，我们就可以使用子查询。将子查询放到括号之中并为其赋予一个别名后，就可以像使用其他数据表一样使用子查询了。

在前面的例子中就用到了子查询`from ( 子查询语句 )`，这里不再单独举例。

#### 多表关联（Join）

当我们需要从相关的多个表分别取数据，或者从同一个表分别取不同的数据并连接到一起时，就需要使用多表关联。多表关联的基本语法为：`from table_a inner join table_b on table_a.field_name = table_b.field_name`。其中`table_a`和`table_b`可以是不同的表，也可以是同一个表，可以有不同的别名。

下面的查询使用`tokens.erc20`与其自身关联，来筛选出同时存在于以太坊区块链和币安区块链上且代币符号相同的记录：

```sql
select a.symbol,
    a.decimals,
    a.blockchain as blockchain_a,
    a.contract_address as contract_address_a,
    b.blockchain as blockchain_b,
    b.contract_address as contract_address_b
from tokens.erc20 a
inner join tokens.erc20 b on a.symbol = b.symbol
where a.blockchain = 'ethereum'
    and b.blockchain = 'bnb'
limit 100
```



#### 集合（Union）

当我们需要将来自不同数据表的记录合并到一起，或者将由同一个数据表取出的包含不同字段的结果集合并到一起时，可以使用`Union`或者`Union All`集合子句来实现。`Union`会自动去除合并后的集合里的重复记录，`Union All`则不会做去重处理。对于包括海量数据的链上数据库表，去重处理有可能相当耗时，所以建议尽可能使用`Union All`以提升查询效率。

因为暂时我们尽可能保持简单，下面演示集合的SQL语句可能显得意义不大。不过别担心，这里只是为了显示语法。后续我们在做数据看板的部分有更合适的例子：

```sql
select contract_address, symbol, decimals
from tokens.erc20
where blockchain = 'ethereum'

union all

select contract_address, symbol, decimals
from tokens.erc20
where blockchain = 'bnb'

limit 100
```



#### Case 语句

使用Case语句，我们可以基于某个字段的值来生成另一种类型的值，通常是为了让结果更直观。举例来说，ERC20代币表有一个`decimals`字段，保存各种代币支持的小数位数。如果我们想按支持的小数位数把各种代币划分为高精度、中等精度和低精度、无精度等类型，则可以使用Case语句进行转换。

```sql
select (case when decimals >= 10 then 'High precision'
            when decimals >= 5 then 'Middle precision'
            when decimals >= 1 then 'Low precision'
            else 'No precision'
        end) as precision_type,
    count(*) as token_count
from tokens.erc20
group by 1
order by 2 desc
```



#### CTE公共表表达式

公共表表达式，即CTE（Common Table Expression），是一种在SQL语句内执行（且仅执行一次）子查询的好方法。数据库将执行所有的WITH子句，并允许你在整个查询的后续任意位置使用其结果。

CTE的定义方式为`with cte_name as ( sub_query )`，其中`sub_query`就是一个子查询语句。我们也可以在同一个Query中连续定义多个CTE，多个CTE之间用英文逗号分隔即可。按定义的先后顺序，后面的CTE可以访问使用前面的CTE。在后续数据看板部分的“查询6”中，你可以看到定义多个CTE的示例。将前面子查询的例子用CTE格式改写：

```sql
with blockchain_token_count as (
    select blockchain, count(*) as token_count
    from tokens.erc20
    group by blockchain
)

select count(*) as blockchain_count,
    sum(token_count) as total_token_count,
    avg(token_count) as average_token_count,
    min(token_count) as min_token_count,
    max(token_count) as max_token_count
from blockchain_token_count
```



## 总结

恭喜！你已经熟悉了创建第一个Dune数据看板所需要的全部知识点。在下一篇教程中，我们将一起创建一个Dune数据看板。

你还可以通过以下链接学习更多相关的内容：

- [Dune平台的官方文档](https://dune.com/docs/)（Dune）
- [Dune入门指南](https://mirror.xyz/0xa741296A1E9DDc3D6Cf431B73C6225cFb5F6693a/iVzr5bGcGKKCzuvl902P05xo7fxc2qWfqfIHwmCXDI4)（SixdegreeLab成员Louis Wang翻译）
- [Dune Analytics零基础极简入门指南](https://mirror.xyz/gm365.eth/OE_CGx6BjCd-eQ441139sjsa3kTyUsmKVTclgMv09hY)（Dune社区用户gm365撰写）



# 4 创建第一个Dune数据看板

在上一篇“[新手上路](http://wtf.academy/analysis-101/ch02/)”中，我们学习了创建第一个数据看板需要的预备知识，掌握了基础SQL查询的编写技巧。现在让我们一起来编写查询并创建一个Dune数据看板。为了帮助大家更快上手实践，我们这个数据看板将结合具体的项目来制作。完成后的数据看板的示例：https://dune.com/sixdegree/uniswap-v3-pool-tutorial。

我们不会详细描述每一个操作步骤。关于如何使用Dune的查询编辑器（Query Editor）和数据看板（Dashboard）的基础知识，你可以通过[Dune平台的官方文档](https://dune.com/docs/)来学习。

## 背景知识

开始创建看板之前，我们还需要了解一些额外的背景知识。Uniswap是最流行的去中心化金融（DeFi）协议之一，是一套持久的且不可升级的智能合约，它们共同创建了一个自动做市商（AMM），该协议主要提供以太坊区块链上的点对点ERC20代币的交换。Uniswap工厂合约（Factory）部署新的智能合约来创建流动资金池（Pool），将两个ERC20代币资产进行配对，同时设置不同的费率（fee）。流动性（Liquidity）是指存储在Uniswap资金池合约中的数字资产，可供交易者进行交易。流动性提供者（Liquidity Provider，简称LP）是将其拥有的ERC20代币存入给定的流动性池的人。流动性提供者获得交易费用的补偿作为收益，同时也承担价格波动带来的风险。普通用户（Swapper）通过可以在流动资金池中将自己拥有的一种ERC20代币兑换为另一种代币，同时支付一定的服务费。比如你可以在费率为0.30%的USDC-WETH流动资金池中，将自己的USDC兑换为WETH，或者将WETH兑换为USDC，仅需支付少量的服务费即可完成兑换。Uniswap V3协议的工作方式可以简要概括为：工厂合约创建流动资金池（包括两种ERC20代币） -> LP用户添加对应资产到流动资金池 -> 其他用户使用流动资金池兑换其持有的代币资产，支付服务费 -> LP获得服务费奖励。

初学者可能对这部分引入的一些概念比较陌生，不过完全不用紧张，你无需了解更多DeFi的知识就可以顺利完成本教程的内容。本篇教程不会深入涉及DeFi协议的各种细节，我们只是想通过实际的案例，让你对“链上数据分析到底分析什么”有一个更感性的认识。在我们将要创建的这个数据看板中，主要使用Uniswap V3的流动资金池作为案例. 对应的数据表为`uniswap_v3_ethereum.Factory_evt_PoolCreated`。同时，部分查询也用到了前面介绍过的`tokens.erc20`表。开始之前，你只需要了解这些就足够了：可以创建很多个不同的流动资金池（Pool），每一个流动资金池包含两种不同的ERC20代币（称之为代币对，Pair），有一个给定的费率；相同的代币对（比如USDC-WETH）可以创建多个流动资金池，分别对应不同的收费费率。

## Uniswap流动资金池表

流动资金池表`uniswap_v3_ethereum.Factory_evt_PoolCreated`的结构如下：

| **列名**         | **数据类型** | **说明**                                        |
| ---------------- | ------------ | ----------------------------------------------- |
| contract_address | string       | 合约地址                                        |
| evt_block_number | long         | 区块编号                                        |
| evt_block_time   | timestamp    | 区块被开采的时间                                |
| evt_index        | integer      | 事件的索引编号                                  |
| evt_tx_hash      | string       | 事件归属交易的唯一哈希值                        |
| fee              | integer      | 流动资金池的收费费率（以“百万分之N”的形式表示） |
| pool             | string       | 流动资金池的地址                                |
| tickSpacing      | integer      | 刻度间距                                        |
| token0           | string       | 资金池中的第一个ERC20代币地址                   |
| token1           | string       | 资金池中的第二个ERC20代币地址                   |

流动资金池表的部分数据如下图所示（这里只显示了部分字段）：



![image_00.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051317401.png)



## 数据看板的主要内容

我们的第一个Dune数据看板将包括以下查询内容。每个查询会输出1个或多个可视化图表。

- 查询流动资金池总数
- 不同费率的流动资金池数量
- 按周汇总的新建流动资金池总数
- 最近30天的每日新建流动资金池总数
- 按周汇总的新建流动资金池总数-按费率分组
- 统计资金池数量最多的代币Token
- 最新的100个流动资金池记录

## 查询1: 查询流动资金池总数

通过使用汇总函数Count()，我们可以统计当前已创建的全部资金池的数量。

```sql
select count(*) as pool_count
from uniswap_v3_ethereum.Factory_evt_PoolCreated
```



我们建议你复制上面的代码，创建并保存查询。保存查询时为其起一个容易识别的名称，比如我使用“uniswap-pool-count”作为这个查询的名称。当然你也可以直接Fork下面列出的参考查询。Fork查询的便利之处是可以了解更多可视化图表的细节。

本查询在Dune上的参考链接：https://dune.com/queries/1454941

## 创建数据看板并添加图表

### 创建看板

首先请登录进入[Dune网站](https://dune.com/)。然后点击头部导航栏中的“My Creation”，再点击下方的“Dashboards”，进入到已创建的数据看板页面https://dune.com/browse/dashboards/authored。要创建新的数据看板，点击右侧边栏中的“New dashboard”按钮即可。在弹出对话框中输入Dashboard的名称，然后点击“Save and open”按钮即可创建新数据看板并进入预览界面。我这里使用“Uniswap V3 Pool Tutorial”作为这个数据看板的名称。

### 添加查询图表

新创建的数据看板是没有内容的，预览页面会显示“This dashboard is empty.”。我们可以将上一步“查询1”中得到的资金池数量转为可视化图表并添加到数据看板中。在一个新的浏览器Tab中打开“My Creations”页面https://dune.com/browse/queries/authored，找到已保存的“查询1”Query，点击名称进入编辑页面。因为查询已经保存并执行过，我们可以自己点击“New visualization”按钮来新建一个可视化图表。单个数值类型的的查询结果，通常使用计数器（Counter）类型的可视化图表。从下拉列表“Select visualization type”中选择“Counter”，再点击“Add Visualization”按钮。然后可以给这个图表命名，将Title值从默认的“Counter”修改为“流动资金池总数”。最后，通过点击“Add to dashboard“按钮，并在弹出对话框中点击对应数据看板右边的“Add”按钮，就把这个计数器类型的图表添加到了数据看板中。

此时我们可以回到数据看板页面，刷新页面可以看到新添加的可视化图表。点击页面右上方的“Edit”按钮可以对数据看板进行编辑，包括调整各个图表的大小、位置，添加文本组件等。下面是对“流动资金池总数”这个计数器图表调整了高度之后的截图。



![image_01.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051316416.png)



### 添加文本组件

在数据看板的编辑页面，我们可以通过点击“Add text widget”按钮，添加文本组件到看板中。文本组件可以用来为数据看板的核心内容添加说明，添加作者信息等。文本组件支持使用Markdown语法实现一些格式化处理，在添加文本组件的对话框中点击“Some markdown is supported”展开可以看到支持的相关语法。请根据需要自行添加相应的文本组件：

| Bold            | ***\*text\****                                               |
| --------------- | ------------------------------------------------------------ |
| Italic          | *_text_*                                                     |
| Heading 1       | # Text                                                       |
| Heading 2       | ## Text                                                      |
| Heading 3       | ### Text                                                     |
| Anchor Links    | [Heading 1](#heading-1) *How to enable anchor links:*Hover over a Heading to see a 🔗.Click the 🔗 to copy the hashtag link from URL.Paste it inside parentheses like `[Heading 1](#heading-1)` to create a clickable link. |
| Link            | [Link][(https://dune.com)](https://dune.com/)                |
| Image or GIF    | ![image][(https://cutt.ly/1AKJVWx)](https://cutt.ly/1AKJVWx) |
| Inline code     | \`code\`\`                                                   |
| Code block      | \``` code block \```                                         |
| Horizontal rule | ---                                                          |
| Ordered list    | First item<br />Second item<br />Third item                  |
| List            | - First item<br />- Second item<br />- Third item            |

## 查询2：不同费率的流动资金池数量

根据我们需要的结果数据的格式，有不同的方式来统计。如果想使用计数器（Counter）类型的可视化图表，可以把相关统计数字在同一行中返回。如果想用一个扇形图（Pie Chart）来显示结果，则可以选择使用Group By分组，将结果数据以多行方式返回。

**使用Filter子句：**

```sql
select count(*) filter (where fee = 100) as pool_count_100,
    count(*) filter (where fee = 500) as pool_count_500,
    count(*) filter (where fee = 3000) as pool_count_3000,
    count(*) filter (where fee = 10000) as pool_count_10000
from uniswap_v3_ethereum.Factory_evt_PoolCreated
```



本查询在Dune上的参考链接：https://dune.com/queries/1454947

这个查询返回了4个输出值，我们为他们添加相应的计数器组件，分别命名为“0.01%资金池数量”、“0.05%资金池数量”等。然后添加到数据看板中，在数据看板编辑界面调整各组件的大小和顺序。调整后的显示效果如下图所示：



![image_02.png](https://www.wtf.academy/assets/images/image_02-1518a00b39d4f31bb08cfad1acf6d6d9.png)



**使用Group By子句：**

```sql
select fee,
    count(*) as pool_count
from uniswap_v3_ethereum.Factory_evt_PoolCreated
group by 1
```



费率“fee”是数值形式，代表百万分之N的收费费率。比如，3000，代表3000/1000000，即“0.30%”。用`fee`的值除以10000 （1e4）即可得到用百分比表示的费率。 将数值转换为百分比表示的费率更加直观。我们可以使用修改上面的查询来做到这一点：

```sql
select concat(format('%,.2f', fee / 1e4), '%') as fee_tier,
    count(*) as pool_count
from uniswap_v3_ethereum.Factory_evt_PoolCreated
group by 1
```



其中，`concat(format('%,.2f', fee / 1e4), '%') as fee_tier`部分的作用是将费率转换为百分比表示的值，再连接上“%”符号，使用别名`fee_tier`输出。关于format()函数的具体语法，可以查看Trino 的帮助（Trino是Dune SQL的底层引擎）。Trino帮助链接：https://trino.io/docs/current/functions.html 。

本查询在Dune上的参考链接：https://dune.com/queries/1455127

我们为这个查询添加一个扇形图图表。点击“New visualization”，从图表类型下拉列表选择“Pie Chart”扇形图类型，点击“Add visualization”。将图表的标题修改为“不同费率的资金池数量”。图表的水平坐标轴（X Column）选择“fee_tier“，垂直坐标轴“Y Column 1”选择“pool_count”。勾选左侧的“Show data label”选项。然后用“Add to dashboard”把这个可视化图表添加到数据看板中。其显示效果如下：



![image_03.png](https://www.wtf.academy/assets/images/image_03-b517b68f7de1da2da2a0c5e127607b10.png)



## 查询3：按周汇总的新建流动资金池总数

要实现汇总每周新建的流动资金池数量的统计，我们可以先在一个子查询中使用date_trunc()函数将资金池的创建日期转换为每周的开始日期（星期一），然后再用Group By进行汇总统计。

```sql
select block_date, count(pool) as pool_count
from (
    select date_trunc('week', evt_block_time) as block_date,
        evt_tx_hash,
        pool
    from uniswap_v3_ethereum.Factory_evt_PoolCreated
)
group by 1
order by 1
```



本查询在Dune上的参考链接：https://dune.com/queries/1455311

按时间统计的数据，适合用条形图、面积图、折线图等形式来进行可视化，这里我们用条形图。点击“New visualization”，从图表类型下拉列表选择“Bar Chart”条形图类型，点击“Add visualization”。将图表的标题修改为“每周新建资金池数量统计”。图表的水平坐标轴（X Column）选择“block_date“，垂直坐标轴“Y Column 1”选择“pool_count”。取消勾选左侧的“Show chart legend”选项。然后用“Add to dashboard”把这个可视化图表添加到数据看板中。其显示效果如下：



![image_04.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051316979.png)



## 查询4：最近30天的每日新建流动资金池总数

类似的，要实现汇总每天新建的流动资金池数量的统计，我们可以先在一个子查询中使用date_trunc()函数将资金池的创建日期转换为天（不含时分秒值），然后再用Group By进行汇总统计。这里我们使用公共表表达式（CTE）的方式来查询。与使用子查询相比，CTE能让查询逻辑更加直观易懂、定义后可以多次重用以提升效率、也更方便调试。后续的查询都会倾向于使用CTE方式。

```sql
with pool_details as (
    select date_trunc('day', evt_block_time) as block_date, evt_tx_hash, pool
    from uniswap_v3_ethereum.Factory_evt_PoolCreated
    where evt_block_time >= now() - interval '29' day
)

select block_date, count(pool) as pool_count
from pool_details
group by 1
order by 1
```

> [!TIP]
>
> **`date_trunc('day', evt_block_time) as block_date`**:
>
> - **`evt_block_time`** 是表中的原始字段，表示区块的时间戳。
> - **`date_trunc('day', evt_block_time)`** 是对 `evt_block_time` 进行的处理，使用 `date_trunc` 函数将时间戳精确到“天”。这意味着只保留日期部分（去掉时、分、秒），例如 `2024-10-05 15:34:20` 会变成 `2024-10-05`。
> - **`as block_date`** 是为处理后的结果起的别名（alias），即将其命名为 `block_date`，方便后续引用。
>
> **`evt_tx_hash`**:
>
> - 这是原始字段，代表与事件相关的交易哈希值，每次交易在区块链上都有一个唯一的哈希值。这个字段未进行处理，直接被选中。
>
> **`pool`**:
>
> - 这个字段表示池子（liquidity pool）的地址或标识符，它同样是表中的原始字段，也没有进行额外的处理。

本查询在Dune上的参考链接：https://dune.com/queries/1455382

我们同样使用条形图来做可视化。添加一个条形图类型的新图表，将标题修改为“近30天每日新增资金池数量”。图表的水平坐标轴（X Column）选择“block_date“，垂直坐标轴“Y Column 1”选择“pool_count”。取消勾选左侧的“Show chart legend”选项，同时勾选上“Show data labels”选项。然后把这个可视化图表添加到数据看板中。其显示效果如下：



![image_05.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051316061.png)



## 查询5：按周汇总的新建流动资金池总数-按费率分组

我们可以对分组统计的维度做进一步的细分，按费率来汇总统计每周内新建的流动资金池数量。这样我们可以对比不同费率在不同时间段的流行程度。这个例子中我们演示Group by多级分组，可视化图表数据的条形图的叠加等功能。

```sql
with pool_details as (
    select date_trunc('week', evt_block_time) as block_date, fee, evt_tx_hash, pool
    from uniswap_v3_ethereum.Factory_evt_PoolCreated
)

select block_date,
    concat(format('%,.2f', fee / 1e4), '%') as fee_tier,
    count(pool) as pool_count
from pool_details
group by 1, 2
order by 1, 2
```



本查询在Dune上的参考链接：https://dune.com/queries/1455535

我们同样使用条形图来做可视化。添加一个条形图类型的新图表，将标题修改为“不同费率每周新建流动资金池数量”。图表的水平坐标轴（X Column）选择“block_date“，垂直坐标轴“Y Column 1”选择“pool_count”。同时，我们需要在“Group by”中选择“fee_tier”作为可视化图表的分组来实现分组显示，同时勾选左侧的“Enable stacking”选项让同一日期同一分组的数据叠加到一起显示。把这个可视化图表添加到数据看板中的显示效果如下：



![image_06.png](https://www.wtf.academy/assets/images/image_06-ea27786cc1345c0795e60a8cef0c17d9.png)



## 查询6：统计资金池数量最多的代币Token

如果想分析哪些ERC20代币在Uniswap资金池中更流行（即它们对应的资金池数量更多），我们可以按代币类型来做分组统计。

每一个Uniswap流动资金池都由两个ERC20代币组成（token0和token1），根据其地址哈希值的字母顺序，同一种ERC20代币可能保存在token0中，也可能保存在token1中。所以，在下面的查询中，我们通过使用集合（Union）来得到完整的资金池详细信息列表。

另外，资金池中保存的是ERC20代币的合约地址，直接显示不够直观。Dune社区用户提交的魔法书生成的抽象数据表`tokens.erc20`保存了ERC20代币的基本信息。通过关联这个表，我们可以取到代币的符号（Symbol），小数位数（Decimals）等。这里我们只需使用代币符号。

因为Uniswap V3 一共有8000多个资金池，涉及6000多种不同的ERC20代币，我们只关注资金池最多的100个代币的数据。下面的查询演示以下概念：多个CTE，Union，Join，Limit等。

```sql
with pool_details as (
    select token0 as token_address,
        evt_tx_hash, pool
    from uniswap_v3_ethereum.Factory_evt_PoolCreated

    union all

    select token1 as token_address,
        evt_tx_hash, pool
    from uniswap_v3_ethereum.Factory_evt_PoolCreated
),

token_pool_summary as (
    select token_address,
        count(pool) as pool_count
    from pool_details
    group by 1
    order by 2 desc
    limit 100
)

select t.symbol, p.token_address, p.pool_count
from token_pool_summary p
inner join tokens.erc20 t on p.token_address = t.contract_address
order by 3 desc
```

> [!TIP]
>
> 好的，让我们再详细地分解每一部分的查询逻辑。
>
> ### 1. **CTE (Common Table Expression): `pool_details`**
>
> ```sql
> with pool_details as (
>     select token0 as token_address,
>         evt_tx_hash, pool
>     from uniswap_v3_ethereum.Factory_evt_PoolCreated
> 
>     union all
> 
>     select token1 as token_address,
>         evt_tx_hash, pool
>     from uniswap_v3_ethereum.Factory_evt_PoolCreated
> )
> ```
>
> #### 第一部分解读：
> - `with pool_details as` 是一个 CTE，用来在后续的查询中引用。这个 CTE 被用来生成一个中间表 `pool_details`，表中的每一行代表 Uniswap V3 池子中的一个代币及其关联的交易和池子信息。
>   
> #### 两个查询：
> 1. **第一个查询：**
>    ```sql
>    select token0 as token_address,
>        evt_tx_hash, pool
>    from uniswap_v3_ethereum.Factory_evt_PoolCreated
>    ```
>    - **`token0 as token_address`**：从 `Factory_evt_PoolCreated` 表中选择 `token0`，这是 Uniswap V3 中池子第一个代币的地址。通过 `as token_address` 起别名，将这个字段命名为 `token_address`，表示池子中关联的代币地址。
>    - **`evt_tx_hash`**：选择 `evt_tx_hash`，代表创建池子的交易哈希，用来标识这笔交易。这个字段并未在后续的聚合中使用，但可能是为了后续查询中保持交易的可追溯性。
>    - **`pool`**：选择 `pool`，代表池子的地址，每个池子都有唯一的标识。
>
> 2. **第二个查询：**
>    ```sql
>    select token1 as token_address,
>        evt_tx_hash, pool
>    from uniswap_v3_ethereum.Factory_evt_PoolCreated
>    ```
>    - **`token1 as token_address`**：从 `Factory_evt_PoolCreated` 表中选择 `token1`，即池子中的第二个代币的地址。同样将其命名为 `token_address`，方便和 `token0` 的地址统一处理。
>    - 其他字段 (`evt_tx_hash` 和 `pool`) 同样与第一个查询一致。
>
> #### `union all`：
> - **`union all`**：将两个查询的结果合并。`union all` 的特点是会保留所有重复项，不会进行去重操作。这里我们需要保留每个池子的两个代币（`token0` 和 `token1`），所以使用 `union all`。每个池子会分别记录两个代币的地址，这样每个池子会被拆成两行，分别对应两个代币。
>
> ### 2. **CTE: `token_pool_summary`**
>
> ```sql
> token_pool_summary as (
>     select token_address,
>         count(pool) as pool_count
>     from pool_details
>     group by 1
>     order by 2 desc
>     limit 100
> )
> ```
>
> #### 第二部分解读：
> - 这个 CTE `token_pool_summary` 从第一个 CTE `pool_details` 中获取数据，对代币地址（`token_address`）进行池子数量的汇总，并按池子数量从多到少排序，最后取出前 100 个代币。
>
> #### 关键操作：
> - **`select token_address, count(pool) as pool_count`**：
>   - **`token_address`**：从 `pool_details` 中提取代币地址，作为主键。
>   - **`count(pool) as pool_count`**：对 `pool` 进行计数（`count(pool)`），统计每个代币所关联的池子的数量，并将这个值命名为 `pool_count`。
>   
> - **`group by 1`**：按第一个字段 `token_address` 进行分组，这样每个代币的池子数量会被聚合到一行。
>   
> - **`order by 2 desc`**：按第二个字段，也就是 `pool_count`，从大到小排序，确保最多池子相关的代币排在前面。
>
> - **`limit 100`**：只取前 100 个代币，即与最多池子关联的 100 个代币。
>
> ### 3. **最终查询**
>
> ```sql
> select t.symbol, p.token_address, p.pool_count
> from token_pool_summary p
> inner join tokens.erc20 t on p.token_address = t.contract_address
> order by 3 desc
> ```
>
> #### 第三部分解读：
> 这是最终的选择查询部分，目的是将代币地址与其对应的代币符号关联起来，并按池子数量进行排序。
>
> #### 关键操作：
> - **`select t.symbol, p.token_address, p.pool_count`**：
>   - **`t.symbol`**：从 `tokens.erc20` 表中选择代币的符号（`symbol`），例如 ETH、USDT 等。
>   - **`p.token_address`**：从 `token_pool_summary` 中选择代币地址（`token_address`），这是前一步已经汇总的地址。
>   - **`p.pool_count`**：从 `token_pool_summary` 中选择池子数量（`pool_count`），表示该代币关联的池子数量。
>
> - **`inner join tokens.erc20 t on p.token_address = t.contract_address`**：
>   - **`inner join`** 是连接两个表的操作，它将 `token_pool_summary` 中的代币地址（`p.token_address`）与 `tokens.erc20` 表中的合约地址（`t.contract_address`）进行匹配。`tokens.erc20` 表保存了每个代币的符号（`symbol`）和合约地址，通过匹配代币地址可以获取代币符号。
>
> - **`order by 3 desc`**：按第三个字段，也就是 `pool_count`，从大到小排序，确保与最多池子关联的代币排在前面。
>
> ### 总结：
> 该查询的流程是：
> 1. 从 Uniswap V3 的池子创建事件表中提取 `token0` 和 `token1`，并通过 `union all` 将这两个代币地址作为单独的行保存，生成一个包含池子信息的表 `pool_details`。
> 2. 将 `pool_details` 按代币地址分组，并计算每个代币与多少个池子相关联，返回池子数量最多的前 100 个代币。
> 3. 通过 `inner join`，将代币地址与其符号进行匹配，最后按池子数量从大到小排序，返回代币的符号、地址和池子数量。
>
> 这个查询可以帮助你了解哪些代币与 Uniswap V3 上的池子关联最多，这通常能反映代币在市场中的活跃度和流动性。
>
> ### 别名
>
> **`from token_pool_summary p`**：这里为 `token_pool_summary` CTE 起了别名 `p`。这样后面所有引用 `token_pool_summary` 中字段的地方都可以用 `p.` 来表示。例如，`p.token_address` 和 `p.pool_count` 分别代表 `token_pool_summary` 中的 `token_address` 和 `pool_count` 字段。
>
> **`inner join tokens.erc20 t`**：这里为 `tokens.erc20` 表起了别名 `t`。因此，查询中引用 `tokens.erc20` 表的字段时，可以用 `t.` 来表示。例如，`t.symbol` 代表 `tokens.erc20` 表中的 `symbol` 字段，`t.contract_address` 代表该表中的 `contract_address` 字段。

本查询在Dune上的参考链接：https://dune.com/queries/1455706

我们同样使用条形图来做可视化。添加一个条形图类型的新图表，将标题修改为“不同ERC20代币的资金池数量（Top 100）”。图表的水平坐标轴（X Column）选择“symbol“，垂直坐标轴“Y Column 1”选择“pool_count”。为了保持排序顺序（按数量从多到少），取消勾选右侧的“Sort values”选项。虽然我们限定了只取前面的100个代币的数据，从查询结果中仍然可以看到，各种Token的资金池数量差异很大，最多的有5000多个，少的则只有几个。为了让图表更直观，请勾选右侧的“Logarithmic”选项，让图表数据以对数化后显示。把这个可视化图表添加到数据看板中的显示效果如下：



![image_07.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051317900.png)



由于对数化显示处理从视觉上弱化了差异值，我们可以同时添加一个“Table“数据表类型的可视化图表，方便用户查看实际的数值。继续为这个查询添加新的可视化图表，选择“Table”图表类型。标题设置为“前100种ERC20代币的资金池数量统计”。可以根据需要对这个可视化表格的相关选项做调整，然后将其添加到Dashboard中。



![image_08.png](https://www.wtf.academy/assets/images/image_08-2bdbca60a3cde0f3d9ed5f6156d3f361.png)



你可能留意到表格返回的数据实际上没有100行，这是因为部分新出现的代币可能还未被添加到到Dune到数据表中。

## 查询7：最新的100个流动资金池记录

当某个项目方发行了新的ERC20代币并支持上市流通时，Uniswap用户可能会在第一时间创建相应的流动资金池，以让其他用户进行兑换。比如，XEN代币就是近期的一个比较轰动的案例。

我们可以通过查询最新创建的资金池来跟踪新的趋势。下面的查询同样关联`tokens.erc20`表获，通过不同的别名多次关联相同的表来获取不同代币的符号。本查询还演示了输出可视化表格，连接字符串生成超链接等功能。

```sql
with last_created_pools as (
    select p.evt_block_time,
        t0.symbol as token0_symbol,
        p.token0,
        t1.symbol as token1_symbol,
        p.token1,
        p.fee,
        p.pool,
        p.evt_tx_hash
    from uniswap_v3_ethereum.Factory_evt_PoolCreated p
    inner join tokens.erc20 t0 on p.token0 = t0.contract_address and t0.blockchain = 'ethereum'
    inner join tokens.erc20 t1 on p.token1 = t1.contract_address and t1.blockchain = 'ethereum'
    order by p.evt_block_time desc
    limit 100
)

select evt_block_time,
    token0_symbol || '-' || token1_symbol || ' ' || format('%,.2f', fee / 1e4) || '%' as pool_name,
    '<a href=https://etherscan.io/address/' || cast(pool as varchar) || ' target=_blank>' || cast(pool as varchar) || '</a>' as pool_link,
    token0,
    token1,
    fee,
    evt_tx_hash
from last_crated_pools
order by evt_block_time desc
```

> [!TIP]
>
> 这个查询的目标是获取最近创建的 Uniswap V3 池子的信息，并生成一个带有代币符号、手续费百分比、池子链接的输出表。让我们逐步详细分析每个部分：
>
> ### 1. **CTE: `last_crated_pools`**
> ```sql
> with last_crated_pools as (
>     select p.evt_block_time,
>         t0.symbol as token0_symbol,
>         p.token0,
>         t1.symbol as token1_symbol,
>         p.token1,
>         p.fee,
>         p.pool,
>         p.evt_tx_hash
>     from uniswap_v3_ethereum.Factory_evt_PoolCreated p
>     inner join tokens.erc20 t0 on p.token0 = t0.contract_address and t0.blockchain = 'ethereum'
>     inner join tokens.erc20 t1 on p.token1 = t1.contract_address and t1.blockchain = 'ethereum'
>     order by p.evt_block_time desc
>     limit 100
> )
> ```
>
> #### 分解：
> - **CTE 名称：**`last_crated_pools`（拼写应为 `last_created_pools`，但这里沿用了原始写法）。
>   
> - **查询字段：**
>   - **`p.evt_block_time`**：选择池子创建时的区块时间，记录了事件发生的时间。
>   - **`t0.symbol as token0_symbol`** 和 **`t1.symbol as token1_symbol`**：分别从 `tokens.erc20` 表中获取池子里两个代币的符号，并为它们分别起别名 `token0_symbol` 和 `token1_symbol`。
>   - **`p.token0`** 和 **`p.token1`**：获取池子里的两个代币的地址。
>   - **`p.fee`**：选择池子的手续费等级（`fee`），这通常是一个以 `10000` 为单位的整数，表示池子创建时设置的交易手续费率。
>   - **`p.pool`**：选择池子的合约地址，代表这个池子在区块链上的唯一标识。
>   - **`p.evt_tx_hash`**：选择池子创建时的交易哈希，表示触发这个事件的交易。
>
> - **`inner join` 操作：**
>   - **`inner join tokens.erc20 t0 on p.token0 = t0.contract_address`**：将池子中的 `token0` 与 `tokens.erc20` 表中的 `contract_address` 进行匹配，从而获取 `token0` 的符号。
>   - **`inner join tokens.erc20 t1 on p.token1 = t1.contract_address`**：同样的操作应用于 `token1`，匹配 `token1` 的合约地址以获取其符号。
>   - **`t0.blockchain = 'ethereum'`** 和 **`t1.blockchain = 'ethereum'`**：确保只匹配属于以太坊区块链的代币。
>
> - **`order by p.evt_block_time desc`**：根据池子创建时间降序排序，以便显示最新创建的池子。
>
> - **`limit 100`**：只获取最近创建的 100 个池子。
>
> ### 2. **主查询**
> ```sql
> select evt_block_time,
>     token0_symbol || '-' || token1_symbol || ' ' || format('%,.2f', fee / 1e4) || '%' as pool_name,
>     '<a href=https://etherscan.io/address/' || cast(pool as varchar) || ' target=_blank>' || cast(pool as varchar) || '</a>' as pool_link,
>     token0,
>     token1,
>     fee,
>     evt_tx_hash
> from last_crated_pools
> order by evt_block_time desc
> ```
>
> #### 分解：
> - **`select` 语句：**
>   - **`evt_block_time`**：显示池子创建的区块时间，记录了事件发生的确切时间。
>   
>   - **`token0_symbol || '-' || token1_symbol || ' ' || format('%,.2f', fee / 1e4) || '%' as pool_name`**：
>     - 这里使用 `||` 运算符将字符串拼接。
>     - **`token0_symbol || '-' || token1_symbol`**：将两个代币符号拼接，中间用 `-` 连接，表示这个池子是由这两个代币配对而成。
>     - **`format('%,.2f', fee / 1e4) || '%'`**：将池子的手续费 `fee` 除以 `10000`，然后格式化为百分比。`fee` 通常以 `10000` 为单位表示，因此需要通过 `fee / 1e4` 转换为百分比格式。`format` 函数格式化为包含逗号分隔符且保留两位小数的字符串，后面加上 `%` 号表示手续费率。例如，3000 会被格式化为 `0.30%`。
>     - **`as pool_name`**：将拼接后的字符串命名为 `pool_name`，表示池子的名称。
>
>   - **`'<a href=https://etherscan.io/address/' || cast(pool as varchar) || ' target=_blank>' || cast(pool as varchar) || '</a>' as pool_link`**：
>     - 这里是生成一个 HTML 超链接，指向 Etherscan 上显示该池子信息的页面。
>     - **`cast(pool as varchar)`**：将池子的地址 `pool` 转换为字符串形式。
>     - **`<a href=...>`**：生成一个 `<a>` 标签，点击后会打开 Etherscan 上显示该池子地址的页面。`target="_blank"` 表示在新标签页中打开链接。
>     - **`as pool_link`**：将生成的 HTML 超链接命名为 `pool_link`，在结果中以超链接的形式显示池子地址。
>
>   - **`token0`** 和 **`token1`**：直接显示池子中两个代币的地址。
>   
>   - **`fee`**：显示池子的手续费（整数形式，未转换为百分比）。
>   
>   - **`evt_tx_hash`**：显示池子创建时的交易哈希，便于追踪创建池子的交易。
>
> - **`order by evt_block_time desc`**：根据池子创建时间降序排序，确保最新的池子显示在最前面。
>
> ### 最终输出结果：
> 该查询最终会返回最近创建的 100 个 Uniswap V3 池子的信息，包括：
> - **创建时间 (`evt_block_time`)**
> - **池子的名称 (`pool_name`)**：以 `token0-symbol-token1-symbol` 格式显示，并附带手续费百分比。例如，`ETH-USDC 0.30%`。
> - **池子的超链接 (`pool_link`)**：链接到 Etherscan 页面，显示池子地址的详细信息。
> - **代币地址 (`token0`, `token1`)**：参与池子的两个代币的合约地址。
> - **手续费 (`fee`)**：显示手续费（未格式化的整数）。
> - **交易哈希 (`evt_tx_hash`)**：池子创建的交易哈希。

本查询在Dune上的参考链接：https://dune.com/queries/1455897

我们为查询添加一个“Table“数据表类型的可视化图表，将标题设置为“最新创建的资金流动池列表”。可以根据需要对这个可视化表格的相关选项做调整，然后将其添加到Dashboard中。



![image_09.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051317785.png)



# 总结

至此，我们就完成了第一个Dune数据看板的创建。这个数据看板的完整界面显示效果如下图所示：



![dashboard.png](https://www.wtf.academy/assets/images/dashboard-28e8be1b5f432b6849149e95bd104dd7.png)



为了避免内容太过深奥难懂，我们只是做了一些基本的查询，整个数据看板的图表看起来可能不一定那么炫酷。但是这个并不重要，我们更关心的是你能否通过这篇教程开始走上自己的链上数据分析之路。 希望大家在看完之后动手尝试一下，选例Uniswap是一个DEX，类似的我们可以对任意链上的DEX进行分析。结合上一讲中的技巧，大家可以尝试对其他DEX，甚至同一Dex不同链上数据进行分析比较（如UniSwap在Ethereum和Optimism上的数据）。成为链上数据分析师，看板就是你的简历，认真做起来吧！

# 作业内容

请结合教程内容，制作对任意DEX进行不少于5个查询的数据看板，看板命名格式为SixdegreeAssignment1-称呼，如SixdegreeAssignment1-Spring，方便大家互相学习，也方便我们把握教学质量。为了鼓励大家积极动手制作看板，我们将对作业完成情况和质量进行记录，之后追溯为大家提供一定的奖励，包括但不限于Dune社区身份，周边实物，API免费额度，POAP，各类合作的数据产品会员，区块链数据分析工作机会推荐，社区线下活动优先报名资格以及其他Sixdegree社区激励等。

加油！欢迎大家将自己的数据看板链接分享到Dune交流微信群、Dune的Discord中文频道。

# 5. 熟悉数据表

以Dune为代表的数据平台将区块链数据解析保存到数据库中。数据分析师针对具体的分析需求，编写SQL从相应的数据表中查询数据进行分析。目前市面上流行的区块链越来越多，新的区块链还在不断出现，部署到不同区块链上的各类项目也越来越丰富。如何快速找到待分析的项目对应的数据表，理解掌握对应数据表里每个字段的含义和用途，是每一个分析师必须掌握的技能。

目前我们熟悉的几个数据平台提供的基础数据集的整体结构比较相似，我们这里只围绕Dune平台来讲解。如果你偏好使用其他数据平台，可以通过该平台对应的文档了解详情。由于Dune已经正式宣布在2023年内全面切换到Dune SQL查询引擎，我们已将本教程中的全部Query升级到Dune SQL 版本。

## Dune V2数据引擎数据表介绍

Dune 平台的数据集分为几种不同的类型：

- **原始数据（Raw）**：存储了未经编辑的区块链数据。包括blocks、transactions、traces等数据表。这些原始数据表保存了最原始的链上数据，可用于灵活的数据分析。
- **已解析项目（Decoded Projects）**：存储了经过解码后的智能合约事件日志及调用数据表。比如Uniswap V3相关的表，Opensea Seaport相关的表等。Dune使用智能合约的 ABI(Application Binary Interface) 和标准化代币智能合约的接口标准（ERC20、ERC721 等）来解析数据，并将每一个事件或者方法调用的数据单独保存到一个数据表中。
- **魔法表（Spells）**：魔法表在Dune V1中也叫抽象表（Abstractions），是Dune和社区用户一起通过spellbook github存储库来建设和维护，并通过dbt编译生成的数据表，这些数据表通常使用起来更为便捷高效。
- **社区贡献数据（Community）**：这部分是由第三方合作组织提供的数据源，自动接入到Dune的数据集里供分析师使用。目前Dune上主要有`flashbots`和`reservoir`两个社区来源数据集。
- **用户生成的数据表（User Generated Tables）**：目前Dune V2引擎尚未开放此功能，只能通过魔法表的方式来上传（生成）自定义数据表。

在Dune平台的Query编辑页面，我们可以通过左边栏来选择或搜索需要的数据表。这部分界面如下图所示：



![image_01.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051317130.png)



图片中间的文本框可以用于搜索对应的数据模式(Schema)或数据表。比如，输入`erc721`将筛选出名称包含这个字符串的所有魔法表和已解析项目表。图片中上方的红框部分用于选择要使用的数据集，途中显示的“v2 Dune SQL”就是我们通常说的“Dune SQL引擎”。Dune 将于2023年下半年全面过渡到Dune SQL引擎，所以现在大家只需熟悉Dune SQL的语法即可。

上图中下方的红框圈出的是前面所述Dune V2 引擎目前支持的几大类数据集。点击粗体分类标签文字即可进入下一级浏览该类数据集中的各种数据模式以及各模式下的数据表名称。点击分类标签进入下一级后，你还可以看到一个默认选项为“All Chains”的下拉列表，可以用来筛选你需要的区块链下的数据模式和数据表。当进入到数据表层级时，点击表名可以展开查看表中的字段列表。点击表名右边的“》”图标可以将表名（格式为`schema_name.table_name`插入到查询编辑器中光标所在位置。分级浏览的同时你也可以输入关键字在当前浏览的层级进一步搜索过滤。不同类型的数据表有不同的层次深度，下图为已解析数据表的浏览示例。



![image_03.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051317944.png)



## 原始数据表

区块链中典型的原始数据表包括：区块表（Blocks）、交易表（Transactions）、内部合约调用表（Traces）、事件日志表（Logs）以及合约创建跟踪表（creation_traces）。原始数据表的命名格式为`blockchain_name.table_name`，例如arbitrum.logs，bnb.blocks，ethereum.transactions，optimism.traces等。部分区块链有更多或者更少的原始数据表，我们使用以太坊为例做简单介绍。

### 区块表（ethereum.blocks）

区块（Block）是区块链的基本构建组件。一个区块包含多个交易记录。区块表记录了每一个区块生成的日期时间(block time)、对应的区块编号(block number)、区块哈希值、难度值、燃料消耗等信息。除了需要分析整个区块链的区块生成状况、燃料消耗等场景外，我们一般并不需要关注和使用区块表。其中最重要的是区块生成日期时间和区块编号信息，它们几乎都同时保存到了其他所有数据表中，只是对应的字段名称不同。

### 交易表（ethereum.transactions）

交易表保存了区块链上发生的每一个交易的详细信息（同时包括成功交易和失败交易）。以太坊的交易表结构如下图所示：



![image_02.png](https://www.wtf.academy/assets/images/image_02-4e16be5e383ed5931c8c1e883a8bd6ce.png)



交易表中最常用的字段包括block_time（或block_number）、from、to、value、hash、success等。Dune V2引擎是基于列存贮的数据库，每个表里的数据是按列存贮的。按列存贮的数据表无法使用传统意义上的索引，而是依赖于保存有“最小值/最大值”属性的元数据来提升查询性能。对于数值类型或者日期时间类型，可以很容易计算出一组值中的最小值/最大值。相反，对于字符串类型，因为长度可变，很难高效计算出一组字符串数据中的最小值/最大值。这就导致V2引擎在做字符串类型的查询时比较低效，所以我们通常需要同时结合使用日期时间类型或者数值类型的过滤条件来提升查询执行性能。如前所述，block_time, block_number字段几乎存在于所有的数据表中（在不同类型数据表中名称不同），我们应充分利用它们来筛选数据，确保查询可以高效执行。更多的相关信息可以查看[Dune V2查询引擎工作方式](https://docs.dune.com/dune-engine-v2-beta/query-engine#changes-in-how-the-database-works)来了解。

### 内部合约调用表（ethereum.traces）

一个交易（Transactions）可以触发更多的内部调用操作，一个内部调用还可能进一步触发更多的内部调用。这些调用执行的信息会被记录到内部合约调用表。内部合约调用表主要包括block_time、block_number、tx_hash、success、from、to、value、type等字段。

内部合约调用表有两个最常见的用途：

1. 用于跟踪区块链原生代币（Token）的转账详情或者燃料消耗。比如，对于以太坊，用户可能通过某个DAPP的智能合约将ETH转账到另一个（或者多个）地址。这种情况下，`ethereum.transactions`表的`value`字段并没有保存转账的ETH的金额数据，实际的转账金额只保存在内部合约调用表的`value`值中。另外，由于原生代币不属于ERC20代币，所以也无法通过ERC20协议的Transfer事件来跟踪转账详情。区块链交易的燃料费用也是用原生代币来支付的，燃料消耗数据同时保存于交易表和内部合约调用表。一个交易可能有多个内部合约调用，调用内部还可以发起新的调用，这就导致每个调用的`from`，`to`并不一致，也就意味着具体支付调用燃料费的账户地址不一致。所以，当我们需要计算某个地址或者一组地址的原生代币ETH余额时，只有使用`ethereum.traces`表才能计算出准确的余额。 这个查询有计算ETH余额的示例：[ETH顶级持有者余额](https://dune.com/queries/1001498/1731554)
2. 用于筛选合约地址。以太坊上的地址分为两大类型，外部拥有的地址（External Owned Address, EOA）和合约地址（Contract Address）。EOA外部拥有地址是指由以太坊用户拥有的地址，而合约地址是通过部署智能合约的交易来创建的。当部署新的智能合约时，`ethereum.traces`表中对应记录的`type`字段保存的值为`create`。我们可以使用这个特征筛选出智能合约地址。Dune V2里面，Dune团队已经将创建智能合约的内部调用记录整理出来，单独放到了表`ethereum.creation_traces`中。通过直接查询这个表就能确定某个地址是不是合约地址。

### 事件日志表（ethereum.logs）

事件日志表存储了智能合约生成的所有事件日志。当我们需要查询分析那些尚未被解码或者无法解码（由于代码非开源等原因）的智能合约，事件日志表非常有用。通常，我们建议优先使用已解析的数据表，这样可以提高效率并降低在查询中引入错误的可能性。但是，有时由于时效性（合约还未来得及被解码）或者合约本身不支持被解码的原因，我们就不得不直接访问事件日志表来查询数据进行分析。

事件日志表主要包括block_time、block_number、tx_hash、contract_address、topic1、topic2、topic3、topic4、data等字段。使用时需要注意的要点包括：

- `topic1` 存贮的是事件对应的方法签名的哈希值。我们可以同时使用contract_address 和topic1筛选条件来找出某个智能合约的某个方法的全部事件日志记录。
- `topic2`、`topic3`、`topic4` 存贮的是事件日志的可索引参数（主题），每个事件最多支持3个可索引主题参数。当索引主题参数不足3个时，剩余的字段不保存任何值。具体到每一个事件，这几个主题参数所保存的值各不相同。我们可以结合EtherScan这样的区块链浏览器上显示的日志来对照确认每一个主题参数代表什么含义。或者也可以查阅对应智能合约的源代码来了解事件参数的详细定义。
- `data`存贮的是事件参数中没有被标记为索引主题类型的其他字段的16进制的组合值，字符串格式，以`0x`开头，每个参数包括64个字符，实际参数值不足64位则在左侧填充`0`来补足位数。当我们需要从data里面解析数据时，就要按照上述特征，从第3个字符开始，以每64个字符为一组进行拆分，然后再按其实际存贮的数据类型进行转换处理（转为地址、转为数值或者字符串等）。

这里是一个直接解析logs表的查询示例：https://dune.com/queries/1510688。你可以复制查询结果中的tx_hash值访问EtherScan站点，切换到“Logs”标签页进行对照。下图显示了EtherScan上的例子：



![image_04.png](https://www.wtf.academy/assets/images/image_04-148abbd3f227c50fec9dcc20ea94db79.png)



## 已解析项目表

已解析项目表是数量最庞大的数据表类型。当智能合约被提交到Dune进行解析时，Dune为其中的每一个方法调用（Call）和事件日志（Event）生成一个对应的专用数据表。在Dune的查询编辑器的左边栏中，这些已解析项目数据表按如下层级来逐级展示：

```text
category name -> project name (namespace) -> contract name -> function name / event name

-- Sample
Decoded projects -> uniswap_v3 -> Factory -> PoolCreated
```



已解析项目表的命名规则如下： 事件日志：`projectname_blockchain.contractName_evt_eventName` 函数调用：`projectname_blockchain.contractName_call_functionName` 例如，上面的Uniswap V3 的 PoolCreated 事件对应的表名为`uniswap_v3_ethereum.Factory_evt_PoolCreated`。

一个非常实用的方法是查询`ethereum.contracts`魔法表来确认你关注的智能合约是否已经被解析。这个表存贮了所有已解析的智能合约的记录。如果查询结果显示智能合约已被解析，你就可以用上面介绍的方法在查询编辑器界面快速浏览或搜索定位到对应的智能合约的数据表列表。如果查询无结果，则表示智能合约尚未被解析，你可以将其提交给Dune团队去解析处理：[提交解析新合约](https://dune.com/contracts/new)。可以提交任意的合约地址，但必须是有效的智能合约地址并且是可以被解析的（Dune能自动提取到其ABI代码或者你有它的ABI代码）。

我们制作了一个数据看板，你可以直接查询[检查智能合约是否已被解码](https://dune.com/sixdegree/decoded-projects-contracts-check)

## 魔法表

魔法书（Spellbook）是一个由Dune社区共同建设的数据转换层项目。魔法（Spell）可以用来构建高级抽象表格，魔法可以用来查询诸如 NFT 交易表等常用概念数据。魔法书项目可自动构建并维护这些表格，且对其数据质量进行检测。 Dune社区中的任何人都可以贡献魔法书中的魔法，参与方式是提交github PR，需要掌握github源代码管理库的基本使用方法。如果你希望参与贡献魔法表，可以访问[Dune Spellbook](https://dune.com/docs/spellbook/)文档了解详情。

Dune社区非常活跃，已经创建了非常多的魔法表。其中很多魔法表已被广泛使用在我们的日常数据分析中，我们在这里对重要的魔法表做一些介绍。

### 价格信息表（prices.usd，prices.usd_latest）

价格信息表`prices.usd`记录了各区块链上主流ERC20代币的每分钟价格。当我们需要将将多种代币进行统计汇总或相互对比时，通常需要关联价格信息表统一换算为美元价格和金额后再进行汇总或对比。价格信息表目前提供了以太坊、BNB、Solana等链的常见ERC20代币价格信息，精确到每分钟。如果你需要按天或者按小时的价格，可以通过求平均值的方式来计算出平均价格。下面两个示例查询演示了两种同时获取多个token的每日价格的方式：

- [获取每日平均价格](https://dune.com/queries/1507164)
- [获取每天的最后一条价格数据](https://dune.com/queries/1506944)

最新价格表（prices.usd_latest）提供了相关ERC20代币的最新价格数据。

### DeFi交易信息表(dex.trades，dex_aggregator.trades)

DeFi交易信息表`dex.trades`提供了主流DEX交易所的交易数据，因为各种DeFi项目比较多，Dune社区还在进一步完善相关的数据源，目前已经集成的有uniswap、sushiswap、curvefi、airswap、clipper、shibaswap、swapr、defiswap、dfx、pancakeswap_trades、dodo等DEX数据。DeFi交易信息表是将来自不同项目的交易信息合并到一起，这些项目本身也有其对应的魔法表格，比如Uniswap 有`uniswap.trades`，CurveFi有`curvefi_ethereum.trades`等。如果我们只想分析单个DeFi项目的交易，使用这些项目特有的魔法表会更好。

DEX聚合器交易表`dex_aggregator.trades`保存了来自DeFi聚合器的交易记录。这些聚合器的交易通常最终会提交到某个DEX交易所执行。单独整理到一起可以避免与`dex.trades`记录重复计算。编写本文时，暂时还只有`cow_protocol`的数据。

### Tokens表（tokens.erc20，tokens.nft）

Tokens表目前主要包括ERC20代币表`tokens.erc20`和NFT表（ERC721）`tokens.nft`。`tokens.erc20`表记录了各区块链上主流ERC20代币的定义信息，包括合约地址、代币符号、代币小数位数等。`tokens.nft`表记录了各NFT项目的基本信息，这个表的数据源目前还依赖社区用户提交PR来进行更新，可能存在更新延迟、数据不完整等问题。由于区块链上数据都是已原始数据格式保存的，金额数值不包括小数位数，我们必须结合`tokens.erc20`中的小数位数才能正确转换出实际的金额数值。

### ERC代表信息表（erc20_ethereum.evt_Transfer，erc721_ethereum.evt_Transfer等）

ERC代币信息表分别记录了ERC20， ERC721（NFT），ERC1155等几种代币类型的批准（Approval）和转账（Transfer）记录。当我们要统计某个地址或者一组地址的ERC代币转账详情、余额等信息是，可以使用这一组魔法表。

### ENS域名信息表（ens.view_registrations等）

ENS域名信息相关的表记录了ENS域名注册信息、反向解析记录、域名更新信息等。

### 标签信息表（labels.all等）

标签信息表是一组来源各不相同的魔法表，允许我们将钱包地址或者合约地址关联到一个或者一组文字标签。其数据来源包括ENS域名、Safe钱包、NFT项目、已解析的合约地址等多种类型。当我们的查询中希望把地址以更直观更有可读性的方式来显示是，可以通过Dune内置的`get_labels()`函数来使用地址标签。

### 余额信息表（balances_ethereum.erc20_latest等）

余额信息表保存了每个地址每天、每小时、和最新的ERC20， ERC721（NFT），ERC1155几种代币的余额信息。如果我们要计算某组地址的最新余额，或者跟踪这些地址的余额随时间的变化情况，可以使用这一组表。

### NFT交易信息表（nft.trades等）

NFT交易信息表记录了各NFT交易平台的NFT交易数据。目前集成了opensea、magiceden、looksrare、x2y2、sudoswap、foundation、archipelago、cryptopunks、element、superrare、zora、blur等相关NFT交易平台的数据。跟DeFi交易数据类似，这些平台也各自有对应的魔法表，比如`opensea.trades`。当只需分析单个平台时，可以使用它特有的魔法表。

### 其他魔法表

除了上面提到的魔法表之外，还有很多其他的魔法表。Dune的社区用户还在不断创建新的魔法表。要了解进一步的信息，可以访问[Dune 魔法书](https://spellbook-docs.dune.com/#!/overview)文档网站。

## 社区贡献数据和用户生成数据表

如前文所述，目前Dune上主要有`flashbots`和`reservoir`两个社区来源数据集。Dune文档里面分别对这两个数据集做了简介：

[Dune社区来源数据表](https://dune.com/docs/reference/tables/community/)

# 6. SQL基础（一）

## 基础概念

**1、数据仓库是什么？**
说人话就是说就是出于数据统计的需要，把一些数据分门别类地存储起来,存储的载体是【数据表】。针对某一个或者一些主题的一系列【数据表】合在一起就是数据仓库。
注意: 这里的数据可以是结果数据(比如Uniswap上线以来某个交易对每天的交易量统计) 也可以是过程数据(Uniswap上线以来某个交易对发生的每一条交易记录明细：谁发起的，用A换B，交易时间，tx_hash，交易数量….)。

**2、SQL是什么？**
假设你想吃脆香米巧克力，但是你这会儿出不了门，你就叫个跑腿说：我需要一盒巧克力，他的牌子是脆香米。跑腿去了趟超市把巧克力买来送到你家。 类比过来SQL就是你说的那句话，Dune Analytics就是个跑腿儿，他可以让你可以跟数据仓库对话，并且将数据仓库里的数据给你搬出来给你。SQL最基本的结构或者语法就3个模块，几乎所有的SQL都会包含这3个部分:

**select**: 取哪个字段？
**from**：从哪个表里取？
**where**：限制条件是什么？

**3、数据表长什么样？**
你可以认为表就是一个一个的Excel 表，每一个Excel 表里存的不同的数据。以ethereum.transactions(以太坊上的transactions记录)为例：



![query-page](https://www.wtf.academy/assets/images/raw_data-c8f0d7f98ebfd0022a021f2c99b563a6.png)



顺便说下表里用比较多的几个字段

- **block_time**:交易被打包的时间
- **block_number**：交易被打包的区块高度
- **value**：转出了多少ETH(需要除以power(10,18)来换算精度)
- **from**：ETH从哪个钱包转出的
- **to**： ETH转到了哪个钱包
- **hash**：这个transaction的tx hash
- **success**：transaction是否成功

## 常见语法以及使用案例

### 1.基础结构·运算符·排序

**案例1**:我想看看孙哥钱包(0x3DdfA8eC3052539b6C9549F12cEA2C295cfF5296)在2022年1月份以来的每一笔ETH的大额转出(>1000ETH)是在什么时候以及具体的转出数量

#### SQL

```sql
select --Select后跟着需要查询的字段，多个字段用英文逗号分隔
    block_time 
    ,"from"
    ,"to"
    ,hash
    ,value /power(10,18) as value --通过将value除以/power(10,18)来换算精度，18是以太坊的精度
from ethereum.transactions --从 ethereum.transactions表中获取数据
where block_time > date('2022-01-01')  --限制Transfer时间是在2022年1月1日之后
and "from" = 0x3DdfA8eC3052539b6C9549F12cEA2C295cfF5296 --限制孙哥的钱包
and value /power(10,18) >1000 --限制ETH Transfer量大于1000
order by block_time --基于blocktime做升序排列，如果想降序排列需要在末尾加desc
```





![query-page](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051317865.png)



#### Dune Query URL

https://dune.com/queries/1523799

#### 语法说明

- SELECT
  - SELECT后边跟着，需要查询的字段，多个字段用英文逗号隔开
- FROM
  - FROM 后边跟着数据来源的表
- WHERE
  - WHERE后跟着对数据的筛选条件
- 运算符：and / or
  - 如果筛选条件条件有多个，可以用运算符来连接
    - and:多个条件取并集
    - or:多个条件取交集
- 排序：order by [字段A] ,按照字段A升序排列，如果需要按照降序排列就在末尾加上 desc
- 幂乘计算：用于换算Value的精度，函数是Power(Number,Power)，其中number表示底数；power表示指数
- 字符串中字母换算大小写
  - lower():字符串中的字母统一换成小写
  - upper():字符串中的字母统一换成大写

### 2.聚合函数

**案例2**:表里都是明细数据，我不想看细节，我只想通过一些统计数据去了解概况

#### SQL

```sql
select 
    sum( value /power(10,18) ) as value --对符合要求的数据的value字段求和
    ,max( value /power(10,18) ) as max_value --求最大值
    ,min( value /power(10,18) )  as min_value--求最小值
    ,count( hash ) as tx_count --对符合要求的数据计数，统计有多少条
    ,count( distinct to ) as tx_to_address_count --对符合要求的数据计数，统计有多少条(按照去向地址to去重)
from ethereum.transactions --从 ethereum.transactions表中获取数据
where block_time > date('2022-01-01')  --限制Transfer时间是在2022年1月1日之后
and "from" = 0x3DdfA8eC3052539b6C9549F12cEA2C295cfF5296
and value /power(10,18) > 1000 --限制ETH Transfer量大于1000
```





![query-page](https://www.wtf.academy/assets/images/agg-db65ff3a13c089535572eb1bd8904699.png)



#### Dune Query URL

https://dune.com/queries/1525555

#### 语法说明

- 聚合函数
  - count()：计数，统计有多少个；如果需要去重计数，括号内加distinct
  - sum()：求和
  - min()：求最小值
  - max()：求最大值
  - avg()：求平均

### 3.日期时间函数·分组聚合

**案例3**:我不想只看一个单独的数字，想分小时/天/周来看一下趋势

#### 3.1 把时间戳转化成小时/天/周的格式，方便进一步做聚合统计

##### SQL

```sql
-- 把粒度到秒的时间转化为天/小时/分钟(为了方便后续按照天或者小时聚合)
select --Select后跟着需要查询的字段，多个字段用空格隔开
    block_time --transactions发生的时间
    ,date_trunc('hour',block_time) as stat_hour --转化成小时的粒度
    ,date_trunc('day',block_time) as stat_date --转化成天的粒度
    ,date_trunc('week',block_time) as stat_week--转化成week的粒度
    ,"from"
    ,"to"
    ,hash
    ,value /power(10,18) as value --通过将value除以/power(10,18)来换算精度，18是以太坊的精度
from ethereum.transactions --从 ethereum.transactions表中获取数据
where block_time > date('2021-01-01')  --限制Transfer时间是在2022年1月1日之后
and "from" = 0x3DdfA8eC3052539b6C9549F12cEA2C295cfF5296
and value /power(10,18) >1000 --限制ETH Transfer量大于1000
order by block_time --基于blocktime做升序排列，如果想降序排列需要在末尾加desc
```





![query-page](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051317091.png)



##### Dune Query URL

https://dune.com/queries/1527740

##### 语法说明

- DATE_TRUNC('datepart', timestamp)
  - 时间戳的截断函数
  - 根据datepart参数的不同会得到不同的效果
    - minute:将输入时间戳截断至分钟
    - hour:将输入时间戳截断至小时
    - day:将输入时间戳截断至天
    - week:将输入时间戳截断至某周的星期一
    - year:将输入时间戳截断至一年的第一天

#### 3.2 基于之前得到的处理后的时间字段，使用group by + sum 完成分组聚合

##### SQL

```sql
select 
    date_trunc('day',block_time) as stat_date
    ,sum( value /power(10,18) ) as value --对符合要求的数据的value字段求和
from ethereum.transactions --从 ethereum.transactions表中获取数据
where block_time > date('2022-01-01')  --限制Transfer时间是在2022年1月1日之后
and "from" = 0x3DdfA8eC3052539b6C9549F12cEA2C295cfF5296
and value /power(10,18) > 1000 --限制ETH Transfer量大于1000
group by  1 /*根据date_trunc('day', block_time) as stat_date分组*/
order by 1
```





![query-page](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051317392.png)



##### Dune Query URL

https://dune.com/queries/1525668

##### 语法说明

- 分组聚合(group by)
  分组聚合的语法是group by。分组聚合顾名思义就是先分组后聚合，需要配合聚合函数一起使用。



![query-page](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051317712.png)



假设上边表格是一个家庭(3个人)2020年前2个月的生活开销明细，如果你只用简单的sum，那你只能得到总计的12900；如果你想的到右边2种统计数据，那就需要用到分组聚合group by（按照【人员】分组聚合或者按照【月份】分组聚合）

### 4.联表查询·子查询

**案例4**:我想从转出ETH的USD金额的角度去看孙哥的转出行为

#### 4.1 转出数据看到的都是ETH的量，我想看下每次转出价值多少USD

##### SQL

```sql
select
     block_time
     ,transactions_info.stat_minute  as stat_minute
    ,"from"
    ,"to"
    ,hash
    ,eth_amount --通过将value除以/power(10,18)来换算精度，18是以太坊的精度
    ,price
    ,eth_amount * price as usd_value
from 
(
    select --Select后跟着需要查询的字段，多个字段用空格隔开
        block_time
        ,date_trunc('minute',block_time) as stat_minute --把block_time用date_trunc处理成分钟，方便作为主键去关联
        ,"from"
        ,"to"
        ,hash
        ,value /power(10,18) as eth_amount --通过将value除以/power(10,18)来换算精度，18是以太坊的精度
    from ethereum.transactions --从 ethereum.transactions表中获取数据
    where block_time > date('2022-01-01')  --限制Transfer时间是在2022年1月1日之后
    and "from" = 0x3DdfA8eC3052539b6C9549F12cEA2C295cfF5296
    and value /power(10,18) >1000 --限制ETH Transfer量大于1000
    order by block_time --基于blocktime做升序排列，如果想降序排列需要在末尾加desc
) transactions_info
left join --讲transactions_info与price_info的数据关联，关联方式为 left join
(
    --prices.usd表里存的是分钟级别的价格数据
    select
        date_trunc('minute',minute) as stat_minute --把minute用date_trunc处理成分钟，方便作为主键去关联
        ,price
    from prices.usd
    where blockchain = 'ethereum' --取以太坊上的价格数据
    and symbol = 'WETH' --取WETH的数据
) price_info on  transactions_info.stat_minute = price_info.stat_minute --left join关联的主键为stat_minute
```

> [!TIP]
>
> 这段 SQL 查询的目标是将以太坊交易数据与相应的价格数据关联，计算每笔交易的以太坊数量及其相应的美元价值。查询的逻辑可以分为几个部分来详细分析：
>
> ### 1. **内部查询：`transactions_info`**
> ```sql
> select
>     block_time,
>     date_trunc('minute', block_time) as stat_minute,
>     "from",
>     "to",
>     hash,
>     value /power(10,18) as eth_amount
> from ethereum.transactions
> where block_time > date('2022-01-01')
> and "from" = 0x3DdfA8eC3052539b6C9549F12cEA2C295cfF5296
> and value /power(10,18) > 1000
> order by block_time
> ```
> #### 解释：
> - **目标**：从以太坊交易表（`ethereum.transactions`）中获取大于 1000 ETH 的交易，并计算精确的 ETH 数量。
>   
> - **字段选择**：
>   - `block_time`: 交易发生的时间。
>   - `stat_minute`: 使用 `date_trunc('minute', block_time)` 将交易的区块时间精确到分钟，以便于后续与价格数据关联。
>   - `"from"` 和 `"to"`: 分别表示交易的发送地址和接收地址。
>   - `hash`: 交易哈希，用于唯一标识交易。
>   - `eth_amount`: 通过将 `value` 字段（交易中转移的 ETH 值）除以 10^18，得到以太坊的真实数量，18 是以太坊精度。
>
> - **条件限制**：
>   - `block_time > date('2022-01-01')`: 限制查询范围为 2022 年 1 月 1 日之后的交易。
>   - `"from" = 0x3DdfA8eC3052539b6C9549F12cEA2C295cfF5296`: 只查询特定地址的转账交易。
>   - `value / power(10,18) > 1000`: 只查询转移 ETH 数量大于 1000 的交易。
>
> - **排序**：根据 `block_time` 进行升序排列。
>
> ### 2. **价格数据查询：`price_info`**
> ```sql
> select
>     date_trunc('minute', minute) as stat_minute,
>     price
> from prices.usd
> where blockchain = 'ethereum'
> and symbol = 'WETH'
> ```
> #### 解释：
> - **目标**：从 `prices.usd` 表中获取分钟级别的 WETH（Wrapped ETH）的价格数据，按分钟聚合价格。
>
> - **字段选择**：
>   - `stat_minute`: 使用 `date_trunc('minute', minute)`，将价格记录的时间精确到分钟，这样可以与交易数据的时间戳进行关联。
>   - `price`: 代表特定时间的 WETH 价格（假设以美元计价）。
>
> - **条件限制**：
>   - `blockchain = 'ethereum'`: 只获取以太坊区块链上的价格数据。
>   - `symbol = 'WETH'`: 只获取 WETH（Wrapped ETH）的价格。
>
> ### 3. **外部查询：关联交易数据和价格数据**
> ```sql
> select
>     block_time,
>     transactions_info.stat_minute as stat_minute,
>     "from",
>     "to",
>     hash,
>     eth_amount,
>     price,
>     eth_amount * price as usd_value
> from (
>     -- 上述 transactions_info 内部查询
> ) transactions_info
> left join (
>     -- 上述 price_info 内部查询
> ) price_info on transactions_info.stat_minute = price_info.stat_minute
> ```
> #### 解释：
> - **外部查询的功能**：
>   - 将从 `transactions_info` 中查询到的以太坊交易数据与 `price_info` 中的 WETH 价格数据通过 `stat_minute`（时间精确到分钟）进行关联。
>
> - **字段选择**：
>   - `block_time`: 交易的时间。
>   - `stat_minute`: 交易发生的分钟（关联主键）。
>   - `"from"` 和 `"to"`: 交易的发送和接收地址。
>   - `hash`: 交易的哈希值。
>   - `eth_amount`: 每笔交易中转移的以太坊数量。
>   - `price`: 交易发生时相应的 WETH 价格（来自 `price_info`）。
>   - `usd_value`: 计算以太坊数量乘以价格，得到交易的美元价值。
>
> - **`left join`**：使用 `left join` 将 `transactions_info` 与 `price_info` 按 `stat_minute` 进行关联。由于使用 `left join`，即使某些交易在 `price_info` 中找不到匹配的价格数据，交易数据仍会显示出来，但 `price` 和 `usd_value` 会为空。
>
> ### 总结：
> - **查询目的**：计算某个以太坊地址在 2022 年 1 月 1 日之后的大额交易（转移 ETH 数量大于 1000）的美元价值。
> - **查询流程**：
>   1. 获取符合条件的以太坊交易信息，并将时间精确到分钟。
>   2. 获取相应时间段内的 WETH 价格数据，精确到分钟。
>   3. 将交易数据和价格数据通过分钟精度的时间戳进行关联，并计算每笔交易的美元价值。



![query-page](https://www.wtf.academy/assets/images/left_join-b85967df02be14ddbf65466172e12995.png)



##### Dune Query URL

https://dune.com/queries/1528027

##### 语法说明

- 联表查询

  - 大部分情况下我们需要的数据不是在同一张表里，比如transaction表存储的就是只有transaction数据，没有价格数据。如果我们希望能够计算出transaction对应USD 价值，那就需要用联表查询把价格数据给关联进来
  - 联表查询可以理解为把两个表通过一定的条件关联起来形成一张虚拟的表，你可以方便地对这虚拟表做更多处理。

- 联表查询有2个部分构成

  - 联表方式(join,left join ,right join ,cross join,full join)
  - 关联条件(on)

- 用得最多的联表方式是join 跟left join，以这2个为例子去解释下具体的用法

  

  ![query-page](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051317206.png)

  

  ```text
   - join:把两个表按照关联条件(on)关联在一起，取交集   
     - Table A 跟 Table B通过姓名关联，其中交集是小红和小明，因为join是取交集，因此最终结果里姓名就只有小明和小红  
     - 两表中所有符合要求的数据都需要关联，因为Table B中小明有2条记录，所以关联的结果中小明也有两条数据  
   - left join：以左表为主，把右表按照关联条件(on)往左表去关联，如果关联不到就用null填充  
     - Table A 跟 Table B通过姓名关联，因为是以左表为主，所以尽管左表中小兰和小绿在右表中没有符合关联条件的数据，但是小兰和小绿也会出现在结果中，右表那部分因为关联不到数据，因此都用null填充
   
  ```

  

#### 4.2 我想把4.1的明细数据按照天去分组聚合，但是不想写嵌套太多层的sql

##### SQL

```sql
with  transactions_info as --通过with as 建立子查询命名为transactions_info
(
    select
         block_time
         ,transactions_info.stat_minute  as stat_minute
        ,"from"
        ,"to"
        ,hash
        ,eth_amount --通过将value除以/power(10,18)来换算精度，18是以太坊的精度
        ,price
        ,eth_amount* price as usd_value
    from 
    (
        select --Select后跟着需要查询的字段，多个字段用空格隔开
            block_time
            ,date_trunc('minute',block_time) as stat_minute --把block_time用date_trunc处理成分钟，方便作为主键去关联
            ,"from"
            ,"to"
            ,hash
            ,value /power(10,18) as eth_amount --通过将value除以/power(10,18)来换算精度，18是以太坊的精度
        from ethereum.transactions --从 ethereum.transactions表中获取数据
        where block_time > date('2022-01-01')  --限制Transfer时间是在2022年1月1日之后
            and "from" = 0x3DdfA8eC3052539b6C9549F12cEA2C295cfF5296
            and value /power(10,18) >1000 --限制ETH Transfer量大于1000
        order by block_time --基于blocktime做升序排列，如果想降序排列需要在末尾加desc
    ) transactions_info
    left join --讲transactions_info与price_info的数据关联，关联方式为 left join
    (
        --prices.usd表里存的是分钟级别的价格数据
        select
            date_trunc('minute',minute) as stat_minute --把minute用date_trunc处理成分钟，方便作为主键去关联
            ,price
        from prices.usd
        where blockchain = 'ethereum' --取以太坊上的价格数据
            and symbol = 'WETH' --取WETH的数据
    ) price_info on  transactions_info.stat_minute = price_info.stat_minute --left join关联的主键为stat_minute
)

select date_trunc('day',block_time) as stat_date
    ,sum(eth_amount) as eth_amount
    ,sum(usd_value) as usd_value
from transactions_info --从子查询形成的‘虚拟表’transactions_info中取需要的数据
group by 1
order by 1
```

> [!TIP]
>
> 这段 SQL 查询的目的是计算特定以太坊地址在2022年1月1日之后的所有大额交易的每日以太坊总量及其相应的美元总价值。我们可以将其拆分为几个部分进行详细分析：
>
> ### 1. **定义子查询 `transactions_info`**
> ```sql
> with transactions_info as (
>     select
>         block_time,
>         date_trunc('minute', block_time) as stat_minute,
>         "from",
>         "to",
>         hash,
>         value / power(10, 18) as eth_amount,
>         price,
>         (value / power(10, 18)) * price as usd_value
>     from (
>         select
>             block_time,
>             date_trunc('minute', block_time) as stat_minute,
>             "from",
>             "to",
>             hash,
>             value / power(10, 18) as eth_amount
>         from ethereum.transactions
>         where block_time > date('2022-01-01')
>             and "from" = 0x3DdfA8eC3052539b6C9549F12cEA2C295cfF5296
>             and value / power(10, 18) > 1000
>         order by block_time
>     ) transactions_info
>     left join (
>         select
>             date_trunc('minute', minute) as stat_minute,
>             price
>         from prices.usd
>         where blockchain = 'ethereum'
>             and symbol = 'WETH'
>     ) price_info on transactions_info.stat_minute = price_info.stat_minute
> )
> ```
>
> #### 解释：
> - **子查询定义**：使用 `WITH` 子句定义了一个名为 `transactions_info` 的子查询，这个子查询中包含了从 `ethereum.transactions` 表中提取的交易数据和从 `prices.usd` 表中提取的价格数据。
>   
> - **字段选择**：
>   - `block_time`: 交易的时间。
>   - `stat_minute`: 将交易时间精确到分钟，以便与价格数据进行关联。
>   - `"from"` 和 `"to"`: 交易的发送和接收地址。
>   - `hash`: 交易的哈希值。
>   - `eth_amount`: 将 `value` 转换为以太坊数量。
>   - `price`: WETH 的价格（来自 `price_info`）。
>   - `usd_value`: 计算每笔交易的美元价值（`eth_amount * price`）。
>
> - **内部查询**：从 `ethereum.transactions` 表中获取大于 1000 ETH 的交易，并将交易时间精确到分钟。
>
> - **左连接**：使用 `left join` 将 `transactions_info` 与 `price_info` 进行关联，确保每笔交易都有对应的价格（即使某些时间点没有价格数据，交易数据也会显示）。
>
> ### 2. **主查询**
> ```sql
> select 
>     date_trunc('day', block_time) as stat_date,
>     sum(eth_amount) as eth_amount,
>     sum(usd_value) as usd_value
> from transactions_info
> group by 1
> order by 1
> ```
>
> #### 解释：
> - **目标**：从 `transactions_info` 子查询中提取数据，计算每一天的总 ETH 转移量和对应的美元价值。
>
> - **字段选择**：
>   - `stat_date`: 将交易时间精确到天。
>   - `sum(eth_amount)`: 计算每天转移的总 ETH 数量。
>   - `sum(usd_value)`: 计算每天的总美元价值。
>
> - **分组**：使用 `group by 1` 按 `stat_date` 进行分组，以便得到每一天的统计信息。
>
> - **排序**：使用 `order by 1` 按日期升序排列结果。
>
> ### 总结：
> 这段 SQL 查询的整体逻辑是：
> 1. 从以太坊交易表中筛选出特定地址在2022年1月1日之后的所有大额交易（ETH 转移量大于 1000）。
> 2. 获取与这些交易相应的分钟级别的 WETH 价格。
> 3. 计算每天的总 ETH 转移量及其对应的美元价值，并按日期进行排序。
>
> 这样可以帮助分析某个地址在特定时间范围内的交易活动及其经济价值。



![query-page](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051317907.png)



##### Dune Query URL

https://dune.com/queries/1528564

##### 语法说明

- 子查询(with as )
- 通过with as 可以构建一个子查询，把一段SQL的结果变成一个'虚拟表'（可类比为一个视图或者子查询），接下来的SQL中可以直接从这个'虚拟表'中取数据
- 通过with as 可以比较好地提高SQL的逻辑的可读性，也可以避免多重嵌套

# 7. SQL基础（二）

在“SQL基础（一）”部分我们介绍了一些SQL的基础知识，包括SQL查询语句的基础结构语法说明、日期时间、分组聚合、子查询和关联查询等内容。接下来我们继续介绍一些常用的SQL基础知识点。

## 常用日期函数和日期时间间隔使用

区块链的数据都按交易发生的时间先后顺序被记录保存，日常数据分析中经常需要对一段时间范围内对数据进行统计。上一部分介绍过的`date_trunc()`函数用于按指定的间隔（天、周、小时等）截断日期值。除此之外还有一些常用的函数和常见用法。

### 1. Now()和Current_Date()函数

函数`now()`用于获取当前系统的日期和时间值。需要注意，其内部保存的是包括了时分秒值的，但是Dune的查询编辑器默认只显示到“时:分”。当我们要将日期字段跟价格表`prices.usd`中的`minute`字段进行关联时，必须先按分钟进行截取。否则可能关联不到正确的价格记录。

函数`current_date()`用于获取==当前日期（不含时分秒部分）==。当我们需要按日期、时间筛选数据时，常常需要结合使用它们其中之一，再结合相关日期时间函数来换算出需要的准确日期或者时间。函数`current_date()`相当于`date_trunc('day', now())`，即对`now()`函数的值按“天”进行截取。还可以省略`current_date()`的括号，直接写成`current_date`形式。

```sql
select now() -- 当前系统日期和时间
    ,current_date() -- 当前系统日期
    ,current_date   -- 可以省略括号
    ,date_trunc('day', now()) -- 与current_date相同
```



### 2. DateAdd()、Date_Add()、Date_Sub()和DateDiff()函数

函数`dateadd(unit, value, expr)`在一个日期表达式上添加一个的日期时间单位。这里的“日期时间单位”使用常量表示，常用的有HOUR、DAY、WEEK、MONTH等。其中的value值可以为负数，表示从后面的表达式减去对应的日期时间单位。也正是因为可以用负数表示减去一个日期时间间隔，所以不需要也确实没有`datesub()`函数。

函数`date_add(startDate, numDays)`在一个日期表达式上加上或者减去指定的天数，返回另外一个日期。参数`numDays`为正数表示返回`startDate`之后指定天数的日期，为负表示返回之前指定天数的日期。函数`date_sub(startDate, numDays)`作用类似，但表示的意思正好相反，即负数表示返回之后的日期，正数表示之前的日期。

函数`datediff(endDate, startDate)`返回两个日期表达式之间间隔的天数。如果`endDate`在`startDate`之后，返回正值，在之前则返回负值。

SQL示例如下：

```sql
select date_add('MONTH', 2, current_date) -- 当前日期加2个月后的日期
    ,date_add('HOUR', 12, now()) -- 当前日期时间加12小时
    ,date_add('DAY', -2, current_date) -- 当前日期减去2天
    ,date_add('DAY', 2, current_date) -- 当前日期加上2天
    ,date_add('DAY', -5, current_date) -- 当前日期加上-5天，相当于减去5天
    ,date_diff('DAY', date('2022-11-22'), date('2022-11-25')) -- 结束日期早于开始日期，返回负值
    ,date_diff('DAY', date('2022-11-25'), date('2022-11-22')) -- 结束日期晚于开始日期，返回正值
```



### 3. INTERVAL 类型

Interval是一种数据类型，以指定的日期时间单位表示某个时间间隔。以Interval 表示的时间间隔使用起来非常便利，避免被前面的几个名称相似、作用也类似的日期函数困扰。

```sql
select now() - interval '2' hour -- 2个小时之前
    ,current_date - interval '7' day -- 7天之前
    ,now() + interval '1' month -- 一个月之后的当前时刻
```



更多日期时间相关函数的说明，请参考[日期、时间函数和运算符](https://trino.io/docs/current/functions/datetime.html)

## 条件表达式Case、If

当我们需要应用条件逻辑的时候，可以应用`case`语句。CASE语句的常用语法格式为`CASE {WHEN cond1 THEN res1} [...] [ELSE def] END`，它可以用多个不同的条件评估一个表达式，并返回第一个评估结果为真值（True）的条件后面的值，如果全部条件都不满足，则返回`else`后面的值。其中的`else`部分还可以省略，此时返回NULL。

我们在“Lens实践案例：创作者个人资料域名分析”部分就多次用到了CASE语句。其中部分代码摘录如下：

```sql
-- ...省略部分代码...

profiles_summary as (
    select (
            case
                when length(short_name) >= 20 then 20 -- 域名长度大于20时，视为20对待
                else length(short_name) -- 域名长度小于20，直接使用其长度值
            end) as name_length, -- 将case语句评估返回的结果命名为一个新的字段
        handle_type,
        count(*) as name_count
    from profile_created
    group by 1, 2
),

profiles_total as (
    select count(*) as total_profile_count,
        sum(case
                when handle_type = 'Pure Digits' then 1 -- 类型值等于给定值，返回1
                else 0  -- 类型值不等于给定值，返回 0
            end
        ) as pure_digit_profile_count,
        sum(case 
                when handle_type = 'Pure Letters' then 1  -- 类型值等于给定值，返回1
                else 0  -- 类型值不等于给定值，返回 0
            end
        ) as pure_letter_profile_count
    from profile_created
)

-- ...省略部分代码...
```



可以看到，通过CASE语句，我们可以根据实际的需要对数据进行灵活的转换，方便后续的统计汇总。

上述示例查询的相关链接：

- 查询：https://dune.com/queries/1535541
- 说明：[Lens创作者个人资料域名分析](https://sixdegreelab.gitbook.io/mastering-chain-analytics/ru-men-jiao-cheng/06_pratical_case_lens_protocol)

函数`if(cond, expr1, expr2)` 的作用时根据条件值评估的真假，返回两个表达式中的其中一个值。如果条件评估结果为真值，则返回第一个表达式，如果评估为假值，则返回第二个表达式。

```sql
select if(1 < 2, 'a', 'b') -- 条件评估结果为真，返回第一个表达式
    ,if('a' = 'A', 'case-insensitive', 'case-sensitive') -- 字符串值区分大小写
```



## 字符串处理的常用函数

- Substring() 函数

当有时我们因为某些特殊的原因不得不使用原始数据表`transactions`或`logs`并解析其中的`data`数据时，需要先从其中提取部分字符串，然后进行针对性的转换处理，此时就需要使用Substring函数。Substring函数的语法格式为`substring(expr, pos [, len])`或者`substring(expr FROM pos [FOR len] ] )`，表示在表达式`expr`中，从位置`pos`开始，截取`len`个字符并返回。如果省略参数`len`，则一直截取到字符串末尾。

- Concat() 函数和 || 操作符

函数`concat(expr1, expr2 [, ...] )`将多个表达式串接到一起，常用来链接字符串。操作符`||`的功能和Concat函数相同。

```sql
select concat('a', ' ', 'b', ' c') -- 连接多个字符串
    , 'a' || ' ' || 'b' || ' c' -- 与concat()功能相同
```



- Right() 函数 

函数`right(str, len)`从字符串`str`中返回右边开始计数的`len`个字符。如前所述，在`logs`这样的原始数据表里数据是按64个字符一组连接到一起后放入`data`里面的，对于合约地址或用户地址，其长度是40个字符，在保存时就会在左边填充`0`来补足64位长度。解析提取地址的时候，我们就需要提取右边的40个字符，再加上`0x`前缀将其还原为正确的地址格式。

注意，在Dune SQL中，直接使用`right()`函数可能返回语法错误，可以将函数名放到双引号中来解决，即使用`"right"()`。由于这种方式显得比较繁琐，我们可以使用substring函数的负数开始位置参数来表示从字符串右边开始计数确定截取的开始位置。

下面是一个使用上述函数的一个综合例子，这个例子从`logs`表解析跨链到Arbitrum的记录，综合使用了几个方式：

```sql
select date_trunc('day', block_time) as block_date, --截取日期
    concat('0x', "right"(substring(cast(data as varchar), 3 + 64 * 2, 64), 40)) as address, -- 提取data中的第3部分转换为用户地址，从第3个字符开始，每64位为一组
    concat('0x', "right"(substring(cast(data as varchar), 3 + 64 * 3, 64), 40)) as token, -- 提取data中的第4部分转换为用户地址
    concat('0x', substring(substring(cast(data as varchar), 3 + 64 * 3, 64), -40, 40)) as same_token, -- 提取data中的第4部分转换为用户地址
    substring(cast(data as varchar), 3 + 64 * 4, 64) as hex_amount, -- 提取data中的第5部分
    bytearray_to_uint256(bytearray_substring(data, 1 + 32 * 4, 32)) as amount, -- 提取data中的第5部分，转换为10进制数值
    tx_hash
from ethereum.logs
where contract_address = 0x5427fefa711eff984124bfbb1ab6fbf5e3da1820   -- Celer Network: cBridge V2 
    and topic0 = 0x89d8051e597ab4178a863a5190407b98abfeff406aa8db90c59af76612e58f01  -- Send
    and substring(cast(data as varchar), 3 + 64 * 5, 64) = '000000000000000000000000000000000000000000000000000000000000a4b1'   -- 42161，直接判断16进制值
    and substring(cast(data as varchar), 3 + 64 * 3, 64) = '000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2' -- WETH，直接判断16进制值
    and block_time >= now() - interval '30' day
limit 10
```

> [!TIP]
>
> 好的，下面将 SQL 查询分成几个段落进行详细分析：
>
> ### 1. 选择字段（SELECT）
> ```sql
> select date_trunc('day', block_time) as block_date,
>     concat('0x', "right"(substring(cast(data as varchar), 3 + 64 * 2, 64), 40)) as address,
>     concat('0x', "right"(substring(cast(data as varchar), 3 + 64 * 3, 64), 40)) as token,
>     concat('0x', substring(substring(cast(data as varchar), 3 + 64 * 3, 64), -40, 40)) as same_token,
>     substring(cast(data as varchar), 3 + 64 * 4, 64) as hex_amount,
>     bytearray_to_uint256(bytearray_substring(data, 1 + 32 * 4, 32)) as amount,
>     tx_hash
> ```
> - **`date_trunc('day', block_time) as block_date`**:
>   - 使用 `date_trunc` 函数将 `block_time` 的时间精确到天，以便后续进行日期聚合。
>   
> - **`concat('0x', "right"(substring(cast(data as varchar), 3 + 64 * 2, 64), 40)) as address`**:
>   - 从 `data` 字段提取用户地址。它通过 `substring` 函数获取 `data` 的第三部分（第 3 个 64 字节段），并使用 `right` 函数取右侧的 40 个字符，最后将其格式化为以 `0x` 开头的字符串。
>
> - **`concat('0x', "right"(substring(cast(data as varchar), 3 + 64 * 3, 64), 40)) as token`**:
>   - 类似于上一个字段，但提取的是代币地址（`data` 的第四部分）。
>
> - **`concat('0x', substring(substring(cast(data as varchar), 3 + 64 * 3, 64), -40, 40)) as same_token`**:
>   - 也提取代币地址，但使用了不同的方式，直接从第四部分中提取最后 40 个字符。
>
> - **`substring(cast(data as varchar), 3 + 64 * 4, 64) as hex_amount`**:
>   - 提取 `data` 的第五部分，以十六进制字符串形式表示的金额。
>
> - **`bytearray_to_uint256(bytearray_substring(data, 1 + 32 * 4, 32)) as amount`**:
>   - 将 `data` 中的某部分（实际上是 `data` 的第六部分）转换为无符号 256 位整数，以便于数值计算。
>
> - **`tx_hash`**:
>   - 直接选择交易哈希（`tx_hash`）以便于跟踪特定交易。
>
> ---
>
> ### 2. 数据来源（FROM）
> ```sql
> from ethereum.logs
> ```
> - 从 `ethereum.logs` 表中提取数据。这张表存储了以太坊合约事件的日志数据，允许用户检索与特定合约相关的事件。
>
> ---
>
> ### 3. 条件筛选（WHERE）
> ```sql
> where contract_address = 0x5427fefa711eff984124bfbb1ab6fbf5e3da1820
>     and topic0 = 0x89d8051e597ab4178a863a5190407b98abfeff406aa8db90c59af76612e58f01
>     and substring(cast(data as varchar), 3 + 64 * 5, 64) = '000000000000000000000000000000000000000000000000000000000000a4b1'
>     and substring(cast(data as varchar), 3 + 64 * 3, 64) = '000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2'
>     and block_time >= now() - interval '30' day
> ```
> - **`contract_address = 0x5427fefa711eff984124bfbb1ab6fbf5e3da1820`**:
>   - 只选择与 Celer Network 的 cBridge V2 合约相关的日志。
>
> - **`topic0 = 0x89d8051e597ab4178a863a5190407b98abfeff406aa8db90c59af76612e58f01`**:
>   - 筛选出特定类型的事件（在这里是 Send 事件），通过检查 `topic0` 来实现。
>
> - **`substring(cast(data as varchar), 3 + 64 * 5, 64) = '000000000000000000000000000000000000000000000000000000000000a4b1'`**:
>   - 仅选择 `data` 字段的第六部分（金额）为 42161 的日志。
>
> - **`substring(cast(data as varchar), 3 + 64 * 3, 64) = '000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2'`**:
>   - 仅选择代币地址为 WETH 的日志。
>
> - **`block_time >= now() - interval '30' day`**:
>   - 限制结果为过去 30 天内的日志记录，确保数据的时效性。
>
> ---
>
> ### 4. 结果限制（LIMIT）
> ```sql
> limit 10
> ```
> - 最后，限制结果集的返回数量为 10 条，以避免过多数据的输出并保持查询的高效性。
>
> ---
>
> ### 总结
> 这个查询从以太坊的日志中提取了与特定合约相关的交易数据，筛选出发送特定数量的 WETH 的交易。查询中使用了多种字符串和数据处理函数，以格式化和计算出所需的用户地址、代币地址、金额等信息。通过条件筛选确保了数据的准确性和相关性。

上述示例查询的相关链接：

- https://dune.com/queries/1647016
- [字符串函数和运算符](https://trino.io/docs/current/functions/string.html)

## 窗口函数

多行数据的组合成为窗口（Window）。对窗口中的一组行进行操作并根据该组行计算每一行的返回值的函数叫窗口函数。窗口函数对于处理任务很有用，例如计算移动平均值、计算累积统计量或在给定当前行的相对位置的情况下访问行的值。窗口函数的常用语法格式：

```sql
function OVER window_spec
```



其中，`function`可以是排名窗口函数、分析窗口函数或者聚合函数。`over`是固定必须使用的关键字。`window_spec`部分又有两种可能的变化：`partition by partition_feild order by order_field`或者`order by order_field`，分别表示先分区再排序和不分区直接排序。除了把所有行当作同一个分组的情况外，分组函数必须配合 `order by`来使用。

1. LEAD()、 LAG() 函数

Lead()函数从分区内的后续行返回指定表达式的值。其语法为`lead(expr [, offset [, default] ] )`。Lag()函数从从分区中的前序行返回指定表达式的值。当我们需要将结果集中某一列的值，跟上一行或者下一行的相同列的值进行比较（当然也可以间隔多行取值）时，这两个函数就非常有用。

我们之前的教程中介绍过一个查询，用于统计Uniswap V3 近30天每日新增资金池数量。其SQL为：

```sql
with pool_details as (
    select date_trunc('day', evt_block_time) as block_date, evt_tx_hash, pool
    from uniswap_v3_ethereum.Factory_evt_PoolCreated
    where evt_block_time >= now() - interval '29' day
)

select block_date, count(pool) as pool_count
from pool_details
group by 1
order by 1
```



如果我们在目前的条形图基础上还希望添加一条曲线来显示每天新建资金池数量的变化情况，就可以使用Lag()函数来计算出每天相较于前一天的变化值，然后将其可视化。为了保持逻辑清晰，我们增加了一个CTE，修改后的SQL如下：

```sql
with pool_details as (
    select date_trunc('day', evt_block_time) as block_date, evt_tx_hash, pool
    from uniswap_v3_ethereum.Factory_evt_PoolCreated
    where evt_block_time >= now() - interval '29' day
),

pool_summary as (
    select block_date,
        count(pool) as pool_count
    from pool_details
    group by 1
    order by 1
)

select block_date,
    pool_count,
    lag(pool_count, 1) over (order by block_date) as pool_count_previous, -- 使用Lag()函数获取前一天的值
    pool_count - (lag(pool_count, 1) over (order by block_date)) as pool_count_diff -- 相减得到变化值
from pool_summary
order by block_date
```

> [!TIP]
>
> 这段 SQL 代码的目的是从 `pool_summary` 表中提取每天创建的池数量，并计算与前一天的变化。以下是对每一部分的详细解释：
>
> ### 1. 选择字段
>
> ```sql
> select block_date,
>     pool_count,
> ```
>
> - **`block_date`**：表示日期，这里是通过之前的公共表表达式 `pool_summary` 中的汇总数据得到的，表示每一天的日期。
> - **`pool_count`**：表示在 `block_date` 这一天创建的池的数量，是通过计数得出的。
>
> ### 2. 使用 `LAG()` 函数
>
> ```sql
> lag(pool_count, 1) over (order by block_date) as pool_count_previous,
> ```
>
> - **`LAG()` 函数**：这个窗口函数用于获取前一行的值。在这里，`pool_count` 是我们想要获取的前一行的列名。
>   - **`pool_count`**：当前行的池数量。
>   - **`1`**：这是 `LAG()` 函数的第二个参数，表示我们想要获取前一行的值（即前一天的池数量）。
>   - **`over (order by block_date)`**：指定窗口函数的排序依据。在这里，我们按照 `block_date` 进行排序，以确保获取的是时间上前一天的值。
> - **`as pool_count_previous`**：将获取的前一天的池数量命名为 `pool_count_previous`。
>
> ### 3. 计算变化值
>
> ```sql
> pool_count - (lag(pool_count, 1) over (order by block_date)) as pool_count_diff
> ```
>
> - **计算表达式**：这里通过 `pool_count` 减去前一天的池数量（使用 `LAG()` 函数获取）来计算变化量。
>   - **`pool_count`**：当前行的池数量。
>   - **`lag(pool_count, 1) over (order by block_date)`**：获取前一行的池数量。
> - **`as pool_count_diff`**：将这个计算结果命名为 `pool_count_diff`，表示今天和昨天之间的池数量差异。
>
> ### 4. 从 `pool_summary` 提取数据
>
> ```sql
> from pool_summary
> ```
>
> - **`pool_summary`**：这部分的结果来自前面创建的公共表表达式 `pool_summary`，其中包含了 `block_date` 和 `pool_count` 的汇总数据。
>
> ### 5. 最终排序
>
> ```sql
> order by block_date
> ```
>
> - **`order by block_date`**：最终结果集根据 `block_date` 进行升序排序，确保输出的日期是从最早到最新排列的，便于观察每天的变化趋势。
>
> ### 总结
>
> 整体来看，这段 SQL 代码的作用是：
> 1. 从 `pool_summary` 表中选择每天创建的池数量。
> 2. 使用 `LAG()` 函数获取前一天的池数量。
> 3. 计算当前池数量与前一天池数量的变化值。
> 4. 最终按日期排序输出结果。
>
> 这样的分析可以帮助用户直观地了解在指定时间范围内池数量的变化趋势，有助于评估 Uniswap V3 的流动性动态。

> [!IMPORTANT]
>
> 在 SQL 中，`LAG()` 函数用于获取当前行的前一行的值，而 `OVER` 子句则定义了这个窗口函数的行为。具体到这段代码中的 `order by block_date` 的使用，以下是详细解释：
>
> ### 理由分析
>
> 1. **定义行的顺序**：
>    - `LAG(pool_count, 1) OVER (ORDER BY block_date)` 的作用是告诉 SQL 数据库在计算 `LAG()` 函数时，应该按照 `block_date` 的顺序来读取数据。
>    - 这意味着数据库将以 `block_date` 为排序标准，逐行扫描数据。这使得对于每一行数据，`LAG()` 函数可以准确找到它的“前一行”。
>
> 2. **确保正确的时间关系**：
>    - 在这个查询中，`pool_count` 表示每天创建的池数量。为了获得前一天的池数量，必须确保数据按日期顺序排列。
>    - 如果不按 `block_date` 排序，`LAG()` 函数可能会返回与当前行不相关的值，导致结果不准确。
>
> 3. **数据的时间序列特性**：
>    - 在分析时间序列数据时，通常需要比较相邻时间点的值（例如今天和昨天、上个月和这个月等）。在这个场景中，使用 `ORDER BY block_date` 能确保时间关系的正确性。
>
> ### 示例说明
>
> 假设有以下数据：
>
> | block_date | pool_count |
> | ---------- | ---------- |
> | 2024-10-01 | 5          |
> | 2024-10-02 | 8          |
> | 2024-10-03 | 10         |
>
> - 对于 `2024-10-03` 这一行：
>   - `LAG(pool_count, 1) OVER (ORDER BY block_date)` 将查找 `2024-10-02` 这一行的 `pool_count`（即 8）。
>   - 因此，`pool_count_previous` 将为 8，`pool_count_diff` 将计算为 10 - 8 = 2。
>
> 如果没有使用 `ORDER BY block_date`，则 `LAG()` 可能返回随机的 `pool_count` 值，而不是我们期待的前一天的值，这样会导致结果无法反映真实的变化趋势。
>
> ### 结论
>
> 综上所述，`ORDER BY block_date` 在 `LAG()` 函数中是必不可少的，它确保了数据按日期顺序处理，从而使得对时间序列数据的比较和分析能够准确无误。

将`pool_count_diff`添加到可视化图表（使用右侧坐标轴，图形类型选择Line），效果如下图：



![part_2_01.png](https://www.wtf.academy/assets/images/part_2_01-73e9005fda1fcbc46bfcaeff40365eb0.png)



当我们需要向“前”对比不同行的数据时，就可以使用Lead()函数。比如，我们之前在Lens实例中介绍过发布帖子最多的创作者账号查询，我们将其做一些调整，返回发帖最多的50个账号，同时对比这些账号发帖数量的差异（第一名和第二名之差、第二名和第三名之差，等等）。关键部分查询代码如下：

```sql
with post_data as (
    -- 获取原始发帖详细数据，请参考完整SQL链接
),

top_post_profiles as (
    select profile_id,
        count(*) as post_count
    from post_data
    group by 1
    order by 2 desc
    limit 50
)

select row_number() over (order by post_count desc) as rank_id, -- 生成连续行号，用来表示排名
    profile_id,
    post_count,
    lead(post_count, 1) over (order by post_count desc) as post_count_next, -- 获取下一行的发帖数据
    post_count - (lead(post_count, 1) over (order by post_count desc)) as post_count_diff -- 计算当前行和下一行的发帖数量差
from top_post_profiles
order by post_count desc
```



查询结果如下图所示，其中可以看到有些账号之间的发帖数量差异很小：



![part_2_02.png](https://www.wtf.academy/assets/images/part_2_02-94376dd2a0682d8332c03ba05b9cf038.png)



完整的SQL参考链接：

- https://dune.com/queries/1647422

1. Row_Number() 函数

Row_Number() 是一个排名类型的窗口函数，用于按照指定的排序方式生成不同的行号，从1开始连续编号。在上一个例子中，我们已经使用了`row_number() over (order by post_count desc) as rank_id`来生成行号用来表示排名，这里不再举例。如果结合`partition by`分区字句，Row_Number()将在每一个分区内部从1开始编号。利用这个特性，我们可以用来实现一些高级筛选。例如，我们有一组Token地址，需要计算并返回他们最近1小时内的平均价格。考虑到Dune的数据会存在一到几分钟的延迟，如果按当前系统日期的“小时”数值筛选，并不一定总是能返回需要的价格数据。相对更安全的方法是扩大取值的时间范围，然后从中筛选出每个Token最近的那条记录。这样即使出现数据有几个小时的延迟的特殊情况，我们的查询仍然可以工作良好。此时我们可以使用Row_Number()函数结合`partition by`来按分区生成行号再根据行号筛选出需要的数据。

```sql
with latest_token_price as (
    select date_trunc('hour', minute) as price_date, -- 按小时分组计算
        contract_address,
        symbol,
        decimals,
        avg(price) as price -- 计算平均价格
    from prices.usd
    where contract_address in (
        0xdac17f958d2ee523a2206206994597c13d831ec7,
        0x2260fac5e5542a773aa44fbcfedf7c193bc2c599,
        0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2,
        0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48,
        0x7fc66500c84a76ad7e9c93437bfc5ac33e2ddae9
    )
    and minute > now() - interval '1' day -- 取最后一天内的数据，确保即使数据有延迟也工作良好
    group by 1, 2, 3, 4
),

latest_token_price_row_num as (
    select  price_date,
        contract_address,
        symbol,
        decimals,
        price,
        row_number() over (partition by contract_address order by price_date desc) as row_num -- 按分区单独生成行号
    from latest_token_price
)

select contract_address,
    symbol,
    decimals,
    price
from latest_token_price_row_num
where row_num = 1 -- 按行号筛选出每个token最新的平均价格
```



以上查询结果如下图所示：



![part_2_03.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051318292.png)



完整的SQL参考链接：

- https://dune.com/queries/1647482

窗口函数的更多完整资料：

- [分析窗函数](https://trino.io/docs/current/functions/window.html)

## array_agg()函数

如果你想将查询结果集中每一行数据的某一列合并到一起，可以使用 array_agg()函数。如果希望将多列数据都合并到一起（想象将查询结果导出为CSV的情形），你可以考虑用前面介绍的字符串连接的方式将多列数据合并为一列，然后再应用 array_agg()函数。这里举一个简单的例子：

```sql
select array_agg(contract_address) from
(
    select contract_address 
    from ethereum.logs
    where block_time >= current_date
    limit 10
) t
```



## 总结

每一种数据库都有几十个甚至上百个内置的函数，而我们这里介绍的只是其中一小部分常用的函数。如果你想要成为熟练的数据分析师，我们强烈建议阅读并了解这里的每一个内置函数的用法： [Trino 函数](https://trino.io/docs/current/functions.html)。

# 8. 实践案例：制作Lens Protocol的数据看板（一）

为了让大家尽快上手开始数据分析，我们会将一些偏理论的内容放到教程的后续部分，前半部分则更多讲解一些可以结合起来实践的内容。本篇教程我们一起来为Lens Protocol项目制作一个数据看板。

## Lens协议是什么？

来自[Lens官网](https://docs.lens.xyz/docs/what-is-lens)的介绍整理如下： Lens协议（Lens Protocol，简称 Lens）是Polygon区块链上的 Web3 社交图谱生态系统。它旨在让创作者拥有自己与社区之间的联系，形成一个完全可组合的、用户拥有的社交图谱。该协议从一开始就考虑到了模块化，允许添加新功能和修复问题，同时确保用户拥有的内容和社交关系不可变。Lens旨在解决现有社交媒体网络中的一些主要问题。Web2 网络都从其专有的集中式数据库中读取数据。用户的个人资料、朋友关系和内容被锁定在特定网络中，其所有权归网络运营商拥有。各网络之间互相竞争，争夺用户注意力，变成一种零和游戏。Lens通过成为用户拥有的、任何应用程序都可以接入的开放社交图谱来纠正这一点。由于用户拥有自己的数据，他们可以将其带到任何基于Lens协议构建的应用程序中。作为其内容的真正所有者，创作者不再需要担心基于单个平台的算法和政策的突然变化而失去他们的内容、观众和收入来源。此外，使用Lens协议的每个应用程序都有益于整个生态系统，从而将零和游戏变成了协作游戏。

Lens协议里面主要涉及以下角色（实体）：个人资料（Profile）、出版物（Publication）、评论（Comment）、镜像（Mirror）、收藏（Collect)）、关注（Follow）。同时，协议里面存在3种类型的NFT，即：个人资料NFT（Profile NFT）、关注NFT（Follow NFT）、收藏NFT（Collect NFT）。

Lens上的典型使用场景包括：

- 创作者注册创建他们的Profile，铸造其专属的ProfileNFT。可以设置个性化名称（Profile Handle Name，可简单类比为域名，即“Lens域名”）。同时，可以设置账号头像图片URL、被关注时的规则（通过设置特殊的规则，可以产生收益，比如可以设置用户需要支付一定的费用才能关注Profile）。目前仅许可名单内的地址可以创建个人资料账号。
- 创作者发布内容出版物（Publication），包括文章（帖子，Post）、镜像（Mirror）、评论（Comment）等。
- 普通用户可以关注创作者，收藏感兴趣的出版物。
- 在相关操作步骤中，3种不同类型NFT被分别铸造并传输给不同的用户地址。

## Lens 协议主要分析内容

针对Lens这样的项目，我们可以从整体上分析其概况，也可以从不同角度、针对其中的不同角色类型进行数据分析。以下是一些可以分析的内容的概况：

- 总用户数量、总的创作者数量、创作者占比等
- 总出版物数量、总评论数量、总镜像数量、总关注数量、总收藏数量等
- 用户相关的分析：每日新增用户数量、每日新增创作者数量、每日活跃用户数量、活跃创作者数量、用户整体活跃度的变化趋势等
- Lens账号个性化域名的相关分析：域名注册数量、不同类型域名的注册情况（纯数字、纯字母、不同长度）等
- 创作者的活跃度分析：发布出版物的数量、被关注的次数、被镜像的次数、最热门创作者等
- 出版物的相关分析：内容发布数量、增长趋势、被关注次数、被收藏次数、最热门出版物等
- 关注的相关分析：关注的数量及其变化趋势、关注者的成本分析、关注创作者最多的用户等
- 收藏的相关分析：每日收藏数量、热门收藏等
- 创作者的收益分析：通过关注产生的收益、其他收益等
- 从NFT的角度进行相关分析：每日铸造数量、涉及的成本（关注费用）等

可以分析的内容非常丰富。在这个看板中，我们仅使用部分内容做案例。其他内容请大家分别去尝试分析。

## 数据表介绍

在Lens的官方文档[已部署的智能合约](https://docs.lens.xyz/docs/deployed-contract-addresses)页面，提示使用LensHub代理（LensHub Proxy）这个智能合约作为交互的主要合约。除了少部分和NFT相关的查询需要用到智能合约FollowNFT下的数据表外，我们基本上主要关注LensHub这个智能合约下面的已解析表就可以了。下图列出了这个智能合约下部分数据表。



![image_01.png](https://www.wtf.academy/assets/images/image_01-65915317456971ccd64302e0499cbb0a.png)



之前的教程提过，已解析的智能合约数据表有两大类型：事件日志表(Event Log)和函数调用表（Function Call）。两种类型的表分别以：`projectname_blockchain.contractName_evt_eventName`和：`projectname_blockchain.contractName_call_functionName`格式命名。浏览LensHub合约下的表格列表，我们可以看到下面这些主要的数据表：

- 收藏表（collect/collectWithSig）
- 评论表（comment/commentWithSig）
- 个人资料表（createProfile）
- 关注表（follow/followWithSig）
- 镜像表（mirror/mirrorWithSig）
- 帖子表（post/postWithSig）
- Token传输表（Transfer）

除了Token传输表是事件表之外，上述其他表格都是函数调用表。其中后缀带有`WithSig`的数据表，表示通过签名（Signature）授权来执行的操作。通过签名授权，可以方便地通过API或者允许其他授权方代表某个用户执行某项操作。当我们分析帖子表等类型时，需要将相关表里的数据集合到一起进行分析。

大家可以在列表中看到还有其他很多不同方法的数据表，由于这些表全部都是在LensHub智能合约下生成的，所以他们交互的contract_address全部都是LensHub这个地址，即`0xdb46d1dc155634fbc732f92e853b10b288ad5a1d`。当我们要分析Lens的总体用户数据时，应该使用polygon.transactions 原始表，查询其中与这个合约地址交互的数据，这样才能得到完整的数据。

## Lens协议概览分析

通过查看[LensHub智能合约创建交易详情](https://polygonscan.com/tx/0xca69b18b7e2daf4695c6d614e263d6aa9bdee44bee91bee7e0e6e5e5e4262fca)，我们可以看到该智能合约部署于2022年5月16日。当我们查询`polygon.transactions`原始表这样的原始数据表时，通过设置日期时间过滤条件，可以极大地提高查询执行性能。

### 总交易数量和总用户数量

如前所述，最准确的查询用户数量的数据源是`polygon.transactions`原始表，我们可以使用如下的query来查询Lens当前的交易数量和总用户数量。我们直接查询发送给LensHub智能合约的全部交易记录，通过`distinct`关键字来统计独立用户地址数量。由于我们已知该智能合约的创建日期，所以用这个日期作为过滤条件来优化查询性能。

```sql
select count(*) as transaction_count,
    count(distinct "from") as user_count    -- count unique users
from polygon.transactions
where "to" = 0xdb46d1dc155634fbc732f92e853b10b288ad5a1d   -- LensHub
    and block_time >= date('2022-05-16')  -- contract creation date
```



创建一个新的查询，使用上面的SQL代码，运行查询得到结果后，保存Query。然后为其添加两个`Counter`类型到可视化图表，标题分别设置为“Lens Total Transactions”和“Lens Total Users”。

本查询在Dune上的参考链接：https://dune.com/queries/1533678

现在我们可以将可视化图表添加到数据看板。由于这是我们的第一个查询，我们可以在添加可视化图表到数据看板的弹出对话框中创建新的数据看板。切换到第一个Counter，点击“Add to dashboard”按钮，在对话框中，点击底部的“New dashboard”按钮，输入数据看板的名称后，点击“Save dashboard”按钮创建空白的数据看板。我这里使用“Lens Protocol Ecosystem Analysis”作为看板的名称。保存之后我们就可以在列表中看到刚创建的数据看板，点击其右边的“Add”按钮，就可以将当前Counter添加到数据看板中。关闭对话框后切换到另一个Counter，也将其添加到新创建的数据看板。

此时，我们可以点击Dune网站头部的“My Creations”链接，再选择“Dashboards” Tab来切换到数据看板列表。点击我们新创建的看板名称，进入看板的预览界面。我们可以看到刚才添加的两个Counter类型可视化图表。在这里，通过点击“Edit”按钮进入编辑模式，你可以对图表的大小、位置做相应的调整，可以通过点击“”按钮来添加文本组件，对数据看板做一些说明或者美化。下图是调整后的数据看板的界面示例。



![image_02.png](https://www.wtf.academy/assets/images/image_02-495c4d2c6ba3d1fb8a63917ebf87abda.png)



我们新创建的数据看板的链接是：[Lens Protocol Ecosystem Analysis](https://dune.com/sixdegree/lens-protocol-ecosystem-analysis)

### 按天统计的交易数量和独立用户数量

要想分析Lens协议在活跃度方面的增长变化趋势，我们可以创建一个查询，按日期来统计每天的交易数量和活跃用户地址数量。通过在查询中添加`block_time`字段并使用`date_trunc()`函数将其转换为日期（不含时分秒数值部分），结合`group by`查询子句，我们就可以统计出每天的数据。查询代码如下所示：

```sql
select date_trunc('day', block_time) as block_date,
    count(*) as transaction_count,
    count(distinct "from") as user_count
from polygon.transactions
where "to" = 0xdb46d1dc155634fbc732f92e853b10b288ad5a1d   -- LensHub
    and block_time >= date('2022-05-16')  -- contract creation date
group by 1
order by 1
```



保存查询并为其添加两个`Bar Chart`类型的可视化图表，`Y column 1`对应的字段分别选择`transaction_count`和`user_count`，可视化图表的标题分别设置为“Lens Daily Transactions”和“Lens Daily Users”。将它们分别添加到数据看板中。效果如下图所示：



![image_03.png](https://www.wtf.academy/assets/images/image_03-f78380398ad48b1e35f865532cb8ba40.png)



通常在按日期统计查询到时候，我们可以按日期将相关数据汇总到一起，计算其累计值并将其与每日数据添加到同一张可视化图表中，以便对整体的数据增长趋势有更直观的认识。通过使用`sum() over ()`窗口函数，可以很方便地实现这个需求。为了保持逻辑简单易懂，我们总是倾向于使用CTE来将复杂的查询逻辑分解为多步。将上面的查询修改为：

```sql
with daily_count as (
    select date_trunc('day', block_time) as block_date,
        count(*) as transaction_count,
        count(distinct "from") as user_count
    from polygon.transactions
    where "to" = 0xdb46d1dc155634fbc732f92e853b10b288ad5a1d   -- LensHub
        and block_time >= date('2022-05-16')  -- contract creation date
    group by 1
    order by 1
)

select block_date,
    transaction_count,
    user_count,
    sum(transaction_count) over (order by block_date) as accumulate_transaction_count,
    sum(user_count) over (order by block_date) as accumulate_user_count
from daily_count
order by block_date
```



查询执行完毕后，我们可以调整之前添加的两个可视化图表。分别在`Y column 2`下选择`accumulate_transaction_count`和`accumulate_user_count`将它们作为第二个指标值添加到图表中。由于累计值跟每天的数值往往不在同一个数量级，默认的图表显示效果并不理想。我们可以通过选择“Enable right y-axis”选项，然后把新添加的第二列设置为使用右坐标轴，同时修改其“Chart Type”为“Area”（或者“Line”，“Scatter”），这样调整后，图表的显示效果就比较理想了。

为了将每日交易数量与每日活跃用户数量做对比，我们可以再添加一个可视化图表，标题设置为“Lens Daily Transactions VS Users”，在Y轴方向分别选择transaction_count和user_count列。同样，因为两项数值不在同一个数量级，我们启用右侧坐标轴，将user_count设置为使用右坐标轴，图表类型选择“Line”。也将这个图表添加到数据看板。通过查看这个图表，我们可以看到，在2022年11月初的几天里，Lens的每日交易量出现了一个新的高峰，但是每日活跃用户数量的增长则没有那么明显。

这里需要额外说明的是，因为同一个用户可能中不同的日期都有使用Lens，当我们汇总多天的数据到一起时，累计得到的用户数量并不代表实际的独立用户总数，而是会大于实际用户总数。如果需要统计每日新增的独立用户数量及其总数，我们可以先取得每个用户最早的交易记录，然后再用相同的方法按天汇总统计。具体这里不再展开说明，请大家自行尝试。另外如果你想按周、按月来统计，只需Fork这个查询，修改`date_trunc()`函数的第一个参数为“week”或者“month”即可实现。作为对比，我们Fork并修改了一个按月统计的查询，只将其中的“”加到了数据看板中。

调整完成后，数据看板中的图表会自动更新为最新的显示结果，如下图所示。



![image_04.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051318961.png)



以上两个查询在Dune上的参考链接：

- https://dune.com/queries/1534604
- https://dune.com/queries/1534774

## 创作者个人资料（Profile）数据分析

Lens的创作者个人资料账号目前仅限于许可白名单内的用户来创建，创建个人资料的数据保存在`createProfile`表中。用下面的查询，我们可以计算出当前已经创建的个人资料的数量。

```sql
select count(*) as profile_count
from lens_polygon.LensHub_call_createProfile
where call_success = true   -- Only count success calls
```



创建一个Counter类型的可视化图表，Title设置为“Total Profiles”，将其添加到数据看板中。

我们同样关心创作者个人资料随日期的变化和增长情况。用下面的查询可以统计出每日、每月的个人资料创建情况。

```sql
with daily_profile_count as (
    select date_trunc('day', call_block_time) as block_date,
        count(*) as profile_count
    from lens_polygon.LensHub_call_createProfile
    where call_success = true
    group by 1
    order by 1
)

select block_date,
    profile_count,
    sum(profile_count) over (order by block_date) as accumulate_profile_count
from daily_profile_count
order by block_date
```



用类似的方法创建并添加可视化图表到数据看板。显示效果如下图所示：



![image_05.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051318876.png)



以上两个查询在Dune上的参考链接：

- https://dune.com/queries/1534486
- https://dune.com/queries/1534927
- https://dune.com/queries/1534950

## 创作者个人资料域名分析

Lens致力于打造一个社交图谱生态系统，每个创作者可以给自己的账号设置一个个性化的名称（Profile Handle Name），这也是通常大家说的Lens域名。与ENS等其他域名系统类似，我们会关注一些短域名、纯数字域名等的注册情况、不同字符长度的域名已注册数量等信息。在`createProfile`表中，字段`vars`以字符串格式保存了一个json对象，里面就包括了用户的个性化域名。在Dune V2中，我们可以直接使用`:`符号来访问json字符串中的元素的值，例如用`vars:handle`获取域名信息。

使用下面的SQL，我们可以获取已注册Lens域名的详细信息：

```sql
select json_value(vars, 'lax $.to') as user_address,
    json_value(vars, 'lax $.handle')  as handle_name,
    replace(json_value(vars, 'lax $.handle') , '.lens', '') as short_handle_name,
    call_block_time,
    output_0 as profile_id,
    call_tx_hash
from lens_polygon.LensHub_call_createProfile
where call_success = true
```

> [!TIP]
>
> `json_value(vars, 'lax $.to')` 是用于从 JSON 数据中提取指定字段值的 SQL 函数。`json_value()` 函数在 SQL 中用于从 JSON 文本提取单个标量值（如字符串、数字等）。在这个表达式中，`vars` 是一个包含 JSON 数据的列，而 `'lax $.to'` 是一个指定路径的参数，用于从 JSON 对象中定位并提取相应字段的值。
>
> ### 逐部分解释：
>
> #### 1. `json_value(vars, ...)`
> - **`json_value`**：这是 SQL 中用于提取 JSON 数据的函数。它返回指定 JSON 路径的标量值。
> - **`vars`**：这是一个包含 JSON 数据的列名，通常是 JSON 格式的字符串。在这个查询中，`vars` 可能包含类似 `{ "to": "0x123456...", "handle": "username.lens", ... }` 这样的 JSON 对象。
>
> #### 2. `'lax $.to'`
> - **`'lax $.to'`** 是 JSON 路径表达式，用于指定要提取的字段。路径表达式由以下部分组成：
>   - **`lax`**：表示路径模式的容错模式。`lax` 模式在路径表达式出错时，会允许柔性处理并返回 `null` 或者忽略无效路径；而如果使用 `strict`，则会严格要求路径匹配并抛出错误。`lax` 通常更常用，因为它容错性更好。
>   - **`$`**：美元符号 `"$"` 代表 JSON 对象的根节点，即整个 JSON 数据。它告诉解析器从根节点开始查找数据。
>   - **`.to`**：点符号 `.` 表示在 JSON 对象中访问其某个字段。在这里，它访问 JSON 对象中的 `to` 字段。`$.to` 表示“从根节点开始，找到对象中的 `to` 字段”。
>
> #### 示例：
>
> 假设 `vars` 列中包含如下 JSON 数据：
>
> ```json
> {
>   "to": "0x1234567890abcdef",
>   "from": "0xfedcba0987654321",
>   "handle": "username.lens"
> }
> ```
>
> 在这种情况下，`json_value(vars, 'lax $.to')` 的结果将是字符串 `"0x1234567890abcdef"`，即从 JSON 中提取 `to` 字段的值。
>
> #### `$` 的含义：
>
> - **`$`** 在 JSON 路径表达式中表示 JSON 文档的根节点。在根节点后，使用点 `.` 来访问 JSON 对象的字段。例如：
>   - `$.to`：表示从根节点提取 `to` 字段的值。
>   - `$.handle`：表示提取 `handle` 字段的值。
>
> #### 总结：
> - `json_value(vars, 'lax $.to')` 的作用是从 `vars` 列中的 JSON 数据中提取 `to` 字段的值。
> - **`$`** 表示从 JSON 对象的根节点开始。
> - **`lax`** 模式提供了容错性，防止由于路径不匹配导致的错误。

为了统计不同长度、不同类型（纯数字、纯字母、混合）Lens域名的数量以及各类型下已注册域名的总数量，我们可以将上面的查询放到一个CTE中。使用CTE的好处是可以简化逻辑（你可以按顺序分别调试、测试每一个CTE）。同时，CTE一经定义，就可以在同一个查询的后续SQL脚本中多次使用，非常便捷。鉴于查询各类域名的已注册总数量和对应不同字符长度的已注册数量都基于上面的查询，我们可以在同一个查询中将它们放到一起。因为前述统计都需要区分域名类型，我们在这个查询中增加了一个字段`handle_type`来代表域名的类型。修改后的查询代码如下：

```sql
with profile_created as (
    select json_value(vars, 'lax $.to') as user_address,
        json_value(vars, 'lax $.handle') as handle_name,
        replace(json_value(vars, 'lax $.handle'), '.lens', '') as short_name,
        (case when regexp_like(replace(json_value(vars, 'lax $.handle'), '.lens', ''), '^[0-9]+$') then 'Pure Digits'
            when regexp_like(replace(json_value(vars, 'lax $.handle'), '.lens', ''), '^[a-z]+$') then 'Pure Letters'
            else 'Mixed'
        end) as handle_type,
        call_block_time,
        output_0 as profile_id,
        call_tx_hash
    from lens_polygon.LensHub_call_createProfile
    where call_success = true    
),

profiles_summary as (
    select (case when length(short_name) >= 20 then 20 else length(short_name) end) as name_length,
        handle_type,
        count(*) as name_count
    from profile_created
    group by 1, 2
),

profiles_total as (
    select count(*) as total_profile_count,
        sum(case when handle_type = 'Pure Digits' then 1 else 0 end) as pure_digit_profile_count,
        sum(case when handle_type = 'Pure Letters' then 1 else 0 end) as pure_letter_profile_count
    from profile_created
)

select cast(name_length as varchar) || ' Chars' as name_length_type,
    handle_type,
    name_count,
    total_profile_count,
    pure_digit_profile_count,
    pure_letter_profile_count
from profiles_summary
join profiles_total on true
order by handle_type, name_length
```

> [!TIP]
>
> ### 代码分段解释：
>
> #### 第一部分：`with profile_created as (...)`
> 这部分代码创建了一个子查询（CTE，Common Table Expression），用于提取 Lens 网络中注册的 profile 的详细信息。
>
> ```sql
> select json_value(vars, 'lax $.to') as user_address, 
>        json_value(vars, 'lax $.handle') as handle_name,
>        replace(json_value(vars, 'lax $.handle'), '.lens', '') as short_name,
>        (case when regexp_like(replace(json_value(vars, 'lax $.handle'), '.lens', ''), '^[0-9]+$') then 'Pure Digits'
>              when regexp_like(replace(json_value(vars, 'lax $.handle'), '.lens', ''), '^[a-z]+$') then 'Pure Letters'
>              else 'Mixed'
>        end) as handle_type,
>        call_block_time,
>        output_0 as profile_id,
>        call_tx_hash
> from lens_polygon.LensHub_call_createProfile
> where call_success = true
> ```
>
> - **`json_value(vars, 'lax $.to') as user_address`**：从 `vars` 中提取 `to` 字段，表示用户的地址。
> - **`json_value(vars, 'lax $.handle') as handle_name`**：提取注册的用户名。
> - **`replace(json_value(vars, 'lax $.handle'), '.lens', '') as short_name`**：移除用户名中的 `.lens` 后缀，生成更短的名字 `short_name`。
> - **`case` 语句**：根据 `short_name` 的内容类型，将用户名分为三类：
>   - `Pure Digits`：完全由数字组成。
>   - `Pure Letters`：完全由字母组成。
>   - `Mixed`：由字母和数字混合组成。
> - **`call_block_time`**：注册事件的区块时间。
> - **`output_0 as profile_id`**：存储 profile 的 ID。
> - **`call_tx_hash`**：交易的哈希值。
>
> 这部分构建了一个新的“表”`profile_created`，保存了 Lens 上注册的 profile 信息。
>
> #### 第二部分：`profiles_summary as (...)`
> 这部分是一个统计子查询，按用户名长度和类型进行聚合，生成用户 profile 名称的统计信息。
>
> ```sql
> select (case when length(short_name) >= 20 then 20 else length(short_name) end) as name_length,
>        handle_type,
>        count(*) as name_count
> from profile_created
> group by 1, 2
> ```
>
> - **`case when length(short_name) >= 20 then 20 else length(short_name) end`**：如果用户名长度大于等于 20，则将长度视为 20（为了简化统计），否则返回实际的用户名长度。
> - **`handle_type`**：使用上一步的 `handle_type` 字段，对 profile 的类型（纯数字、纯字母、混合）进行分类。
> - **`count(*) as name_count`**：统计每种用户名长度和类型的数量。
> - **`group by 1, 2`**：按用户名长度和类型进行分组，分别统计不同类型和长度的 profile 数量。
>
> #### 第三部分：`profiles_total as (...)`
> 这部分汇总所有 profile，计算不同类型的 profile 总数。
>
> ```sql
> select count(*) as total_profile_count,
>        sum(case when handle_type = 'Pure Digits' then 1 else 0 end) as pure_digit_profile_count,
>        sum(case when handle_type = 'Pure Letters' then 1 else 0 end) as pure_letter_profile_count
> from profile_created
> ```
>
> - **`count(*) as total_profile_count`**：计算 profile 的总数量。
> - **`sum(case when handle_type = 'Pure Digits' then 1 else 0 end)`**：计算纯数字 profile 的数量。
> - **`sum(case when handle_type = 'Pure Letters' then 1 else 0 end)`**：计算纯字母 profile 的数量。
>
> #### 第四部分：主查询
> 最后一部分是主查询，它将汇总的 profile 数据和统计数据结合，返回最终结果。
>
> ```sql
> select cast(name_length as varchar) || ' Chars' as name_length_type,
>        handle_type,
>        name_count,
>        total_profile_count,
>        pure_digit_profile_count,
>        pure_letter_profile_count
> from profiles_summary
> join profiles_total on true
> order by handle_type, name_length
> ```
>
> - **`cast(name_length as varchar) || ' Chars' as name_length_type`**：将 `name_length` 转换为字符串，并拼接上 `' Chars'`，生成类似 `'10 Chars'` 这样的字段表示用户名长度。
> - **`handle_type`**：展示用户名的类型。
> - **`name_count`**：展示对应长度和类型的用户名的数量。
> - **`total_profile_count`**、**`pure_digit_profile_count`**、**`pure_letter_profile_count`**：这些字段展示 profile 的总体统计数据，用于参考。
> - **`order by handle_type, name_length`**：按 `handle_type` 和 `name_length` 进行排序，确保输出按用户名类型和长度有序显示。

修改后的查询代码相对比较复杂，解读如下：

1. CTE `profile_created`通过使用“:“符号来从保存于`vars`字段中的json字符串里面提取出Profile的域名信息和域名归属的用户地址。由于保存的域名包括了`.lens`的后缀，我们通过`replace()`方法将后缀部分清除并命名新的字段为`short_name`，方便后面计算域名的字符长度。进一步，我们通过一个CASE语句，结合正则表达式匹配操作符`rlike`来判断域名是否由纯数字或者纯字母组成，并赋予一个字符串名称值，命名此字段为`handle_type`。可参考[rlike operator](https://docs.databricks.com/sql/language-manual/functions/rlike.html)了解正则表达式匹配的更多信息。
2. CTE `profiles_summary`基于`profile_created`执行汇总查询。我们首先使用`length()`函数计算出每一个域名的字符长度。因为存在少量特别长的域名，我们使用一个CASE语句，将长度大于20个字符的域名统一按20来对待。然后我们基于域名长度`name_length`和`handle_type`执行`group by`汇总统计，计算各种域名的数量。
3. CTE `profiles_total`中，我们统计域名总数量、纯数字域名的数量和纯字母域名的数量。
4. 最后，我们将`profiles_summary`和`profiles_total`这两个CTE关联到一起输出最终查询结果。由于`profiles_total`只有一行数据，我们直接使用`true`作为JOIN的条件即可。另外，因为`name_length`是数值类型，我们将其转换为字符串类型，并连接到另一个字符串来得到可读性更强的域名长度类型名称。我们将输出结果按域名类型和长度进行排序。

执行查询并保存之后，我们为其添加下列可视化图表并分别添加到数据看板中：

1. 添加两个Counter，分别输出纯数字域名的数量和纯字母域名的数量。因为之前已经有一个域名注册总数量的Counter，我们可以将这两个新的Counter图表跟它放置到同一行。
2. 添加一个域名类型分布的扇形图（Pie Chart），Title设置为“Profiles Handle Name Type Distribution”，“X Column“选择`handle_type`字段，“Y Column 1”选择`name_count`字段。
3. 添加一个域名长度分布的扇形图（Pie Chart），Title设置为“Profiles Handle Name Length Distribution”，“X Column“选择`name_length_type`字段，“Y Column 1”选择`name_count`字段。
4. 添加一个域名长度分布的柱状图（Bar Chart），Title设置为“Profiles Handle Name Count By Length”，“X Column“选择`name_length_type`字段，“Y Column 1”选择`name_count`字段，“Group by”选择`handle_type`字段。同时取消勾选“Sort values”选项，再勾选“Enable stacking”选项。
5. 添加一个域名长度分布的面积图（Area Chart），Title设置为“Profile Handle Name Count Percentage By Type”，“X Column“选择`name_length_type`字段，“Y Column 1”选择`name_count`字段，“Group by”选择`handle_type`字段。取消勾选“Sort values”选项，再勾选“Enable stacking”选项，另外再勾选“Normalize to percentage”选项。

将上述可视化图表全部添加到数据看板中，调整显示顺序后，如下图所示：



![image_06.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051318980.png)



本查询在Dune上的参考链接：

- https://dune.com/queries/1535541

## 已注册域名搜索

除了对已注册Lens域名的分布情况的跟踪，用户也关注已注册域名的详细情况。为此，可以提供一个搜索功能，允许用户搜索已注册域名的详细列表。因为目前已经注册了约10万个Lens账号，我们在下面的查询中限制最多返回10000条搜索结果。

首先，我们可以在查询中定义一个参数`{{name_contains}}`（Dune 使用两个花括号包围住参数名称，默认参数类型为字符串`Text`类型）。然后使用`like`关键词以及`%`通配符来搜索名称中包含特定字符的域名：

```sql
with profile_created as (
    select json_value(vars, 'lax $.to') as user_address,
        json_value(vars, 'lax $.handle') as handle_name,
        replace(json_value(vars, 'lax $.handle'), '.lens', '') as short_name,
        call_block_time,
        output_0 as profile_id,
        call_tx_hash
    from lens_polygon.LensHub_call_createProfile
    where call_success = true    
)

select call_block_time,
    profile_id,
    handle_name,
    short_name,
    call_tx_hash
from profile_created
where short_name like '%{{name_contains}}%' -- 查询名称包含输入的字符串的域名
order by call_block_time desc
limit 1000
```

> [!TIP]
>
> 这段代码的作用是从 `profile_created` 表中查询 Lens 网络中注册的 profile，并提供了一个筛选功能来查找用户名包含特定字符的 profile 列表。它使用了 SQL 的 `LIKE` 关键词和通配符 `%` 来实现模糊搜索，以下是逐行解释：
>
> ### 代码逐行解析：
>
> ```sql
> select call_block_time,
>     profile_id,
>     handle_name,
>     short_name,
>     call_tx_hash
> ```
>
> - **`call_block_time`**：提取用户 profile 注册事件的区块时间（时间戳）。
> - **`profile_id`**：提取用户的 profile ID。
> - **`handle_name`**：提取用户的完整 Lens 名称（带 `.lens` 后缀）。
> - **`short_name`**：提取用户的短用户名（不带 `.lens` 后缀）。
> - **`call_tx_hash`**：提取交易哈希，表示该 profile 注册事件对应的链上交易。
>
> ```sql
> from profile_created
> ```
>
> - 数据来源是之前通过 `WITH` 子查询创建的 `profile_created` 表，存储了所有注册的 profile 及其详细信息。
>
> ```sql
> where short_name like '%{{name_contains}}%' -- 查询名称包含输入的字符串的域名
> ```
>
> - **`short_name like '%{{name_contains}}%'`**：使用 `LIKE` 关键字实现模糊搜索，`{{name_contains}}` 是一个参数，表示用户希望查询的特定字符串。
>   - `%`：通配符，表示任意数量的字符。因此，`'%{{name_contains}}%'` 会匹配任何包含 `{{name_contains}}` 子串的用户名。
>   - **`{{name_contains}}`**：在 Dune SQL 查询中，双花括号包围的内容表示动态参数，用户可以在执行查询时输入该参数，用于筛选包含某个字符串的用户名。
>
> ```sql
> order by call_block_time desc
> ```
>
> - 结果按 **`call_block_time`**（注册时间）倒序排序，最新的 profile 会排在前面。
>
> ```sql
> limit 1000
> ```
>
> - 返回最多 1000 条结果，以防止返回过多数据导致性能问题。
>
> ### 总结
> 该查询的功能是：
> - 查找 Lens 网络中包含特定字符串的 profile。
> - 返回用户的 profile ID、用户名、注册时间、交易哈希等信息。
> - 最多返回 1000 条数据，并按注册时间倒序排序。

在查询执行之前，Dune 引擎会用输入的参数值替换SQL语句中的参数名称。当我们输入“john”时，`where short_name like '%{{name_contains}}%'`子句会被替换为`where short_name like '%john%'`，其含义就是搜索`short_name`包含字符串`john`的所有域名。注意虽然参数类型是字符串类型，但是参数替换时不会自动给我们添加前后的单引号。单引号需要我们直接输入到查询中，如果忘记输入了则会引起语法错误。

如前所述，域名的长度也很关键，越短的域名越稀缺。除了搜索域名包含的字符，我们可以再添加一个域名长度过滤的参数`{{name_length}}`，将其参数类型修改为下拉列表类型，同时填入数字5-20的序列作为参数值列表，每行一个值。因为Lens域名目前最少5个字符，而且超过20个字符的域名很少，所以我们选择5到20作为区间。参数设置如下图所示。



![image_08.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051318988.png)



添加了新的参数后，我们调整SQL语句的WHERE子句为如下所示。其含义为查询名称包含输入的关键字，同时域名字符长度等于选择的长度值的域名列表。注意，虽然我们的`name_length`参数的值全部是数字，但List类型参数的默认类型是字符串，所以我们使用`cast()`函数转换其类型为整数类型后再进行比较。

```sql
where short_name like '%{{name_contains}}%' -- 名称包含输入的字符串的域名
    and length(short_name) = cast('{{name_length}}' as integer) -- 域名长度等于选择的长度值
```



同样，我们可以再添加一个域名字符串模式类型的参数`{{name_pattern}}`，用来过滤纯数字域名或纯字母域名。这里同样设置参数为List类型，列表包括三个选项：Any、Pure Digits、Pure Letters。SQL语句的WHERE子句相应修改为如下所示。跟之前的查询类似，我们使用一个CASE语句来判断当前查询域名的类型，如果查询纯数字或者纯字母域名，则使用相应的表达式，如果查询任意模式则使用`1 = 1`这样的总是返回真值的相等判断，相当于忽略这个过滤条件。

```sql
where short_name like '%{{name_contains}}%' -- 名称包含输入的字符串的域名
    and length(short_name) = cast('{{name_length}}' as integer) -- 域名长度等于选择的长度值
    and (case when '{{name_pattern}}' = 'Pure Digits' then regexp_like(short_name, '^[0-9]+$')
            when '{{name_pattern}}' = 'Pure Letters' then regexp_like(short_name, '^[a-z]+$')
            else 1 = 1
        end)
```

> [!TIP]
>
> 这个 `WHERE` 子句增加了对用户名长度和模式的筛选逻辑：
>
> 1. **`{{name_contains}}`**：筛选包含指定字符串的用户名。
> 2. **`{{name_length}}`**：筛选长度等于指定值的用户名。
> 3. **`{{name_pattern}}`**：筛选特定模式的用户名（纯数字、纯字母，或不做模式限制）。
>
> 这使得查询更加灵活，可以根据多个条件同时筛选出符合需求的 Lens 域名。

因为我们在这几个搜索条件之间使用了`and`连接条件，相当于必须同时满足所有条件，这样的搜索有一定的局限性。我们对其做适当调整，name_length参数也再增加一个默认选项“0”。当用户未输入或者未选择某个过滤条件时，我们忽略它。这样搜索查询就变得非常灵活了。完整的SQL语句如下：

```sql
with profile_created as (
    select json_value(vars, 'lax $.to') as user_address,
        json_value(vars, 'lax $.handle') as handle_name,
        replace(json_value(vars, 'lax $.handle'), '.lens', '') as short_name,
        call_block_time,
        output_0 as profile_id,
        call_tx_hash
    from lens_polygon.LensHub_call_createProfile
    where call_success = true    
)

select call_block_time,
    profile_id,
    handle_name,
    short_name,
    '<a href=https://polygonscan.com/tx/' || cast(call_tx_hash as varchar) || ' target=_blank>Polyscan</a>' as link,
    call_tx_hash
from profile_created
where (case when '{{name_contains}}' <> 'keyword' then short_name like '%{{name_contains}}%' else 1 = 1 end)
    and (case when cast('{{name_length}}' as integer) < 5 then 2 = 2
            when cast('{{name_length}}' as integer) >= 20 then length(short_name) >= 20
            else length(short_name) = cast('{{name_length}}' as integer)
        end)
    and (case when '{{name_pattern}}' = 'Pure Digits' then regexp_like(short_name, '^[0-9]+$')
            when '{{name_pattern}}' = 'Pure Letters' then regexp_like(short_name, '^[a-z]+$')
            else 3 = 3
        end)
order by call_block_time desc
limit 1000
```

> [!IMPORTANT]
>
> 这段 SQL 通过对搜索条件的灵活处理，解决了当用户未输入或未选择某个过滤条件时，忽略它的需求。具体来说，它通过 `CASE` 表达式检查用户是否提供了参数值，并根据参数值是否有效来决定是否应用过滤条件。
>
> ### 逐步解析代码：
>
> 1. **基础数据提取**：
>    ```sql
>    with profile_created as (
>        select json_value(vars, 'lax $.to') as user_address,
>            json_value(vars, 'lax $.handle') as handle_name,
>            replace(json_value(vars, 'lax $.handle'), '.lens', '') as short_name,
>            call_block_time,
>            output_0 as profile_id,
>            call_tx_hash
>        from lens_polygon.LensHub_call_createProfile
>        where call_success = true    
>    )
>    ```
>    这部分提取 Lens 已创建的 Profile 信息，如 `user_address`、`handle_name` 和 `short_name`，用于后续查询。
>
> 2. **搜索条件 1：关键词搜索**：
>    ```sql
>    where (case when '{{name_contains}}' <> 'keyword' then short_name like '%{{name_contains}}%' else 1 = 1 end)
>    ```
>    - **解释**：`{{name_contains}}` 参数表示用户想要查找的关键字。通过 `case when '{{name_contains}}' <> 'keyword'` 检查用户是否输入了关键词。如果输入了关键词（即 `{{name_contains}}` 不等于默认值 `'keyword'`），则筛选 `short_name` 中包含该关键词的记录。如果没有提供关键词，则忽略此条件，返回所有结果。
>    - **`else 1 = 1`** 部分**：这是一个总是为 `true` 的表达式，用来确保在没有关键词时不会筛选掉任何结果。
>
> 3. **搜索条件 2：长度筛选**：
>    ```sql
>    and (case when cast('{{name_length}}' as integer) < 5 then 2 = 2
>            when cast('{{name_length}}' as integer) >= 20 then length(short_name) >= 20
>            else length(short_name) = cast('{{name_length}}' as integer)
>        end)
>    ```
>    - **解释**：`{{name_length}}` 参数表示用户想要查找的域名长度。这里通过 `CASE` 表达式来灵活处理：
>      - 如果用户没有输入或选择长度（`{{name_length}}` 小于 5），则忽略此条件。
>      - 如果 `{{name_length}}` 大于或等于 20，则返回长度大于等于 20 的记录。
>      - 否则，匹配长度等于用户输入的值。
>    - **`2 = 2`** 部分：这也是一个总是为 `true` 的表达式，用于忽略该条件。
>
> 4. **搜索条件 3：模式筛选**：
>    ```sql
>    and (case when '{{name_pattern}}' = 'Pure Digits' then regexp_like(short_name, '^[0-9]+$')
>            when '{{name_pattern}}' = 'Pure Letters' then regexp_like(short_name, '^[a-z]+$')
>            else 3 = 3
>        end)
>    ```
>    - **解释**：`{{name_pattern}}` 表示用户想要筛选的域名模式。根据 `{{name_pattern}}` 的不同值：
>      - 如果选择了 `Pure Digits`，则只返回纯数字域名。
>      - 如果选择了 `Pure Letters`，则只返回纯字母域名。
>      - 否则，忽略该条件。
>    - **`3 = 3`**：这个总是为 `true` 的表达式确保在没有指定模式时不筛选掉任何结果。
>
> 5. **结果排序和限制**：
>    ```sql
>    order by call_block_time desc
>    limit 1000
>    ```
>    - **`order by call_block_time desc`**：按 `call_block_time`（Profile 创建时间）从最近到最早排序。
>    - **`limit 1000`**：限制最多返回 1000 条结果，避免查询数据量过大。
>
> ### 结论：
> 这段 SQL 的灵活性体现在：
> - 通过 `CASE` 表达式根据用户输入的不同过滤条件，动态调整查询行为。
> - 如果某个条件未被指定，则通过 `1 = 1`、`2 = 2` 或 `3 = 3` 来确保忽略该条件，从而提高查询的灵活性和适用性。
>
> 这使得用户可以按需筛选域名，无论是根据关键字、长度还是模式，都可以非常灵活地组合应用这些过滤条件。

我们给这个查询增加一个表格（Table）类型的可视化图表，并将其添加到数据看板中。当添加代参数的查询到数据看板时，所有的参数也被自动添加到看板头部。我们可以进入编辑模式，拖拽参数到其希望出现的位置。将图表加入数据看板后的效果图如下所示。



![image_07.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051318758.png)



以上查询在Dune上的参考链接：

- https://dune.com/queries/1535903
- https://dune.com/queries/1548540
- https://dune.com/queries/1548574
- https://dune.com/queries/1548614

## 总结

至此，我们已经完成了对Lens协议的基本概况和创作者个人资料、域名信息的分析，也添加了一个域名搜索功能。前面“数据看板的主要分析内容”部分我们列出了更多可以分析的内容，在本篇教程的第二部分，我们将继续围绕创作者发布的出版物、关注、收藏、NFT等方面进行分析。你也可以自行探索创建新的查询。

## 作业

请结合教程内容，制作你自己的Lens 协议数据看板，可参考“数据看板的主要分析内容”部分提示的内容尝试新的查询分析。请大家积极动手实践，创建数据看板并分享到社区。我们将对作业完成情况和质量进行记录，之后追溯为大家提供一定的奖励，包括但不限于Dune社区身份，周边实物，API免费额度，POAP，各类合作的数据产品会员，区块链数据分析工作机会推荐，社区线下活动优先报名资格以及其他Sixdegree社区激励等。

# 9. 实践案例：制作Lens Protocol的数据看板（二）

在本教程的第一部分中，我们给大家介绍了Lens协议，并为其制作了一个初步的看板，分析了包括总交易数量和总用户数量、按天统计的交易数量和独立用户数量、创作者个人资料（Profile）分析、Lens域名分析、已注册域名搜索等相关内容。让我们继续给这个数据看板添加新的查询和可视化图表。我们将分析并添加以下内容：同一个地址创建多个Profile、关注数据、发帖数据、评论数据、收藏数据、镜像数据、创作者的操作综合情况、普通用户地址的操作综合情况。

## 同一个地址创建多个Profile分析

Lens协议允许一个地址创建多个Profile。我们可以编写一个查询来统计创建了多个Profile的地址的数据分布情况。在下面的查询中，我们先用CTE `profile_created`取得所有已创建的Profile的数据详情，然后使用`multiple_profiles_addresses`来统计每一个地址创建的Profile数量。最后，我们使用CASE语句，按每个地址创建的Profile的数量对其进行归类，返回综合的统计数据。

```sql
with profile_created as (
    select json_value(vars, 'lax $.to') as user_address,
        json_value(vars, 'lax $.handle') as handle_name,
        replace(json_value(vars, 'lax $.handle'), '.lens', '') as short_name,
        call_block_time,
        output_0 as profile_id,
        call_tx_hash
    from lens_polygon.LensHub_call_createProfile
    where call_success = true    
),

multiple_profiles_addresses as (
    select user_address,
        count(profile_id) as profile_count
    from profile_created
    group by 1
    order by 2 desc
)

select (case when profile_count >= 10 then '10+ Profiles'
            when profile_count >= 3 then '5+ Profiles'
            when profile_count = 2 then '2 Profiles'
            else '1 Profile'
        end) as profile_count_type,
    count(user_address) as user_address_count,
    sum(profile_count) as profile_count
from multiple_profiles_addresses
group by 1
```

> [!IMPORTANT]
>
> 在 SQL 中，`WITH` 子句用于定义“公用表表达式”（CTE，Common Table Expression），允许你在查询中定义一个临时结果集，并在后续的查询中引用它。你可以通过 `WITH` 定义多个 CTE。
>
> 具体来说，你的问题提到的 `multiple_profiles_addresses` 是在 `WITH` 子句中的第二个 CTE。之所以不需要在每个 CTE 前面都加 `WITH`，是因为 `WITH` 只需要在第一次定义 CTE 时使用，而后续 CTE 直接通过逗号分隔即可。

做这类数据统计时，通常我们也需要得到一些Counter类型的统计值，比如创建过多个Profile的地址总数、这些地址一共创建了多少个Profile，这些Profile在所有已创建的Profile中的占比等等。查询这些数据时可以共用上面的CTE子查询代码，所以我们对其稍做修改，添加了两个额外的CTE来统计这些Counter类型的数值。为这个查询添加可视化图表并分别加入到数据看板中，显示效果如下：



![image_09.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051318274.png)



以上查询在Dune上的参考链接：

- https://dune.com/queries/1562662
- https://dune.com/queries/1553030

## 发帖数据分析

### 发帖最多的账号数据分析

Lens的创作者有两种发帖（Post）的方式，一直是直接用自己的账号发布Post，另一种是委托其他账号或者通过API的方式来发布。Post数据分别保存在`LensHub_call_post`和`LensHub_call_postWithSig`表中。每一个主题Post的内容以JSON字符串的形式保存在字段`vars`中，包括作者的ProfileID，帖子内容的URL等信息。对于字符串形式的JSON内容，我们可以使用`:`操作符来访问其中的值。下面的查询可以获得部分示范数据：

```sql
select call_block_time,
    call_tx_hash,
    output_0 as post_id,
    json_value(vars, 'lax $.profileId') as profile_id, -- Access element in json string
    json_value(vars, 'lax $.contentURI') as content_url,
    json_value(vars, 'lax $.collectModule') as collection_module,
    json_value(vars, 'lax $.referenceModule') as reference_module,
    vars
from lens_polygon.LensHub_call_post
where call_success = true
limit 10
```



鉴于发帖的Profile数量很多，我们可以像前面分析“同一个地址创建多个Profile”那样，对不同发帖数量的Profile做一个分类统计，还可以关注头部用户，即发帖最多的那些账号的数据。这里我们对发帖最多的账号进行分析，同时将这部分账号的发帖数量和总体发帖数量的进行对照，输出Counter图表。完整的SQL如下：

```sql
with post_data as (
    select call_block_time,
        call_tx_hash,
        output_0 as post_id,
        json_value(vars, 'lax $.profileId') as profile_id, -- Access element in json string
        json_value(vars, 'lax $.contentURI') as content_url,
        json_value(vars, 'lax $.collectModule') as collection_module,
        json_value(vars, 'lax $.referenceModule') as reference_module,
    from lens_polygon.LensHub_call_post
    where call_success = true
    
    union all
    
    select call_block_time,
        call_tx_hash,
        output_0 as post_id,
        json_value(vars, 'lax $.profileId') as profile_id, -- Access element in json string
        json_value(vars, 'lax $.contentURI') as content_url,
        json_value(vars, 'lax $.collectModule') as collection_module,
        json_value(vars, 'lax $.referenceModule') as reference_module,
    from lens_polygon.LensHub_call_postWithSig
    where call_success = true
),

posts_summary as (
    select count(*) as total_post_count,
        count(distinct profile_id) as posted_profile_count
    from post_data
),

top_post_profiles as (
    select profile_id,
        count(*) as post_count
    from post_data
    group by 1
    order by 2 desc
    limit 1000
)

select profile_id,
    post_count,
    sum(post_count) over () as top_profile_post_count,
    total_post_count,
    posted_profile_count,
    cast(sum(post_count) over () as double) / total_post_count * 100 as top_profile_posts_ratio
from top_post_profiles
inner join posts_summary on true
order by 2 desc
```

> [!TIP]
>
> ```sql
> cast(sum(post_count) over () as double)
> ```
>
> ### 分解解释：
>
> 1. **`sum(post_count)`**：这是一个聚合函数，它对 `post_count` 列进行求和。通常，聚合函数像 `SUM`、`AVG`、`COUNT` 等需要和 `GROUP BY` 一起使用来对特定组进行汇总。
>    
> 2. **`over()`**：这是窗口函数的一部分，表示我们希望对整个结果集应用 `sum(post_count)`，而不是通过 `GROUP BY` 将行汇总成单独的组。`over()` 中没有任何参数，意味着它作用于整个查询返回的所有行，而不是分组计算。
>
> 3. **`cast(... as double)`**：这个部分将计算结果转换为 `double` 类型。因为 `SUM` 的返回值可能默认是整数（如果 `post_count` 是整数），所以我们使用 `CAST` 来将其显式地转换为浮点数，以确保精度。
>
> ### 作用：
> 在这个场景下，`sum(post_count) over ()` 会计算 `post_count` 列的总和，但它不会像 `GROUP BY` 那样将查询结果按组进行聚合。每一行仍会保留原始数据，同时每一行都会显示总和的值。换句话说，它在每一行上重复显示整个结果集的 `post_count` 总和。
>
> ### 示例：
> 假设查询结果返回了以下 `post_count` 数据：
>
> | post_count |
> | ---------- |
> | 10         |
> | 20         |
> | 30         |
>
> 执行 `sum(post_count) over ()` 后：
>
> | post_count | sum(post_count) over () |
> | ---------- | ----------------------- |
> | 10         | 60                      |
> | 20         | 60                      |
> | 30         | 60                      |
>
> 每一行都保留了其自身的 `post_count`，但同时也展示了整个列的总和。

> [!NOTE]
>
> 这段 SQL 查询结合了多个 CTE（Common Table Expressions）来分析 Lens 协议中的发帖数据。以下是对每个部分的详细解释：
>
> ### 1. **CTE: `post_data`**
> 这个 CTE 从两个表中获取发帖数据：`LensHub_call_post` 和 `LensHub_call_postWithSig`。它们通过 `union all` 将数据合并到一个结果集中。
>
> ```sql
> with post_data as (
>     select call_block_time,
>         call_tx_hash,
>         output_0 as post_id,
>         json_value(vars, 'lax $.profileId') as profile_id,
>         json_value(vars, 'lax $.contentURI') as content_url,
>         json_value(vars, 'lax $.collectModule') as collection_module,
>         json_value(vars, 'lax $.referenceModule') as reference_module
>     from lens_polygon.LensHub_call_post
>     where call_success = true
>     
>     union all
>     
>     select call_block_time,
>         call_tx_hash,
>         output_0 as post_id,
>         json_value(vars, 'lax $.profileId') as profile_id,
>         json_value(vars, 'lax $.contentURI') as content_url,
>         json_value(vars, 'lax $.collectModule') as collection_module,
>         json_value(vars, 'lax $.referenceModule') as reference_module
>     from lens_polygon.LensHub_call_postWithSig
>     where call_success = true
> )
> ```
>
> - **`json_value(vars, 'lax $.profileId')`** 等提取 `vars` 字段中对应 JSON 数据的值（例如 `profileId`, `contentURI` 等）。
> - 两个 `select` 均从不同的表中获取类似的字段并通过 `union all` 合并，这允许将所有成功的发帖数据汇总起来。
>
> ### 2. **CTE: `posts_summary`**
> 这个 CTE 生成整个发帖数据的汇总。
>
> ```sql
> posts_summary as (
>     select count(*) as total_post_count,
>         count(distinct profile_id) as posted_profile_count
>     from post_data
> )
> ```
> - **`count(*)`**：统计所有发帖的数量（`total_post_count`）。
> - **`count(distinct profile_id)`**：统计不同发帖的账户数量（`posted_profile_count`）。
>
> ### 3. **CTE: `top_post_profiles`**
> 此 CTE 统计每个 `profile_id` 发帖的数量，并根据发帖数量进行降序排序，取前 1000 名。
>
> ```sql
> top_post_profiles as (
>     select profile_id,
>         count(*) as post_count
>     from post_data
>     group by 1
>     order by 2 desc
>     limit 1000
> )
> ```
> - **`group by 1`**：根据 `profile_id` 分组统计发帖数量。
> - **`order by 2 desc`**：按发帖数量（`post_count`）降序排列，提取发帖最多的前 1000 名。
>
> ### 4. **最终查询**
> 最后一个查询通过 `inner join` 将 `top_post_profiles` 和 `posts_summary` 两个 CTE 结合，计算出一些重要指标。
>
> ```sql
> select profile_id,
>     post_count,
>     sum(post_count) over () as top_profile_post_count,
>     total_post_count,
>     posted_profile_count,
>     cast(sum(post_count) over () as double) / total_post_count * 100 as top_profile_posts_ratio
> from top_post_profiles
> inner join posts_summary on true
> order by 2 desc
> ```
> - **`sum(post_count) over () as top_profile_post_count`**：计算在 `top_post_profiles` 中所有发帖数的总和（即前 1000 名账户发的总帖数）。
> - **`cast(sum(post_count) over () as double) / total_post_count * 100 as top_profile_posts_ratio`**：计算这些前 1000 名账户发帖数占总发帖数的比例，并将其转换为百分比格式。
> - **`inner join posts_summary on true`**：结合 `top_post_profiles` 和 `posts_summary`，以便能在查询中同时访问总发帖数和账户发帖数据。
>
> ### 结论：
> - 此查询分析了 Lens 上前 1000 个账户的发帖情况，计算了这些账户在所有发帖中的占比。

以上SQL解读：因为Post数据分别保存在两个表里，在CTE `post_data`中，我们使用`union all`将两个表中取出的数据合并到一起。我们通过`posts_summary`来统计所有发帖的Profile数量和他们累计发布的Post数量。在`top_post_profiles`中，我们按照每个Profile的发帖数量最多的1000个Profile的数据。最后，我们关联查询`top_post_profiles`和`posts_summary`，输出发帖最多的账号数据以及它们和总发帖数据的对比。将查询结果可视化并加入数据看板后的显示效果如下：



![image_10.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051318463.png)



以上查询在Dune上的参考链接：

- https://dune.com/queries/1554541

### 每日新发帖数量统计

Lens用户每日的新发帖数量是观察整体活跃度变化趋势的一个重要指标，我们编写一个查询来统计每天的发帖数量。这个查询中的`post_data` CTE与之前的完全相同，所以我们在下面的代码中省略它的详情。因为我们还希望将每天的发帖数量进行累加返回累计发帖数量，我们定义`post_daily_summary` CTE作为中间步骤，以让SQL代码简单易懂。对应的SQL如下：

```sql
with post_data as (
    -- Get post data from LensHub_call_post and LensHub_call_postWithSig tables
),

post_daily_summary as (
    select date_trunc('day', call_block_time) as block_date,
        count(*) post_count,
        count(distinct profile_id) as profile_count
    from post_data
    group by 1
)

select block_date,
    post_count,
    profile_count,
    sum(post_count) over (order by block_date) as accumulate_post_count
from post_daily_summary
order by block_date
```

> [!TIP]
>
> 这段 SQL 查询的目的是从 Lens 数据中获取每日发帖的汇总信息，以下是对每个部分的详细解释：
>
> ### 1. **CTE: `post_data`**
> 此部分通过 CTE 获取发帖数据。
>
> ```sql
> with post_data as (
>     -- Get post data from LensHub_call_post and LensHub_call_postWithSig tables
> ),
> ```
>
> - 这部分应该从 `LensHub_call_post` 和 `LensHub_call_postWithSig` 表中提取发帖数据，通常会包含发帖的时间、用户信息和其他相关字段。
>
> ### 2. **CTE: `post_daily_summary`**
> 在这个 CTE 中，我们对从 `post_data` 提取的数据进行汇总，按日统计发帖数量和用户数量。
>
> ```sql
> post_daily_summary as (
>     select date_trunc('day', call_block_time) as block_date,
>         count(*) as post_count,
>         count(distinct profile_id) as profile_count
>     from post_data
>     group by 1
> )
> ```
>
> - **`date_trunc('day', call_block_time) as block_date`**: 将 `call_block_time` 截断到日，以便按日汇总数据。
> - **`count(*) as post_count`**: 计算每一天的总发帖数。
> - **`count(distinct profile_id) as profile_count`**: 计算每一天发布帖子的独立用户数（不同的 `profile_id`）。
> - **`group by 1`**: 按 `block_date` 进行分组，确保每一天的数据汇总在一行。
>
> ### 3. **最终查询**
> 最后一部分查询从 `post_daily_summary` 中获取每日的发帖和用户数量，并计算累计发帖数。
>
> ```sql
> select block_date,
>     post_count,
>     profile_count,
>     sum(post_count) over (order by block_date) as accumulate_post_count
> from post_daily_summary
> order by block_date
> ```
>
> - **`block_date`**: 返回每一天的日期。
> - **`post_count`**: 返回该日期的发帖总数。
> - **`profile_count`**: 返回该日期的独立用户数。
> - **`sum(post_count) over (order by block_date) as accumulate_post_count`**: 计算从开始到当前日期的累计发帖数。使用 `OVER (ORDER BY block_date)` 子句使得这个累计值是动态计算的，即随着日期的变化而变化。
> - **`order by block_date`**: 将结果按照日期升序排列。
>
> ### 总结
> 此查询用于分析 Lens 协议中每日的发帖活动，提供了每日发帖数量、独立用户数量及其累积发帖数，为了解用户行为和内容生成提供了重要数据。

将查询结果可视化并加入数据看板后的显示效果如下：



![image_11.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051318085.png)



以上查询在Dune上的参考链接：

- https://dune.com/queries/1555124

### 近30天发帖最活跃的Profile统计

同样，我们可能关心最近一段时间内发帖最活跃的Profile的情况。为此我们只需要在前述`post_data` CTE中，分别添加日期过滤条件来筛选最近30天内的发帖，然后按日期汇总统计即可。SQL如下：

```sql
with post_data as (
    select call_block_time,
        call_tx_hash,
        output_0 as post_id,
        json_value(vars, 'lax $.profileId') as profile_id, -- Access element in json string
        json_value(vars, 'lax $.contentURI') as content_url,
        json_value(vars, 'lax $.collectModule') as collection_module,
        json_value(vars, 'lax $.referenceModule') as reference_module
    from lens_polygon.LensHub_call_post
    where call_success = true
        and call_block_time >= now() - interval '30' day
    
    union all
    
    select call_block_time,
        call_tx_hash,
        output_0 as post_id,
        json_value(vars, 'lax $.profileId') as profile_id, -- Access element in json string
        json_value(vars, 'lax $.contentURI') as content_url,
        json_value(vars, 'lax $.collectModule') as collection_module,
        json_value(vars, 'lax $.referenceModule') as reference_module
    from lens_polygon.LensHub_call_postWithSig
    where call_success = true
        and call_block_time >= now() - interval '30' day
)

select profile_id,
    count(*) as post_count
from post_data
group by 1
order by 2 desc
limit 100
```

> [!TIP]
>
> 这段 SQL 查询的目的是从 Lens 的发帖数据中提取最近 30 天内的发帖信息，并按用户（`profile_id`）对发帖数量进行汇总。以下是对代码各部分的详细解释：
>
> ### 1. **CTE: `post_data`**
> 该部分通过公共表表达式（CTE）提取发帖数据，主要分为两个来源的表：`LensHub_call_post` 和 `LensHub_call_postWithSig`。
>
> ```sql
> with post_data as (
>     select call_block_time,
>         call_tx_hash,
>         output_0 as post_id,
>         json_value(vars, 'lax $.profileId') as profile_id, -- Access element in json string
>         json_value(vars, 'lax $.contentURI') as content_url,
>         json_value(vars, 'lax $.collectModule') as collection_module,
>         json_value(vars, 'lax $.referenceModule') as reference_module
>     from lens_polygon.LensHub_call_post
>     where call_success = true
>         and call_block_time >= now() - interval '30' day
>     
>     union all
>     
>     select call_block_time,
>         call_tx_hash,
>         output_0 as post_id,
>         json_value(vars, 'lax $.profileId') as profile_id, -- Access element in json string
>         json_value(vars, 'lax $.contentURI') as content_url,
>         json_value(vars, 'lax $.collectModule') as collection_module,
>         json_value(vars, 'lax $.referenceModule') as reference_module
>     from lens_polygon.LensHub_call_postWithSig
>     where call_success = true
>         and call_block_time >= now() - interval '30' day
> )
> ```
>
> - **提取字段**:
>   - `call_block_time`: 发帖的区块时间。
>   - `call_tx_hash`: 发帖的交易哈希。
>   - `output_0 as post_id`: 将输出字段 `output_0` 作为发帖 ID。
>   - `json_value(vars, 'lax $.profileId') as profile_id`: 从 JSON 字符串中提取用户 ID（`profileId`）。
>   - `json_value(vars, 'lax $.contentURI') as content_url`: 从 JSON 字符串中提取内容链接。
>   - `json_value(vars, 'lax $.collectModule') as collection_module`: 从 JSON 字符串中提取收藏模块。
>   - `json_value(vars, 'lax $.referenceModule') as reference_module`: 从 JSON 字符串中提取参考模块。
>
> - **过滤条件**:
>   - `where call_success = true`: 仅选择成功的交易记录。
>   - `and call_block_time >= now() - interval '30' day`: 仅选择过去 30 天内的记录。
>
> - **`union all`**:
>   - 将来自两个不同表的结果合并为一个数据集。
>
> ### 2. **主查询**
> 在这个主查询中，我们从 `post_data` 中获取每个用户的发帖数量，并按发帖数量降序排列。
>
> ```sql
> select profile_id,
>     count(*) as post_count
> from post_data
> group by 1
> order by 2 desc
> limit 100
> ```
>
> - **`select profile_id`**: 获取用户 ID。
> - **`count(*) as post_count`**: 统计每个用户的发帖数量。
> - **`from post_data`**: 从之前定义的 CTE `post_data` 中获取数据。
> - **`group by 1`**: 按 `profile_id` 分组，以便计算每个用户的发帖数量。
> - **`order by 2 desc`**: 按 `post_count` 降序排列结果，确保发帖数量最多的用户排在前面。
> - **`limit 100`**: 限制结果为前 100 个用户。
>
> ### 总结
> 这个查询通过结合两个数据源（`LensHub_call_post` 和 `LensHub_call_postWithSig`），获取过去 30 天内的发帖数据，并对每个用户的发帖数量进行统计，帮助识别在该时间段内发帖最多的用户。

我们可以分别添加一个柱状图来显示过去30天内发帖最多的100个账号的发帖数量，同时添加一个Table类型的图表来输出详情。相关图表加入数据看板后的显示效果如下：



![image_12.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051318742.png)



以上查询在Dune上的参考链接：

- https://dune.com/queries/1559981

## 评论数据分析

### 评论最多的账号数据分析

Lens的评论数据与发帖数据类似，按数据产生来源不同，分别保存在`LensHub_call_comment`和`LensHub_call_commentWithSig`表中。基于Lens协议目前的功能，用户必须已经创建了自己的Profile才能对其他人创作者对Post进行评论。在评论数据表中，是通过评论者的Profile ID来进行追踪的。同时，每个创作者的发帖，其编号是从1开始累加的。也就是说，不同创作者的发帖，其编号可能相同。我们需要将创作者的Profile ID 和其Publication ID关联起来这样才能得到唯一的编号。SQL如下：

```sql
select call_block_time,
    call_tx_hash,
    output_0 as comment_id, -- 评论编号
    json_value(vars, 'lax $.profileId') as profile_id_from, -- 评论者的Profile ID
    json_value(vars, 'lax $.contentURI') as content_url, -- 评论内容链接
    json_value(vars, 'lax $.pubIdPointed') as publication_id_pointed, -- 被评论的Publication ID
    json_value(vars, 'lax $.profileIdPointed') as profile_id_pointed, -- 被评论的创作者的Profile ID
    json_value(vars, 'lax $.profileIdPointed') || '-' || json_value(vars, 'lax $.pubIdPointed') as unique_publication_id  -- 组合生成唯一编号
from lens_polygon.LensHub_call_comment
where call_success = true
limit 10
```



我们同样通过定义额外的CTE来获取总的评论数据，从而可以在同一个查询中输出Counter图表，对比评论最多的1000个账号的评论数据和所有账号的评论数据。将查询结果可视化并加入到数据看板后的显示效果如下：



![image_13.png](https://www.wtf.academy/assets/images/image_13-9ed6421c644f25e5638335d528ccb9ae.png)



以上查询在Dune上的参考链接：

- https://dune.com/queries/1560028

### 评论最多的Publication统计

每个评论都是针对一个具体的对象（Publication）（这里作者认为应该就是Post，如有理解错误敬请指正）。分析被评论最多的Publication就具有一定的价值。我们编写一个查询来统计前500个被评论最多的Publication，同时将其与所有评论数据进行对比。SQL如下：

```sql
with comment_data as (
    -- get comment data from LensHub_call_comment and LensHub_call_commentWithSig tables
)

select profile_id_pointed,
    publication_id_pointed,
    unique_publication_id,
    count(*) as comment_count
from comment_data
group by 1, 2, 3
order by 4 desc
limit 500
```



如法炮制，我们添加额外的CTE来获取全部评论的数据，并将上面统计的前500个评论最多的Publication的数据与全局数据进行对比。添加相应的可视化图表到数据看板，效果如下：



![image_14.png](https://www.wtf.academy/assets/images/image_14-13991dbbad3804df3f8f2d9103c30d54.png)



以上查询在Dune上的参考链接：

- https://dune.com/queries/1560578

## 镜像数据分析

镜像数据与评论数据高度相似，用户也必须先创建自己的Profile才能镜像其他人的Publication。我们分别编写两个查询，统计出镜像操作最多的前1000个账号数据和前500个被镜像最多的Publication数据。同样将它们跟整体镜像数据进行对比。加入数据看板后的效果如下图所示：



![image_15.png](https://www.wtf.academy/assets/images/image_15-78be0c67cb9f609e9034b4cd64b605f6.png)



以上查询在Dune上的参考链接：

- https://dune.com/queries/1561229
- https://dune.com/queries/1561558

## 收藏数据分析

Lens的收藏数据同样分别保存在`LensHub_call_collect`和`LensHub_call_collectWithSig`这两个表里。与评论或镜像数据有所不同的是，收藏一个Publication时并不要求收藏者拥有自己的Lens Profile。也就是说，任何地址（用户）都可以收藏其他Profile下的Publication。所以我们要通过收藏者的地址来跟踪具体的收藏操作。特别之处在于，在`LensHub_call_collect`表中并没有保存收藏者的地址数据，`LensHub_call_collectWithSig`表中则有这个数据。我们需要从`LensHub_call_collect`表关联到`transactions`表，获取当前操作收藏的用户地址。SQL示例如下：

```sql
select call_block_time,
    t."from" as collector,
    c.profileId as profile_id,
    c.pubId as publication_id,
    cast(c.profileId as varchar) || '-' || cast(c.pubId as varchar) as unique_publication_id,
    c.output_0 as collection_id
from lens_polygon.LensHub_call_collect c
inner join polygon.transactions t on c.call_tx_hash = t.hash -- 关联交易表获取用户地址
where call_block_time >= date('2022-05-18') -- Lens合约的发布日期，提升查询效率
    and block_time >= date('2022-05-18')
    and c.call_success = true
limit 10
```

> [!TIP]
>
> 这段 SQL 查询的目的是从 Lens 协议的数据中提取收藏活动（`collect`）的相关信息，并关联到 Polygon 区块链上的交易表以获取更详细的用户地址信息。以下是对代码的分步解析：
>
> ### 1. **选择字段**
>
> ```sql
> select call_block_time,
>     t."from" as collector,
>     c.profileId as profile_id,
>     c.pubId as publication_id,
>     cast(c.profileId as varchar) || '-' || cast(c.pubId as varchar) as unique_publication_id,
>     c.output_0 as collection_id
> ```
>
> - **`call_block_time`**：指收藏操作发生的区块时间，记录该操作在哪个时间点进行。
> - **`t."from" as collector`**：来自 `polygon.transactions` 表中的 `from` 字段，表示执行收藏操作的用户地址，别名为 `collector`。
> - **`c.profileId as profile_id`**：Lens 协议中，表示被收藏的内容的创作者的 Profile ID。
> - **`c.pubId as publication_id`**：Lens 协议中的 Publication ID，表示被收藏的具体作品的唯一标识符。
> - **`cast(c.profileId as varchar) || '-' || cast(c.pubId as varchar) as unique_publication_id`**：通过将 `profileId` 和 `pubId` 组合成一个字符串，以创建一个唯一的标识符 `unique_publication_id`，用来唯一标识被收藏的内容。
> - **`c.output_0 as collection_id`**：Lens 协议中生成的 `collection_id`，表示具体的收藏操作的唯一 ID。
>
> ### 2. **数据来源**
>
> ```sql
> from lens_polygon.LensHub_call_collect c
> inner join polygon.transactions t on c.call_tx_hash = t.hash
> ```
>
> - **`lens_polygon.LensHub_call_collect c`**：从 `LensHub_call_collect` 表中提取 Lens 收藏操作的数据，表的别名为 `c`。
> - **`polygon.transactions t`**：通过 `inner join` 关联 Polygon 网络上的交易表 `transactions`，别名为 `t`。
> - **`on c.call_tx_hash = t.hash`**：通过 `call_tx_hash`（交易哈希）关联两个表，以获取更多的交易信息，如交易发起者的地址 `from`，即用户地址。
>
> ### 3. **过滤条件**
>
> ```sql
> where call_block_time >= date('2022-05-18') -- Lens合约的发布日期，提升查询效率
>     and block_time >= date('2022-05-18')
>     and c.call_success = true
> ```
>
> - **`call_block_time >= date('2022-05-18')`**：过滤条件，用于获取 `2022-05-18` 之后发生的收藏操作，这个日期是 Lens 协议的发布日，过滤掉不必要的数据从而提高查询效率。
> - **`block_time >= date('2022-05-18')`**：同样的过滤条件，适用于区块时间 `block_time`，确保只查询 2022-05-18 之后的交易。
> - **`c.call_success = true`**：仅选择成功执行的收藏操作，避免不必要的错误或失败交易。
>
> ### 4. **结果限制**
>
> ```sql
> limit 10
> ```
>
> - **`limit 10`**：限制返回的结果集为 10 条记录，目的是控制结果数量，方便调试或快速获取部分数据。
>
> ### 总结
> 这段 SQL 查询通过从 `LensHub_call_collect` 表中提取 Lens 协议上的收藏操作数据，并通过交易哈希与 `polygon.transactions` 表进行关联，从而获得发起收藏操作的用户地址。查询结果包含收藏时间、用户地址、被收藏的内容以及收藏的唯一标识符。过滤条件确保仅检索 2022-05-18 之后的成功收藏操作。

由于交易表记录相当庞大，查询耗时将明显增加。一个经验法则是，能避免针对原始数据表（transactions, logs, traces）的join操作就尽量避免。

收藏数据分析SQL的其他部分跟前面的例子基本相同，这里不再赘述。同样，我们也针对被收藏最多的Publication进行统计分析。相关可视化图片加入数据看板后显示效果如下图所示：



![image_16.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051318204.png)



以上查询在Dune上的参考链接：

- https://dune.com/queries/1560847
- https://dune.com/queries/1561009

## 关注数据分析

### 关注最多的Profile数据

Lens协议的关注数据仍然是分别保存在`LensHub_call_follow`和`LensHub_call_followWithSig`两个表里。任何地址（用户）都可以关注其他Profile。与收藏类似，`LensHub_call_follow`表里没有保存关注者的地址，所以我们也需要通过关联到`transactions`表来获取当前操作收藏的用户地址。另外，关注还有一个特殊的地方，就是一个交易里面可以同时批量关注多个Profile。`LensHub_call_follow`表中，被关注的Profile数据保存在数组类型字段`profileIds`里，这个相对容易处理。而表`LensHub_call_followWithSig`中，则是JSON字符串格式里面的数组值。其中字段`vars`的一个实例如下（部分内容做了省略）：

```json
{"follower":"0xdacc5a4f232406067da52662d62fc75165f21b23","profileIds":[21884,25271,39784],"datas":["0x","0x","0x"],"sig":"..."}
```



使用Dune SQL的JSON函数，可以从JSON字符串中读取数组值。我们可以先使用`json_extract()`从json 字符串中提取需要的元素值，再使用`cast()`方法将其转换为指定类型的数组。示例代码如下：

```sql
select
json_query(vars, 'lax $.follower') AS follower, -- single value
json_query(vars, 'lax $.profileIds') AS profileIds, -- still string
from_hex(cast(json_extract(vars,'$.follower') as varchar)) as follower2, -- cast to varbinary
cast(json_extract(vars,'$.profileIds') as array(integer)) as profileIds2, -- cast to array
vars
from lens_polygon.LensHub_call_followWithSig
where cardinality(output_0) > 1
limit 10
```

> [!TIP]
>
> 这段 SQL 查询的目的是从 `lens_polygon.LensHub_call_followWithSig` 表中提取与关注操作相关的数据，特别是与用户关注者和关注的个人资料 ID 相关的信息。以下是对每一部分代码的详细解析：
>
> ### 1. **选择字段**
>
> ```sql
> select
> json_query(vars, 'lax $.follower') AS follower, -- single value
> json_query(vars, 'lax $.profileIds') AS profileIds, -- still string
> from_hex(cast(json_extract(vars,'$.follower') as varchar)) as follower2, -- cast to varbinary
> cast(json_extract(vars,'$.profileIds') as array(integer)) as profileIds2, -- cast to array
> vars
> ```
>
> - **`json_query(vars, 'lax $.follower') AS follower`**：
>   - 使用 `json_query` 函数从 `vars` JSON 对象中提取 `follower` 字段，并将其命名为 `follower`。
>   - 这个字段可能包含某个用户的关注者信息，提取结果为单个值。
>
> - **`json_query(vars, 'lax $.profileIds') AS profileIds`**：
>   - 从 `vars` JSON 对象中提取 `profileIds` 字段，并将其命名为 `profileIds`。
>   - 提取的结果依然是一个字符串，可能是一个以某种格式编码的数组。
>
> - **`from_hex(cast(json_extract(vars,'$.follower') as varchar)) as follower2`**：
>   - 先使用 `json_extract` 提取 `follower` 字段（结果为字符串），然后将其转换为 `varchar` 类型。
>   - 接着用 `from_hex` 函数将十六进制字符串转换为二进制格式，结果命名为 `follower2`。
>
> - **`cast(json_extract(vars,'$.profileIds') as array(integer)) as profileIds2`**：
>   - 使用 `json_extract` 提取 `profileIds` 字段（同样为字符串），并将其转换为 `array(integer)` 类型。
>   - 这个字段的转换将字符串表示的数组转换为实际的整数数组，结果命名为 `profileIds2`。
>
> - **`vars`**：
>   - 直接选择 `vars` 字段，可以查看原始的 JSON 数据。
>
> ### 2. **数据来源**
>
> ```sql
> from lens_polygon.LensHub_call_followWithSig
> ```
> - 从 `lens_polygon.LensHub_call_followWithSig` 表中提取数据，这个表存储有关关注操作的信息，通常包含关注者、被关注者以及相关的交易信息。
>
> ### 3. **过滤条件**
>
> ```sql
> where cardinality(output_0) > 1
> ```
> - **`cardinality(output_0) > 1`**：这个条件确保只选择 `output_0` 字段中元素数量大于 1 的记录。`cardinality` 函数用于获取数组或集合的元素数量，这里可能是为了确保至少有两个关注者或被关注的个人资料。
>
> ### 4. **结果限制**
>
> ```sql
> limit 10
> ```
> - **`limit 10`**：限制查询结果返回的行数为 10 条，以便快速查看结果或进行调试。
>
> ### 总结
>
> 这段 SQL 查询从 Lens 协议的 `LensHub_call_followWithSig` 表中提取关注操作的相关信息，包括关注者和关注的个人资料 ID。查询使用了 JSON 函数提取和转换字段，并包含了用于过滤的条件和结果的限制，以确保返回的数据是相关且可用的。具体提取的字段包括原始的 JSON 数据、处理后的关注者和个人资料 ID 的数组等。

读取关注详情的完整SQL代码如下：

```sql
with follow_data as (
    select f.follower, p.profile_id
    from (
        select from_hex(cast(json_extract(vars,'$.follower') as varchar)) as follower, -- cast to varbinary
            cast(json_extract(vars,'$.profileIds') as array(integer)) as profile_ids -- cast to array
        from lens_polygon.LensHub_call_followWithSig
            
        union all
        
        select t."from" as follower,
            cast(f.profileIds as array(integer)) as profile_ids
        from lens_polygon.LensHub_call_follow f
        inner join polygon.transactions t on f.call_tx_hash = t.hash
        where call_block_time >= date('2022-05-18') -- Lens launch date
            and block_time >= date('2022-05-18')
            and call_success = true
    ) f
    cross join unnest(f.profile_ids) as p(profile_id)
)

select * from follow_data
limit 100
```

这里需要说明一下，我们使用了`cross join unnest(f.profile_ids) as p(profile_id)`子句，将子查询中的数组进行拆解，并获取拆开的单个ID值。同时，因为`lens_polygon.LensHub_call_follow`表中的元素类型为`uint256`，这是一个Dune 的自定义类型，我们无法在从json字符串提取值时使用这个类型，所以我们==用`cast(f.profileIds as array(integer))`将`uint256`转换为`integer`类型==。

> [!TIP]
>
> 这段 SQL 查询的目的是从 LensHub 合约中提取与关注操作相关的数据，具体是关于关注者及其所关注的个人资料 ID。下面是对这段代码的逐段解析：
>
> ### 1. **CTE: follow_data**
>
> ```sql
> with follow_data as (
>     select f.follower, p.profile_id
>     from (
>         select from_hex(cast(json_extract(vars,'$.follower') as varchar)) as follower, -- cast to varbinary
>             cast(json_extract(vars,'$.profileIds') as array(integer)) as profile_ids -- cast to array
>         from lens_polygon.LensHub_call_followWithSig
>             
>         union all
>         
>         select t."from" as follower,
>             cast(f.profileIds as array(integer)) as profile_ids
>         from lens_polygon.LensHub_call_follow f
>         inner join polygon.transactions t on f.call_tx_hash = t.hash
>         where call_block_time >= date('2022-05-18') -- Lens launch date
>             and block_time >= date('2022-05-18')
>             and call_success = true
>     ) f
>     cross join unnest(f.profile_ids) as p(profile_id)
> )
> ```
>
> #### a. **选择关注者和个人资料 ID**
>
> - **`with follow_data as (...)`**：
>   - 创建一个名为 `follow_data` 的公共表表达式（CTE），用于存储关注者及其所关注的个人资料 ID。
>
> #### b. **内部查询：提取关注者和个人资料 IDs**
>
> - **第一部分：**
>
> ```sql
> select from_hex(cast(json_extract(vars,'$.follower') as varchar)) as follower, 
>        cast(json_extract(vars,'$.profileIds') as array(integer)) as profile_ids
> from lens_polygon.LensHub_call_followWithSig
> ```
>
> - 使用 `json_extract` 函数从 `vars` 字段提取 `follower` 和 `profileIds`，然后将 `follower` 转换为 `varbinary` 类型，将 `profileIds` 转换为整数数组。
> - 这个部分从 `lens_polygon.LensHub_call_followWithSig` 表中提取数据，通常是通过签名的关注操作。
>
> - **第二部分：**
>
> ```sql
> select t."from" as follower,
>        cast(f.profileIds as array(integer)) as profile_ids
> from lens_polygon.LensHub_call_follow f
> inner join polygon.transactions t on f.call_tx_hash = t.hash
> where call_block_time >= date('2022-05-18') -- Lens launch date
>     and block_time >= date('2022-05-18')
>     and call_success = true
> ```
>
> - 从 `lens_polygon.LensHub_call_follow` 表中提取关注者信息，使用 `inner join` 将关注操作与交易信息结合起来，以获取关注者的地址（`t."from"`）。
> - 通过 `where` 子句过滤出在 Lens 发布日期之后的成功关注操作。
>
> - **`union all`**：
>   - 将两个部分的结果合并成一个表格，包含关注者及其关注的个人资料 ID。
>
> #### c. **跨连接和展开**
>
> ```sql
> cross join unnest(f.profile_ids) as p(profile_id)
> ```
>
> - **`cross join unnest(f.profile_ids) as p(profile_id)`**：
>   - 使用 `cross join` 和 `unnest` 函数将 `profile_ids` 数组中的每个元素展开为单独的行。这样，每个关注者将对应其所关注的个人资料 ID。
>   - 结果是一个包含关注者和他们所关注的每个个人资料 ID 的数据集。
>
> ### 2. **选择数据**
>
> ```sql
> select * from follow_data
> limit 100
> ```
>
> - **`select * from follow_data`**：
>   - 从 `follow_data` CTE 中选择所有列，结果包括关注者和他们所关注的个人资料 ID。
>
> - **`limit 100`**：
>   - 限制查询结果返回的行数为 100 条，以便快速查看结果。
>
> ### 总结
>
> 这段 SQL 查询从 LensHub 的关注操作表中提取关注者和他们所关注的个人资料 ID。通过将两个表（包含签名和未签名的关注操作）中的数据合并，利用 JSON 函数提取所需信息，并将个人资料 IDs 展开，最终得到了一个包含关注者及其关注对象的清晰视图。这种结构使得分析和使用关注数据变得更加容易。

同样，我们也在上面的查询基础上添加获取全部关注数据的CTE定义，从而可以在取得最多关注的Proile列表时，将其与整体关注数量进行对比。查询结果可视化并加入数据看板后的效果如下：



![image_17.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051318223.png)



以上查询在Dune上的参考链接：

- https://dune.com/queries/1554454

### 按关注数量范围统计Profile分布

我们看到几乎绝大部分Profile都有被关注，我们可以用一个查询来对各Profile的关注量的分布情况做一个分析。SQL代码如下：

```sql
with follow_data as (
    -- Get follow data from table LensHub_call_follow and LensHub_call_followWithSig
),

profile_follower as (
    select profile_id,
        count(follower) as follower_count
    from follow_data
    group by 1
)

select (case when follower_count >= 10000 then '10K+ Followers'
            when follower_count >= 1000 then '1K+ Followers'
            when follower_count >= 100 then '100+ Followers'
            when follower_count >= 50 then '50+ Followers'
            when follower_count >= 10 then '10+ Followers'
            when follower_count >= 5 then '5+ Followers'
            else '1 - 5 Followers'
        end) as follower_count_type,
    count(profile_id) as profile_count
from profile_follower
group by 1
```



将以上查询结果使用一个Pie chart饼图进行可视化。加入到数据看板后到显示效果如下图所示：



![image_18.png](https://www.wtf.academy/assets/images/image_18-978434168e2b0fc4359811bbc1eddcea.png)



以上查询在Dune上的参考链接：

- https://dune.com/queries/1554888

### 每日新增关注数量统计

Lens用户每日的新增关注数量也是观察整体活跃度变化的一个重要指标，我们编写一个查询来统计每天的发帖数量。这个查询中的`follow_data` CTE与之前的完全相同。查询处理方式也与前面讲过的每日发帖数量统计高度相似，这里不再详述细节。给查询结果添加可视化图表并将其加入数据看板，显示效果如下：



![image_19.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051318274.png)



以上查询在Dune上的参考链接：

- https://dune.com/queries/1555185

## 创作者操作综合分析

结合前述内容可以看出，创作者（拥有Profile的用户）可以发帖（Post）、评论（Comment）或者镜像（Mirror）其他创作者的数据，而普通用户（未创建Profile）则可以关注（Follow）创作者和收藏创作者发布的作品（Publication）。所以我们可以将创作者可以操作的数据合并到一起来进行综合分析。

我们定义一个`action_data` CTE，在其内部使用嵌套定义CTE的方式将相关数据集中到一起，其中post_data、comment_data和mirror_data都分别跟前面相关查询里面的定义完全相同。我们使用union all将以上数据合并到一起，同时分布指定对应的动作类型，生成一个用于分类的字段`action_type`。然后我们只需按照分类字段进行汇总统计即可计算出每种操作类型的交易数量和相应的Profile数量。SQL示例如下：

```sql
with action_data as (
    with post_data as (
        -- get post data from relevant tables
    ),
    
    comment_data as (
        -- get comment data from relevant tables
    ),
    
    mirror_data as (
        -- get mirror data from relevant tables
    )
 
    select 'Post' as action_type, * from post_data
    union all
    select 'Mirror' as action_type, * from mirror_data
    union all
    select 'Comment' as action_type, * from comment_data
)

select action_type,
    count(*) as transaction_count,
    count(distinct profile_id) as profile_count
from action_data
group by 1
```

> [!TIP]
>
> 这段 SQL 查询的目的是汇总来自不同社交媒体活动（例如发布、评论和镜像）的数据，并对这些活动进行计数，以分析每种活动的数量和参与的用户数量。以下是对代码的逐段解析：
>
> ### 1. **CTE: action_data**
>
> ```sql
> with action_data as (
>     with post_data as (
>         -- get post data from relevant tables
>     ),
>     
>     comment_data as (
>         -- get comment data from relevant tables
>     ),
>     
>     mirror_data as (
>         -- get mirror data from relevant tables
>     )
>  
>     select 'Post' as action_type, * from post_data
>     union all
>     select 'Mirror' as action_type, * from mirror_data
>     union all
>     select 'Comment' as action_type, * from comment_data
> )
> ```
>
> - **`with action_data as (...)`**：
>   - 创建一个名为 `action_data` 的公共表表达式（CTE），用于整合来自不同社交媒体活动的数据。
>
> - **`post_data`, `comment_data`, `mirror_data`**：
>   - 这些 CTE（尚未实现的部分）将分别从相关表中提取发布、评论和镜像数据。每个 CTE 的具体实现未提供，但预期会包含关于每个活动的详细信息。
>
> - **`select 'Post' as action_type, * from post_data`**：
>   - 从 `post_data` 中选择所有字段，并添加一个名为 `action_type` 的新列，值为 `'Post'`，用于标识该行记录为“发布”。
>
> - **`union all`**：
>   - 合并来自不同活动的结果集。`union all` 确保保留所有记录，包括重复的。
>
> - **`select 'Mirror' as action_type, * from mirror_data`**：
>   - 类似于上面，对 `mirror_data` 的结果进行处理，将 `action_type` 设置为 `'Mirror'`。
>
> - **`select 'Comment' as action_type, * from comment_data`**：
>   - 对 `comment_data` 的结果进行处理，将 `action_type` 设置为 `'Comment'`。
>
> ### 2. **最终查询**
>
> ```sql
> select action_type,
>     count(*) as transaction_count,
>     count(distinct profile_id) as profile_count
> from action_data
> group by 1
> ```
>
> - **`select action_type`**：
>   - 选择 `action_type` 列，以便区分不同类型的活动。
>
> - **`count(*) as transaction_count`**：
>   - 计算每种活动类型的总交易数量。
>
> - **`count(distinct profile_id) as profile_count`**：
>   - 计算每种活动类型中独特用户的数量，即参与该活动的不同用户数量。
>
> - **`from action_data`**：
>   - 从 `action_data` CTE 中选择数据。
>
> - **`group by 1`**：
>   - 根据 `action_type` 进行分组，以便为每种活动类型返回统计结果。
>
> ### 总结
>
> 这段 SQL 查询整合了来自发布、评论和镜像活动的数据，并对这些活动进行了汇总。通过计数每种活动的总数量和参与的用户数量，能够更清晰地了解社交媒体平台上的用户行为和互动情况。这种汇总可以用于分析用户参与度，评估不同类型活动的受欢迎程度等。

我们可以用相似的方法，新建一个按日期汇总每日各种操作数量的查询。示例代码如下：

```text
with action_data as (
    -- same as above query
)

select date_trunc('day', call_block_time) as block_date,
    action_type,
    count(*) as transaction_count
from action_data
group by 1, 2
order by 1, 2
```



将以上查询结果可视化并加入数据看板，显示效果如下：



![image_20.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051319387.png)



以上查询在Dune上的参考链接：

- https://dune.com/queries/1561822
- https://dune.com/queries/1561898

## 普通用户操作综合分析

与创作者类似，我们可以将普通用户可执行的关注和收藏操作合并到一起进行分析。我们同样编写两个查询，分别统计总体的操作分布和按日期的操作数量。查询里面的`action_data`数据同样来源于前面介绍过的收藏查询和关注查询，其SQL示例如下：

```sql
with action_data as (
    with follow_data as (
        -- get follow data from relevant tables
    ),
    
    collect_data as (
        -- get collect data from relevant tables
    )

    select 'Follow' as action_type, * from follow_data
    union all
    select 'Collect' as action_type, * from collect_data
)
```



除了数据来源不同，这两个查询与创作者操作综合分析基本相同。将查询结果可视化并加入数据看板，显示效果如下：



![image_21.png](https://cdn.jsdelivr.net/gh/zey9991/mdpic/202410051319476.png)



以上查询在Dune上的参考链接：

- https://dune.com/queries/1562000
- https://dune.com/queries/1562178

## 总结与作业

非常好！我们已经完成了对Lens协议的整体分析。不过，由于篇幅问题，仍然有很多值得分析的指标我们尚未涉及，包括但不限于：三种NFT的相关数据分析、创作者的收益分析、Profile账号的转移情况分析等。这部分留给大家去继续探索。

请结合教程内容，继续完善你自己的Lens协议数据看板，你可以Fork本教程的查询去修改，可以按自己的理解做任何进一步的扩展。请大家积极动手实践，创建数据看板并分享到社区。我们将对作业完成情况和质量进行记录，之后追溯为大家提供一定的奖励，包括但不限于Dune社区身份，周边实物，API免费额度，POAP，各类合作的数据产品会员，区块链数据分析工作机会推荐，社区线下活动优先报名资格以及其他Sixdegree社区激励等。