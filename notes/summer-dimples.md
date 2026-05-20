---
timezone: UTC+0
---

# summer-dimples

**GitHub ID:** summer-dimples

**Telegram:** @Purple_cat10421

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->
今日最大收获：AI × Web3 概念对照

| AI 概念 | Web3 对应 | 关键差异 |

| API Key | 私钥 | 私钥泄露不可重置，资产永久丢失 |

| RAG 向量检索 | The Graph | 都是给系统注入外部信息的索引机制 |

| MCP 协议 | RPC 协议 | 都是"系统↔工具"的标准通信接口 |

| Guardrails | 访问控制 | 都是限制系统行为的边界机制 |

| AI 幻觉 | 合约 Bug | 都必须验证，不能盲目信任 |

\---

\## 实操任务

\- 测试钱包创建（MetaMask + Sepolia）

\- Sepolia 测试交易

\- SimpleStorage 合约部署（Remix）
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->

阅读 Handbook AI 板块 8 个章节，系统建立 AI 基础认知框架。

**核心收获：**

1.  **LLM**：自回归生成，概率预测，擅长语言/代码，不擅长精确事实和跨会话记忆
    
2.  **Prompt**：System Prompt 设身份，用户消息传意图，Few-shot + CoT 是核心技巧
    
3.  **Context**：上下文 = 模型的工作内存；关键信息放开头/结尾，避免"Lost in the Middle"
    
4.  **RAG**：检索增强解决知识截止和幻觉问题；向量数据库 + Embedding 是核心组件
    
5.  **Agent**：ReAct Loop 是基础；AI × Web3 中签名/转账/合约写入必须保留人工确认节点
    
6.  **Frameworks**：Hermes（已配置）适合长期运行，LangGraph 适合有状态复杂 workflow
    
7.  **Vibe Coding**：工作重心从写代码转向描述意图+审查；安全审查和架构决策不可外包给 AI
    
8.  **MCP**：Anthropic 开放标准；只读操作可自动，写入操作必须人工确认
    

**产出：** 8 份结构化学习笔记存入 GitHub repo
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->


今天从零完成 Hermes Agent 完整部署，Hermes Agent → GLM/[Z.ai](http://Z.ai) API → Telegram + 微信。

**完成内容：**

-   安装配置 Hermes Agent v0.14.0，接入 GLM-5.1
    
-   配置 Telegram Bot + 微信 ClawBot
    
-   创建 GitHub 学习仓库，提交首次打卡
    
-   让 Hermes 执行一次完整的"写文件+推送GitHub"任务
    

**今日资源发现：**

-   AI 学习文档：[https://wooded-yellowhorn-1cd.notion.site/AI-docs-10b1a400ef9483e7822981942213be94](https://wooded-yellowhorn-1cd.notion.site/AI-docs-10b1a400ef9483e7822981942213be94)
    
-   Web3 系统课程：[https://updraft.cyfrin.io/career-tracks](https://updraft.cyfrin.io/career-tracks)
    

**学习方法思考：** 对于 LLM、Agent、钱包、签名这些新概念，单纯正向学习容易停留在表面。计划采用**反推式学习**——从实际运行结果倒推原理，先跑通再理解为什么，用具体报错和现象重建概念框架，而不是死记名词定义。

**今日最大收获：** 第一次感受到 Agent 真正"做事"——一条指令完成多步操作，理解了 Prompt/Workflow/Agent 三者的边界差异。
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
