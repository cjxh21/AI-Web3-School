---
timezone: UTC+8
---

# Alley

**GitHub ID:** egak09

**Telegram:** @parad0614

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-22
<!-- DAILY_CHECKIN_2026-05-22_START -->
将目前为止关于agent的所有工作汇合成了笔记，并上传到了GitHub，  
链接：[https://github.com/egak09/hermes-skills/tree/master/AI-Web3-School](https://github.com/egak09/hermes-skills/tree/master/AI-Web3-School)

## **🗺️ 课程路线图**

```
01 AI Agents     ─→  02 Crypto Trading  ─→  03 Web3 Data
       │                      │                      │
       └──────────────────────┼──────────────────────┘
                              │
              04 DevOps & Infra  ←→  05 Systems Thinking
                              │
                        06 Esoteric × Trading
```

## **📚 六大模块**

| # | 模块 | 核心内容 | 关键词 |
| --- | --- | --- | --- |
| 01 | AI Agents | Hermes Agent 框架深度解析 | Skills, Cron, Delegation, Prompts |
| 02 | Crypto Trading | 妖币合约策略 v2.2 + 风控 | K线形态, 凯利公式, OI/Vol, 回测 |
| 03 | Web3 Data | BlockBeats API · 链上数据 · 内容自动化 | 情绪指标, 宏观, 热点狙击 |
| 04 | DevOps & Infra | Windows 下 AI Agent 运维实战 | Junction, Proxy, Python环境分裂 |
| 05 | Systems Thinking | 工程控制论 × AI Agent 设计模式 | 闭环验证, 冗余, 意图重建 |
| 06 | Esoteric × Trading | 八字+紫微+星盘三合一交易辅助 | 己土日主, 周期能量 |

## **🛠️ 技术栈**

-   **Agent**: Hermes Agent (Nous Research) · DeepSeek V4
    
-   **Trading**: Binance Futures · CCXT · Kelly Formula
    
-   **Data**: BlockBeats API · On-chain Netflow
    
-   **Infra**: Windows 10 · Git · Telegram Gateway
    
-   **Systems**: 钱学森工程控制论 · 闭环反馈 · 冗余验证
    

## **📖 使用方式**

每篇笔记都是 **自我完足的独立文章**，可以按任意顺序阅读。推荐按模块编号顺序，因为它们之间有递进关系。

* * *

_最后更新: 2026-05-22_  
_作者: Paradigme × Hermes_
<!-- DAILY_CHECKIN_2026-05-22_END -->

# 2026-05-21
<!-- DAILY_CHECKIN_2026-05-21_START -->

**✅ 已完成事项**  
• 事项: **BlockBeats API 验证**  
• 详情: 确认 API Key 有效，18 个数据端点全部就绪，成功拉取 AI 赛道快讯 15 条并完成结构化输出

• 事项: **内容策略设计**  
• 详情: 基于你的 Twitter 人设（反理中客/情绪叙事派），确定「BlockBeats 采集 → 然然过滤推送 → 你手动润色发推」的三段式内容流水线；自动发推环节砍掉，保留你的人味

• 事项: **数据采集脚本开发**  
• 详情: 编写 `daily_briefing.py`（7 端点 + 情绪/AI/ETF/链上/稳定币）和 `hotspot_sniper.py`（3 链 Top10 净流入），部署至 `~/.hermes/scripts/`，C 盘占用 < 4KB

• 事项: **每日加密简报上线**  
• 详情: Cron job `855b1caf6635`，每天 12:00 推送：市场情绪 + 重要快讯 + ETF + 链上 + AI + Solana 热点 + 交易灵感，明日首跑

• 事项: **链上热点狙击上线**  
• 详情: Cron job `910146663cb8`，每 4 小时推送：Solana/Base/Ethereum 三链净流入 Top3，今日 16:00 首跑

**📊 当前定时任务总览**

**10:00 每日**  
• 时间: 10:00 每日  
• 任务: 🔮 玄学日报  
• 状态: ✅ 运行中

**12:00 每日**  
• 时间: 12:00 每日  
• 任务: 📊 加密市场简报  
• 状态: 🆕 明日首跑

**每 4 小时**  
• 时间: 每 4 小时  
• 任务: 🔍 链上热点狙击  
• 状态: 🆕 今日 16:00 首跑

**🎯 核心产出**

> **BlockBeats 全面接入，形成「数据采集 → 智能过滤 → 定时推送 → 手动润色发推」的内容生产流水线，三条 cron 共同构成 推特 的每日信息基础设施**
<!-- DAILY_CHECKIN_2026-05-21_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->


今天从零到一：把 Telegram 接上了（踩了 SOCKS5→HTTP 代理的坑），装好了 gh CLI 并完成 GitHub 认证，给 Hermes 做了 C 盘大瘦身（sessions/caches/skills 全迁 D 盘），存储器从内置升级到 scope-recall（SQLite + LanceDB 双层架构），构建了三套完整的交易基础设施——币安交易模块（含凯利仓位）、妖币合约策略 v2.2（68 分 + 1K 线确认）并完成 8 妖币回测验证、实盘扫描 16 币（市场安静无信号属正常），还把玄学三合一每日推送设成了 cron。

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/egak09/images/2026-05-20-1779291544684-image.png)
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->



今天主要讲进行了hermes的部署，现在还在学习怎么使用和自己编译skills
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->




**自我评估：**  
**对于ai的理解：**  
对LLM、Prompt、Workflow、Agent、Tool Use、AI Coding 概念都有理解，但实践不足  
**关于Web3基础：**  
深度使用钱包，对于签名、交易、Gas、合约、测试网和区块浏览器如何构成一条链上操作链有较为深刻的了解，有实际使用或查询经验  
**本周最优策略是：**  
快速复习概念 → 大量补 AI 实践 → 重点完成高质量的 AI×Web3 最小交叉实验。

**当前短板：**

-   AI 实践经验不足，尤其是 Agent + Tool Use + Workflow 的真实落地。
    
-   缺乏把 AI 输出直接转化为链上操作的完整闭环经验。
    

**Week 1 个人目标调整：**

-   AI 部分：至少完成 2-3 个高质量实践（而非 1 个）
    
-   Web3 部分：快速验证，不需要从零学
    
-   交叉实验：做 1-2 个有一定复杂度的实验，体现「AI 决策 + 人工确认 + 链上执行」
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
