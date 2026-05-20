---
timezone: UTC+8
---

# Tiya丶Degurechaff

**GitHub ID:** tiyadegure

**Telegram:** @tiyadegure

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->
# Daily Note – 2026-05-20

## Today’s Focus

Day 3 – Web3 practical tasks (testnet transaction, smart contract deployment), online events.

## Handbook Reading

-   **Chapters**: Web3 实操相关章节复习
    
-   **Key Takeaways**:
    
    -   EOA vs Smart Account vs Multisig 权限模型差异
        
    -   测试网交易流程：钱包签名 → RPC广播 → 验证者打包 → 确认
        
    -   智能合约生命周期：编写 → 编译 → 部署 → 交互
        

## Tasks & Progress

-   \[ \] 完成一笔测试网交易 (20pts) → submission pending
    
-   \[ \] 部署或调用一个最小智能合约 (30pts) → submission pending
    
-   \[ \] 比较 EOA/智能账户/多签权限差异 (30pts) → submission pending
    
-   \[ \] 画出 AI×Web3 最小交叉流程图 (30pts) → submission pending
    
-   \[ \] 参加 5.20 线上活动 → submission pending
    

## Online Events (5.20)

-   **Web3 运行原理** (17:00-18:00, Zoom: 86334195288)
    
-   **Co-learning 任务推进与答疑** (19:00-20:00, Zoom: 89182753424)
    

## Testnet Preparation

### MetaMask Setup Checklist

-   \[ \] Install MetaMask Chrome extension
    
-   \[ \] Create wallet and save recovery phrase
    
-   \[ \] Add Sepolia testnet (Chain ID: 11155111)
    
