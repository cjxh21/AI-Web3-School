---
timezone: UTC+8
---

# add-cmd

**GitHub ID:** add-cmd

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->
Day 3 — 上下文（Context）打卡笔记

📖 学了什么

Context 核心概念：

| 概念 | 一句话理解 |

|---------------------|------------------------------------------------------------|

| Context Window | 模型一次请求能处理的最大上下文范围 — 窗口大不等于用得好 |

| Context Engineering | 设计什么数据进上下文、排序、裁剪、标注来源、隔离不可信内容 |

| Memory | 跨请求保留的信息（用户偏好、历史任务）— 不能替代实时授权 |

| Knowledge Base | 可检索的外部知识库（文档、SDK、FAQ）— 按需取用 |

第一性原理：

\> Context 不是简单的长文本拼接，而是一套信息治理问题。你要为每类信息标注来源、时效、权限和可信度。否则模型会把"用户说的""网页写的""链上查到的""系统规定的"混在同一层处理。

🔧 做了个什么项目

钱包授权检查 Agent — Foundry + Go + React + DeepSeek

常规的 approve 检查只关注 Prompt 怎么写（Instruction / Few-shot）。这次换了一个角度：放什么进上下文、从哪里来、可信度如何。

核心设计：每个上下文块带 3 个标签

| 标签 | 取值 |

|----------|---------------------------------|

| \[SOURCE\] | rpc / cache / simulation / user |

| \[TRUST\] | high / medium / low |

| \[FRESH\] | realtime / cached / user-input |

6 个上下文块按可信度排序发给 LLM：

1\. 🟢 Chain Context (RPC, high) — chain id + 区块号

2\. 🟢 Token Info (RPC, high) — name/symbol

3\. 🟢 User State (RPC, high) — balance + allowance

4\. 🟢 Simulation (simulation, high) — eth\_call 模拟 approve

5\. 🟡 Spender Cache (cache, medium) — 本地可信列表

6\. 🔴 User Input (user, low) — 交易参数 + 意图，标记不可信

✅ 测试结果

| 场景 | 结果 |

|-------------------------------|----------------------------------------|

| 正常 approve 到可信合约 | 🟡 Medium — LLM 注意到意图与代币不匹配 |

| 钓鱼：无限 approve + 黑洞地址 | 🚨 Critical — 拒绝签名 |

关键观察：LLM 主动引用了来源标注，如"缓存数据有1小时延迟，需注意合约状态可能已变化"。 这说明来源标注真的改变了模型的行为。

💡 最小实践收获

1\. 来源标注是 Context Engineering 的第一步。 每个数据块都应该知道自己是哪里来的。

2\. 高可信数据和低可信数据要分开。 放同一段 LLM 会默认同等对待。

3\. Simulation 是最被低估的安全工具。 eth\_call 模拟 + LLM 解读 = 强大的事前检查。

4\. Cache 数据一定要标注时效。 "spender 在可信列表" 和 "spender 1小时前在可信列表" 是两回事。

📦 技术栈

Foundry (Solidity) + Go (Backend) + React (Frontend) + DeepSeek (LLM) + Sepolia

GitHub: github.com/add-cmd/ai-web3-school-cohort-0/tree/master/2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->

Day 2 完成总览

📘 Prompt 章节核心要点：

\- Prompt 是软约束，安全靠代码不是靠提示词

\- Instruction 实用 四段式：任务目标 / 可用输入 / 禁止行为 / 输出格式

\- Few-shot 要跟 eval 一起维护，协议升级后会误导

\- Structured Output 让后续代码可检查可回归

\- Prompt Injection 不能只靠一句话挡——要外部隔离 + 参数校验 + human approval

🔐 Cryptography 章节核心要点：

\- Hash ≠ 加密，是固定长度指纹，用来验证完整性

\- 私钥 = 控制权，泄漏不可逆（不截图、不传云盘、不给 AI）

\- 签名 = 对具体内容的授权证明，不是"弹窗确认"

\- Merkle Tree：少量 proof 验证大量数据（空投、轻客户端）

\- 链上身份 = 数学证明，不是平台发给你

明日计划（Day 3）：

\- \[ \] Context 章节 — 上下文窗口管理

\- \[ \] 开发栈（Dev Stack）章节 — Web3 开发工具链
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->



1\. AI × Web3 School 环境搭建

\- 创建了 GitHub repo: add-cmd/ai-web3-school-cohort-0

\- 克隆到本地 ~/ai-web3-school-cohort-0

\- 初始化了完整项目结构（README、profile、learning-plan、模板等）

\- 所有文件已 commit 并 push

2\. Day 1 学习计划

\- 双轨制：AI 基础（LLM 章节）+ Web3 基础（Network / Wallet / Smart Contract 章节）

\- 创建了 daily/[2026-05-18.md](http://2026-05-18.md)

3\. 关键认知更新

\- LLM 是概率推理层，不是事实数据库

\- 核心原则：区分模型生成与链上可验证事实
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
