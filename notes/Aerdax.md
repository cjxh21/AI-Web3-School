---
timezone: UTC+8
---

# YoungAd

**GitHub ID:** Aerdax

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-23
<!-- DAILY_CHECKIN_2026-05-23_START -->
今天由于一直在外面没有电脑不方便更深度的学习，所以只是用手机看了昨天和今天的课程录播，并且阅读了handbook第二章节的内容，目前学习中靠之前掌握的知识和工作中内容暂时还没有遇到什么阻碍，看到群里有很多优秀的人分享自己的学习方法或者自制的小工具，向优秀的人学习
<!-- DAILY_CHECKIN_2026-05-23_END -->

# 2026-05-22
<!-- DAILY_CHECKIN_2026-05-22_START -->

**今日完成：**

阅读 Handbook「大语言模型（LLM）」章节，完成最小实践「交易解释器」。输入以太坊交易哈希，系统读取链上事实（RPC）、 解码合约调用（ABI），并将结构化数据传给 LLM 生成带来源标注的解释。

**学到的关键点：**

把"LLM 输出不可全信"这个原则落地成代码：用

\_sources

元数据字段声明每一层数据的可信度，强制 LLM 区分 \[链上事实\] 和 \[模型推断\]，把 Hallucination 的风险限制在推断层。

**遇到的问题：**

公共 RPC 节点稳定性差异大，换用稳定节点解决。用 Uniswap V3 的真实 swap 交易验证，成功解码出

exactInputSingle

函数调用和滑点参数。

**明日计划：**

继续阅读 Handbook 下一章节，尝试给交易解释器加入 ERC-20 Transfer 事件的通用解码（不依赖主合约 ABI）。
<!-- DAILY_CHECKIN_2026-05-22_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->


今天补齐了之前所有的录播课，下班前刚好有空终于可以参加一次直播了。由于公司本来就从事web3领域，虽然在大陆公司业务能接触到的公链业务场景和技术有限，不过还好是不少了解，并且日常对ai也是深度使用，目前学习起来还挺轻松，继续努力

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/Aerdax/images/2026-05-20-1779269636559-image.png)
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->



补交18号的学习，已完成本地环境搭建
<!-- DAILY_CHECKIN_2026-05-19_END -->
<!-- Content_END -->
