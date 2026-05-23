---
timezone: UTC+8
---

# BBBINGW

**GitHub ID:** BBBINGW

**Telegram:** @hash0x666

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-23
<!-- DAILY_CHECKIN_2026-05-23_START -->
**🔗 一、LLM × Cryptography 交叉疑问（6条）**  
这些是你的 PhD 视角独有的 crossover：  
**1**  
  
• #: 1  
  
• 问题: **能用 ZK proof 验证 LLM 无 hallucination 吗？**  
  
**2**  
  
• #: 2  
  
• 问题: **Session key / Agent wallet 怎么跟 tool calling 交互？** — 需不需要 prover layer？  
  
**3**  
  
• #: 3  
  
• 问题: 「Model output = verifiable objects」→ 能否用 **typed signature** 形式化？  
  
**4**  
  
• #: 4  
  
• 问题: **Hallucination ≈ Byzantine fault？** — 概念同构？  
  
**5**  
  
• #: 5  
  
• 问题: **Embedding similarity ≠ truth ≈ probabilistic verification ≠ proof？**  
  
**6**  
  
• #: 6  
  
• 问题: LLM audit trail 能否做成 **Merkle proof** 结构？  
  
**🛡️ 二、Prompt 作为接口 vs 安全边界（4条）**  
**7**  
  
• #: 7  
  
• 问题: 安全链 `Prompt→Context→Model→Code→Guard→Human` 各层责任边界在哪？  
  
**8**  
  
• #: 8  
  
• 问题: Few-shot 的维护成本怎么跟 eval 配合管理？  
  
**9**  
  
• #: 9  
  
• 问题: Instruction 四段式写法够用吗？  
  
**10**  
  
• #: 10  
  
• 问题: 「出事了人兜底」vs「每层可验证」的界限？  
  
**🧩 三、Context & Agent 结构追问（3条）**  
**11**  
  
• #: 11  
  
• 问题: **Agent 前必须先读 Context 吗？** → 是，你当时自己纠正了我 🙂  
  
**12**  
  
• #: 12  
  
• 问题: 钱包授权 Agent 的 **Context Spec 字段分类** — 实时/缓存/不可信  
  
**13**  
  
• #: 13  
  
• 问题: **可信数据源 vs 不可信外部内容** — 谁来做判断？
<!-- DAILY_CHECKIN_2026-05-23_END -->

# 2026-05-22
<!-- DAILY_CHECKIN_2026-05-22_START -->

# Context

Note

Context 是模型这一次能看到、能使用、能被影响的信息空间。真正难的不是把更多内容塞进去，而是把系统规则、用户目标、历史状态、工具结果和外部文档分清楚。

在实际产品里，context window 应该配合检索、摘要和结构化数据使用。关键状态直接给，长文档按需取，低可信内容隔离标注。

一个稳定的工具型 Agent 上下文，通常不只是“用户问题 + 一段 JSON”。它还应该包括：

-   当前任务状态
    
-   工具返回结果
    
-   相关日志或证据
    
-   可信数据来源
    
-   外部检查结果
    
-   用户原始意图
    
-   系统禁止事项和输出 schema
    

**Context Engineering 的目标不是塞满窗口，而是让模型在正确的信息层级里工作。**

Memory 不能替代实时授权。用户过去允许某个动作，不代表现在仍然允许。**所有涉及身份、权限、资产或外部副作用的记忆，都必须重新绑定当前会话和当前授权。**

一个靠谱的 Agent 上下文通常会分层：

-   指令层：系统规则、工具使用规则、禁止事项。
    
-   任务层：用户目标、本次会话参数。
    
-   事实层：链上状态、工具结果、simulation。
    
-   知识层：文档、标准、论坛、历史案例。
    
-   记忆层：用户偏好和项目配置。
    

层级越清楚，后续越容易做权限控制、prompt injection 防护和审计。
<!-- DAILY_CHECKIN_2026-05-22_END -->

# 2026-05-21
<!-- DAILY_CHECKIN_2026-05-21_START -->


今天没有太多时间看东西，就查了一些名词。

# [RPC](https://aiweb3.school/zh/handbook/web3/indexing/#rpc)

RPC 是应用和节点交互的接口，用来读取链状态、查询日志、估算 gas 和发送交易。

```
你的钱包/MetaMask/dApp  ← →  RPC  ← →  区块链节点
                                    ↑
                              "帮我查一下这个地址的余额"
                              "帮我估算一下这笔 gas"
                              "帮我把这笔交易广播出去"
```

# Slashing

罚没

```
正常情况：
  你被选中做记录 → 好好记 → 其他人检查没问题 → 下周继续

被 Slashing 的情况：
  ❌ 你同一轮提议了两个不同的区块（搞分裂）
  ❌ 你明明没被选中，却假装被选中到处发假记录
  ❌ 你离线太久不工作（某些链会罚）

处罚：
  ⚔️ 系统砍掉你一部分质押金（最高砍到全部！）
  🚫 你可能被踢出验证者队伍
```

# MEV

MEV = **Maximal Extractable Value**（最大可提取价值）  
**MEV 就是：你能通过**重新排列交易顺序**赚到的额外钱。**  
**经典例子：三明治攻击**

```
你看到一个交易在 mempool 里：
  「小明的交易：用 100 USDC 买 1 ETH」

如果你有权力调整顺序，你可以这样做：
  
  ① 你先买（价格推高）     ← 你的交易
  ② 小明买（在高价买入）   ← 小明的交易（被坑）
  ③ 你再卖掉（赚差价）     ← 你的交易

  💰 你赚了小明多付的那部分差价
```

