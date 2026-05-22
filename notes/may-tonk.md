---
timezone: UTC+8
---

# Justin Li

**GitHub ID:** may-tonk

**Telegram:** @maytonk

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-22
<!-- DAILY_CHECKIN_2026-05-22_START -->
### 1\. 基本概念概述

-   **EOA（Externally Owned Account，外部拥有账户）** 传统钱包账户，由私钥直接控制。最常见的 MetaMask 默认账户。
    
-   **智能账户（Smart Account / ERC-4337 Account Abstraction）** 基于智能合约实现的账户（也称 AA 账户）。用户不直接用私钥签名，而是通过 EntryPoint 合约和 UserOperation 发起交易。代表项目：ERC-4337、Pimlico、Alchemy Account、ZeroDev 等。  
    **智能账户（智能账户/ERC-4337 账户抽象）** 基于智能合约实现的账户（也称 AA 账户）。用户不直接用私钥签名，而是通过 EntryPoint 合约和 UserOperation 发起交易。代表项目：ERC-4337、Pimlico、Alchemy Account、ZeroDev 等。
    
-   **多签账户（Multi-Signature Wallet）** 需要多个私钥共同批准才能执行交易的智能合约钱包。代表项目：Gnosis Safe（现 Safe）、Gnosis MultiSig 等。
    

* * *

### 2\. 详细维度对比

| 维度 | EOA（传统钱包） | 智能账户（Smart Account） | 多签账户（Multi-Sig）  多签名 |
| --- | --- | --- | --- |
| 1. 谁持有控制权 | 单一私钥持有者 谁掌握私钥，谁就完全控制账户 | 合约 + 签名者 合约拥有逻辑控制权，私钥仅用于签名 UserOp。支持多因素或社交恢复 | 多人/组织共同控制 合约拥有最终控制权，需要设定阈值（Threshold） |
| 2. 谁可以发起交易 | 只有私钥持有者本人 必须用私钥签名 | 任何被授权的签名者或 Bundler 支持 Gasless、批量、自动化发起 | 任意签名者可提出交易，但需达到多人确认 一人无法单独执行 |
| 3. 是否支持多人确认 | 不支持 单签 | 支持（高度灵活） 可设置多签名者、不同权重、临时授权 | 原生强支持 典型 2/3、3/5、M-of-N 模式 |
| 4. 是否支持恢复、限额或自动化策略 | 极弱 丢私钥 = 资产永久丢失 几乎无限额、自动化功能 | 最强 • 社交恢复（朋友/邮箱/Guardian） • 每日限额 • 自动化支付、条件触发 • 模块化插件 | 较强 • 可设置多签恢复机制 • 限额模块 • 但自动化较弱（需额外模块） |
| 5. 典型使用场景 | • 个人日常小额交易 • DeFi 个人操作 • 新手入门 | • 个人高级钱包（Gasless、批量交易） • 团队/DAO 日常支出 • 企业级支付自动化 • 移动端友好钱包 | • DAO 国库管理 • 团队/公司资产共管 • 大额资金托管 • 机构/高净值用户 |
| 6. 主要风险点 | • 私钥泄露 = 资产全部丢失 • 单点故障 • 钓鱼签名风险高 • 无法挽回 | • 合约漏洞风险（虽经审计） • 依赖 Bundler / EntryPoint • 复杂度高，新手易误操作 • 部分实现仍有中心化风险 | • 审批流程慢 • 签名者勾结风险（内部作恶） • 合约漏洞 • 密钥管理复杂 |

* * *

### 3\. 权限与风险深度解读

**控制权本质差异**

-   **EOA**：控制权 = 私钥。极简但脆弱，一人掌控一切。
    
-   **智能账户**：控制权从“私钥”转移到“智能合约逻辑”。私钥只是“钥匙”之一，可随时更换或增加防护。
    
-   **多签**：控制权被明确分散到多人。任何单人无法独占资产。
    

**交易发起与批准流程**

-   EOA：签名即执行。
    
