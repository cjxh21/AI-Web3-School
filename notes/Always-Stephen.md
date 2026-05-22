---
timezone: UTC+8
---

# Always-Stephen

**GitHub ID:** Always-Stephen

**Telegram:** @Stephenalys

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-22
<!-- DAILY_CHECKIN_2026-05-22_START -->
\# Daily Note — 2026-05-22

\## 今日学习：Web3 网络（Network）基础

\- **Handbook**: [https://aiweb3.school/zh/handbook/web3/network/](https://aiweb3.school/zh/handbook/web3/network/)

\- **时间**: ~2h

\- **状态**: ✅ 已完成

\## 核心收获

\### 第一性原理

区块链网络的核心不是"存数据"，而是让\*\*互不信任的参与者对状态变化达成一致\*\*。

| 传统应用 | 链上应用 |

|----------|----------|

| 服务器直接更新数据库 | 交易需节点传播→执行→打包→验证→确认 |

| 即时响应 | 按区块批量推进，有延迟和费用 |

| 信任服务器 | 信任共识机制 |

\### 知识链路

\#### Block（区块）⭐⭐ 初级

\- 区块 = 交易批量提交和排序的单位

\- 三个关键理解：交易有顺序、区块有 gas limit、链式可验证历史

\#### Consensus（共识）⭐⭐ 中级

\- 网络决定"哪段历史有效"的机制

\- 影响：交易需等 confirmation，区块可能重组，RPC 异常时状态延迟

\#### PoS（权益证明）⭐⭐ 中级

\- 用质押+惩罚机制替代 PoW，网络安全来自经济质押

\- 不免费——来自验证者质押 ETH 的真金白银

\#### Testnet（测试网）⭐⭐ 初级

\- 测流程 OK，不能替代主网安全审查

\- 项目记录：部署在哪条网、合约地址、RPC、chain id

\#### L2（二层网络）⭐⭐ 中级

\- 优势：费用低、确认快；代价：桥、提现等待、跨链复杂度

\- 产品设计必须明确当前网络和合约地址

\#### Rollup ⭐⭐⭐ 高级

\- Optimistic vs ZK Rollup：证明方式、提现延迟、数据可用性不同

\- 核心判断：降低单笔成本，但没消除链上系统复杂度

\### AI × Web3 视角

\> Agent 读链上状态时，不能靠模型"猜"。必须返回结构化信息：chain id、RPC、区块高度、确认数、explorer 链接。

\### 最小实践（待完成）

\- \[ \] 测试网领 ETH → 发转账

\- \[ \] 区块浏览器查交易状态、区块号、gas、logs

\- \[ \] 记录 pending→confirmed 耗时

\- \[ \] 切另一条网，观察同一地址差异

\- \[ \] 思考：AI Agent 辅助时，哪些字段必须由工具读取？

\## 产出的可交互产物

\- \[Web3 概念地图\](experiments/web3-concept-map.html) — 10 个概念 + AI × Web3 Bridge 交叉分析

\## 今日活动

\- 🔴 19:00 Co-learning 答疑（Zoom: 891 8275 3424 / 815963）

\- 🔴 20:00 **Week 1 例会**（Zoom: 858 2160 2823 / 330279）

\## Handbook 关联

\- \[\[Cryptography\]\] — 哈希和签名是交易底层基础

\- \[\[Wallet\]\] — 钱包是签名入口

\- \[\[Smart Contract\]\] — 合约是交易目标

\- \[\[Account Abstraction\]\] — Smart Account 与 L2 结合

\- \[\[Chain-aware Context\]\] — 链上状态如何进入 Agent 上下文

\## Check-in Draft

\`\`\`

#AIWeb3School #Day6

今日学习 Web3 Network 基础：

1\. 理解区块链第一性原理：让互不信任的参与方对状态变化达成一致

2\. 掌握 Block → Consensus → PoS → Testnet → L2 → Rollup 完整链路

3\. 关键洞察：AI Agent 读链上状态不能靠"猜"，必须返回结构化可验证信息

4\. 产出 Web3 概念地图交互页面（10 概念 + Bridge 交叉分析）

5\. 参加 Week 1 例会

下一步：完成测试网交易追踪最小实践

\`\`\`

\## WCB Submission

\- 打卡链接: [https://web3career.build/zh/programs/AI-Web3-School#tab=learning](https://web3career.build/zh/programs/AI-Web3-School#tab=learning)

\- 提交状态: pending
<!-- DAILY_CHECKIN_2026-05-22_END -->

# 2026-05-21
<!-- DAILY_CHECKIN_2026-05-21_START -->

\# Daily Note — 2026-05-21

\## 今日课程

🔴 **AI 下乡计划｜AI 在 Web3 的应用**（20:00 直播）

\- Zoom: 861 4916 2743 / 密码 856868

\- 回放: [https://x.com/i/broadcasts/1kJzDMjMVBwKv](https://x.com/i/broadcasts/1kJzDMjMVBwKv)

\- 状态: ✅ 已参加

\## 今日收获

\### AI 下乡计划 — 关键笔记

\-

\## 其他进展

\### Hermes Agent 深度配置

\- WebUI 成功迁移到 Windows 原生运行（8788 端口），与 CLI 共享同一 HERMES\_HOME

\- 微信 Gateway 正常运行，已配对

\- GitHub 学习仓库 + Gitee → 最终只保留 GitHub

\- Obsidian Vault 知识库接入，建立完整 ingest 工作流

\### 知识库建设

\- 摄入文章：「比龙虾更强？我是如何用 Hermes 打造 7x24 全职员工」

\- 提炼核心工作流契约：丢什么 → 干什么 → 留下什么 → 怎么复用

\- 创建 Skill`stephen-workflowgithub-demand-radar`

\### 学习工具链

\- WCB Agent API 连接成功（学号 #4209）

\- Learning Agent 完整初始化

\- 每日提醒：14:00 + 20:00

\## Handbook 关联

\- \[\[AI 下乡计划\]\] 涉及 AI 在真实场景中的落地应用

\- 关联 \[\[AI\_Security\]\]、\[\[Verifiable\_AI\]\]、\[\[Agent\_Workflow\]\]

\## Check-in Draft

\`\`\`

#AIWeb3School #Day5

今日完成：

1\. ✅ AI 下乡计划｜AI 在 Web3 的应用（直播）

2\. ✅ Hermes Agent 完整配置：WebUI + Gateway + Obsidian 知识库

3\. ✅ 建立 6 条工作流契约：链接/群聊/GitHub/文章/重复任务/定时任务

4\. ✅ WCB Agent API 连接，学习工具链打通

5\. ✅ 补完 Week 1 全部笔记（5/17-5/21）

明天预告：

\- 19:00 Co-learning 答疑（Zoom: 891 8275 3424 / 815963）

\- 20:00 Week 1 例会（Zoom: 858 2160 2823 / 330279）

\`\`\`

\## WCB Submission

\- 打卡链接: [https://web3career.build/zh/programs/AI-Web3-School#tab=learning](https://web3career.build/zh/programs/AI-Web3-School#tab=learning)

\- 提交状态: pending
<!-- DAILY_CHECKIN_2026-05-21_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->


今天参加了Web3 运行原理的课程，补齐了账户、钱包、签名、交易、Gas、合约、区块浏览器和测试网验证如何组成一次完整链上操作等知识，并且继续学习hermes的进阶玩法
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->



今天配置好了hermes，并观看了18号8pm的**AI时代，Web3开发者需要具备的基础知识和架构能力**的回放视频，学习了钱包、gas、ai的一些基础概念
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->




今天观看了开学营的回放视频，参与了co-learning的会议，并打算开始自行配置Hermes
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
