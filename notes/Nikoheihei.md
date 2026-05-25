---
timezone: UTC+8
---

# Jing Xia

**GitHub ID:** Nikoheihei

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-25
<!-- DAILY_CHECKIN_2026-05-25_START -->
ETH的特性决定它适配成为AI的基础网络。审查抗性：如智能合约，第三方试图中止交易这种尝试会失败。

![截屏2026-05-25 21.18.07.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/Nikoheihei/images/2026-05-25-1779715813667-__2026-05-25_21.18.07.png)

eth更加中立，而中心化的机构会导致不同公司掌握不同agent的结果。（之前和朋友聊到未来不会我们的数据都不属于我们而是属于不同大厂吧这个话题，这样看来确实eth很中立）

eth向agent economy infra转型的优势是可编程货币。天然适配agent。
<!-- DAILY_CHECKIN_2026-05-25_END -->

# 2026-05-24
<!-- DAILY_CHECKIN_2026-05-24_START -->

GG18协议整个生命周期主要分为两个阶段，分布式密钥生成阶段和分布式签名阶段。分布式密钥生成阶段：各个参与方在本地生成一个秘密随机数，通过同态加密和零知识证明，在不公开随机数的同时，共同推导出全局的公钥。每个参与方获得自己的私钥分片。没有任何一个人知道完整的私钥。分布式签名阶段（共 9 轮交互）：当需要发起交易时，选定 ‭M个在线节点。为了在不拼接私钥的情况下算出 ECDSA 签名（涉及求逆元等复杂操作），这 ‭M个节点需要进行复杂的数学运算。  

GG18 的缺陷：在 GG18 的多轮签名计算中，如果突然有一个节点作恶，系统虽然能发现签名失败，但无法揪出到底是哪个节点在使坏。这就导致攻击者可以通过不断捣乱来实施拒绝服务攻击。GG20 的改进：利用更高级的零知识证明，确保一旦签名过程中断或出错，系统可以精准锁定作恶或断线的节点 ID，方便系统将其踢出或惩罚。

其他优化：

离线预计算：GG20 引入了预计算机制。节点可以在没有实际交易时，提前把最消耗时间的那些乘法同态加密步骤做完。

在线 1 轮通信：当真实的交易和哈希值到来时，节点只需要进行1轮消息交互，就能瞬间吐出最终的签名。计算公式只含乘法和加法。
<!-- DAILY_CHECKIN_2026-05-24_END -->

# 2026-05-21
<!-- DAILY_CHECKIN_2026-05-21_START -->


完成任务 3：用 agent 生成可交互学习产物

![截屏2026-05-21 21.54.53.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/Nikoheihei/images/2026-05-21-1779372622598-__2026-05-21_21.54.53.png)![截屏2026-05-21 22.05.17.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/Nikoheihei/images/2026-05-21-1779372632713-__2026-05-21_22.05.17.png)![截屏2026-05-21 22.08.33.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/Nikoheihei/images/2026-05-21-1779372669880-__2026-05-21_22.08.33.png)
<!-- DAILY_CHECKIN_2026-05-21_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->



配置hermes成功，同时接入飞书成功

![截屏2026-05-20 21.23.52.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/Nikoheihei/images/2026-05-20-1779286284329-__2026-05-20_21.23.52.png)
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->




我的learning agent 为codebuddy，后续可能会优化为hermes，今日实现了AI 生成命令&合约 → 人工复核 → 链上执行 → Etherscan 验证。遇到的问题：infuria登陆帐号反复闪退，原因未知，更换为alchemy。

![截屏2026-05-19 21.39.17.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/Nikoheihei/images/2026-05-19-1779198183008-__2026-05-19_21.39.17.png)![截屏2026-05-19 22.39.49.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/Nikoheihei/images/2026-05-19-1779201734553-__2026-05-19_22.39.49.png)
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->





在web3，安全和信任非常重要。审计只是保底手段，但是安全要融入到程序内。

![截屏2026-05-18 20.20.27.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/Nikoheihei/images/2026-05-18-1779110274915-__2026-05-18_20.20.27.png)
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
