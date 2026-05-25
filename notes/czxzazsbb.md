---
timezone: UTC+8
---

# czxzazsbb

**GitHub ID:** czxzazsbb

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-26
<!-- DAILY_CHECKIN_2026-05-26_START -->
```
---
theme: 用 Learning Agent 启动 cohort · AI 协作的第一手观察
handbook_link: https://aiweb3.school/learning-agent.zh.txt
---

# 2026-05-26 · Day 9 · 用 Learning Agent 启动 cohort

> 今天和一个真实的 AI Agent 协作完成了 cohort 初始化。这次协作本身就是一堂"AI 怎么用"的实操课，把过程沉淀下来比抄 Handbook 有价值。

## 今日实际路径

把 `https://aiweb3.school/learning-agent.zh.txt` 这个 URL 发给 Claude（自称 Learning Agent），让它按启动 prompt 把整个 cohort 工作流跑起来：画像 → GitHub CLI 登录验证 → 仓库定位 → 目录初始化 → 学习计划 → 今日打卡草稿 → Handbook feedback 流程 → memory 沉淀。

用时约 60–80 分钟（含来回确认）。

## 从这次协作里观察到的 AI 知识点

### 1. "启动 prompt" 不只是聊天的开场白

启动 prompt 是一段独立托管在 URL 上的文本，定义了 Agent 的：

- **角色**（学员的个人 Learning Agent，不是替学员学）
- **固定入口**（Handbook、WCB、GitHub CLI——打不开就让学员自己开，不要猜内容）
- **流程**（8 步：画像 → 登录 → 创仓 → 目录 → 每日 → feedback → API → 输出）
- **设计原则**（轻量优先 / 人工确认 / 开源沉淀 / 隐私 / 闭环 / 边界）

关键观察：**Agent 拿到 URL 后第一件事是 fetch 文本**，所以这个 prompt 的"权威性"来自它被托管在固定 URL，而不是被嵌在某个工具的代码里。这是一种"开源 prompt"的模式。

### 2. 画像收集是分步对话，不是一次性表单

Agent 严格遵守了"每轮最多 2–3 个问题"。第一轮问 AI/Web3/编程基础三档；第二轮问目标/时间/语言。然后**复述**让我确认，确认后才动手。

体感对比：如果一次扔一张大表单给我，我可能乱填或放弃。分两轮 + 复述确认，每一步都能纠偏。

### 3. "人工确认"是 Agent 的护栏，不是麻烦

整个流程里 Agent 在以下节点停下来等我点头：
- 画像复述
- 仓库名/路径/可见性
- 提醒时间
- 发现 repo 已存在 → 复用 vs 新建（这一步如果不停下来，可能就把我之前的笔记搞坏了）
- 发现是 fork → 目录布局调整（顶层 vs `personal/` 子目录）
- 隐私字段（Telegram、邮箱默认全空）
- commit/push 范围
- **git config 不会自动改**（这条挺关键，Agent 主动放弃了便利、把决定还给我）

这告诉我：一个负责任的 Agent，**默认拒绝替我做不可逆决定**。

### 4. Agent 不是 magic——会遇到环境问题

实际过程里出了这些"工程现实"问题，看 Agent 怎么处理的：

| 现象 | Agent 的处理 |
| --- | --- |
| `gh` 装了但 bash PATH 是旧的 | 用 PowerShell 直接读注册表里的 user PATH，绕过老 shell |
| 想建 `ai-web3-school` 但已存在 | 没强建，先 `gh repo view` 看清楚是什么，再问我怎么处理 |
| clone 后发现是 fork | 重新做需求分析（fork 的目录布局 ≠ 独立 repo 的目录布局） |
| `git commit` 报 author identity unknown | **没自动改 global config**，而是查 GitHub 上我的 id 给我推荐 noreply 邮箱，让我选 |

观察：Agent 处理"意外"的方式是**先看清楚再决定**，而不是"重试到成功"。

### 5. Fork-of-shared-repo 是和"个人 repo"不一样的工作模式

启动 prompt 默认每个学员一个独立 public repo。但这个 cohort 实际上是大家 fork 一个共学仓库，每个人维护 `notes/<id>.md` 一个文件，README 由 `sync_status_readme.py` 自动按 commit 频次生成。

布局对策：
- **官方打卡**走 `notes/czxzazsbb.md` 的 `<!-- Content_START --> ... <!-- Content_END -->`——这是被 README 统计的"权威打卡渠道"
- **个人材料**全部放 `personal/` 子目录，不污染顶层、不和 upstream 冲突
- **打卡同步**：详细笔记在 `personal/daily/YYYY-MM-DD.md`，`notes/czxzazsbb.md` 里只放摘要+链接

