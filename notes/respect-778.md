---
timezone: UTC+8
---

# respect-778

**GitHub ID:** respect-778

**Telegram:** @LXYrespect778

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->
今天学习的主题是 **Web3 运行原理**，主要围绕“从钱包到出块，从应用到协议”展开。课程的核心目标是从第一性原理理解 Web3 是如何真正运行起来的，而不是只停留在概念层面。PPT 中提到，本次内容包括钱包、私钥、交易签名、区块链网络运行、智能合约、协议升级以及 Web3 的关键特性。([Google Docs](https://docs.google.com/presentation/d/1801G_C_1CC1n-Ef6hON7w5-rP7VHhnxoA9l7adwSZ9M/htmlpresent))

首先，我对钱包、私钥和地址之间的关系有了更清晰的理解。钱包本身并不是存放资产的地方，它主要负责管理密钥、构造交易和发起签名；真正的余额、NFT 和合约状态都记录在链上。也就是说，钱包更像是一把“钥匙管理工具”，而区块链才是真正保存账本和状态的地方。([Google Docs](https://docs.google.com/presentation/d/1801G_C_1CC1n-Ef6hON7w5-rP7VHhnxoA9l7adwSZ9M/htmlpresent))

其次，我理解了交易并不只是简单的转账。一次交易本质上是一段“我授权网络执行某件事”的数据，它可以是转账，也可以是调用合约、mint NFT、投票或者授权等操作。交易中通常会包含 Gas、Nonce 和签名等信息，其中签名用来证明这笔操作确实是由对应私钥授权发起的。([Google Docs](https://docs.google.com/presentation/d/1801G_C_1CC1n-Ef6hON7w5-rP7VHhnxoA9l7adwSZ9M/htmlpresent))

在区块链网络运行部分，我学习到一笔交易的大致流程是：钱包本地签名后，通过 RPC 或节点广播到网络中，随后进入 Mempool 等待排序，再由 Builder 和 Validator 参与打包、出块和证明，最终写入区块并可以在区块浏览器中查询。这个过程让我明白，Web3 的一次点击确认，背后其实包含了身份验证、交易传播、排序、执行和确认等多个步骤。([Google Docs](https://docs.google.com/presentation/d/1801G_C_1CC1n-Ef6hON7w5-rP7VHhnxoA9l7adwSZ9M/htmlpresent))

智能合约部分让我印象比较深。智能合约可以理解为部署在链上、能够被交易触发执行的代码。它并不是“真的有智能”，而是按照预先写好的规则运行。交易触发合约执行后，链上状态会发生改变，并且执行记录会被写入区块，后续可以公开查询。([Google Docs](https://docs.google.com/presentation/d/1801G_C_1CC1n-Ef6hON7w5-rP7VHhnxoA9l7adwSZ9M/htmlpresent))

这次学习让我对 Web3 的理解从“概念层面”更进一步到了“运行机制层面”。我认识到，Web3 的核心不只是区块链技术本身，而是通过密码学保证所有权，通过经济激励协调参与者，再通过共识机制决定规则。后续我还需要继续深入学习交易签名、Gas 机制、RPC 节点、智能合约安全以及链上数据交互等内容，把这些理论和自己的 DApp 项目实践结合起来。
<!-- DAILY_CHECKIN_2026-05-20_END -->
<!-- Content_END -->
