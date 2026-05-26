---
timezone: UTC+8
---

# Hesper

**GitHub ID:** Y-shuyi

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-26
<!-- DAILY_CHECKIN_2026-05-26_START -->
我想建立一个question bank的workflow，可以自动化地按照我关于课题的需要、我自己的学习路径+目标+习惯，去定制化question bank，让这个问题集合服务于我建立更好的知识系统。众所周知提问是非常重要的，尤其是现在有AI回答问题的速度会越来越快，但反过来说，也不是所有的问题都需要在当地下得到解答；AI的便利性也要求我们能够不迷失在问题里，让每一个问题之间由点成线，由线成面。基于这个理念我希望建立这样一个小的、可视化的学习工具。

-   梳理了Question Bank的基本结构
    

![Screenshot 2026-05-26 at 12.19.02.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/Y-shuyi/images/2026-05-26-1779769199686-Screenshot_2026-05-26_at_12.19.02.png)
<!-- DAILY_CHECKIN_2026-05-26_END -->

# 2026-05-25
<!-- DAILY_CHECKIN_2026-05-25_START -->

# 打卡日志 — 2026-05-25

**学习时长**：\_ \_ 小时

## ✅ 今日完成

-   \[x\] 配置 Claude 工作流 hook（自动提醒 /rename 和 /export）
    
-   \[x\] 修复 hook shell 语法错误
    
-   \[x\] 学习 Hermes Agent 使用逻辑
    
-   \[x\]co-learning session
    

## 💡 核心收获

-   建立了对话管理工作流：新对话用 `/rename` 命名，结束用 `/export` 保存 md
    
-   搞清楚终端对话窗口里不能直接发 shell 命令——输入的所有内容都是"聊天内容"，不是 terminal 指令
    
-   理解了 Hermes vs Claude 的核心差异：Claude 自带"手脚"（Bash/Read/Edit 工具）；Hermes 是纯语言模型，工具执行层需要自己搭
    
-   Hermes 可以通过 tool use / function calling 装手脚，但执行器要自己写
    

### co-learning

Q:不怎么了解黑客松，做哪些方向比较好？ A:马铃薯

-   做有趣的UX，因为交易一般都很无聊；可以去看看有趣的UX是怎么做的。
    
-   隐私赛道也不错。
    
-   多与AI 聊天，积极和学霸组队！
    

## ❓ 遇到的问题 / 待解决

-   Hermes `/resume` / title 功能显示不出历史对话列表（原因待查，下次从 `hermes --help` 入手）
    

## 🔗 参考资料

