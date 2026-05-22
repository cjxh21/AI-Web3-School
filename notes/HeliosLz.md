---
timezone: UTC+8
---

# Helios

**GitHub ID:** HeliosLz

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-22
<!-- DAILY_CHECKIN_2026-05-22_START -->
\# 2026-05-22 学习日志

\## 今日主题

**Frameworks（LangChain / LangGraph / Agents SDK 选型）** —— \[Handbook 章节\]([https://aiweb3.school/zh/handbook/ai/frameworks/](https://aiweb3.school/zh/handbook/ai/frameworks/))

\- 关联 cohort Week：Week 1 / AI 侧

\- 模式：\*\*闭卷读 + 复述\*\*（对照 5.20、5.21 的"边讲边问"做元观察）

\- 提交入口：[https://intensivecolearn.ing/en（"Check-in](https://intensivecolearn.ing/en（"Check-in)" 按钮）

\## 复述前的元约定（执行顺序）

1\. **先**：自己打开 Handbook 闭卷读完整章（Agent 不预先讲、不预先总结）

2\. **再**：关掉 Handbook 标签页，在下面"我用自己的话复述"栏写 → 写完才可参考原文修订

3\. **然后**：Agent 独立读 Handbook 写"精炼摘要"，\*\*与复述对照\*\*找出漏点和误读

4\. **最后**：基于漏点决定卡点 / 最小实验 / 打卡草稿

\## 我用自己的话复述（关掉 Handbook 标签页再写）

\> 维度建议（不强制按顺序）：

\> - LangChain / LangGraph / Agents SDK 各自解决什么核心问题、各自的抽象边界

\> - 三者的取舍轴（状态管理 / 控制流 / 工具调用 / 可观测 / 部署形态）

\> - 什么场景下不该用框架（即"自己写更短"的判据）

\> - 跟我手上的 Hermes Agent 现状结合，今天读完会改变哪个决定

\### 第一轮（一句话定位）

\> LangChain 解决了"组件太多怎么连接"的问题；LangGraph 解决了"模型太不可控，如何用确定性状态机卡死边界"的问题；而 OpenAI Agents SDK 解决了"如何让模型原生、轻量、并具备标准沙盒能力地进行多智能体协同"的问题。

\### 第二轮（按其余维度展开，对照后再写）

\- 取舍轴：

\- "自己写更短"的判据：

\- 跟 Hermes Agent 的决策影响：

\## Agent 整理的精炼摘要（学员复述后独立读 Handbook 再写）

**Handbook 一句话**：框架不是为了让你少写 API 调用，而是把模型 / 工具 / 状态 / 检索 / 评估 / 部署组织成可维护系统。\*\*选错的代价不是"跑不起来"，是"调不动 / 测不了 / 换不掉"。\*\*

**第一性原理（章节宣言）**：\*\*框架是系统边界的表达，不是智能本身。先理解工作流，再决定用不用框架。\*\* 三条具体原则：

1\. **简单链路保持简单**——一次调用 + 一次检索不需要 Agent 框架

2\. **长流程需要显式状态**——多步 / 工具 / 人工确认 / 失败恢复要有可查询 state，不能只靠聊天历史

3\. **框架要能退出**——换模型 / 向量库 / 部署方式不应被锁死

**6 个知识节点**：

| 节点 | Handbook 定位 | 何时用 / 何时不用 |

|---|---|---|

| **LangChain** | 组件库（model / prompt / tools / retriever / agent / output parser） | 适合快速组合能力；\*\*警告"抽象太早"\*\*——工作流没搞清楚就套 chain/agent，后面排查会变难 |

| **LangGraph** | 工作流和状态机（graph = node + edge + state） | **判断标准明确**："只要你开始关心任务走到哪一步、能否恢复、失败后从哪里继续，就应该考虑 graph" |

| **OpenAI Agents SDK** | 把 Agent 工程问题做成可组合结构：\*\*指令+工具 / handoff / guardrails / tracing\*\* | **边界仍然由你定义**：哪些工具可用 / 哪些动作需要确认 / 什么算失败 |

| **DSPy** | 把 prompt / LM pipeline 写成\*\*可优化的程序\*\*（signatures / modules / optimizers） | 适合有数据集 + 评估指标 + 可重复任务（分类 / 抽取 / 问答 / rerank / 复杂推理）。\*\*关键启发\*\*：不要靠感觉调 prompt |

| **Hermes** | **不是通用框架**，是"面向工具调用和结构化输出的模型 / agent 生态" | **提醒**：框架不是唯一抽象层，\*\*模型本身能力\*\*（tool calling / JSON / long context / reasoning）也影响系统设计 |

| **Learning Agent** | 从反馈 / 日志 / 评估改进（不一定训练模型，也可以是更新 prompt / 补规则） | **陷阱**：把线上反馈直接变成行为变化 → 数据污染 / 越权学习 / 不可解释。\*\*纪律\*\*：先进评估闭环再进生产 |

**AI × Web3 中的分工**（章节明确给出）：

\- **AI Framework** 管 prompt / tools / state / eval / trace

\- **Web3 基础设施** 管账户 / 签名 / 合约 / 交易 / 链上状态

\- **产品层** 定义用户目标 / 权限边界 / 确认流程 / 失败处理

\- **关键句**：\*\*框架可以组织 Agent，不能替用户承担资产风险\*\*

**Handbook 推荐的最小实践**：文档问答 + 工具调用，\*\*同一任务两种实现\*\*：

1\. 裸 API：用户问题 + 检索结果 + JSON 输出

2\. 框架版：相同输入输出 + tool schema + trace + 失败重试 + 测试样本

对比 4 件事：可读性 / 加工具难度 / 定错难度 / 写回归测试难度。\*\*重点不是选冠军，是看清框架到底帮了什么。\*\*

\## 对照差异（复述 vs Agent 摘要）

\### 漏点（Handbook 写了 / 我复述没写）

1\. **DSPy** —— 完全没提。是 6 个知识节点之一，"让 prompt/pipeline 可优化"是独立的抽象层（不在 LangChain / LangGraph / Agents SDK 的同一维度上）

2\. **Hermes** —— 完全没提。这条\*\*特别值得警觉\*\*：我手上的项目就叫 Hermes Agent，但读 Handbook 时居然漏过去了。Handbook 把它定位成"模型生态而非框架"，提醒"框架不是唯一抽象层，模型本身能力会影响系统设计"——这跟我项目命名的语义还不一样

3\. **Learning Agent** —— 完全没提。"反馈如何安全进入系统"，明确警告"线上反馈直接变行为 = 数据污染 + 越权 + 不可解释"

4\. **第一性原理本身** —— Handbook 的核心宣言是"\*\*先理解工作流，再决定用不用框架\*\*"。我的复述直接进入"哪个框架解决什么问题"，跳过了"是否要用框架"这一步——\*\*犯了 Handbook 明确警告的错误：先框架后工作流\*\*

5\. **"框架要能退出"** —— 一条工程纪律。我没体现"换模型/向量库/部署"的可逆性约束

6\. **LangGraph 的判断公式** —— "只要你开始关心任务走到哪一步 / 能否恢复 / 失败后从哪里继续，就用 graph"。我写了"卡死边界"但没写\*\*什么时候需要卡\*\*的判据

7\. **AI × Web3 三层分工** —— 这是 Handbook 给的核心 framing，且\*\*跟我昨天的 session key 工作直接接口\*\*：AA / session key 属于 Web3 基础设施层，框架不该越界承担资产风险

8\. **元判断** —— "最重要的判断不是哪个最流行，而是它帮你管哪一层复杂度，又把哪些复杂度藏起来了"。我的复述是"解决什么"，没写"藏起什么"——后者才是债务来源

\### 误读（我写错的）

1\. **"OpenAI Agents SDK = 多智能体协同 + 标准沙盒"** —— 偏了。Handbook 列的 4 个工程要素是 **指令+工具 / handoff / guardrails / tracing**。"沙盒"如果指 guardrails 那只是一个组件不是定位；"多智能体协同"只是 handoff 的解读，SDK 同样适用于单 agent。\*\*它的核心定位是"把 Agent 工程问题做成可组合结构"，不是"多智能体专用"\*\*

2\. **"LangGraph = 用确定性状态机卡死边界"** —— "卡死边界"语义偏向 guardrails。Handbook 的重点是\*\*显式状态让长流程可恢复 / 可查询 / 可分支\*\*。LangGraph 解决的不是"模型不可控"，是"长流程的可追踪性"——这两个问题不一样

\### 额外洞察（我写了 / Handbook 没强调）

1\. **"组件太多怎么连接"** —— 比 Handbook 的"组件库"更生动，\*\*抓住了 LangChain 的本质动机\*\*（用户角度看到的现象是组件爆炸）

2\. **三句对仗结构（解决了 X 的问题）** —— 把三者放在同一对仗里很清晰，但\*\*遮盖了它们不在同一抽象层\*\*这件事：LangChain 是组件层 / LangGraph 是控制流层 / Agents SDK 是工程要素层。\*\*对仗易记，但分层信息丢了\*\*——下次复述要警惕"句式工整 ≠ 模型正确"

\### 元观察（闭卷读+复述 vs 边讲边问）

\- **闭卷复述 = 暴露选择性记忆**：我只记住了"看起来有结构感"的前三个（LangChain / LangGraph / Agents SDK），DSPy / Hermes / Learning Agent 三个就直接漏了。\*\*这是边讲边问模式下不会发生的\*\*——昨天 Agent 一节一节抛题，每节都被迫处理。今天直接证明：\*\*闭卷模式的盲区是"读时未感到信息密度差异"的章节\*\*

\- **闭卷复述 = 暴露句式偏好**：我下意识把三者套进"X 解决了 Y 的问题"的对仗。\*\*对仗压力会扭曲对原文的呈现\*\*（让我把 SDK 强行解读成"多智能体"以匹配"模型不可控"那种戏剧性叙述）

\- **结论**：两种模式不是优劣，是测试不同东西。\*\*边讲边问测的是当下理解；闭卷复述测的是事后留存 + 自发结构\*\*。盲区不同，\*\*应该交替使用而不是择一\*\*

\## 边讲边问对话精要（11 题）

\> 闭卷模式中途因 Agent 程序错误中断（Agent 在学员只答完 1/4 维度时就提前抓 Handbook 写摘要+对照，污染了剩余维度），切回 5.20、5.21 用过的 "Agent 一节一节讲 + 抛 1-2 题" 模式。

**重大上下文揭露（Q6 之后）**：Hermes Agent 是 **ETH solo staking agent**。这条信息\*\*应该开场前就问\*\*——之前 5 题都是在不知道 Agent 干什么的情况下问框架选型，等于让学员盲答。揭露之后所有判断都要重估。

\### 关键认知（按价值排序）

1\. **第一性原理 = "先工作流后框架"**（Q2 应答）

\- 学员第一题就用 Handbook 同源词（"边界"）说明应先画工作流——和章节宣言"框架是系统边界的表达"自然对齐

\- 这条对 ETH staking agent **不只是建议是强制**：staking 协议本身就是工作流（key gen → deposit → activation → attestation → exit），框架是工具

2\. **LangChain 不对症**（Q3 误读暴露）

\- 学员被问"LangChain 能解决你的 state 痛点吗"时，\*\*悄悄把问题滑到"agent 黑盒"\*\*——一个对的但不同的问题

\- 学习点：\*\*当被问 "X 解决你的痛点吗"，下意识切到 "X 没做到的另一件事"——这是常见回答模式，但绕过了原问题\*\*

\- 正确回答应该是"LangChain 解决组件连接，\*\*没解决我的状态管理痛点\*\*，所以不对症"

3\. **LangGraph 判断公式 = FSM 的定义**（Q8 自发推导）

\- Handbook 的判断公式三条触发条件：走到哪一步 / 能否恢复 / 失败后从哪继续

\- 知道 staking 上下文后\*\*三条全部强触发\*\*——deposit 是不可逆事件，"重启"在很多 staking 步骤里 = 损失资金

\- 学员 Q8 用自己的话描述"重启决策点"应该看 **(a) 状态 (b) 失败类型 (c) 时间窗口**——这就是 FSM 的定义`(state, event, elapsed) → next_state`

\- **关键洞察**：\*\*框架不是给你新能力，是强迫你显式写出这张表。不用框架你也得有这张表，没有就是 bug。\*\*

4\. **Guardrails vs Session Key = 层次差异**（Q10 半对）

\- 学员说"同一类，可以自动转译"——结构上对，但\*\*漏了信任边界层级\*\*：

\- Guardrails = 应用层声明（advisory，Agent 自检）

\- Session Key = 共识层强制（enforced，链上他检）

\- 关系是 **mirror 不是 equivalent**：链上 policy 是真理源，guardrails 是镜像（让 Agent fail fast）

\- **这一点直接让 hackathon "Agent Wallet Policy Auditor" 想法的核心浮出**：核心不是"红队自检"，而是 **policy 跨层同步工具**（on-chain canonical → off-chain mirror）。红队是加分功能

5\. **Agents SDK 选型的自相矛盾**（Q9 留作未解决张力）

\- 学员自评 "需要显式 state"，但选了 Agents SDK 而非 LangGraph

\- SDK 不提供 state machine，事实上意思是 "我自己写 FSM + SDK 做 guardrails/tracing"

\- 未做最终决定，留作 follow-up

\### 元观察（闭卷读+复述 vs 边讲边问，对照实验结论）

\- **闭卷复述暴露盲区**：6 个知识节点中只记住 3 个（LangChain/LangGraph/SDK），DSPy / Hermes / Learning Agent **完全没出现在复述里**。闭卷模式的盲区 = "读时未感到信息密度差异"的章节

\- **闭卷复述暴露句式偏好**：下意识用 "X 解决了 Y 的问题" 对仗——对仗压力扭曲了对原文的呈现，强行把 SDK 解读为 "多智能体" 以匹配句式

\- **闭卷被中断暴露另一类风险**：协议本身可能因对方（Agent / 协作者）的错误失败——任何"严格协议"在协作里需要恢复路径，这一点\*\*跟 session key 的 escalation 设计同构\*\*

\- **两种模式不是优劣，是测试不同东西**：边讲边问测当下理解（被迫每节处理）；闭卷复述测事后留存+自发结构。\*\*应该交替使用而不是择一\*\*

\### 没在边讲边问里覆盖的节点

DSPy / Hermes / Learning Agent / AI×Web3 分工 / 最小实践——只在 "Agent 整理的精炼摘要" 中文本性覆盖，\*\*未做对话式深加工\*\*。明天或后续补做。

\## 今日最小实验

\> 今天没跑代码实验。\*\*实质性"实验"是用 11 题的边讲边问把 Frameworks 章节跟 Hermes ETH staking 上下文对接\*\*，并暴露了两个值得记录的认知点（FSM 定义浮现 + guardrails/session-key 层次差异）。

\- **完成的"概念实验"**：把 Handbook 6 节点中前 3 个（LangChain / LangGraph / Agents SDK）跟 Hermes 实际需求做对症分析

\- **Handbook 推荐的代码实验未做**："文档问答 + 工具调用" 两种实现（裸 API vs 框架）对比 4 件事——\*\*滚动到 follow-up，最迟 5.24 Week 1 复盘前补上\*\*

\- **已产生的副产品**：Auditor 想法的\*\*核心定位\*\*从"红队自检"修正为"policy 跨层同步工具"——这是今天对 hackathon ideation 最实质的推进

\## 我的卡点

\> 任何卡点同步整理一份到 `handbook-feedback/`，包含：Handbook 链接、问题描述、建议改法。

\- \[ \] **Hermes 项目命名 vs Handbook Hermes 节点**：Handbook 的 Hermes 指 Nous Research 的 "面向工具调用和结构化输出的模型生态"。我项目叫 Hermes Agent 但做的是 ETH solo staking——\*\*两者同名不同源\*\*？还是我的命名隐含了对 Nous Hermes 的引用？需要确认（5 分钟工作，但要做，避免后续误会）

\- \[ \] **Q9 未决张力**：自评需要 state machine 但选了不提供 state machine 的 SDK。三个出路（自己写 FSM + SDK / 换 LangGraph / LangGraph + SDK 组合）需要做架构决定——这是一个设计问题，不是今天能定的

\- \[ \] **DSPy 在 staking 场景的相关度未评估**：DSPy 强调 "数据集 + 评估指标 + 可重复任务"——staking 的哪些子任务匹配这个模式？validator performance 评估？exit 时机决策？需要补

\- \[ \] **Learning Agent 的安全模式 vs Agent 自主决策**：Handbook 警告"线上反馈不能直接变行为"——但 staking agent 长期运行就是要从 validator 历史学。这两条怎么调和？需要补

\## Follow-up

\### 从 5.21 继承

\- \[ \] **决策**：etherscan 读 USDC + AA 钱包对比实验——已推迟 3 次，\*\*判定为放弃\*\*（hackathon 方向已经聚焦到 Auditor，对比实验对当前路径价值不足）

\- \[ \] **已修正**：把 "Agent Wallet Policy Auditor" 落进 `hackathon/ideation.md`——\*\*核心定位修正为 policy 跨层同步工具\*\*（不是红队自检）。下一日开 `hackathon/ideation.md` 写第一份候选条目，用 cohort 5 问框架

\- \[ \] ERC-4337 + ERC-7562 原文阅读（推到 5.23 Evaluation 节点之前——Evaluation 跟 staking validator 表现评估强相关，前后顺序对的）

\- \[ \] Rhinestone Smart Sessions 文档 + ZeroDev SDK 文档——\*\*已升级优先级\*\*：Auditor 想法落地必须先确认这些库的 policy schema 是什么样

\### 今日新增

\- \[ \] **代码实验补做**：Handbook 推荐的 "文档问答 + 工具调用" 两种实现对比——\*\*最迟 5.24 Week 1 复盘前\*\*做，否则 Frameworks 节点等于只读不练

\- \[ \] **DSPy / Hermes / Learning Agent 节点补做**：今天边讲边问只覆盖前 3 节，剩下 3 节需要补——建议 5.24 复盘日批量补

\- \[ \] **Q11 架构决定**：FSM 实现路径（自研 / LangGraph / LangGraph+SDK 组合）——在 Week 2 开始前做出决定

\- \[ \] **元观察归档**：闭卷复述 vs 边讲边问的对照结论已经稳定，从下周开始\*\*显式标注每天用哪种模式\*\*，4 周后累计够做一次小复盘

\## Handbook / 课程反馈

\- \[ \] **建议**：Frameworks 章节缺少一张\*\*"如何选"的决策树\*\*。读完 6 个节点容易记住每个"是什么"，但 "我的项目应该用哪个" 没有引导。建议加一张：从"任务复杂度 / state 需求 / 可观测需求 / 是否多 Agent" 出发的 2 层决策树

\- \[ \] **建议**：Hermes 节点容易和 Nous Research 的 Hermes 模型系列混淆，节点开头建议加一句"这里指 Nous Research 的 Hermes 系列"避免歧义（特别是有人项目就叫 Hermes 的时候）

\- \[ \] **建议**：章节宣言 "框架是系统边界的表达，不是智能本身" 是整章最锋利的一句，但\*\*藏在"第一性原理"小节中段\*\*——建议提到章节开头副标题位置，避免读者快速浏览时跳过

\- \[ \] **建议**：最小实践给了"裸 API vs 框架"对比 4 件事，但\*\*没给推荐数据集 / 任务示例\*\*——建议提供一个最小可复制任务（比如"用 SEC 文档问答 + 1 个工具调用"），降低读者动手成本

\- \[ \] 凑够 5 条进 `handbook-feedback/`：今天 4 条 + 5.21 已写 2 条 - 重叠 = **6 条左右**，可以开始统一整理提交

\## 打卡草稿（粘到 [intensivecolearn.ing](http://intensivecolearn.ing) Check-in 表单的 Markdown）

\`\`\`markdown

**Frameworks 章节 —— 先工作流后框架；以及 Hermes Agent (ETH solo staking) 的状态机困局**

今天读 Handbook 的 Frameworks 章节，最锋利的一句是开篇的宣言：\*\*"框架是系统边界的表达，不是智能本身。先理解工作流，再决定用不用框架。"\*\* 这句话排在所有具体框架介绍之前，反对的失败模式是"先引入框架，再让产品逻辑迁就框架"。

学习模式上做了一次对照实验：原计划用闭卷读+复述（vs 5.20、5.21 的边讲边问）。闭卷复述结果暴露两个盲区——(1) **选择性记忆**：6 个知识节点只记住前 3 个（LangChain / LangGraph / Agents SDK），DSPy / Hermes / Learning Agent 完全没出现在复述里；(2) **句式偏好扭曲**：下意识用 "X 解决了 Y 的问题" 对仗，为了句式工整把 SDK 强行解读为 "多智能体专用"——但 Handbook 的 4 个工程要素（指令+工具 / handoff / guardrails / tracing）并不暗示 SDK 是多 Agent 专用。\*\*结论：闭卷测事后留存+自发结构，边讲边问测当下理解，应该交替而不是择一。\*\*

切回边讲边问后讨论的关键认知：

**1\. LangGraph 判断公式 = FSM 的定义**。Handbook 说"只要你关心任务走到哪一步 / 能否恢复 / 失败后从哪继续，就考虑 graph"。我自己描述"重启决策点"应该看的变量是 **(状态, 失败类型, 时间窗口)**——这就是有限状态机`(state, event, elapsed) → next_state`。\*\*框架不是给你新能力，是强迫你显式写出这张表。不用它你也得有这张表，没有就是 bug。\*\*

**2\. 我的 Hermes Agent 是 ETH solo staking agent**——多个一次性不可逆步骤（key gen、deposit、attestation 签名），"重启"在很多步骤里 = 损失资金。Handbook 的判断公式三条全部强触发。Agents SDK 的 4 要素里 guardrails+tracing 对 staking 是必备，但 SDK **不提供 state machine**——我之前选 SDK 的判断其实是 "我自己写 FSM + SDK 做外围"，是一个明确的工程决定，不是"比较简单"的轻量选择。

**3\. Guardrails vs Session Key 不是同一类东西，是 mirror 关系**。两者表面都是"哪些动作允许"，但\*\*信任边界差一层\*\*：guardrails 是 Agent 自检（应用层，advisory），session key 是链上他检（共识层，enforced）。这一条\*\*让昨天 follow-up 里的 "Agent Wallet Policy Auditor" 想法的核心从"红队自检"修正为"policy 跨层同步工具"——给定链上 policy 自动生成应用层 mirror guardrails，让 Agent 在发起 UserOp 前 fail fast。红队是加分功能，不是核心。\*\* 这是单 AI 侧和单 Web3 侧都做不出来的真交叉。

**4\. AI × Web3 三层分工**（Handbook 给的，直接接 Hermes）：AI Framework 管 prompt / tools / state / eval / trace；Web3 基础设施管账户 / 签名 / 合约；产品层定义 human-in-the-loop 边界。\*\*框架可以组织 Agent，不能替用户承担资产风险\*\*——这正是 staking agent 必须守住的红线。

今天没跑代码实验（Handbook 推荐的"裸 API vs 框架"对比留作 follow-up，最迟 5.24 复盘前补）。明天进 Evaluation 节点——跟 staking validator 表现评估强相关，前后顺序刚好。

\`\`\`

\- 提交入口：[https://intensivecolearn.ing/en](https://intensivecolearn.ing/en) → 登录 → AI × Web3 School → 左侧 "Check-in"

\- 提交后回填提交时间 / 截图：
<!-- DAILY_CHECKIN_2026-05-22_END -->

# 2026-05-21
<!-- DAILY_CHECKIN_2026-05-21_START -->

\# 2026-05-21 学习日志

\## 今日主题

**账户抽象（Account Abstraction）** —— \[Handbook 章节\]([https://aiweb3.school/zh/handbook/web3/account-abstraction/](https://aiweb3.school/zh/handbook/web3/account-abstraction/))

cohort Week 1 / Web3 侧。AA 是 Agent Wallet 的前置——昨天读完 Smart Contract，今天看"合约如何吃掉账户"。

\## Agent 整理的精炼摘要

**一句话**：账户抽象把"账户如何验证、谁付 gas、哪些权限自动执行"从协议硬编码里释放出来，让账户变成可编程合约。\*\*核心不是免 gas，是把账户控制权从私钥扩展成可编程规则。\*\*

**第一性原理**：账户可编程之后，权限模型从"有私钥/没私钥"变成"在什么条件下允许什么动作"。引申三条可定制：

\- **验证逻辑可定制**：多签 / Passkey / 社交恢复 / 模块规则

\- **支付逻辑可定制**：用户 / 应用 / Paymaster / 其他资产承担 gas

\- **权限可最小化**：session key 限定合约 / 方法 / 额度 / 时间 / 链

**5 个知识节点**：

| 节点 | 难度 | 一句话 |

|---|---|---|

| **ERC-4337** | 中级 | 不改协议、用 alt mempool + EntryPoint 合约塞进可编程账户。流程：UserOp → Bundler 打包 → EntryPoint 验证执行 → 可选 Paymaster 付费 |

| **Smart Account** | 中级 | 账户即合约。多签/恢复/批量/策略全写进账户。\*\*继承所有合约风险\*\*（bug / 模块 / 升级 / 外部依赖） |

| **Bundler** | 中级 | 收集 UserOp，\*\*先模拟再上链\*\*。失败面：模拟与执行不一致（状态漂移） |

| **Paymaster** | 中级 | 第三方代付 gas / 用非原生资产付。失败面：\*\*spam 与套利\*\*（静态规则 vs 对抗博弈） |

| **Session Key** | 高级 | capability-based security 的链上实现。钥匙形状 = 合约 × 方法 × 额度 × 时间 × 链 的合取，\*\*blast radius 有界且可证\*\* |

**4337 流程示意**：

\`\`\`

用户/应用生成 UserOperation

→ Bundler 收集 + 模拟（验证签名、nonce、余额、策略）

→ 提交到 EntryPoint 合约

→ EntryPoint 调用 Smart Account.validateUserOp（可编程验证）

→ EntryPoint 调用 Smart Account 执行目标动作

→ Paymaster 可选介入决定谁付 gas

→ 成功：状态更新 + emit event

→ 失败：revert（但 Bundler 已付了底层 tx gas）

\`\`\`

**对比表（EOA vs 4337）**：

| | 普通 EOA | ERC-4337 |

|---|---|---|

| 用户发什么 | Transaction | `UserOperation`（\*\*意图\*\*，不是真交易） |

| 验证 | 钱包本地验 ECDSA | EntryPoint 调 Smart Account 合约验签（可编程） |

| 打包 | 矿工 / Sequencer | **Bundler**（包装成普通 tx 发出去） |

| Gas | 用户原生代币 | **Paymaster** 可代付 / 用别的资产付 |

| 权限 | 单私钥 = 全权限 | Smart Account 规则 + **Session Key** 切片 |

**AI × Web3 中的位置**：

\> 没有 AA，Agent 只能停留在"给建议"或"让用户每一步都签名"。

\> 有 AA，Agent 可以在\*\*受限范围内\*\*自动执行。

\> **账户抽象不是让 AI 更自由，而是让 AI 的自由被规则包起来。**

\## 我用自己的话复述（边讲边问模式）

\> 沿用昨天 mode：Agent 一节一节讲，每节抛 1–2 题让我回答。下面是对话中真实输出过的我的版本。

\- **"AA 的核心不是免 gas" 怎么读**：免 gas 是营销卖点，\*\*可编程权限\*\*才是主线。把"免 gas"放在主线外，是 Handbook 在防"AA = 让别人帮我付钱"的肤浅理解——它强调本体是可编程，免 gas 只是支付逻辑可编程的一个\*\*特例\*\*。

\- **三条可定制中我最在意哪条**：\*\*权限最小化\*\*。理由："\*\*金融产品中最重要的是损失可控\*\*"。Agent 拿主私钥 = blast radius 等于整个钱包；session key 把"全有/全无"拆成维度 × 阈值，损失就有界了。

\- _Agent 补的 nuance_：这就是 capability-based security 的链上实现——传统 ACL 是"你是谁→你能做什么"（基于身份），capability 是"你拿着什么形状的钥匙→只能开那把锁"（基于能力）。

\- **Bundler 模拟通过但上链失败会在什么情况下发生**：\*\*链上状态被抢先改变\*\*（front-run / 状态漂移）或\*\*模拟环境与真实执行环境不一致\*\*。

\- _Agent 补的细节_：社区有 **ERC-7562**（validation rules）限制 Smart Account 在\*\*验证阶段\*\*能访问什么 storage、不能调外部合约、不能读 oracle——目的就是让模拟贴近现实。但\*\*执行阶段\*\*没有这种限制，所以状态漂移仍然存在。实操含义：模拟是必要不充分条件，关键检查要落到 `validateUserOp` 里。

\- **Paymaster 风控 5 问最难的是哪个**：\*\*如何防止 spam 和套利\*\*。理由：白名单、额度、过期都是\*\*静态规则\*\*，写一次就定型；spam/套利是\*\*对抗博弈\*\*，攻击者主动找规则边缘。

\- _Agent 补的攻击范式_：通过被赞助的 UserOp 去触发 DEX 套利路径，让 Paymaster 替自己付 gas 完成提取——你的 Paymaster 成了对手方的免费工具。这跟 Web2 反欺诈同构，但 Paymaster 的"水龙头"对任何地址全开。

**最重要的概念串联**：跟昨天 Smart Contract 的"三时间轴 audit 框架"接上了——

\- **写合约时定规则**（事前 = Upgrade audit）

\- **签 session key 时定规则**（事前 = 授权契约）

\- **Agent 执行时按规则**（事中 = Solidity / EVM / ABI）

\- **执行后写 event**（事后 = 审计日志）

四层都是"把自由包进规则里"。AA 不是新事物，是\*\*把合约的"事先可验证"模型从'我能不能调用'扩展到'账户该不该执行'\*\*。

\## 读 Handbook 时的 scratchpad

\> 第二天用边讲边问模式，Handbook 没自己闭卷读。

\> 元观察（第二次确认）：边讲边问对\*\*概念密集\*\*章节有效——每节抛题让我答，"卡点"被实时压到当下，不会留到笔记里。

\> 但今天有一个 follow-up 卡点没消化：\*\*ERC-7562 的具体存储隔离规则\*\*（验证阶段到底能/不能读哪些 slot）—— Agent 提了名字没展开，我自己也没追问，先记着。

\## 今日最小实验

✅ **完成** —— 写了一份完整的 Session Key 策略：

📄 `experiments/session-keys/2026-05-21-hermes-tool-payment.md`

**场景**：Hermes Agent 在 Base Sepolia 上自动为已注册工具调用付费。

**策略要点（4 层切片）**：

1\. **Identity**：session\_id + issuer (Smart Account) + holder (Agent 临时密钥) + 签发签名

2\. **Scope**：chain\_id 84532；只允许 ToolRegistry.payForCall + USDC.approve（spender 限定 ToolRegistry）

3\. **Limits**：单笔 2 USDC / 24h 累计 20 USDC / 最多 20 笔 / paymaster 0.005 ETH 24h cap

4\. **Lifecycle**：3 天有效 / issuer 可即时撤销 / 连续 3 笔失败暂停 30 min / escalation 列表 5 条 / 双轨审计日志

**红队自检底线**：拿到 holder 私钥的最坏 3 日总损失 ≤ 60 USDC + 0.015 ETH + ToolRegistry 合约风险。

**关键设计原则**（写完才显出来的）：

\- **default-deny**：白名单制，每加一行是从全宇宙圈出一小块允许区

\- **按可承受损失定额**：单笔 = 最坏一次愿意一次性损失多少；窗口 = 反应时间内的总上限

\- **必须列 escalation\_to\_user**：不写这条 session key 就退化成"小号私钥"

**Follow-up 转化**：策略里的 TODO 列表是后续真要上链的路径（部署 Smart Account → 选 Paymaster → 转 Rhinestone Smart Sessions policy → 跑一笔真实 UserOp）。\*\*昨天计划的"etherscan 读 USDC + AA 钱包对比"今天先没做\*\*——session key policy 写完优先级更高，对比实验推到 Frameworks 节点（5.22）或更后面再做。

\## 我的卡点

\- **ERC-7562 验证阶段存储隔离的具体规则**：Agent 提了名字没展开。需要自己读 EIP 原文确认"账户只能访问自己的 storage"具体到哪些 slot 算"自己的"。

\- **Bundler 经济学**：Bundler 失败模拟自己亏 gas，那现实里 Bundler 怎么定价才能不亏？没追问。如果 hackathon 真要做 Agent 自动化交易，这个会成实际成本问题。

\- **escalation 在 Rhinestone Smart Sessions 里怎么落**：我表里写的"非白名单 → 回到用户签名"概念清晰，但具体到 Smart Sessions module 里是 policy 拒绝后\*\*自动\*\*走主签名，还是要 Agent 代码层主动 fallback？影响 Agent 实现复杂度。

\## Follow-up

\- \[ \] 读 EIP-4337 原文 + ERC-7562 原文，确认 UserOp 字段和验证阶段限制

\- \[ \] **AI × Web3 联想**：把"session key 策略 = capability-based security 链上实现"这条线拓展进 hackathon 候选——\*\*Agent Wallet Policy Auditor\*\*，给定一份 session key policy yaml 自动做红队自检（穷举所有"组合允许动作"算最大可提取价值）。归到 `hackathon/ideation.md`。

\- \[ \] etherscan 读 USDC + AA 钱包对比实验（昨天就推迟过一次，再推可能就放弃了——5.22 Frameworks 节点之后必须决定做不做）

\- \[ \] Rhinestone Smart Sessions 文档 + ZeroDev SDK 文档——把今天的 yaml 策略映射成真实可部署配置

\- \[ \] **元观察追踪**：边讲边问 vs 闭卷读+复述，今天是第 2 天使用边讲边问。明天可以\*\*故意切换回闭卷读\*\*做一个对照——5.22 Frameworks 试试。

\## Handbook / 课程反馈

\- \[ \] **建议**：Account Abstraction 章节"知识节点"5 个之间的\*\*关系图\*\*缺失。读者读完不一定能立刻把 ERC-4337（协议）/ Bundler（基础设施）/ Paymaster（基础设施）/ Smart Account（账户）/ Session Key（权限模型）的\*\*层次\*\*串起来。建议加一张流程图或对比表。

\- \[ \] **建议**：最小实践写得很好（"重点不是马上部署完整 AA 钱包，而是学会把权限从'全部允许'拆成可验证规则"），但缺少\*\*红队自检\*\*这一步——只写 policy 不做攻击面分析，等于只画了允许区没画风险。建议在最小实践后加一句："写完后做一次红队自检：穷举攻击者拿到 session key 后能在策略范围内提取的最大价值。"

\- \[ \] 考虑整理上面两条进 `handbook-feedback/`，凑够 5 条统一提交（北极星之一）。

\## 打卡草稿（粘到 [intensivecolearn.ing](http://intensivecolearn.ing) Check-in 表单的 Markdown）

\`\`\`markdown

**账户抽象（AA）—— Session Key 作为 capability-based security 的链上实现**

今天读 Handbook 账户抽象章节，最锋利的认知：\*\*AA 的核心不是"免 gas"，是把账户控制权从单一私钥扩展成可编程规则。\*\* 免 gas 只是"支付逻辑可编程"的一个特例。盯住"免 gas"会把 AA 降级成营销工具，盯住"可编程"才看得到社交恢复 / 批量执行 / session key 都属于同一棵树。

第一性原理：账户可编程之后，权限模型从"有私钥/没私钥"变成"\*\*在什么条件下允许什么动作\*\*"。这正是 Agent Wallet 的关键——Agent 不该拿主私钥，也不该有无限权限。

走完 5 个知识节点：ERC-4337（不改协议、用 alt mempool + EntryPoint 把可编程账户硬塞进去的工程妥协）、Smart Account（账户即合约，\*\*继承所有合约风险\*\*）、Bundler（先模拟再上链——模拟与执行不一致是经典失败面，ERC-7562 限制验证阶段就是为了缓解这个）、Paymaster（\*\*spam 与套利是最难解的\*\*，静态规则打不过对抗博弈，攻击者会让 Paymaster 替自己付 gas 跑 DEX 套利）、Session Key（最高级也最关键的节点）。

最重要的认知是 **Session Key = capability-based security 的链上实现**：传统 ACL 基于身份（你是谁→能做什么），capability 基于能力（你拿什么形状的钥匙→只能开那把锁）。session key 的"钥匙形状"是 5 个维度的合取：合约 × 方法 × 额度 × 时间 × 链。每加一个维度就把 blast radius 砍一刀。\*\*这就是"损失可控"在合约层的具体形态。\*\*

今天的最小实验是写了一份完整的 session key 策略（experiments/session-keys/[2026-05-21-hermes-tool-payment.md](http://2026-05-21-hermes-tool-payment.md)），4 层切片（Identity / Scope / Limits / Lifecycle），算出"拿到 holder 私钥最坏 3 日损失 ≤ 60 USDC + 0.015 ETH"，并列出 5 条必须 escalation 回到用户签名的情况——\*\*escalation\_to\_user 是 session key 区别于"小号私钥"的关键字段\*\*。

跟昨天的"三时间轴 audit"接上了：昨天框架是审别人合约（事前=Upgrade / 事中=Solidity-EVM-ABI / 事后=Event），今天发现写自己 Agent 的 session key 策略也是\*\*完全同构\*\*的三时间轴——只是从 audit 视角切到 design 视角。Handbook 原文：\*\*账户抽象不是让 AI 更自由，而是让 AI 的自由被规则包起来。\*\*

明天主题 Frameworks（LangChain / LangGraph / Agents SDK 选型）。

\`\`\`

\- 提交入口：[https://intensivecolearn.ing/en](https://intensivecolearn.ing/en) → 登录 → AI × Web3 School → 左侧 "Check-in"

\- 提交后回填提交时间 / 截图：
<!-- DAILY_CHECKIN_2026-05-21_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->


\# 2026-05-20 学习日志

\## 今日主题

\*\*智能合约（Smart Contract）\*\* —— \[Handbook 章节\]([https://aiweb3.school/zh/handbook/web3/smart-contract/](https://aiweb3.school/zh/handbook/web3/smart-contract/))

cohort Week 1 / Web3 侧打基础。

\## Agent 整理的精炼摘要（读完 Handbook 后用自己的话再写一遍）

\*\*一句话\*\*：合约 = 部署在链上的程序。把规则、资产、状态放进公开可验证的执行环境 —— 同时把错误、权限和升级风险也暴露给所有人。

\*\*第一性原理\*\*：合约的价值来自\*\*可验证执行\*\*，不是"代码看起来聪明"。三条引申：

\- 状态公开可查（链上不是私有 DB）

\- 调用有成本和顺序（gas / 区块顺序 / 外部状态影响）

\- 权限必须显式（mint / pause / upgrade / withdraw 不能靠默认信任）

\*\*5 个知识节点\*\*：

| 节点 | 难度 | 一句话 |

|---|---|---|

| \*\*Solidity\*\* | 初级 | EVM 合约语言。关键：storage / msg.sender / modifier / event / external call / revert / 权限控制 |

| \*\*EVM\*\* | 中级 | 合约执行环境。解释 gas 贵、storage 贵、外部调用风险、多链兼容来源 |

| \*\*ABI\*\* | 初级 | "能调用什么"的机器可读接口。\*\*不是\*\*安全说明书。是 Agent 理解合约能力的关键上下文 |

| \*\*Event\*\* | 初级 | 合约对外的可索引日志。前端列表/历史/看板大多读 event 不直接读 storage |

| \*\*Upgrade\*\* | 高级 | "可升级 vs 不可升级"的权衡。判断升级风险 4 问：升级权限谁手里 / 用户能否提前看提案 / 升级能否改资产/权限逻辑 / 管理员密钥泄漏最坏结果 |

\*\*一次调用怎么发生\*\*（vote(proposalId) 为例）：

\`\`\`

前端读钱包+网络 → 前端用 ABI 编码 vote(proposalId) → 钱包确认签名

→ 广播到 RPC 节点 → 验证者打包进区块 → EVM 执行

↳ 成功：更新 storage + emit event

↳ 失败：revert

→ 前端监听回执 → 索引器读 event 更新看板

\`\`\`

\*\*5 个常见错误\*\*：

1\. view 函数和写交易混（读不需签名，写需要）

2\. 没处理 decimals（amount ≠ 用户看到的 "1.5"，是按 decimals 放大的整数）

3\. 只测成功路径（权限/余额/重复/过期/暂停都得测）

4\. owner 当永远可信

5\. 忽略事件设计

\*\*AI × Web3 中的位置\*\*：

\> AI 做建议和编排，钱包做授权确认，合约做可验证执行，监控系统记录结果。

即使 AI 输出不稳定，链上规则仍有明确边界。

\## 我用自己的话复述（边讲边问模式，对话中已完成）

\> 今天换了模式：没有先读再答，是 Agent 一节一节讲，每节我答一题。下面是对话中真实输出过的我的版本（不是 Agent 摘要）。

\- \*\*第一性原理\*\*：合约 vs Web 后端最锋利的差别是"\*\*事先能验证规则\*\*" —— 链上合约源码公开，部署前就能读"付款 = 转账 + emit Paid 事件"；Web 后端代码私有，你只能信"机构事后裁决"。所以"可验证执行"指\*\*任何人 + 任何时间 + 链上交易记录 + 链上规则源码\*\*四件一起公开。

\- \*\*Solidity / `msg.sender` 为什么最关键\*\*：所有权限判断如果不显式绑定它，合约就无从知道"谁在操作"—— 它是 Solidity 给你的\*\*唯一\*\*身份原语，没有 HTTP header / session / JWT 这种东西。

\- \*\*EVM / 无限循环\*\*：不是被拒绝执行，是\*\*先付 gas 后执行\*\*，超出 gas limit 自动 out-of-gas → revert，但 gas 不退。这是 EVM 的"经济熔断"，让 EVM 敢执行陌生合约。

\- \*\*ABI / 自动转账最容易踩的坑\*\*：decimals 单位 —— Agent 看 ABI 调 `transfer(to, 100)` 以为转 100 USDC，实际转 0.0001 USDC（USDC decimals=6）。ABI \*\*不告诉你\*\* decimals，必须先调 `decimals()` 读再放大。

\- \*\*Event vs Storage / 审计\*\*：链上审计核心需求是"可追溯、不可篡改的行为日志"。Event 写 transaction log，成本低 + 永久存档；Storage 可被后续交易覆盖 + Gas 贵很多。\*\*拿最贵的资源做最不该被修改的事 = 错配\*\*。

\- _Agent 补的 nuance_：合约自己读不到 event。所以场景判断 = 合约自己要读 → storage；链外读 → event；两者都要 → 双写。

\- \*\*Upgrade 4 问 audit / "我们通过多签控制升级" 这句话\*\*：

\- Q1 多签几/几 没说

\- Q2 用户能提前看 没说

\- Q3 能改资产逻辑吗 没说

\- Q4 密钥泄漏后果 没说

\- \*\*判断：4 问回答了 ≈ 0.25/4。这句话是信号词，不是承诺。\*\*

\*\*今日 best\*\*（综合题）：构造了一个用满 5 节点的攻击场景 —— 透明代理 + 无 timelock 升级，把 withdraw() 提款逻辑换成转给攻击者地址。\*\*关键洞察\*\*："日志里有 Event 留痕，但资金已经走了" → \*\*可验证 ≠ 安全\*\*。Event = 事后追溯，Solidity/EVM/ABI = 发生时，\*\*Upgrade = 发生前\*\*（最可怕，改的是规则本身）。三个时间轴都要审才完整。

\## 读 Handbook 时的 scratchpad

\> 今天没用上 —— 因为没读 Handbook 自己，而是走"Agent 边讲边问"模式。

\> 元观察：这模式让"嗯？"瞬间被实时纠正了（Agent 立刻在下一句话补），所以本来想记的点都消化在对话里了。

\> 后续观察：是不是边讲边问比闭卷读 + 复述更高效？需要再过几天看对比。

\## 今日最小实验

\*\*今天没做\*\* —— 选择把时间留在对话引导 + 打卡。

\*\*Follow-up 转化\*\*：原计划的 etherscan 读 USDC 推迟。考虑明天 Account Abstraction 后做"读 AA 钱包合约 + 对比 USDC"组合实验 —— 一举两得。

\## 我的卡点

\- 今天没卡（边讲边问模式实时纠错了），但 \*\*元观察待验证\*\*：边讲边问 vs 闭卷读+复述，哪种长期更高效？需要再过几天对比。

\- ✋ 还想自己确认的点：\*\*透明代理 vs UUPS 代理 vs Beacon 代理\*\*的区别 —— 今天 Upgrade 节点只讲了 transparent proxy，没区分模式。下次读到 OpenZeppelin Upgrades 文档时补。

\## Follow-up

\- \[ \] etherscan 读 USDC 合约（今天推迟到明天，和 AA 合约一起做对比实验）

\- \[ \] \*\*AI × Web3 联想\*\*：把今天的"三时间轴 audit 框架"（事前 Upgrade / 事中 Solidity-EVM-ABI / 事后 Event）写成一个 hackathon 候选项目雏形 —— \*\*Web3 合约审计 Agent\*\*，用 Handbook 4 问 + 三时间轴当 prompt 框架。归到 `hackathon/ideation.md`。

\- \[ \] OpenZeppelin Contracts / Upgrades 文档 —— Handbook 给的扩展阅读，作为 Solidity / Upgrade 节点的深化。

\## Handbook / 课程反馈

\- \[ \] 建议：Upgrade 节点里如果能加一段对比 transparent / UUPS / Beacon proxy 的快速表格，对学员更友好（现在 4 问框架很好，但读者可能不知道这 4 问应用到哪种 proxy 模式）。考虑整理成正式 feedback 进 `handbook-feedback/`。

\## 打卡草稿（粘到 [intensivecolearn.ing](http://intensivecolearn.ing) Check-in 表单的 Markdown）

\`\`\`markdown

\*\*智能合约（Smart Contract）—— 第一性原理与三时间轴 audit 框架\*\*

今天读 Handbook 智能合约章节，最锋利的认知：\*\*合约 vs Web 后端的本质差别不是"自动化"或"去中心化"，而是事先能验证规则\*\*。Web 后端代码私有，你只能事后让支付机构裁决；合约源码公开，部署前就能确认"付款=转账+emit Paid 事件"。"可验证执行" = 任何人 + 任何时间 + 链上交易记录 + 链上规则源码，四件一起公开。

走完 5 个节点：Solidity`msg.sender` 是合约\*\*唯一\*\*身份原语，没有 HTTP/session/JWT）、EVM（gas 不是技术限制，是\*\*经济熔断保险丝\*\*，让节点敢执行陌生合约）、ABI（机器可读接口，但\*\*不告诉你\*\*安全性 —— Agent 调 `transfer(to, 100)` 没读 decimals 就把 100 USDC 转成 0.0001 USDC）、Event（拿最贵的 storage 做最不该被修改的事 = 错配；审计应该用 event 写 transaction log）、Upgrade（产品分"可升级"和"不可升级"两类，不是同一种产品的两种实现）。

最重要的产出是\*\*三时间轴 audit 框架\*\*：把 5 节点按"调用时间轴"重排 → Solidity/EVM/ABI 管"发生时"、Event 管"发生后"、\*\*Upgrade 管"发生前"\*\*。Upgrade 是最可怕的一类风险，因为它改的是\*\*规则本身\*\*：今天有人用透明代理 + 无 timelock 升级，把 withdraw 逻辑换成转给攻击者地址 —— 日志里 Event 留痕，但\*\*资金已经走了\*\*。这是 Handbook 第一性原理隐含但没显式写的关键洞察：\*\*可验证 ≠ 安全\*\*。

实操收获：Handbook 给的 Upgrade 4 问（升级权限谁手里 / 用户能否提前看 / 能改资产逻辑吗 / 密钥泄漏最坏结果）今天用一个真实信号词"我们通过多签控制升级"反向 audit，结果 4 问回答了 ≈ 0.25/4 —— 这是产品方常用的安全话术，但只是信号词不是承诺。下次看到一律追问到底。

明天主题 Account Abstraction，正好把 etherscan 读合约的最小实验和 AA 钱包合约对比做。

\`\`\`

\- 提交入口：[https://intensivecolearn.ing/en](https://intensivecolearn.ing/en) → 登录 → AI × Web3 School → 左侧 "Check-in"

\- 提交后回填提交时间 / 截图：
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->



\# 2026-05-19 学习日志

\## 留给自己的作业

如果 Hermes Agent 帮你完成了一个"自动整理邮件"的任务，它在背后经历了哪几个步骤？它下次再做类似任务时，会有什么不同？  

\- 第一次：用 LLM 决定调用什么工具 → 调用邮件 API → 返回结果 → 判断"这个流程有用 → 生成 [SKILL.md](http://SKILL.md) 描述步骤、入参、典型陷阱"

\- 第二次：检索到 skill → 直接按 skill 步骤执行 → 完成后自问"这次有没有更好的写法" → 增量更新 skill

\- 关键差异：从"每次让 LLM 重新推理工具序列"变成"读已有 skill + 必要时小幅改写"，token 成本和延迟都下降。  

\## 今日主题

\*\***模型上下文协议（MCP）**\*\* —— \[Handbook 章节\]([https://aiweb3.school/zh/handbook/ai/mcp/](https://aiweb3.school/zh/handbook/ai/mcp/))

\## Agent 整理的精炼摘要（看完 Handbook 后用自己的话再写一遍）

\*\***一句话**\*\*：MCP 把"模型 ↔ 外部工具/数据/上下文"的连接标准化成协议，让工具接入变得可描述、可发现、可限制。

\*\***第一性原理**\*\*：模型不应该直接拥有世界，应该通过明确协议访问被授权的上下文和工具。

\*\***4 个知识节点**\*\*：

| 节点 | 它是谁 | 设计要点 |

|—|—|—|

| \*\***Server**\*\* | 提供能力的一侧（暴露 resources / tools / prompts） | 边界：只读 vs 副作用、schema 清晰、错误明确、需否授权、审计日志 |

| \*\***Client**\*\* | 连接模型和 server（IDE / Agent runtime / 聊天客户端） | 发现能力 → 传给模型 → 用户确认 → 权限提示 → 会话隔离 |

| \*\***Tool Schema**\*\* | 描述工具名 / 用途 / 参数 / 返回 / 约束 | 不只是字段类型：何时用、参数含义、必填、是否改外部状态、失败返回什么 |

| \*\***Permission**\*\* | 最容易被低估 | 区分：只读/写、会话/长期、需否确认、敏感访问、可撤销、可审计 |

\*\***AI × Web3 中的位置**\*\*：

\- ✅ MCP 可作为 Agent 接链上工具的接口层：读区块浏览器、查合约文档、调 RPC、生成交易草稿

\- ❌ MCP \*\***不是**\*\*钱包安全方案 —— 最终权限和执行边界归 Web3 账户系统

\- 稳的设计 = MCP（工具发现/调用格式）+ Web3 账户系统（最终权限/执行边界）

\## 我用自己的话复述（读完 Handbook 后填）

\- \*\***Server**\*\*：提供能力的一侧。暴露 resources / tools / prompts 给 Client，用 schema 描述。设计要点是边界 —— 哪些暴露、哪些只读、哪些有副作用、错误怎么返回、要不要授权。

\- _自我纠错_：第一次把"tools"错答成"协议"；漏了 schema 这个关键词。

\- \*\***Client**\*\*：夹在模型和 Server 中间的"外壳层"，本身不思考也不执行业务。例：Claude Code / Cursor / ChatGPT Desktop（Claude 这个模型本身\*\***不是**\*\* Client）。

\- 3 步搬运：①从 Server 拉工具清单 ②把清单递给模型 ③双向中转模型的调用请求和 Server 的返回。

\- 4 件用户那一面的事（容易漏）：用户确认、权限提示、会话隔离、工具调用展示 —— 因为模型看不见屏幕，必须 Client 代劳。

\- _自我纠错_：把模型和 Client 混了；以为 Client 指挥工具（其实工具属于 Server，调谁由模型决定）；完全漏掉用户那一面的 4 件事。

\- \*\***Tool Schema**\*\*：工具的"说明书" —— 描述名字、用途、参数、返回、约束。\*\***模型唯一看得见的工具就是 schema 本身**\*\*：它读不到 Server 代码、运行时风险、副作用、用法约定，全靠 schema 文本来决定调不调、怎么调。所以 schema 不是 Server 的实现细节，是 \*\***Model ↔ Tool 之间的接口契约**\*\*，是 prompt engineering 和 API design 的交集。schema 模糊 → 模型用错误参数填空。

\- _自我纠错_：知道 schema 重要，但"模型只能读 schema"这点没立刻想到 —— 是为什么 schema 这么关键的根。

\- \*\***Permission**\*\*：权限边界，控制 AI 能做什么、不能做什么。Handbook 把它列为"最容易被低估"的问题 —— 因为 MCP 让工具一接就跑，方便≠安全。读 doc 和发转账风险完全不同，必须拆 \*\***6 个维度**\*\*：①只读 vs 写入 ②会话授权 vs 长期授权 ③是否需用户确认 ④是否敏感访问 ⑤是否有外部副作用 ⑥是否可撤销 / 可审计。

\- _自我纠错_：6 个维度只想出 3 个（只读/确认/敏感），漏了"会话 vs 长期"“副作用”“可撤销可审计” —— 但这三条恰恰是今天 audit Notion server 时直接看到反面教材的（env token 长期、协议层无确认、默认无审计）。说明今天的 audit 没和 Permission 节点形成回路。

\- \*\***第一性原理（我的话）**\*\*：MCP 就像\*\***带白名单和权限标签的 USB**\*\*。

\- \*\***标准化半**\*\*：没有 USB 之前每个设备都要定制接口；有了 USB 之后任何合规设备插上就用。MCP 对 AI 生态做的就是 USB 对硬件生态做的事 —— 标准化 Client ↔ Server 接口，避免 N×M 适配。

\- \*\***授权半（普通 USB 不覆盖）**\*\*：MCP 默认\*\***禁止**\*\* —— 模型不能直接拥有世界，必须 schema 显式描述、permission 显式授权才看得到工具。普通 USB 是 plug-and-play，MCP 是 plug-and-审批。

\- _自我纠错_：USB 比喻刚开始只抓到"标准化"那半，漏了"授权 / 受限"那半 —— 这恰恰是 Handbook 原句两段并列的下半段。

\## 我的卡点

\- 读 Handbook + 做 audit 时\*\***实时没卡**\*\* —— 但闭卷复述时暴露 5 个错点（见复述节"自我纠错"行）。

\- 元观察：\*\***不卡 ≠ 懂**\*\*。读的时候顺，是因为我把"看着合理"当成"理解了"。明天起读 Handbook 旁边开个 scratchpad，凡是"嗯？……哦"的地方都先记一笔，别让它无痕过去。

\## 今日最小实验：拆 Notion 官方 MCP server 的 `query-data-source` schema

\> 不写代码，纯 audit。产物：\[experiments/mcp-notion-audit/[README.md](http://README.md)\](…/experiments/mcp-notion-audit/[README.md](http://README.md))

\*\***意外发现** #1\*\***：Notion 不是手写每个 tool，而是把 REST API 的 OpenAPI v3 spec（66KB）丢给** `MCPProxy` **自动转 MCP Tool。22 个工具几乎零成本派生。**

\*\***意外发现** #2\*\***：proxy.ts 有专门的** `deserializeParams` **函数，注释指向 \[issue** #176\]([https://github.com/makenotion/notion-mcp-server/issues/176](https://github.com/makenotion/notion-mcp-server/issues/176)) —— Claude Code / Cursor 会把递归 schema 双重序列化。这是真实工程坑。

\*\***Handbook 四维度对照**\*\*：

| 维度 | Notion `query-data-source` 实际 |

|—|—|

| name | ✅ 干净的 `query-data-source` |

| description | ⚠️ 偏弱 —— 没说"何时用 vs `retrieve-a-data-source`"、没说有无副作用 |

| inputSchema | ✅ 大部分清晰；⚠️ filter 是递归 schema，body 整体无 required（空 body 即全量读取） |

| 副作用 / 权限 | ❌ OpenAPI `security:[]` 假装无 auth，实际靠 HttpClient 注入 env token —— 长期、不可会话隔离、无审计、协议层无确认 |

\*\***最大启发**\*\*：MCP 不能假装权限是协议层的事。Notion README 自己警告"暴露给 LLM 有非零风险"。\*\***只读和写入应分 server，或加 capability flag。**\*\*

\## Follow-up

\- \[ \] \*\***AI × Web3 联想**\*\*：Notion MCP 把 OpenAPI auto-derive 成工具的模式 —— Web3 RPC / 合约 ABI 是不是也能自动派生成 MCP tool？这对应 Handbook Bridge 的 \[Web3 Tool Use\]([https://aiweb3.school/zh/handbook/bridge/web3-tool-use/](https://aiweb3.school/zh/handbook/bridge/web3-tool-use/)) 章节，是 Hackathon Dev Tooling 赛道的候选方向。

\- \[ \] 把"只读 vs 写入分 server"做成真实最小例子（对应 Handbook MCP 章节最小实践 A 方案），下次实验。

\- \[ \] 看一下 Notion \*\***Remote MCP**\*\*（OAuth）vs \*\***Local**\*\*（env token）两种授权模型的对比 —— OAuth 路线是不是 Handbook \*\***Permission**\*\* 章节里"会话授权"的标准答案？

\## Handbook / 课程反馈

\- \[ \]

\## 打卡草稿（粘到 [intensivecolearn.ing](http://intensivecolearn.ing) Check-in 表单的 Markdown）

\`\`\`markdown

\*\***MCP（模型上下文协议）—— 拆 Notion 官方 MCP server**\*\*

今天读 Handbook 的 MCP 章节，第一性原理一句话总结：模型不应该直接拥有世界，应该通过明确协议访问被授权的上下文和工具。MCP 把这层标准化成 Server / Client / Tool Schema / Permission 四个节点。

为了不停留在概念，找了 \[makenotion/notion-mcp-server\]([https://github.com/makenotion/notion-mcp-server](https://github.com/makenotion/notion-mcp-server)) 拆 `query-data-source` 这个 tool。两个意外：

1\. \*\***OpenAPI → MCP 自动派生**\*\*：Notion 不手写每个 tool，把 REST API 的 OpenAPI v3 spec 丢给 `MCPProxy` 类自动转成 22 个 MCP Tool。Web3 那边的 RPC / 合约 ABI 同理可派生 —— 这是 Dev Tooling 方向的一个明显切入点。

2\. \*\***协议** `security:[]` **假装无 auth，实际靠 HttpClient 注入 env token**\*\*。是长期授权、不可会话隔离、协议层无确认、默认无审计 —— Handbook Permission 节里说"权限要在协议外也成立"，这里就是反面教材。

把四维度（name / description / inputSchema / 副作用）扣到 `query-data-source` 上发现：description 没说"何时用 vs `retrieve-a-data-source`"，body schema 也没声明 required —— 空 body 即全量读取。Notion README 自己警告"暴露给 LLM 有非零风险"。

\*\***给自己的 checklist**\*\*：以后写 MCP server 必须把"副作用 / 是否需要用户确认"放进 description，只读和写入要分 server 或加 capability flag，每次调用要写审计日志。

完整 audit：[https://github.com/HeliosLz/ai-web3-school-cohort-0/blob/master/experiments/mcp-notion-audit/README.md](https://github.com/HeliosLz/ai-web3-school-cohort-0/blob/master/experiments/mcp-notion-audit/README.md)

\*\***今日复盘**\*\*：闭卷复述 Server / Client / Tool Schema / Permission / 第一性原理 5 个概念，暴露 5 个错点 —— 其中 Permission 那 6 维度漏的 3 个（会话 vs 长期、副作用、可撤销/可审计）恰好是今天 audit Notion server 时亲眼看见反面教材的。读 Handbook 时实时没卡，但闭卷暴露了 gap。元教训：“不卡 ≠ 懂”；明天起读 Handbook 旁边开 scratchpad，记任何"嗯？……哦"的瞬间。

\`\`\`

\- 提交位置：[https://intensivecolearn.ing/en](https://intensivecolearn.ing/en) → 登录 → AI × Web3 School 详情页 → 左侧 “Check-in” 按钮

\- 提交后回填提交时间 / 截图：
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->




**Hermes 从 0 到 1 教程**  
  
它最大的特点是**内置学习循环**：**每次完成任务后，它会自动从经验中提炼出可复用的 Skill，存入持久记忆，下次遇到类似任务时会自动改进和调用。**

这个记忆是持久的，能逐步构建对你的“用户模型”。它是一个能自主成长的代理，常用于长期项目辅助、自动化任务、研究等。  
  
最简单的解释  
  
想象你有一个**超级聪明的助手**。普通助手是这样的：你说"帮我订披萨"，他订了，然后就忘了这件事。下次你还得重新说一遍。

**Hermes Agent 更像一个会成长的学徒：**

> 你第一次教他怎么订披萨，他不仅做了——他还**把这个技能写进了笔记本**。下次你不用教了，他自己就知道怎么做。而且每次做，他都在想"我上次怎么做的？有没有更好的方法？"

三个关键点：

-   🧠 **记忆** — 他记得你们之前聊过什么
    
-   📚 **技能本** — 他把学到的方法存起来，以后复用
    

🔄 **自我改进** — 他越用越聪明，不是每次从零开始

```
普通Agent vs Hermes Agent：

普通Agent：
大模型 → 决定用哪个工具 → 调用工具 → 返回结果
（每次都一样，没有成长）

Hermes Agent：
大模型 → 决定用哪个工具 → 调用工具 → 返回结果
              ↓
        "这个流程有用！写进技能本"
              ↓
        下次直接调用技能，更快更准
              ↓
        还会问自己：这个技能能改进吗？
```

### 它怎么"记住"东西？

Hermes有**三层记忆**，就像人类一样：  

| 层级 | 类比 | 技术实现 |
| --- | --- | --- |
| 短期记忆 | 当前对话内容 | Context Window |
| 长期记忆 | 你的日记本 | 跨Session持久化存储 |
| 用户模型 | 对你这个人的理解 | Honcho dialectic modeling |

关键工程思维：**记忆不是简单存储，而是带索引的检索**——用FTS5全文搜索+LLM摘要，让Agent能从大量历史中快速找到相关片段。

类比：不是把所有日记都读一遍，而是有个聪明的图书管理员帮你找关键页。

### 技能（Skills）到底是什么？

这是Hermes最有意思的设计！

> 技能 = **Agent自己写给自己看的操作手册**

具体来说，一个技能就是一个`SKILL.md`文件，里面写着：

-   这件事是什么
    
-   怎么一步步做
    
-   踩过哪些坑
    
-   什么时候该用它
    

```
工程思维关键点：

第一次做某件事 → 摸索完成
      ↓
Agent判断："这个值得记录吗？"
      ↓
自动生成SKILL.md
      ↓
第二次遇到类似任务 → 直接读技能文件
      ↓
做完后："这次有没有更好的做法？" → 更新技能文件
```

  
Hermes的设计哲学可以用一句话概括：

> **"不要每次从零开始，要把经验变成资产。"**

留给自己的作业：  
  
如果Hermes Agent帮你完成了一个"自动整理邮件"的任务，它在背后经历了哪几个步骤？它下次再做类似任务时，会有什么不同？

官方资源：

-   主站与文档：
    
    [https://hermes-agent.nousresearch.com/docs/](https://hermes-agent.nousresearch.com/docs/)
    
-   Quickstart：
    
    [https://hermes-agent.nousresearch.com/docs/getting-started/quickstart/](https://hermes-agent.nousresearch.com/docs/getting-started/quickstart/)
    
-   GitHub：
    
    [https://github.com/NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
