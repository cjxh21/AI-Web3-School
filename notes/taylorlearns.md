---
timezone: UTC+8
---

# taylorlearns

**GitHub ID:** taylorlearns

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->
今天学习了prompt，context 还有network。

Web3相关的内容确实是更复杂，需要更多的时间理解，但是知识充满脑部的感觉确实非常好，虽然需要从非常基础的概念理解开始，但总体还是非常兴奋的，希望我作为一个完全的Web3小白，在学习的过程中可以发现更多Web3跟AI相结合的机会，挖掘在黑客松里面项目的点！
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->

昨天完成了Hermes的Onboarding，装在WSL里面的学习小助手，赐予了他我家小猫的名字

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/taylorlearns/images/2026-05-18-1779082056096-image.png)

沟通工具，因为没有TG，还是继续用飞书了，其实也蛮好用，比微信好用很多，可读性更强

微信还是更偏即时通讯软件一些，适合阅读一些短句子，agent的输出还是偏长的，如果在微信可读性会比较差

今天开始正式上课，第一天还是过了一些比较基础的概念，希望在这一个月里面，可以真正学习到Web3相关的内容，最理想的状态是能找到一个真的值得我投入时间的方向，实现我做自己产品的理想。

在用Agent接入WCB的过程中，agent反复给我返回任务列表是空的问题，但我没有仔细思考为什么，我发现在网页端可以看到任务列表，后面我让他重新爬一遍handbook，还有网站的文档，发现可能是他漏了一个track ID没有填写，更多还是需要在agent给到你反馈后，反复确认，不能够完全的依赖模型的推理能力，多渠道确认才能最大程度提升抽卡概率

PS，附上茶茶咪自己找到的问题原因

trackId 的来源是 WCB 页面数据里的 `curriculumWeeks[0].trackId`，我是在之前抓 WCB 页面时拿到的那个隐藏 JSON 数据里发现的： \`\`\`json "curriculumWeeks": \[ { "trackId": "cmoy1hces012app01kp9ci5gb", "title": "Week 1｜共学营：AI 与 Web3 基础知识" } \] \`\`\` **教训：** `tasks.listForLearner` 的 `trackId` 是\*\*必填参数\*\*，不传就啥也查不到。Catalog 里写了 `inputExample: {"programId": "<programId>", "trackId": "<trackId>"}`，但我之前的请求少了 trackId 没报错，悄无声息地返回空数组，误导我以为没任务
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