-   Nous Research：[https://nousresearch.com](https://nousresearch.com)
    
-   Clippings/你好，我是小白，能白話的跟我說說啥是Kohaku跟Railgun嗎？[https://x.com/0xMalingshu/status/2016137832465682514](https://x.com/0xMalingshu/status/2016137832465682514)
    

## 📝 Handbook Feedback（如有）

-   章节：
    
-   反馈：
    

* * *

## 🗒 会话总结（/rename about hermes agent）

### 今日决策

-   Claude 工作流规则确立：每次新对话先 `/rename`，结束前 `/export`
    
-   正确命令确认：`/rename`（不是 `/title`），`/export`（不是其他）
    
-   Hermes 学习策略：先理解"模型 vs 客户端"的分层，再看具体功能
    

### 变更文件

-   `~/.claude/settings.json`：新增 SessionStart hook（提醒 /rename）和 Stop hook（提醒 /export）
    

### 明天第一步

-   查 `hermes --help` 或 Hermes 文档，找到历史对话 session 管理的正确用法
    
-   继续 Hermes agent 工具调用（tool use）的实践
<!-- DAILY_CHECKIN_2026-05-25_END -->

# 2026-05-24
<!-- DAILY_CHECKIN_2026-05-24_START -->


![Screenshot 2026-05-24 at 23.57.18.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/Y-shuyi/images/2026-05-24-1779638290862-Screenshot_2026-05-24_at_23.57.18.png)
<!-- DAILY_CHECKIN_2026-05-24_END -->

# 2026-05-23
<!-- DAILY_CHECKIN_2026-05-23_START -->



![Screenshot 2026-05-23 at 23.59.19.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/Y-shuyi/images/2026-05-23-1779551983031-Screenshot_2026-05-23_at_23.59.19.png)![Screenshot 2026-05-23 at 23.59.11.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/Y-shuyi/images/2026-05-23-1779551995589-Screenshot_2026-05-23_at_23.59.11.png)
<!-- DAILY_CHECKIN_2026-05-23_END -->

# 2026-05-22
<!-- DAILY_CHECKIN_2026-05-22_START -->




![Screenshot 2026-05-22 at 23.57.21.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/Y-shuyi/images/2026-05-22-1779465443887-Screenshot_2026-05-22_at_23.57.21.png)

今天诚实地请个假，有优先级更高的事情需要做。
<!-- DAILY_CHECKIN_2026-05-22_END -->

# 2026-05-21
<!-- DAILY_CHECKIN_2026-05-21_START -->





**核心Takeaway：**AI 从"工具"变成"经济参与者"的那一刻，Web3 就从可选项变成了必需品。

/

**问：Web3产品保证安全是最重要的部分吗？安全之外有哪些维度？**

答：安全在AI+web3的产品当中的确比普通的软件产品权重更高。

-   **资产直接在链上**，出了漏洞钱就没了，不像传统软件可以回滚
    
-   **代码公开**，任何人都可以研究你的合约找漏洞
    
-   **用户信任门槛极高**，一次安全事故基本就死了
    

但是我现在所看到的一些情况是为了开发一个AI+链上产品而去做产品，变成了技术找场景，而不是场景找技术。

想到今天老师说的，大意是技术平权之后，真正需要的是**产品设计思维**。产品设计当中最重要的，包括用户真实需求和产品体验；  
技术以外，另一个难点是“冷启动”；关于一个项目团队的配置——如果A做产品，就需要找到运营BD等去做产品的推广。

/

目前对老师聊到的这几个方向还没有一个比较具体的感觉，再摸索下，尤其是如何看懂AI+web3：

1.  Agent需要经济账户
    
2.  每个项目在回答Agent经济栈的一个具体问题
    
3.  Token不是价值本身，重要的是让软件进入可授权、可结算、可审计的经济系统
    

/

Further question/action：

-   Web3 产品普遍体验很差？
    
-   搜索几款常用的和支付等我感兴趣赛道相关的产品，去体验。
<!-- DAILY_CHECKIN_2026-05-21_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->






今天主要听了Bruce分享的Web3的运行基础。之前我也听不同的人讲过这个部分，其它部分Bruce老师的解读其实能发现是从技术底层逻辑上去拆解为什么其中某一个环节的存在对于整个系统会有影响——这一点其实我还不够问自己更深。最后的Takeaway是web3不仅是关于技术，技术只是基础设施，而更涉及到社会学、经济学和密码学。
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->







![Screenshot 2026-05-19 at 15.37.24.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/Y-shuyi/images/2026-05-19-1779191101442-Screenshot_2026-05-19_at_15.37.24.png)

今天主要是在部署Hermes Agent，遇到一些网络问题，不过借助gemini解决了。以及目前已经准备好了TG bot，下一步是接LLM的API。  
  
主要参考内容  
官方deployment：  
[https://hermes-agent.nousresearch.com/docs/](https://hermes-agent.nousresearch.com/docs/)

X博主分享：  
[https://x.com/eternityspring/status/2041735065865220416?s=46](https://x.com/eternityspring/status/2041735065865220416?s=46)
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->








-   **你是带着什么问题来的？**
    
    > 我想解决的核心问题是：了解自己现阶段（至少这3个月）在web3/AI想要深入的方向。
    
-   **一个月之后，你希望自己变成什么样？**
    
    > 一个月后，我希望能：更了解好的产品的形态；对于web3能够从不同角度参与建设（参与的维度增加，比如有跟lxdao社区members更深层的交互）；可以成为朋友问web3/AI相关问题就会来找的那个人。
    
-   **你最想 build 的东西是什么？**  
    目前没有特别想build的东西，以及没有觉得自己非得从无到有创造一个东西。不过会重点关注、了解下agent commerce和数据主权、隐私相关的产品。想build的更多是一种可持续投入的心态吧。
    

选好助教、布置好agent，把注意力集中在网站的资源上，放平心态，共学共建设。
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
