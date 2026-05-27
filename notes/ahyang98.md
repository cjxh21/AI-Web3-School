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
# 2026-05-27
<!-- DAILY_CHECKIN_2026-05-27_START -->
```yaml
title: "Agent Settlement & Escrow 完整架构骨架"
created: 2026-05-28
updated: 2026-05-28
type: concept
tags:
  - "architecture"
  - "escrow"
  - "settlement"
  - "agentic-commerce"
  - "design"
confidence: high
```

# Agent Settlement & Escrow 完整架构骨架

> 本文把 Agent 经济里的结算与托管从问题到架构到实现做一次完整梳理，适合作为系统设计和开发的参考骨架。

* * *

## 一、要解决什么问题

Agent 可以购买 API、委托另一个 Agent 写代码、让服务商跑模型、完成链上操作。但付款和交付之间存在 **信息不对称和时间差**：

| 支付顺序 | 风险 |
| --- | --- |
| 先付款 | 服务方不交付 / 交付不合格 / 跑路 |
| 先交付 | 付款方不付款 / 争议无凭据 |

**Settlement & Escrow 的核心目标**：把"一次转账"变成**可验证、可追溯、有兜底**的完整交易流程。任务、交付、验收、付款必须绑定成可验证的闭环。

* * *

## 二、整体架构：三层模型

```
┌─────────────────────────────────────────────────────────────┐
│                     Agent Layer                              │
│                                                              │
│  Payer Agent       Service Agent       Evaluator Agent       │
│  (任务发起/付款)    (任务执行/收款)      (验收/仲裁)          │
│       │                   │                   │              │
│       │   ┌───────────────┴───────────────┐   │              │
│       │   │       Agent Runtime           │   │              │
│       │   │  (MCP / A2A / API Gateway)    │   │              │
│       │   └───────────────┬───────────────┘   │              │
└───────┼───────────────────┼───────────────────┼──────────────┘
        │                   │                   │
┌───────┼───────────────────┼───────────────────┼──────────────┐
│       ▼                   ▼                   ▼              │
│                   Orchestration Layer                         │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐    │
│  │                  Escrow Engine                         │    │
│  │                                                       │    │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────────────┐    │    │
│  │  │ Task     │  │ State    │  │ Evaluator        │    │    │
│  │  │ Manager  │─→│ Machine  │─→│ Dispatcher       │    │    │
│  │  │ (创建/   │  │ (状态    │  │ (AI / 脚本 /     │    │    │
│  │  │  路由)   │  │  转换)   │  │  人工/混合)      │    │    │
│  │  └──────────┘  └──────────┘  └──────────────────┘    │    │
│  │                                                       │    │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────────────┐    │    │
│  │  │ Timer    │  │ Dispute │  │ Reputation       │    │    │
│  │  │ Watcher  │  │ Manager │  │ Recorder         │    │    │
│  │  │ (超时处理)│  │ (仲裁)   │  │ (声誉写回)       │    │    │
│  │  └──────────┘  └──────────┘  └──────────────────┘    │    │
│  └──────────────────────────────────────────────────────┘    │
│                           │                                  │
└───────────────────────────┼──────────────────────────────────┘
                            │
┌───────────────────────────┼──────────────────────────────────┐
│                           ▼                                  │
│                   Settlement Layer (On-chain)                 │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐    │
│  │              Escrow Contract                          │    │
│  │                                                       │    │
│  │  State:  Open → Funded → Submitted → Completed       │    │
│  │  Funds:  USDC / ETH / ERC-20 escrowed per jobId      │    │
│  │  Roles:  client / provider / evaluator               │    │
│  │  Hook:   IACPHook for extensibility                  │    │
│  │                                                       │    │
│  │  ┌─────────────────────────────────────────────┐     │    │
│  │  │ ERC-8004 Integration                        │     │    │
│  │  │ Identity Registry → agentId → agentWallet   │     │    │
│  │  │ Reputation → feedback from completed jobs   │     │    │
│  │  │ Validation → verifiable delivery proofs     │     │    │
│  │  └─────────────────────────────────────────────┘     │    │
│  └──────────────────────────────────────────────────────┘    │
└──────────────────────────────────────────────────────────────┘
```