# L2

Layer 2 通常把大量交易放到主网之外执行，再把结果或证明提交回主网。对用户来说，L2 常见优势是费用更低、确认更快；但也多了桥、提现等待、排序器和跨链状态同步等复杂性。

产品设计时不能只写“支持 Ethereum”。

## 怎么写

如果支持多个 L2，需要清楚展示当前网络、资产在哪条链、桥接需要多久、合约地址是否不同。

## [Rollup](https://aiweb3.school/zh/handbook/web3/network/#rollup)

**难度：高级。** Rollup 是主流 L2 扩展路线，把执行搬到链下或 L2，再把数据和结果提交到 L1。

常见 rollup 类型包括 optimistic rollup 和 zero-knowledge rollup。它们在证明方式、提现延迟、数据可用性、开发体验和生态工具上都有差异。

对 builder 来说，先抓住一个判断：Rollup 降低了单笔交易成本，但没有消除链上系统复杂度。你仍然要处理跨链资产、RPC、浏览器、合约地址、桥接风险和用户确认。
<!-- DAILY_CHECKIN_2026-05-21_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->



🎓 AI × Web3 School — Phase 1 Day 3: Prompt

📖 读完了 Prompt 章节：

• Prompt = 接口设计，不是安全边界

• Instruction 分四段：目标、输入、禁止行为、输出格式

• Few-shot 好用但有维护成本

• Structured Output 让模型输出可被代码校验

🔧 完成最小实践：交易风险摘要 Prompt + 3组测试用例

🌐 听了 Web3 运行原理课

🎯 接下来：Web3 Network 章节 + 论文 Intro

#AIWeb3School #Cohort0 #Phase1 #Prompt
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->




🎓 AI × Web3 School — Phase 1 Day 3: Tool Workflow Insights

📖 Did not read Prompt chapter today (deferred) — instead explored practical AI tool workflows from the community:

🔧 Key findings:

• Cursor (CC) + CC Switch + Obsidian = powerful personal AI knowledge base

• Codex best for writing tight instructions; DeepSeek best for executing them

• Chinese models (DeepSeek) need very clear, detailed specs to avoid hallucination

• Avoid "new tech" — bleeding-edge APIs are often outside training data

💡 The "orchestrator vs executor" split maps directly to Agent design in Web3: write tight specs, then execute.

🎯 Next: Phase 1 — Prompt chapter (tomorrow)

#AIWeb3School #Cohort0 #Phase1 #ToolWorkflow
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->





# [一个链上 Agent 的基本工作流](https://aiweb3.school/zh/ai-agents/#%E4%B8%80%E4%B8%AA%E9%93%BE%E4%B8%8A-agent-%E7%9A%84%E5%9F%BA%E6%9C%AC%E5%B7%A5%E4%BD%9C%E6%B5%81)

一个典型的链上 Agent，可以拆成下面几步：

1.  读取信息：钱包状态、链上数据、协议价格、用户目标
    
2.  理解上下文：判断当前条件、风险和机会
    
3.  生成计划：决定该执行什么动作
    
4.  调用工具：查询合约、生成交易、请求签名
    
5.  执行与记录：提交交易，并跟踪结果
    

这条链路里，真正复杂的地方通常不是“写一句 Prompt”，而是如何把判断、权限和执行安全地接起来。

## 权限

至少要先定义清楚：

-   哪些动作只允许建议
    
-   哪些动作必须二次确认
    
-   哪些动作可以自动执行
    
-   失败后如何停止或回退
    

没有这一层，Agent 越强，风险越大。

## 举例

如果用户说：“帮我把稳定币按低风险策略分配到几个协议里。”

一个链上 Agent 可能会：

-   读取用户当前钱包和授权状态
    
-   获取协议利率和风险指标
    
-   生成几种候选方案
    
-   根据用户设定的约束选择方案
    
-   请求用户确认
    
-   最后按预设规则执行交易
    

这里真正的产品能力，不在一句回答，而在整条“理解—规划—执行”链路。

# LLM

LLM 位在 AI x Web3 系统的理解和生成层。它负责把用户目标转成可讨论的计划，把复杂链上数据解释成人能读的语言，把文档和代码串成可执行思路。

真正的产品通常还需要这些层配合：

-   数据层：RPC、索引器、预言机、向量库、项目文档。
    
-   编排层：Prompt、Context、RAG、Agent workflow。
    
-   执行层：工具调用、钱包、Smart Account、合约交互。
    
-   安全层：Guard、simulation、权限策略、人工确认、日志。
    

LLM 越靠近执行层，系统越要把它的自然语言输出变成可验证对象。

# Token

Token 直接影响三件事：上下文能放多少、调用成本是多少、模型能不能完整看见关键信息。长文档、代码、JSON、日志和多轮对话都很容易把上下文塞满。你需要决定哪些信息原样放入，哪些先压缩，哪些交给检索系统按需取回。

**不要把“页面很短”误认为“token 很少”**。代码、JSON、长标识符、表格和混合语言文本经常比普通段落更吃 token。

# RAG

RAG 的核心不是让回答更长，而是让回答有来源、有版本、有边界。**没有 citation 和 freshness 的 RAG，只是把幻觉从模型内部搬到了检索系统里。**

一个 RAG 系统至少有三次判断：文档怎么切，查询时取哪些内容，生成时如何引用和拒答。
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
