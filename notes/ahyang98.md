---
timezone: UTC+8
---

# ahyang

**GitHub ID:** ahyang98

**Telegram:** @ahyangchen

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-26
<!-- DAILY_CHECKIN_2026-05-26_START -->
```yaml
title: 智能体工作流（Agent Workflow）
created: 2026-05-26
updated: 2026-05-26
type: concept
tags: [ai, agent, workflow, automation, web3]
sources: [raw/articles/智能体工作流（Agent Workflow）.md]
confidence: high
```

# 智能体工作流（Agent Workflow）

> Agent Workflow 是把"用户目标 → 上下文读取 → 计划生成 → 工具调用 → 风险检查 → 执行 → 记录和复盘"组织成可控流程，而不是让模型自由发挥。

**核心原则：** 高风险 Agent 不能只有"下一步推理"，必须有状态、边界和停止条件。核心是把概率模型放进确定性流程里。

## 第一性原理

-   **流程要显式** — 不要把完整执行链路藏在一段长 prompt 里
    
-   **状态要可恢复** — 工具失败、用户拒绝、交易 pending 时，系统要知道如何继续或停止
    
-   **评估要可回放** — 没有 trace 和 regression set，很难知道改模型后是否更安全
    

## 知识节点

### Task Graph（任务图）— 难度：中级

把目标拆成节点和依赖。例如"评估并执行一次低风险 swap"：

1.  读取用户目标和限制
    
2.  查询余额和 allowance
    
3.  查询价格和流动性
    
4.  生成候选交易
    
5.  模拟交易
    
6.  展示风险
    
7.  用户确认
    
8.  发送交易
    
9.  追踪结果
    

每一步都可设置输入、输出、权限和停止条件。

### State Machine（状态机）— 难度：高级

让 Agent 执行过程有明确状态，而不是只有聊天历史。链上工作流常见状态：

`draft → context_loaded → plan_ready → waiting_user_confirmation → submitted → confirmed / reverted / cancelled`

状态机价值：用户刷新页面、交易 pending、RPC 失败、模型重试时，系统不会忘记自己在哪，也不会重复执行危险动作。

### Human-in-the-loop（人工介入）— 难度：中级

把人类放在关键风险点，而不是让人确认每一个低风险步骤。

合理分层：

-   只读分析 → 自动执行
    
-   交易草稿 → 自动生成
    
-   小额白名单操作 → session key 执行
    
-   高风险交易 → 必须人工确认
    
-   超出 policy → 直接拒绝
    

### Retry / Fallback（重试 / 降级）— 难度：中级

Web3 Agent 不能盲目重试。读取余额失败可重试；发送交易要先判断是否已广播；交易 pending 不能简单再发一笔。

Fallback 也要谨慎：模型不可用时可降级成只读模式，但不应该自动换一个未经评估的模型继续发交易。

### Trace（追踪）— 难度：初级

Agent 每一步输入、判断、工具调用和结果的记录。至少包括：用户目标、模型版本、上下文来源、工具输入输出、policy 判断、simulation 结果、人工确认、交易哈希和最终状态。

没有 trace，出了问题只能看聊天记录。

### Evaluation Harness（评估框架）— 难度：高级

系统测试 Agent 在不同任务、风险和异常场景下的表现。对链上 Agent，eval 测的不只是回答质量，还要测：

-   是否正确拒绝越权请求
    
-   是否识别错误链和错误合约
    
-   是否在缺数据时停止
    
-   是否要求 human check
    
-   是否记录 citation
    
-   是否避免生成危险 calldata
    

### Regression Set（回归测试集）— 难度：中级

一组固定测试用例，防止模型/prompt/工具更新后安全性退化。可包含：正常 swap、错误链、无限 approve、恶意文档诱导、余额不足、预言机价格过旧、用户拒绝签名、交易 pending 超时等。

**每次改模型或工具前，都应该跑这组用例。**

## 在 AI × Web3 中的位置

-   [链感知上下文](chain-aware-context) 提供事实
    
-   [Web3 工具调用](web3-tool-use) 提供能力
    
-   Agent Wallet 提供权限边界
    
-   **Workflow 把它们组织成可执行但可控的路径**
    

没有 workflow，项目很容易变成"模型直接调用工具"——在 demo 里很快，但在真实资产和权限面前不够用。
<!-- DAILY_CHECKIN_2026-05-26_END -->

# 2026-05-25
<!-- DAILY_CHECKIN_2026-05-25_START -->

```yaml
title: 链感知上下文（Chain-aware Context）
created: 2026-05-25
updated: 2026-05-25
type: concept
tags: [ai, web3, context, architecture]
sources: [raw/articles/链感知上下文（Chain-aware Context）.md]
confidence: high
```

# 链感知上下文（Chain-aware Context）

## 概述

