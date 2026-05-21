---
timezone: UTC+8
---

# yrdgjuddgj

**GitHub ID:** yrdgjuddgj

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-22
<!-- DAILY_CHECKIN_2026-05-22_START -->
### 比较 EOA、智能账户、多签在权限控制和自动化执行上的差异

EOA 是最基础的钱包账户，由单个私钥控制。它简单、兼容性好，但权限控制能力弱，一旦私钥丢失或泄露，资产会面临严重风险。EOA 不适合直接交给 AI Agent 自动执行链上操作，因为 AI 一旦接触私钥，就拥有完整控制权。

智能账户通过智能合约定义账户逻辑，可以支持权限分级、每日限额、白名单、Session Key、社交恢复、Gas 代付和批量交易。相比 EOA，智能账户更适合 AI × Web3 场景，因为它可以给 AI Agent 分配有限、可撤销、可审计的执行权限，而不是暴露主私钥。

多签账户通常用于团队或高价值资产管理，例如 Safe。它要求多个 owner 中达到一定数量签名后才能执行交易，可以降低单点私钥风险，适合 DAO 金库、项目方合约管理员权限和大额资产管理。但多签不适合高频自动化操作，更适合作为高风险动作的人工确认层。

因此，在 AI × Web3 场景中，比较理想的结构是：EOA 或硬件钱包作为 owner，智能账户作为日常执行账户，Session Key 授权 AI Agent 执行低风险操作，多签或 Safe 负责高价值资产和关键权限确认。

## 模块 C｜最小交叉实验：AI 输出到链上执行

1\. 使用模块 B 的 SimpleStorage 合约

2\. 让 AI 解释合约函数

3\. 让 AI 生成 Remix 操作说明

4\. 你人工检查合约地址、函数、参数和网络

5\. 用 MetaMask 在 Sepolia 上确认写入

6\. 在 Sepolia Etherscan 记录结果

7\. 让 AI 解释交易哈希

8\. 再次用区块浏览器验证 AI 的解释
<!-- DAILY_CHECKIN_2026-05-22_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->

用 Remix 部署一个最小智能合约，在区块浏览器上查看合约部署信息

完成一次最简单的读取操作、写入操作，在区块浏览器上查看合约部署信息
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->


### 创建个人 GitHub repo

[https://github.com/yrdgjuddgj/web3-learning.git](https://github.com/yrdgjuddgj/web3-learning.git)

### 搭建自己的 learning agent

把 Week 1 模块B内容交给 agent，生成核心知识点解释，实践任务完成方式

### 实践：Web3 基础

MetaMask创建测试钱包，领取 Sepolia 测试币，发送一笔测试交易，在区块浏览器中查看交易结果
<!-- DAILY_CHECKIN_2026-05-19_END -->
<!-- Content_END -->