-   智能账户：签名 → UserOperation → Bundler 打包 → EntryPoint 执行（可实现“一人签名 + 自动执行”或“多人签名”）。
    
-   多签：提出交易 → 多人签名确认 → 达到阈值后执行。
    

**恢复能力**

-   EOA：几乎无恢复能力（除非提前在中心化交易所托管）。
    
-   智能账户：支持 Guardian（守护者）机制，可通过社交恢复、时间锁、邮箱验证等方式找回。
    
-   多签：可通过更换签名者或设置备用多签实现恢复。
    

**自动化与策略支持**

智能账户在这方面优势最大，可集成：

-   消费限额（spending limits）
    
-   自动支付订阅
    
-   条件交易（if-then 逻辑）
    
-   插件系统（Session Keys）  插件系统（会话密钥）
    

* * *

### 4\. 实际选择建议

-   **个人用户**：推荐从 **EOA 起步**，资金量增大后升级到 **智能账户**（兼顾便利性和安全性）。
    
-   **团队 / DAO / 公司**：强烈推荐 **多签账户**（Safe）作为主要资金管理工具，可结合智能账户作为执行层。
    
-   **高安全性需求**：**多签 + 智能账户混合使用**（多签作为最终国库，智能账户作为日常操作账户）。
    
-   **高便利性需求**：优先 **智能账户**（Gasless、批量、移动端友好）。
    

* * *

### 5\. 总结表格（一目了然）

| 账户类型  类类型 | 安全性  安全 | 便利性  方便 | 适合多人  多人 | 恢复能力 | 推荐指数（个人） | 推荐指数（团队） |
| --- | --- | --- | --- | --- | --- | --- |
| EOA | 低 | 高 | 不适合  不匹配 | 极差  不同之处 | ★★★☆☆ | ★☆☆☆☆ |
| 智能账户 | 中高  初中和高中 | 最高 | 支持 | 优秀 | ★★★★★ | ★★★★☆ |
| 多签账户 | 最高 | 中低 | 极适合 | 良好 | ★★★☆☆ | ★★★★★ |
<!-- DAILY_CHECKIN_2026-05-22_END -->

# 2026-05-21
<!-- DAILY_CHECKIN_2026-05-21_START -->

# **2026-05-21 项目进度总结**

## **1\. 今日目标**

今天的工作目标不是直接完成整个 ChainMind 项目，而是先完成以下两件事：

1.  确认当前 Python 工程能够在 PyCharm 中正常运行和测试。
    
2.  用一个真实 BSC 代币完成 Phase 1 Dune 手动分析流程的首轮检验。
    

本次检验采用的目标代币为：

| 字段 | 内容 |
| --- | --- |
| 链 | BSC / BNB Chain |
| 代币名称 | 14 |
| 代币地址 | 0x205f39c39f5fe15d4ef000aeb835de8deb264444 |
| 检验日期 | 2026-05-21 |

## **2\. 今日先完成的工程准备**

### **2.1 项目结构确认**

今天先确认了当前项目已经具备基础工程骨架：

-   `src/chainmind/`：正式 Python 包代码。
    
-   `scripts/`：本地脚本入口。
    
-   `tests/`：自动测试目录。
    
-   `samples/`：样例 token 数据。
    
-   `docs/`：项目设计、路线图和分析手册。
    
-   `experiments/`：实验与阶段检验记录。
    

这说明当前项目已经可以从“只有想法和文档”进入“可运行、可检验”的状态。

### **2.2 PyCharm 运行配置学习**

今天重点理解了 PyCharm `Run/Debug Configuration` 的作用。

当前运行配置中关键字段的含义如下：

| 配置项 | 含义 |
| --- | --- |
| Python Interpreter | 选择用哪个 Python 环境运行项目 |
| Script path | 选择要运行的 Python 脚本 |
| Parameters | 给本次运行传入输入文件和运行选项 |
| Working directory | 指定程序从哪个目录出发查找相对路径 |

本项目当前分析脚本需要传入 snapshot JSON 文件，因此不能只运行脚本本身，还需要给出输入参数。

