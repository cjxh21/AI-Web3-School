---
timezone: UTC+8
---

# weizijie693-hub

**GitHub ID:** weizijie693-hub

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->
Private Key 私钥:

一句话解释:私钥是控制钱包资产和链上身份的核心凭证，谁掌握私钥，谁就能控制这个钱包
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->

今天完成了 AI x Web3 School Learning Agent 工作流的配置记录，同时从零到一构建了一个概念学习工具，并做了迭代。

1\. 提交设置记录

在仓库 submissions/[setting-log-learning-agent.md](http://setting-log-learning-agent.md) 提交了第一份作业：记录了工具选择（Claude Code）、RAG/Agent/Web3

学习任务、关键提示配置、成功输出，以及 3 条人工审核案例（仓库创建、学习计划调整、词汇表审校）。

2\. 构建交互式概念学习工具

想法：Handbook 内容多但散，初学者不知道从哪看。做了 CLI + Web 双版本的概念学习工具，把每个核心概念写成"一句话解释 +

具体例子 + 常见误解"三段式。

v1（原版）：

\- 11 个概念：LLM、Prompt、Agent、RAG、Blockchain、PoS、DeFi、L2、Rollup、Smart Contract、HITL

\- CLI 命令有 list / explain / random / quiz

\- 网页版纯静态 HTML，双击就能打开

v2（迭代版）：在 v1 基础上，把概念库扩大到 35 个（AI 15 + Web3 15 + AIxWeb3 桥接

5），加了深色模式切换、分类筛选、localStorage 学习进度追踪和测验历史记录。

3\. 人机协作记录

AI 做的事：生成概念内容初稿、CLI 框架、网页版 HTML/CSS/JS、README 初稿

我做的事：逐条审校概念准确性、debug Windows 终端编码兼容性（emoji 变乱码 crash）、修复 Quiz 空输入边界问题、设计 UI

布局和分类标签、更新文档

4\. 学到的东西

\- HITL 不是每个操作都要人批准，而是关键节点需要人工把关，比如概念准确性必须审校，但 UI 框架可以直接用

\- GitHub Pages 部署后第一次访问需要等 1-2 分钟

\- JSON 里写中文直接存 UTF-8 没问题，但 Windows cmd 显示会乱码——浏览器和 VS Code 终端正常

\- 对比 v1 到 v2 的改动，增量迭代比一次性做大改更容易落地
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->


今天私下去了解了一下web3 network基础

有了一些理解：区块链网络的核心不是"存数据"，而是让互不信任的参与者对状态变化达成一致。传统应用是直接写数据库，链上应用则是在一个公开、按区块推进、由网络共识维护的状态机上提交请求。

同时配置了一些学习环境和工具库：zoom，cursor，claude code，metamask等

期待今晚的学习
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
