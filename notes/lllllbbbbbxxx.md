---
timezone: UTC+0
---

# lllllbbbbbxxx

**GitHub ID:** lllllbbbbbxxx

**Telegram:** @JuneZhou

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-22
<!-- DAILY_CHECKIN_2026-05-22_START -->
智能合约部署实践

尝试用remix部署了一个简单合约，并结合sepolia和测试钱包完成了读取和写入

部署交易结果：

-   部署 tx：0xf5a20e18d1f6df0ca68ca22a5967e95338d850e58a025c899ccbaf03cc1b63e7
    
-   创建的合约地址：0x4CfBc606D914bd099921b8c18E044425b1537992
    
-   状态：success
    
-   区块：10900495
    
-   部署 Gas：519172
<!-- DAILY_CHECKIN_2026-05-22_END -->

# 2026-05-21
<!-- DAILY_CHECKIN_2026-05-21_START -->

看了智能合约部分的内容，了解了基础知识，明天将尝试部署一个最小合约

账号抽象：现在的传统钱包用户体验不友好，在ai agent的帮助下，很可能能做到让钱包像普通app一样易于操作，当然中间的安全性还是要严格控制
<!-- DAILY_CHECKIN_2026-05-21_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->


今日计划：

### 1.把 Hermes Agent 接入 Telegram

在telegram里搜索botfather和user info，获得token和ID，存入Hermes的.env中，打开和bot的聊天，随便发一句进行测试，发现需要设置/sethome，设置完后可成功运行

### 2.创建测试钱包并试用

下载了metamask，创建了测试钱包，用纸笔记录了助记词和密钥；

用 Sepolia faucet领取了一笔测试币，成功接收，交易细节写入logs/[test-wallet.md](http://test-wallet.md)，没有写上助记词等敏感信息；

在metamask上自己给自己做了一笔测试网转账并记录了交易哈希
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->



今天学习了 Web3 的账户和钱包基础，重点理解了 Account、Address、Wallet、Private Key、Seed Phrase 和 Signature。

了解了为什么区块链能在不依赖单一中心化担保方，通过通过密码学和和公开可验证的账本，让参与者可以验证状态和交易的真实性。

通过哈希验证数据完整性，Merkle Tree可以快速验证大规模数据；

钱包负责保存私钥、本地加密、本地签名、广播交易；

web3的UX比起web2有很多需要格外注意到地方，因为用户需要理解一些复杂的概念，而当前的UX很大程度上把复杂的理解成本转接给用户。

接下来准备创建一个测试钱包，发送一笔转账，了解web3交易流程
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->




创建了个人GitHub repo作为学习区[https://github.com/lllllbbbbbxxx/web3-ai-learning](https://github.com/lllllbbbbbxxx/web3-ai-learning)

配置了Hermes Agent，生成了个人学习计划
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