示例参数：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`samples\tokens\example-healthy-token.json --json`

其含义是：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`使用健康样例 token 数据运行分析，并以 JSON 格式输出结果。`

### **2.3 本地脚本验证**

今天在 PyCharm 中完成了两个样例输入的运行验证。

**健康样例**

输入：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`samples\tokens\example-healthy-token.json`

观察到的结果方向：

| 字段 | 结果 |
| --- | --- |
| symbol | GOOD |
| grade | A |
| action | manual_review |
| risk_score | 20 |
| opportunity_score | 75 |

**风险样例**

输入：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`samples\tokens\example-risky-token.json`

观察到的结果方向：

| 字段 | 结果 |
| --- | --- |
| symbol | RISK |
| grade | D |
| action | filter |
| risk_score | 100 |
| opportunity_score | 30 |

这说明当前最小分析链路已经可以根据不同输入产生不同判断结果。

### **2.4 自动测试验证**

今天运行了当前项目的基础单元测试：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`tests\unit\test_analyze_token_cli_foundation.py`

运行结果：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`1 passed`

该测试确认了当前最小分析流程可以完成：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`TokenSnapshot -> analyze_token -> AnalysisResult`

当前工程层结论：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`PyCharm 本地运行、样例脚本和基础自动测试均已通过。`

## **3\. 今日学习到的工程概念**

### **3.1 命令行脚本与输入参数**

今天明确了一个重要概念：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`程序负责处理规则，参数负责告诉程序本次处理什么输入。`

当前 `scripts/analyze_token.py` 不是最终产品界面，而是早期开发和测试时的本地入口。

它的价值在于：

-   快速验证分析逻辑。
    
-   快速替换不同输入样例。
    
-   方便调试和自动测试。
    
-   后续可以被 API、定时任务或 Hermes 调用。
    

### **3.2 当前结构化结果与未来报告的区别**

当前脚本输出的是结构化分析结果，例如：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`risk_score opportunity_score grade action reasons`

它不是最终面向人的完整报告，而是后续报告层可使用的基础判断结果。

当前阶段的职责可以先这样理解：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`ChainMind 核心逻辑负责结构化判断。 AI 报告层负责把判断解释成人能读懂的摘要。 Hermes 更偏向负责触发、调度和推送。`

## **4\. Phase 1 今日检验内容**

### **4.1 Phase 1 当前理解**

Phase 1 当前先聚焦：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`用 Dune 手动分析 BSC token， 跑通风险过滤所需的数据查询和观察路径。`

今天做的是：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`Phase 1 Dune 手动分析流程首轮检验。`

它不是一次性完成整个项目，也不是马上完成所有后续阶段。

### **4.2 已检验的 Dune 分析模块**

今天已经对目标代币 `14` 检验了以下模块：

1.  DEX 交易活动观察。
    
2.  5 分钟买卖盘与净买入观察。
    
3.  Buyer Analysis 排名买家分析。
    
4.  Tracks All Trades 全量交易行为查看。
    
5.  Holder Analysis 持有人汇总与集中度字段查看。
    
6.  合约创建信息查询。
    
7.  早期买家入场前 BNB 资金来源查询。
    
8.  selected early buyers 的同来源资金汇总。
    

当前检验结论：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`Phase 1 的主要 Dune 查询路径已经能够跑通。`

## **5\. 目标代币检验记录**

### **5.1 合约创建信息**

今天已从 Dune 查询到该代币的创建记录：

| 字段 | 观察结果 |
| --- | --- |
| 创建时间 | 2026-05-17 16:12:21 |
| 区块号 | 98843750 |
| 创建交易 | 0xe9f50e4d32b55431717ee394d54f1615961b3f293dbdeb5d15a4bc8478b80d01 |
| 代币地址 | 0x205f39c39f5fe15d4ef000aeb835de8deb264444 |
| 创建侧地址观察值 | 0x757eba15a64468e6535532fcf093cef90e226f85 |

说明：

-   当前创建记录查询已可用。
    
-   本次只做流程检验，没有展开字节码审计。
    