Chain-aware Context 指的是让 AI 在回答或行动前，能看见正确的链、地址、合约、交易、事件、余额、授权和数据来源，而不是只靠用户一句话猜测链上状态。

## 为什么要学

普通 AI 上下文来自文档和聊天历史。AI×Web3 多了一层：**链上状态持续变化，且直接影响资产和权限**。

如果 Agent 不知道当前 chain id、合约地址、ABI、用户授权、交易历史，就可能给出错误建议甚至生成危险交易。

## 第一性原理

> **模型不能凭语言记忆判断链上事实，链上事实必须从工具和索引层读取。**

### 三项原则

1.  **链上状态有时间性** — 同一地址的余额、授权、仓位随区块变化
    
2.  **上下文要带来源** — 合约地址、区块号、交易哈希、explorer 链接都应可追溯
    
3.  **上下文要区分事实和解释** — 工具返回事实，模型负责解释，不要把模型猜测当事实
    

## 上下文类型

| 上下文 | 难度 | 说明 |
| --- | --- | --- |
| On-chain Data | 初级 | 余额、交易、日志等链上可验证数据。需带 chain id、block number |
| Contract Docs | 初级 | ABI 之外的业务语义。NatSpec、README、审计报告 |
| ABI / Event | 中级 | 合约可调用能力和业务日志。能调用≠应该调用 |
| Transaction History | 中级 | 用户/合约过去行为。需保留 tx hash、block number、logs |
| Explorer Context | 初级 | 区块浏览器提供的可检查入口和证据链接 |
| Indexing Context | 中级 | 把事件整理成面向产品查询的数据。需带时间戳和同步状态 |
| Citation | 初级 | 结论引用具体链上证据。没有 citation 的解释只是观点 |

## 理想上下文包

一个好的链感知上下文应包含：

-   用户目标
    
-   当前 chain id 和网络名称
    
-   用户地址和余额
    
-   相关合约地址、ABI、文档和风险提示
    
-   最近交易和授权
    
-   索引数据更新时间
    
-   每条关键结论的 citation
    

## 关联概念

-   [Web3 工具调用](web3-tool-use) — 依赖本上下文作为输入层
    
-   [AI x Web3 School](ai-web3-school) — 来源课程
<!-- DAILY_CHECKIN_2026-05-25_END -->

# 2026-05-24
<!-- DAILY_CHECKIN_2026-05-24_START -->


# obsidian

1.  obsidian为本地md文档，方便与AI结合
    
2.  可以保存到github进行同步和管理
    
3.  可以采用karpathy模式，进行每日信息收集、AI整理、总结
    

这是目前对obsidian的应用模式

# subagent或者多agent模式

1.  multi agent模式，上下文隔离，互不干扰，可以并行执行
    
2.  hermes中有看板模式，可以控制多任务之间的依赖。
<!-- DAILY_CHECKIN_2026-05-24_END -->

# 2026-05-22
<!-- DAILY_CHECKIN_2026-05-22_START -->



今天了解到obsidian和subagent，明后天会重点学习下。
<!-- DAILY_CHECKIN_2026-05-22_END -->

# 2026-05-21
<!-- DAILY_CHECKIN_2026-05-21_START -->




# task3存在的问题

昨天没调完，存在跨域问题，今天让agent进行了修复，现在测试已经ok
<!-- DAILY_CHECKIN_2026-05-21_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->





# Task3

针对taks3今天用hermes做了一个交互转账的demo，整体按照spec进行开发。

## 需求

1.  选择一个 Week 1 概念，例如 LLM / workflow / agent、钱包 / 签名 / 交易、Gas / 合约执行，你生成一个可交互产物：小页面、CLI、流程图、quiz、概念卡片或最小 demo，你觉着做啥好
    
2.  按照上面的workflow，你做一个用户转账的完整实现吧，先写需求和设计文档，
    

工程放到/home/ahyang/project/web3/ai-web3-school-cohort/demos/task3-transfer-token，

包括前端、后端、合约前端使用Typescript/Vite/Tailwind/Shadcn/WAGMI/VIEM

使用 Fast API作为后端，agent就用你自己吧，当然需要做成可配置的

合约写一个ERC20，使用hardhat创建工程，部署账户、网络做成可配置的

3.  需要能对接hermes agent、再把测试和部署设计加上
    
4.  不用docker，直接本地部署
    

# 开发计划

好了，接下来写开发计划

# 编码

ok，按照开发计划开始开发吧

# 提交

好的，先提交一下github

# 部署

用我的账户、rpc部署合约到sepolia
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->






之前已经在用claude code写代码，分析代码库了，

刚才在安装hermes，配置了deepseek，对接了微信，刚调通了，可惜错过了打卡时间了。

# 2026-05-19

# 任务1：

learning agent已经搭建

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/ahyang98/images/2026-05-19-1779173933371-image.png)
<!-- DAILY_CHECKIN_2026-05-19_END -->
<!-- Content_END -->