### 各层职责

| 层 | 职责 | 技术栈 |
| --- | --- | --- |
| Agent Layer | 任务发起/执行/验收的主体 | AI Agent Framework, MCP, A2A |
| Orchestration Layer | 业务流程编排、状态管理、超时/争议处理 | 后端服务, 事件驱动, 状态机 |
| Settlement Layer | 资金原子操作、链上确权 | Solidity, EVM, ERC-8183 |

### 关键设计原则：链上 vs 链下边界

```
链上只做:                    链下做:
├─ 资金原子操作                ├─ 业务流程编排
│  (lock / release / refund)  │  (任务创建/匹配/报价)
├─ 状态最终确认                ├─ 验收逻辑
│  (不可篡改的状态机)           │  (AI 评估/脚本检查)
├─ 关键事件签名                ├─ 交付物存储
│  (EIP-712 授权)             │  (IPFS/Arweave)
└─ 争议兜底                    ├─ 声誉计算
   (超时退款安全网)             └─ 前端/通知
```

* * *

## 三、核心状态机

### 完整状态流转

```
                         ┌─────────────────┐
                         │    Created      │  ← 任务被创建但未定价
                         └────────┬────────┘
                                  │ setBudget + fund
                                  ▼
                         ┌─────────────────┐
                    ┌───│    Funded       │───┐
                    │   │ (资金已锁定)     │   │
                    │   └────────┬────────┘   │
                    │            │ submit      │ evaluator reject
                    │            ▼            │ (funded 阶段直接拒绝)
                    │   ┌─────────────────┐   │
                    │   │   Submitted     │   │
                    │   │ (交付物已提交)   │   │
                    │   └────────┬────────┘   │
                    │            │             │
                    │    ┌───────┴───────┐     │
                    │    ▼               ▼     │
                    │  ┌─────────┐  ┌────────┐ │
                    │  │Completed│  │Rejected│ │
                    │  │资金释放  │  │资金退回  │ │
                    │  │给provider│  │给client  │ │
                    │  └─────────┘  └────────┘ │
                    │                          │
                    └────── Expired ───────────┘
                          (超时强制退款，安全兜底)
```

### 状态转换规则

| 从 | 到 | 触发 | 谁可调用 |
| --- | --- | --- | --- |
| Created | Funded | fund() | client |
| Created | Rejected | reject() | client |
| Funded | Submitted | submit(deliverable) | provider |
| Funded | Rejected | reject(reason) | evaluator |
| Funded | Expired | claimRefund() (超时) | 任何人 |
| Submitted | Completed | complete(reason) | evaluator |
| Submitted | Rejected | reject(reason) | evaluator |
| Submitted | Expired | claimRefund() (超时) | 任何人 |

### 每个状态的核心数据

```go
type EscrowState struct {
    JobID        string           // 全局唯一任务 ID
    Client       address          // 付款方 (Agent)
    Provider     address          // 收款方 (Agent)
    Evaluator    address          // 验收方 (合约/EOA/DAO)
    Token        address          // 支付代币地址
    Budget       uint256          // 锁定金额
    ExpiredAt    uint256          // 超时时间戳
    Deliverable  [32]byte         // 交付物 hash (IPFS CID / keccak256)
    Reason       [32]byte         // 验收/拒绝时的 attestation
    Status       enum             // Created / Funded / Submitted / Completed / Rejected / Expired
    Hook         address          // IACPHook 合约地址 (可选)
}
```

* * *

## 四、各组件详述

### 4.1 Task Manager（任务管理器）

**职责**：任务的创建、路由、生命周期跟踪。

```
┌──────────────────────────────┐
│         Task Manager          │
├──────────────────────────────┤
│ createTask(desc, budget,     │
│   deadline, evaluator)       │
│ assignProvider(taskId, addr) │
│ getTask(taskId) → Task       │
│ listOpenTasks() → []Task     │
│ cancelTask(taskId)           │
└──────────────────────────────┘
```