### **5.2 交易与持有人字段**

今天从 Dune 看到了以下关键字段：

-   交易者活跃度。
    
-   `net_buy_usd` 变化。
    
-   买卖交易比例。
    
-   trader 的买入额、卖出额、净 token 变化。
    
-   holder 数量与 top holder 集中度字段。
    

Holder 汇总中观察到：

| 字段 | 观察值 |
| --- | --- |
| holder_count | 1985 |
| buy_volume_usd | 2188487.9 |
| sell_volume_usd | 2169786.4 |
| net_buy_usd | 18701.5 |
| top10_supply_pct | 0.2 |
| top20_supply_pct | 0.3 |

注意：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`集中度字段的百分比展示口径后续需要进一步确认， 不能仅凭显示值直接形成正式规则。`

### **5.3 早期买家分析**

今天已拿到前排早期买家的排名、首次买入时间、买入额和当前余额字段。

本次用于资金来源测试的前 5 个 early buyers 为：

| 排名 | 地址 |
| --- | --- |
| 1 | 0x0f80aa9dd2aff0d79455a1f7843c6e39e5a27985 |
| 2 | 0xa9b0295aa2d8486735d3fb3e92ab77e678ae3f9a |
| 3 | 0x79e337339346c9f5786a746916a0600d3f9eda65 |
| 4 | 0x175c6e02f549d9ae58205693854b2f8f8621022a |
| 5 | 0x4dc0c365578ed0b5161ce97551c613354df3e400 |

通过该模块，后续可以继续观察：

-   早期买家是否大量退出。
    
-   前排买家买入时间是否过度集中。
    
-   早期买家当前余额是否快速归零。
    

### **5.4 资金来源与同来源信号**

今天已完成前 5 个 early buyers 的入场前 BNB 资金来源测试。

观察到：

1.  排名第 1 的 early buyer 在首次买入前收到了多笔 BNB 入账。
    
2.  地址 `0x62ccef0b4545166f721caa9fee13c1d3767e27dc` 在选定 early buyers 中覆盖了 2 个买家。
    
3.  地址 `0x10ed43c718714eb63d5aa57b78b54704e256024e` 也覆盖了 2 个买家，但这类基础设施地址不能直接当作真实出资人判断。
    

本次学习到的关键点：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`同来源资金是风险证据之一， 但同一个来源地址不一定代表同一个真实人或同一实体。`

后续若要把 same-funder 信号写入规则，需要先区分：

-   普通钱包地址。
    
-   DEX Router。
    
-   池子合约。
    
-   其他协议基础设施地址。
    

## **6\. Phase 1 当前结论**

### **6.1 已完成**

截至 2026-05-21，已经完成：

-   Phase 1 的首轮流程检验。
    
-   Dune 主要分析模块可执行性验证。
    
-   当前项目 Python 本地运行与测试验证。
    
-   第一份 Phase 1 检验报告落盘。
    

本次检验报告位置：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`experiments/week1-risk-filter/phase1-check-report.md`

### **6.2 当前阶段判断**

当前可以将 Phase 1 状态记录为：

