---
timezone: UTC+8
---

# yogurt2333

**GitHub ID:** yogurt2333

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-28
<!-- DAILY_CHECKIN_2026-05-28_START -->
## 今日完成

### 1\. 项目初步 Proposal ✅

-   完成 AI Guard Wallet 项目提案（`hackathon/project-proposal.md`）
    
-   三个场景：安全转账（MVP）/ DCA 定投（扩展）/ 紧急冻结（安全）
    
-   一句话定位：不只帮你做、还能跟你说清楚——让非技术用户在理解中参与决策
    

### 2\. 补读 Cobo CAW + ERC-4337 ✅

-   Cobo CAW：Pact 机制（Intent/Plan/Policies/Completion）、MPC 签名、3 阶段策略引擎
    
-   ERC-4337：UserOperation / EntryPoint / Bundler / Paymaster / Factory 概念
    
-   **决策：** MVP 阶段用 Cobo CAW MPC + Pact 即可，ERC-4337 后续扩展
    

### 3\. 流程图 ✅

-   Excalidraw 7 步安全弧流程图（已上传可分享）
    

### 4\. 确认了三个关键认知

-   **风险边界：** Agent 是提议者+执行者，永远不是决策者
    
-   **知情同意：** 确认界面不是死板的信息展示，可以追问
    
-   **MVP 原则：** 宁可让用户多点一次确认，也不让 Agent 越权
    

## 问题 / Blocker

-   暂无，今晚三人开会对齐后进入 Week 3 开发排期
    

## 明日计划

-   三人同步会，对齐方向和分工
    
-   确认 Cobo CAW 开发者注册
    
-   Week 3 开发排期
    

## 学习时间

~3h（提案构思 + 文档阅读 + 流程图 + 材料整理）
<!-- DAILY_CHECKIN_2026-05-28_END -->

# 2026-05-27
<!-- DAILY_CHECKIN_2026-05-27_START -->

**问题地图** 扫了全部 6 个方向

**主方向选择** Wallet / Permission，写了为什么不是纯 AI / 不是纯 Web3

**真实用户** 持币但不懂技术的普通人

**问题拆解** 7 步流程图 + 参与方 + AI vs Web3 分工 + 自动化边界 + 风险对策

**Next Steps** 明天出 proposal + 补 Cobo CAW + ERC-4337
<!-- DAILY_CHECKIN_2026-05-27_END -->

# 2026-05-26
<!-- DAILY_CHECKIN_2026-05-26_START -->


**1.Obsidian = RAG** 的顿悟 — 自己的笔记系统本质上就是检索+生成，打算做个 Obsidian Agentic RAG

**2.🚀 部署并验证了首个 Solidity 合约到 Sepolia**

\- 合约: `HelloWorld` — 存储+修改消息