-   任务描述（description）是"合约"——必须包含可验证的验收标准
    
-   支持 provider 延迟设定（先创建 job，后竞价/指派）
    
-   生成唯一 `taskId`，贯穿 escrow、evaluation、reputation 全流程
    

### 4.2 Escrow Engine（结算引擎）

**职责**：管理状态机、协调链上操作、处理超时/重试。

核心流程编排：

```
Client 侧:                                     Provider 侧:
createJob() ────┐                              │
                ▼                              │
setBudget() ────┼──→ 双方达成价格共识 ─────←────┘
                │                              │
fund() ─────────┼──→ 资金锁定至合约 ──────────→│
                │                              ▼
                │                    submit(deliverableHash)
                │                         │
                ▼                         ▼
          Evaluator 验收                    │
         ┌──────┴──────┐                   │
         ▼              ▼                  │
    complete()      reject()               │
    (资金释放)       (资金退回)              │
         │              │                  │
         ▼              ▼                  │
    Receipt生成     Receipt生成              │
         │              │                  │
         ▼              ▼                  │
   Reputation ←────── 完成 ──────────────→│
```

### 4.3 Evaluator Dispatcher（验收调度器）

**职责**：根据任务类型和风险等级，路由到合适的 evaluator。

```
                    ┌─────────────┐
                    │  任务提交     │
                    │ (Submitted)  │
                    └──────┬──────┘
                           │
                    ┌──────┴──────┐
                    │ Risk Classifier
                    │ (任务价值 + 复杂度)
                    └──────┬──────┘
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
        ┌──────────┐ ┌──────────┐ ┌──────────┐
        │ Low Risk │ │ Med Risk │ │ High Risk│
        │          │ │          │ │          │
        │ 脚本检查  │ │ AI 评估   │ │ AI 初审  │
        │ + 格式    │ │ + 自动    │ │ + 人工   │
        │  验证     │ │  判定     │ │  复核    │
        └──────────┘ └──────────┘ └──────────┘
              │            │            │
              └────────────┼────────────┘
                           ▼
                    ┌─────────────┐
                    │ Accept?     │
                    │ Yes: complete│
                    │ No:  reject │
                    │ ?:  dispute │
                    └─────────────┘
```

**验收标准设计原则**：

1.  尽可能拆成可检查条件（字段完整、测试通过、hash 匹配、预算未超出）
    
2.  主观判断标明由谁作出
    
3.  AI 验收 + challenge window + 人工复核组合使用
    
4.  Evaluator 本身也要被评估（记录版本、错误率、历史争议结果）
    

### 4.4 Dispute Manager（争议管理器）

**职责**：处理付款方和服务方对交付是否合格的分歧。

```
Dispute 流程:

付款方发起争议 ──→ 提交证据 ──→ 仲裁方审查 ──→ 裁决
                                                    │
                                     ┌──────────────┴──────────────┐
                                     ▼                             ▼
                               Release to Provider           Refund to Client
                               (仲裁支持服务方)                (仲裁支持付款方)
```

争议设计至少回答：

-   谁能发起？发起成本多少？
    
-   证据提交格式是什么？
    
-   谁有裁决权？（人工仲裁 / 多签 / DAO / optimistic challenge）
    
-   裁决后是否可申诉？
    
-   小额争议 vs 大额争议是否需要不同流程？
    

**关键**：没有成本的争议容易被滥用；成本过高让小额任务无法维权。

### 4.5 Timer Watcher（超时监视器）

**职责**：监控所有活跃 job 的截止时间，在超时后触发退款。

```
┌─────────────────────┐
│  Timer Watcher       │
│                      │
│  监控所有 Funded/    │
│  Submitted 状态的 job│
│                      │
│  if now > expiredAt: │
│    claimRefund(id)   │
│    → 资金退回 client │
│    → 状态 → Expired  │
└─────────────────────┘
```

-   `claimRefund` 不挂 hook（ERC-8183 硬性要求）——确保退款永远是逃生口
    