## 我还没搞懂的问题

- `sync_status_readme.py` 只看**commit 数**还是同时看 Content 区**内容更新**？如果只看 commit 数，那空 commit 也能"水"打卡——但启动 prompt 明确说"不要做空 commit"。
- fork 的 commit 怎么进入 upstream 的统计？需要每次开 PR 合并？还是 sync 脚本直接扫所有 fork？
- WCB Learning 平台和 GitHub 打卡是两套独立系统吗？两边都要做？

> 这些问题写下来，明天去 Handbook / WCB 文档里找答案，或在 TG 群问。

## 今日真实产出

| 文件 | 状态 |
| --- | --- |
| `personal/README.md` | ✅ commit `b78765b6` 已 push |
| `personal/profile.md` | ✅ 同上 |
| `personal/learning-plan.md` | ✅ 同上（3 周计划 Day 8–28） |
| `personal/daily/2026-05-25.md` | ✅ 本文件 |
| `personal/handbook-feedback/README.md` | ✅ 同上 |
| `personal/templates/{daily-note.md, task-note.md}` | ✅ 同上 |
| `notes/czxzazsbb.md` | ⚠️ 本地已改，**未 push**（等正文补完一起走） |
| Claude memory（4 个文件） | ✅ 已落地，下次会话能直接接上 |
| 12:00 / 22:00 提醒 | ❌ 未设（自行记） |
| WCB Learning 打卡 | ❌ 未做（需自行打开链接提交） |


## 打卡同步