\- 地址: `0x11eA5B31C313aE5DA3C224EfAff57CdE6B1aDF18`\]([https://sepolia.etherscan.io/address/0x11eA5B31C313aE5DA3C224EfAff57CdE6B1aDF18](https://sepolia.etherscan.io/address/0x11eA5B31C313aE5DA3C224EfAff57CdE6B1aDF18))

\- 状态: ✅ 编译 ✅ 部署 ✅ Etherscan 验证通过

\- 踩坑: Hardhat v2 vs v3、Node.js 版本兼容、PowerShell 语法、Etherscan 验证字节码匹配

3\. **调研了 Cobo Agentic Wallet** — MPC 非托管 + Pact 协议 + Recipe 技能层的 AI Agent 钱包，跟我的 AdventureX 方向直接相关
<!-- DAILY_CHECKIN_2026-05-26_END -->

# 2026-05-24
<!-- DAILY_CHECKIN_2026-05-24_START -->



\### ✅ 完成：Vibe Coding 架构设计

今天凌晨我们把 vibe coding 的分层架构落地成文档了，存在 `plans/vibe-coding-architecture.md`。

**核心架构（三层）：**

层 谁 模型 干啥

**调度层** Hermes（我） DeepSeek v4（便宜） 规划、答疑、启动 agent、总结

**执行层** OpenCode DeepSeek v4 Pro（强） 写代码、改文件、跑命令

**展示层** VSCode + tmux 无 你 SSH attach 看一手输出

**关键决策已落地：**

\- ✅ Code Agent 选 **OpenCode + DeepSeek v4 Pro**（零摩擦起步，后续无缝切 Claude）

\- ✅ 代码同步用 **VSCode Remote SSH**（零推拉，就像本地文件）

\- ✅ 信息流模式：我不当传话筒 → 规划阶段我介入，执行阶段你直接跟 agent 对话

\- ✅ 成本估算：按 vibe coding 强度月费 ≈ **¥10-30**

**待完成（还没实施的）：**

\- ⬜ 服务器装 tmux

\- ⬜ 安装 OpenCode CLI

\- ⬜ 配置 DeepSeek API Key

\- ⬜ 试跑一次端到端
<!-- DAILY_CHECKIN_2026-05-24_END -->

# 2026-05-22
<!-- DAILY_CHECKIN_2026-05-22_START -->




\### Web3 基础 — 过了一遍

章节 核心收获

🌐 **Network** 区块是批量提交，共识决定历史有效性，L2 更便宜但也更复杂

🔐 **Cryptography** 哈希防篡改、私钥=控制权、签名≠登录、Merkle Tree 高效验证

👛 **Wallet** EOA 限制多、三类动作风险不同、gas 要讲清楚、explorer 可自证

📜 **Smart Contract** 链上程序、EVM 执行环境、ABI 是接口说明书、Event 可索引日志

🏗️ **Account Abstraction** 权限从"有私钥/没私钥"变成"什么条件下允许什么动作"，Session Key 是 Agent Wallet 的核心

\### 穿插知识点

\- **Harness Engineering** — The harness beats the model（记到 Obsidian 了）

\- **MCP vs Function Calling** — FC 是"格式"，MCP 是"完整协议"，互补不互替

\- **游戏自动化** — Cradle / UI-TARS 两条路线
<!-- DAILY_CHECKIN_2026-05-22_END -->

# 2026-05-21
<!-- DAILY_CHECKIN_2026-05-21_START -->





🧭 2026 核心趋势 Agents with Wallets — Agent 自己管钱自己花

📦 项目全景表 基础设施层 / 钱包支付层 / 应用层，每个都有简介

🔥 Base 链生态 目前 Agent 项目最活跃的 L2

🎯 AdventureX 方向建议 3 个具体方向，标明了你和哥们的分工

⚠️ 冷水/批判 安全风险、Agent 智能本质、入口依赖 Web2 等问题

🔗 参考链接 今天提到的文章/视频链接全汇总

🐸 今天吃了好吃的牛蛙 是第一次吃
<!-- DAILY_CHECKIN_2026-05-21_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->






Web3 底层原理

**交易生命周期：** 本机签名 → RPC 广播 → 内存池排队（gas高优先）→ Builder打包 → 验证者共识 → 上链 → 12min Safe → 18min Finalized

**密钥体系：** 私钥=资产控制权，签名在本地，不出门。公钥截后40位=地址。改了签名内容→ec\_recover对不上→节点拒绝

**Gas费：** 基础费🔥销毁（通缩）+ 小费💰给验证者（插队用）

**EVM：** 不跑在某个服务器，跑在每个全节点自己的电脑上。像浏览器各自跑JS渲染 → 所有节点各自跑EVM，结果一致才共识

**智能合约：** 代码部署到链上自动执行，不可篡改。条件不满足→revert回滚

**L2：** L1太慢太贵→L2在链下处理，只交结果到L1。Optimistic（等7天挑战）vs ZK（数学证明立刻确认）

**公链 vs 私链：** 公链任何人可读写，私链授权用户。跨链=连接不同链的桥

**DApp架构：** Vue/React + ethers.js调合约 = 把调API换成调链上函数

**为什么谈Web3必须谈经济：** 区块链信任不靠代码，靠经济博弈。验证者押32ETH ≈ 作恶成本>收益
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->







\## 📋 5月19日学习总结

\### ✅ 已完成

\# 事项 备注

1️⃣ **安装 MetaMask** 手机/浏览器装好，搞定地址 0xED38…a5

2️⃣ **切换到 Sepolia 测试网** 找到了测试网络切过去

3️⃣ **领到测试币** 各 faucet 都挡了（要主网余额），找社群老哥薅到了 🧑‍🤝‍🧑

4️⃣ **🔑 发人生第一笔链上交易** 转了 0.1 ETH 给小伙伴，nonce=0（第一笔处女秀）

5️⃣ **用 RPC 查交易** 拿到了完整的交易原始数据

6️⃣ **学了一堆概念** TxHash / Nonce / Gas / EIP-1559 / Base Fee vs Tip / Burn
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->








📅 今天（Day 1）我干了什么

时间段 做的事 状态

🛠️ 下午 初始化 learning agent、装 gh、建 GitHub repo ✅

📚 下午 获取 Week1 完整课程大纲、更新学习计划 ✅

🏦 下午-晚上 学 Web2 vs Web3 支付区别 ✅

🗣️ 晚上 参加 tc 老师分析会、消化 Web3 术语（EVM/多签/AA/Nonce/Gas/TEE） ✅

🔧 晚上 修好本机 Obsidian Git 插件同步 ✅

累计投入

⏱️ 约 **95 分钟**

其实已经在bootcomp之前部署过Hermes agent了 今天补足一些开发环境部分 明天的任务是装 MetaMask + 测试网交互
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