-   任何人都可调用，防止 watcher 宕机导致资金永久锁定
    
-   超时后的声誉影响由 hook 在 `claimRefund` 之外处理
    

### 4.6 Reputation Recorder（声誉记录器）

**职责**：在交易完成后将结果写入声誉系统。

```
Complete → reputation.giveFeedback(
    agentId, 100, 0, "job_completed", category, evidenceURI, reasonHash
)

Rejected → reputation.giveFeedback(
    agentId, 0, 0, "job_rejected", reasonCategory, evidenceURI, reasonHash
)
```

-   写入 ERC-8004 Reputation Registry（或自定义声誉合约）
    
-   `reason` 参数（attestation hash）作为证据链接
    
-   声誉数据反过来喂给任务发现和竞价选择
    

* * *

## 五、验收（Acceptance）的四种模式

| 模式 | 适用场景 | Evaluator | 延迟 | 安全性 |
| --- | --- | --- | --- | --- |
| 即时自动 | 脚本验证、格式检查、hash 匹配 | 合约 / 脚本 | 即时 | 低（受限于规则完整性） |
| AI 初审 | 报告生成、数据标注、代码任务 | AI Agent | 秒级 | 中 |
| AI + Challenge Window | 中等价值任务 | AI + 等候期 | 小时级 | 高 |
| 人工审核 | 高价值、高风险、复杂任务 | 人类 / DAO | 天级 | 最高 |

**推荐组合策略**：AI 初审 + challenge window + 人工复核。低风险自动通过，高争议不会由模型一次判断决定资金归属。

* * *

## 六、结算全链路数据流

```
步骤          off-chain                           on-chain
────          ─────────                           ────────
1. 发现      Agent A 查 ERC-8004 Registry
             找到 B 的 agentURI / endpoints
             查看 B 的历史声誉
             ↓
2. 报价      B 签名报价，A 选择
             ↓
3. 创建任务  A 创建 job (taskId, desc) ──────→  createJob()
             ↓                                    │
4. 锁定资金  A 批准代币                             │
             ↓                                    │
             fund() ──────────────────────────→  fund()
                                                  │ (资金锁定)
             ↓                                    │
5. 执行      B 执行任务                             │
             交付物存 IPFS                          │
             ↓                                    │
             submit(deliverableHash) ──────────→  submit()
                                                  │ (状态→Submitted)
             ↓                                    │
6. 验收      Evaluation 结果                        │
             (脚本/AI/人工)                         │
             ↓                                    │
             complete(reasonHash) ─────────────→  complete()
                                                  │ (资金释放给B)
             ↓                                    │
7. 沉淀      Reputation Recorder                    │
             写 ERC-8004 Reputation                │
                                                  │
             ←──────────────────────────────────   Receipt Event
```

* * *

## 七、关键架构决策清单

| # | 决策 | 选项 | 推荐 |
| --- | --- | --- | --- |
| 1 | 链上-链下边界 | 资金+状态在链上 vs 全链上 | 资金+终态在链上，业务在链下 |
| 2 | 支付代币 | 单一代币 vs 多币种 | 开始用单一 USDC，后续多币种 |
| 3 | Provider 设定 | 创建时固定 vs 延迟设定 | 支持延迟（bidding 场景） |
| 4 | Evaluator 类型 | EOA vs 智能合约 | 低风险用 EOA(client)，高风险用合约 |
| 5 | 验收方式 | 自动 vs 人工 vs 混合 | AI 初筛 + 人工兜底 |
| 6 | 争议裁决 | 多签 vs DAO vs Optimistic | 小额自动规则，大额多签 |
| 7 | 声誉存储 | 链上 vs 链下 | ERC-8004 Reputation Registry（链上） |
| 8 | Hook 使用 | 无 hook vs 可插拔 | 必选（写声誉的核心接口） |
| 9 | 超时兜底 | 任何人均可 claimRefund | ERC-8183 规范要求 |
| 10 | 费用 | 无 vs 平台抽成 | 可选，只在 Completed 时收取 |