- [ ] 本文件正文已写完
- [ ] 同步摘要到 `notes/czxzazsbb.md` 的 Content 区
- [ ] commit + push 到 origin
- [ ] PR 到 upstream（让打卡进入官方统计）
- [ ] WCB Learning 打卡：https://web3career.build/zh/programs/AI-Web3-School#tab=learning
```

![屏幕截图 2026-05-25 225959.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/czxzazsbb/images/2026-05-25-1779726271875-_____2026-05-25_225959.png)
<!-- DAILY_CHECKIN_2026-05-26_END -->

# 2026-05-25
<!-- DAILY_CHECKIN_2026-05-25_START -->

用 Learning Agent 启动 cohort · AI 协作的第一手观察

|   |   |   |
| --- | --- | --- |
|   |   |   |
|   |   |   |
<!-- DAILY_CHECKIN_2026-05-25_END -->

# 2026-05-23
<!-- DAILY_CHECKIN_2026-05-23_START -->


观看web3运行原理的直播

1.  ![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/czxzazsbb/images/2026-05-23-1779542705454-image.png)
    
    大概路径：身份——授权——传播——排序——执行——确认
    
2.  共识机制:PoW vs PoS
    
    ![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/czxzazsbb/images/2026-05-23-1779544560185-image.png)
3.  智能合约：写在链上能被交易触发的代码
    
4.  web3是三门学科的交叉：密码学、经济学、社会学
<!-- DAILY_CHECKIN_2026-05-23_END -->

# 2026-05-21
<!-- DAILY_CHECKIN_2026-05-21_START -->



Hermes Agent 简介

Hermes Agent 是由 \[Nous Research\]([https://nousresearch.com/](https://nousresearch.com/)) 开发的开源 AI 智能体框架，核心特性：

\- 自进化学习：从交互中自动生成“技能”（Skill），越用越聪明

\- 多模型支持：兼容 OpenAI、Anthropic、DeepSeek、Ollama 等多种后端

\- 多平台接入：支持 Telegram、Discord、QQ、邮箱等

\- 轻量高效：Python 开发，内存占用约 850MB

环境准备

 1. 安装 WSL2（如未安装）

在 PowerShell（管理员）中执行：

powershell

wsl --install -d Ubuntu

 2. 进入 WSL 环境

bash

wsl

安装 Hermes Agent

第一步：安装 uv（Python 包管理器）

bash

curl -LsSf [https://astral.sh/uv/install.sh](https://astral.sh/uv/install.sh) | sh

如果提示 uv: command not found，执行：

bash

echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc

source ~/.bashrc

验证安装：

bash

uv --version

第二步：安装 Hermes

bash

curl -fsSL [https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh](https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh) | bash

安装过程会自动：

\- 检测/安装 Python 3.11+

\- 安装 Node.js（用于浏览器自动化）

\- 克隆代码到 ~/.hermes/hermes-agent

\- 创建虚拟环境并安装依赖

安装完成后：

bash

source ~/.bashrc

hermes --version  验证安装

配置模型提供商

方案一：DeepSeek API（国内推荐）

DeepSeek 国内可直接访问，新用户有免费额度（约 500 万 tokens）。

获取 API Key：

1\. 访问 \[DeepSeek 开放平台\]([https://platform.deepseek.com/](https://platform.deepseek.com/))

2\. 注册账号

3\. 进入“API Keys”页面创建密钥

配置 Hermes：

bash

hermes setup

选择 Quick setup → 在列表中找到 DeepSeek → 依次输入：

\- API Key（粘贴你的密钥）

\- Base URLhttps://[api.deepseek.com](http://api.deepseek.com)

\- 模型deepseek-chat 或 deepseek-coder

方案二：Claude API（Anthropic）

Claude 能力最强，适合高质量对话和复杂推理，需国际信用卡。

获取 API Key：

1\. 访问 \[Anthropic Console\]([https://console.anthropic.com/](https://console.anthropic.com/))

2\. 注册账号（需国外手机号验证）

3\. 进入“API Keys”页面创建密钥（新用户有 $5 赠金）

配置 Hermes：

bash

hermes setup

选择 Quick setup → 在列表中找到 Anthropic (Claude models) → 选择认证方式：

\- 选 2（Anthropic API key - pay-per-token）

\- 粘贴 API Key

\- 选择模型（推荐 claude-sonnet-4-20250514，性价比高）

\> 可选模型claude-opus-4-7（最强）claude-sonnet-4-6（平衡）claude-haiku-4-5（最快最便宜）

方案三：Ollama 本地模型（免费离线）

完全免费，无需网络，适合隐私敏感或不想付费的用户。

安装 Ollama：

bash

curl -fsSL [https://ollama.com/install.sh](https://ollama.com/install.sh) | sh

下载模型（任选一个）：

bash

ollama run deepseek-r1:1.5b  轻量，约 1GB，适合低配电脑

ollama run llama3.2:3b  轻量，约 2GB

ollama run qwen2.5:7b  平衡，约 4GB，需 16GB 内存

ollama run llama3.1:8b  较强，约 4.7GB

配置 Hermes 使用 Ollama：

1\. 保持 Ollama 服务运行（开一个终端执行 ollama serve，或先跑一次 ollama run 并保持不退出）

2\. 在新终端中执行：

bash

hermes setup

3\. 选择 More providers... → Custom endpoint (enter URL manually)

4\. Base URLhttp://127.0.0.1:11434/v1

5\. API Key：直接回车跳过（留空）

6\. 选择已下载的模型（如 deepseek-r1:1.5b）

7\. 其余选项默认，完成

8.配置完成后，直接运行：

bash

hermes
<!-- DAILY_CHECKIN_2026-05-21_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->




1.web3一部分程度上是要解决信任问题

2.如何解决信任问题（区块链）：

•数据不可篡改

•逻辑即代码公开透明

•不同的共识协议（信任模型：POW,POS，DPOS,POH等等）

•私钥签名进行鉴权

3.链只认私钥

4.钱包在 Web3 中扮演着身份与资产管理的双重角色

5.交易更快上链主要是gas

6.nonce：止重放攻击与交易乱序执行，确保账户状态变更的原子性。

7.Data：定义了复杂的业务逻辑与参数传递，是链上应用交互的灵魂。

8.交易模拟：在提交交易前验证执行结果，精准预测交易结果，避免不必要的资产损耗，是交易可视化的非常重要的一环。（在交易签名之前做）

9.可以根据目标倒推东西（就业方面）

10.需要具备能力：

•基础能力更重要：理解协议、共识与安全边界将成为 Web3 时代的唯一护城河。

•Web3 是系统工程：它不仅是合约编写，更是对一致性、安全性与分布式协作的极致追求。
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->





1.了解了Hermes vs OpenClaw一些对比：

想要一个 越用越聪明的贴身 AI 助理，单智能体 + 内置学习闭环 → 选 Hermes

需要 组建一支 AI 团队处理复杂协作 ，多智能体编排 + 网关生态 → 选 OpenClaw

2.了解ai可以实现的web3场景：AI 赋能“交易所用户意图交易”、市场预测与情报分析

[3.hermes](http://3.hermes) agent如何切换模型hermes model

![屏幕截图 2026-05-19 210700.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/czxzazsbb/images/2026-05-19-1779196033538-_____2026-05-19_210700.png)
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->






了解一个新的ai学习软件Hermes Agent很感兴趣，希望可以搭建一个我的专属学习搭档，帮我管理时间、追踪进度和整理知识的智能搭档，有效管理学习节奏。
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