![](http://localhost:63342/markdownPreview/277497423/docs/progress?_ijt=3l4bp4ejcm389oqs945ukjbr59)

`Phase 1 首轮检验完成。`

这表示：

-   手动分析流程可跑通。
    
-   查询模块已被理解和验证。
    
-   可以进入下一阶段准备。
    

这不表示：

-   整个项目已经完成。
    
-   后续规则、报告、实体识别、推送、复盘已经完成。
<!-- DAILY_CHECKIN_2026-05-21_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->


几天继续了链上数据分析，AI+Defi投研报告自动项目的学习详细链接[链接](https://github.com/may-tonk/ai-web3-school-cohort-0/tree/codex/chainmind-foundation)
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->



**今天和AI探讨了链上数据分析，AI+Defi的想法，简单的建立了一个工作项目计划，内容太多了，上传到了AI x Web3school的GitHub了；详细请查看**[**链接**](https://github.com/may-tonk/ai-web3-school-cohort-0/blob/master/daily/2026-05-19/AI_DeFi_Meme_Workflow_%E5%AD%A6%E4%B9%A0%E6%80%BB%E7%BB%93.md)
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->




\# 2026-05-18 — Day 1: 初始化与学习启动

\> 日期：2026-05-18

\> 周次：Week 1

\> 主题：AI and Web3 foundations — 基础对齐 + 数据连接

\---

\## 📝 今日学习内容

\### 课程/资料阅读

\- \[x\] 读取 Learning Agent Prompt: [https://aiweb3.school/learning-agent.zh.txt](https://aiweb3.school/learning-agent.zh.txt)

\- \[x\] 阅读 Handbook 结构和内容：[https://aiweb3.school/zh/handbook/](https://aiweb3.school/zh/handbook/)

\- \[x\] 了解 WCB Agent API 文档: [https://web3career.build/llms.txt](https://web3career.build/llms.txt)

\### 关键收获

\- Learning Agent 设计原则：轻量优先、人工确认、开源沉淀、隐私安全

\- 仓库结构：daily/ tasks/ experiments/ handbook-feedback/ hackathon/ submissions/ templates/

\- 每日流程：课程 → 实践 → 笔记 → 打卡

\- 课程时长确认：\*\*4 周\*\*（2026-05-18 → 2026-06-14）

\---

\## 🚀 今日产出物

\### 1. GitHub 学习仓库（完成初始化）

\- 创建本地仓库并 push 到 GitHub

\- 仓库地址：[https://github.com/may-tonk/ai-web3-school-cohort-0](https://github.com/may-tonk/ai-web3-school-cohort-0)

\- 总计 **5 次 commit**

\### 2. 核心文件

\- \[x\] `profile.md` — 学员画像（技能、目标、方向）

\- \[x\] `learning-plan.md` — 4 周精确学习计划（ChainMind 项目主线）

\- \[x\] `tasks/week1-daily-tasks.md` — Week 1 每日任务清单

\- \[x\] `README.md` — 项目介绍 + Week 1 目标 + 记录结构

\### 3. 目录结构

\- \[x\] `daily/` — 每日学习笔记

\- \[x\] `tasks/` — 每周任务清单

\- \[x\] `experiments/` — 实验记录

\- \[x\] `handbook-feedback/` — 手册反馈

\- \[x\] `submissions/` — 最终交付物

\- \[x\] `templates/` — 笔记模板

\- \[x\] `hackathon/` — 黑客松材料

\### 4. 环境配置

\- \[x\] `.env` 安全存放 WCB Agent Secret API Key（已加入 .gitignore）

\- \[x\] `.gitignore` — 排除敏感文件

\- \[x\] 仓库移至 D 盘`D:\ai-web3-school-cohort-0`）

\### 5. WCB 平台连接

\- \[x\] 验证 WCB API 连接正常

\- \[x\] 确认已录取 AI × Web3 School（Program ID: `cmnx791nl008sru0167pzp4ki`）

\- \[x\] 查看今日活动安排（Co-learning + AI 基础讲座）

\---

\## 📊 今日打卡信息

**打卡类型**：初始化完成 / 学习记录

**主要证据**：GitHub 仓库 + 学习计划 + 每日笔记

**证据链接**：[https://github.com/may-tonk/ai-web3-school-cohort-0](https://github.com/may-tonk/ai-web3-school-cohort-0)

\---

\## 🤔 反思与问题

1\. 平台任务似乎尚未发布`tasks.listForLearner` 返回空），可能需要明天再查。

2\. 今天以工程化初始化为主，明天开始进入核心学习与编码阶段。

3\. 需要了解 Hermes Agent 的具体使用方式，以便更好地将学习流程自动化。

\---

\## 📅 明日计划（Day 2 — 5/19）

\- \[ \] 搭建 `chainmind/core/agent.py` ReAct 骨架

\- \[ \] 学习 Handbook LLM / Tool Use 章节

\- \[ \] 实现多工具支持

\- \[ \] git commit: `feat: multi-tool support with retry`

\---
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