* * *

## 八、与 ERC-8183 + ERC-8004 的关系

本架构骨架是 **ERC-8183 (Agentic Commerce) + ERC-8004 (Trustless Agents)** 的具体化设计：

| 架构组件 | 对应标准 |
| --- | --- |
| Escrow 状态机 | ERC-8183 Core |
| 角色模型 (client/provider/evaluator) | ERC-8183 Roles |
| Hook 扩展 | ERC-8183 IACPHook |
| Attestation (complete/reject reason) | ERC-8183 Events |
| Agent 身份 + 收款地址 | ERC-8004 Identity Registry |
| 声誉数据 | ERC-8004 Reputation Registry |
| 验证请求 | ERC-8004 Validation Registry |

详见：

-   [erc-8183-agentic-commerce](erc-8183-agentic-commerce) — 标准协议细节
    
-   [erc-8004-trustless-agents](erc-8004-trustless-agents) — 身份/声誉/验证标准
    
-   [erc-8183-erc-8004-integration](erc-8183-erc-8004-integration) — 四种串联模式
    

* * *

## 九、最小可行实现（MVP）

### 合约层

```solidity
// 最小 escrow 合约 (基于 ERC-8183 简化)
contract MinimalAgentEscrow {
    struct Job {
        address client;
        address provider;
        address evaluator;
        address token;
        uint256 budget;
        uint256 deadline;
        Status status;
        bytes32 deliverableHash;
    }

    enum Status { Created, Funded, Submitted, Completed, Rejected, Expired }

    mapping(uint256 => Job) public jobs;
    uint256 public nextJobId;

    function createJob(address provider, address evaluator, uint256 deadline, string calldata desc) external returns (uint256);
    function fund(uint256 jobId) external;
    function submit(uint256 jobId, bytes32 deliverable) external;
    function complete(uint256 jobId, bytes32 reason) external;
    function reject(uint256 jobId, bytes32 reason) external;
    function claimRefund(uint256 jobId) external;  // 超时后
}
```

### 编排层（最小结构）

```
backend/
├── cmd/
│   └── escrow-engine/        # 启动入口
├── internal/
│   ├── task/                 # 任务管理
│   ├── statemachine/         # 状态机逻辑
│   ├── evaluator/            # 验收调度
│   ├── timer/                # 超时监控
│   ├── reputation/           # 声誉写回
│   └── contract/             # 链上交互（合约 ABI 封装）
├── pkg/
│   └── types/                # 共享类型
└── config/
    └── config.yaml           # 链 RPC / 代币 / evaluator 配置
```

### 验收配置示例 (config.yaml)

```yaml
evaluators:
  - name: "script-checker"
    type: script
    command: "./check-format.sh"
    risk_max: 100     # USDC
  - name: "ai-evaluator"
    type: llm
    model: "claude-sonnet-4"
    risk_max: 5000
  - name: "human-review"
    type: manual
    risk_min: 5000    # >5000 USDC 必须人工
```

* * *

## 十、总结

Agent Settlement & Escrow 架构的核心要点：

1.  **三层分离**：Agent / Orchestration / Settlement，各层职责清晰
    
2.  **链上只做资金，链下做业务**：降低 gas 成本，同时保留资金安全性
    
3.  **状态机是核心**：每个状态规定谁触发、需要什么证据、超时怎么处理
    
4.  **验收分层**：脚本 → AI → 人工，按风险递进
    
5.  **Hook 是万能胶**：声誉、验证、争议，所有扩展都通过 Hook 接入
    
6.  **超时是安全网**：`claimRefund` 不可被 hook 拦截，保证资金永远可回收
    
7.  **声誉形成闭环**：交易完成 → 声誉沉淀 → 更好的 Agent 发现 → 更高质量的交易
    

这个骨架可以直接作为实现 Agent Commerce 系统的蓝图。从 MVP 开始（最小 escrow 合约 + 编排层），逐步加入验收、争议、声誉模块。
<!-- DAILY_CHECKIN_2026-05-27_END -->

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