-   \[ \] Get test ETH from faucet ([sepoliafaucet.com](http://sepoliafaucet.com))
    
-   \[ \] Export private key to .env file
    

### Task Files Created

-   `tasks/week1-testnet-setup.md` – MetaMask + Sepolia configuration guide
    
-   `tasks/week1-testnet-tx.md` – Testnet transaction task guide
    
-   `tasks/week1-smart-contract.md` – Smart contract deployment guide
    
-   `tasks/week1-eoa-comparison.md` – EOA vs Smart Account vs Multisig comparison
    
-   `tasks/week1-cross-flow.md` – AI x Web3 cross-flow diagram guide
    

## Questions & Observations

-   测试网交易需要 Sepolia ETH，Binance Wallet 不支持测试网
    
-   MetaMask 是最可靠的选择，支持自定义网络
    
-   智能合约部署需要 0.002-0.01 ETH gas 费
    
-   EOA vs Smart Account vs Multisig 的关键区别在于权限控制模型
    

## Check-in Draft (残酷共学打卡)

**今日学习内容**: 完成 Web3 实操环境搭建：安装 MetaMask 钱包、配置 Sepolia 测试网、通过 PoW 水龙头领取 0.062 ETH 测试币。完成第一笔测试网交易（发送 0.001 ETH 给自己），交易在 Sepolia 网络上确认成功。参加两场线上活动：「Web3 运行原理」和「Co-learning 任务推进与答疑」。整理了 EOA/智能账户/多签对比分析、AI×Web3 交叉流程图等任务文档。

**收获与思考**: 测试网交易流程与主网完全一致：钱包签名 → RPC 广播 → 验证者打包 → 链上确认。区别在于测试 ETH 免费且无真实价值，适合学习和调试。MetaMask 是最主流的浏览器钱包，支持自定义网络添加。水龙头有多种类型：Alchemy 需要主网余额，PoW 水龙头通过浏览器挖矿免费获取，适合没有主网 ETH 的新手。

**明日计划**: 完成智能合约部署（SimpleStorage）、EOA/智能账户/多签权限对比分析、AI×Web3 交叉流程图绘制。继续参加线上活动。

* * *

-   WCB Learning: [https://web3career.build/zh/programs/AI-Web3-School#tab=learning](https://web3career.build/zh/programs/AI-Web3-School#tab=learning)
    
-   Handbook: [https://aiweb3.school/zh/handbook/](https://aiweb3.school/zh/handbook/)
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->

# Daily Note — 2026-05-19

## Today’s Focus

Day 2 — AI/Web3 concept cards, interactive demo, Hermes event.

## Handbook Reading

-   **Chapters**: AI 基础概念卡片 (8 chapters) + Web3 基础概念卡片 (10 chapters)
    
-   **Key Takeaways**:
    
    -   AI Agent 核心机制是四步循环：理解目标→调用工具→观察结果→修正执行
        
    -   MCP 是 AI × Web3 的缺失管道层，标准化模型与链上工具的连接
        
    -   Account Abstraction 让账户规则可编程，超越单一私钥控制
        

## Tasks & Progress

-   \[x\] AI 基础概念卡片 (8 chapters) → submission `cmpcj8rn82yzxtl017srs3pmm`
    
-   \[x\] Web3 基础概念卡片 (10 chapters) → submission `cmpck4b9h31y2tl01uo50txay`
    
-   \[x\] AI 可交互学习产物 (Transaction Explainer demo) → submission `cmpckvf0834actl01bnv0qqjk`
    
-   \[x\] 参加 5.19 Hermes 活动 → submission `cmpco766i3ps9tl012pizjatm`
    

## Online Events (5.19)

-   **AI Agent 入门 — Hermes 从 0 到 1** (20:00-21:00)
    
    -   AI Agent 核心运行机制：理解目标→调用工具→观察结果→修正执行
        
    -   这是一个 constrained execution loop，不是一次性回答问题
        
    -   与 Handbook Agent 章节完全吻合
        

## Questions & Observations

-   Agent 不是"更聪明的聊天机器人"，而是一个持续执行和自我调整的系统
    
-   Hermes 的使用路径：学习计划→repo→每日记录→任务提交→反馈，全部由 Agent 串联
    
-   测试网交易和合约部署是下周重点，需要提前准备钱包和环境
    

## Check-in Draft

**今日学习内容**: 整理 AI 基础概念卡片（8 章节：LLM、Prompt、Context、RAG、Agent、Frameworks、MCP、Evaluation）和 Web3 基础概念卡片（10 章节：Cryptography、Wallet、Smart Contract、Dev Stack、Network、Account Abstraction、DeFi、Oracle、Indexing、Security）。完成 AI 可交互学习产物 Transaction Explainer demo（连接 Sepolia 测试网，将原始交易数据翻译成人话）。参加「AI Agent 入门：Hermes 从 0 到 1」线上活动。

**收获与思考**: AI Agent 核心机制是四步循环：理解目标→调用工具→观察结果→修正执行，这是一个 constrained execution loop，不是一次性回答问题。MCP 是 AI × Web3 的缺失管道层，标准化了模型与链上数据/工具的连接方式，让任何 MCP 兼容的 AI agent 都能与区块链基础设施交互。

**明日计划**: 完成测试网交易和智能合约部署，画 AI × Web3 交叉流程图。

* * *

-   WCB Learning: [https://web3career.build/zh/programs/AI-Web3-School#tab=learning](https://web3career.build/zh/programs/AI-Web3-School#tab=learning)
    
-   Handbook: [https://aiweb3.school/zh/handbook/](https://aiweb3.school/zh/handbook/)
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->


# Daily Note — 2026-05-18

## Today’s Focus

![屏幕截图 2026-05-18 213034.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/tiyadegure/images/2026-05-18-1779111656786-_____2026-05-18_213034.png)

Learning Agent 初始化 — 搭建学习仓库、制定学习计划。

## Handbook Reading

-   **Chapter**: [Handbook 首页](https://aiweb3.school/zh/handbook/)
    
-   **Key Takeaways**:
    
    -   Handbook 分四层：AI 基础 → Web3 基础 → AI × Web3 Bridge → 前沿探索
        
    -   不需要线性阅读，按自己的知识缺口选择路径
        
    -   产品研究方向：重点看 Agent Workflow、Agent Wallet、Chain-aware Context
        

## Tasks & Progress

-   \[x\] GitHub CLI 登录确认
    
-   \[x\] 创建学习仓库 `ai-web3-school-cohort-0`
    
-   \[x\] 初始化仓库结构（README, profile, plan, templates）
    
-   \[x\] 制定三阶段学习计划
    
-   \[x\] 配置 WCB Agent API
    
-   \[x\] 提交任务「创建课程 GitHub repo」→ submission `cmpb8bxos1oiemj013e6its0z`
    
-   \[x\] 提交任务「完成 Learning Agent Setup」→ submission `cmpb8bz321oigmj01m3xxecgy`
    
-   \[x\] 提交任务「完成课程工具准备」→ submission `cmpb8hbj71pmpmj018mvdc3ji`
    
-   \[x\] 提交任务「完成 Proof-of-Work 提交测试」→ submission `cmpb8kleq1qafmj01z4xcw3ft`
    
-   \[x\] 提交任务「建立 AI × Web3 行业信息流关注清单」→ submission `cmpb8kmva1qaqmj01596x1cs6`
    
-   \[x\] 提交任务「在 X 发布起点」→ submission `cmpb8wwqo01fztl016pv6k1sl`
    
-   \[x\] 提交任务「加入社群并完成自我介绍」→ submission `cmpb8wy8e01g5tl01kavt5iku`
    
-   \[x\] 提交任务「参加开营仪式」→ submission `cmpb8xcg001i5tl01aujvl69c`
    
-   \[x\] 提交任务「参加 5.18 AI 时代的 Web3 架构能力」→ submission `cmpb8wzih01gdtl01jgz3dmt9`
    
-   \[x\] 提交任务「参加 5.18 Co-learning」→ submission `cmpb8xjnb01ixtl01r21y3fek`
    

## Online Events (5.18)

-   **AI 时代的 Web3 架构能力** — 173 人参加，讨论跨链基础设施（Wormhole、Chainlink、Circle 在做去中心化跨链），LiFi、KelpDAO 等项目
    
-   **Co-learning** — 任务推进与答疑
    

## Questions & Observations

-   Handbook 内容很全面，需要先快速过一遍 AI 基础再深入 Web3 Bridge
    
-   Vibe Coding 和 MCP 这两个概念比较新，需要重点关注
    
-   跨链基础设施是热点方向，Wormhole/Chainlink/Circle 都在布局
    

## Check-in Draft

**今日学习内容**: 初始化 AI × Web3 School 学习环境，创建 GitHub 学习仓库，制定三阶段学习计划（Foundation → Bridge → Frontier），确认 Handbook 学习路径。

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/tiyadegure/images/2026-05-18-1779112529763-image.png)

**收获与思考**: Handbook 的四层结构很清晰，AI × Web3 Bridge 是核心交叉区域。作为产品研究方向，需要重点理解 Agent 如何与链上系统交互。

**明日计划**: 开始阅读 Handbook AI 基础第一章 — LLM（大语言模型）。

* * *

-   WCB Learning: [https://web3career.build/zh/programs/AI-Web3-School#tab=learning](https://web3career.build/zh/programs/AI-Web3-School#tab=learning)
    
-   Handbook: [https://aiweb3.school/zh/handbook/](https://aiweb3.school/zh/handbook/)
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
