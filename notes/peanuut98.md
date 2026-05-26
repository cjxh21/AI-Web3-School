---
timezone: UTC+8
---

# peanuut98

**GitHub ID:** peanuut98

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-24
<!-- DAILY_CHECKIN_2026-05-24_START -->
Day 7 · 2026-05-24 · @peanuut98

今日学习：

\- 复盘了在 Rabby + Base Sepolia 上发的那笔测试网转账（一个测试地址 → 另一个测试地址，全程测试网，无主网资产）。

\- 在 BaseScan 上把 Tx Hash / Status / Block / Timestamp / From / To / Value / Txn Fee 这 7 个字段重新读了一遍，对照 Day 1–Day 3 学的概念，每个字段都能用自己的话解释。

\- 整理了一份「链上验证清单」：钱包说成功不算数，必须 Tx Hash 在 BaseScan 上能搜到才算真的上链；From 余额扣减 = Value + Txn Fee。

\- 划清楚了哪些步骤钱包能帮我做（签名 / 估 Gas / 广播），哪些必须人工确认（网络选择 / 地址核对 / 金额位数 / Gas 量级 / 签名内容）。

最大的认知变化：

\- 区块浏览器不是「一个看交易的网站」，是链上事实的唯一二次验证渠道 — 这是「钱包侧成功」和「链上侧成功」的分界线。

卡点：

\- 还没真正接触合约调用 / ERC-20 转账，BaseScan 的 Token Transfers 和 Input Data 怎么读，下周再补。

明日 / 下周：

\- Day 8：写 Week 1 weekly note，把这一周整理成一份复习材料。

\- Week 2：开始读 Transaction 的细节（mempool、确认数、ERC-20、第一次 Read Contract）。

🔗 [https://github.com/peanuut98/ai-web3-school-cohort-0/blob/main/daily/2026-05-24.md](https://github.com/peanuut98/ai-web3-school-cohort-0/blob/main/daily/2026-05-24.md)
<!-- DAILY_CHECKIN_2026-05-24_END -->

# 2026-05-23
<!-- DAILY_CHECKIN_2026-05-23_START -->

Day 6 · 2026-05-23 · @peanuut98

诚实记录：Day 4 (05-21) 和 Day 5 (05-22) 我没打卡，也没真的学。今天 Day 6 不补假打卡，而是回到主线把 Wallet 这一章稳住。

今日学习：

\- 复习 Day 1–Day 3：把「区块 / 公私钥 / 钱包」这条主线自己复述了一遍，发现 Day 3 关键概念（助记词、派生路径、冷热钱包）当时填得不够实，今天补回来。

\- Handbook: Wallet — 重新读了一次，搞清楚助记词背后是 BIP39，派生路径 m/44'/60'/0'/0/0 里 60' 对应 EVM 链。

\- 链上练习：在 Sepolia Etherscan 上找回 Day 3 自己那笔自转账，把 6 个字段重新读了一遍；又随便点了一笔别人的 tx 做对照。

最大的收获：

\- 「学过」≠「记住」。Day 3 当时以为搞懂了 Wallet，今天复述才知道还有缺口 — daily note 是写给未来的自己的复习材料。

卡点：

\- Keystore 和助记词到底是不是同一份私钥的两种存储格式，没读懂。

\- 别人交易里 Input Data 那串 0x... 现阶段完全读不懂，记下来等讲合约调用时回头看。

明日：

\- 把 Day 4 / Day 5 原计划的 Wallet 后半 + Transaction 开头压成一天读完。

\- 周日晚上做一次 Week 1 小结。

🔗 [https://github.com/peanuut98/ai-web3-school-cohort-0/blob/main/daily/2026-05-23.md](https://github.com/peanuut98/ai-web3-school-cohort-0/blob/main/daily/2026-05-23.md)
<!-- DAILY_CHECKIN_2026-05-23_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->


Day 3 · 2026-05-20 · @peanuut98

今日学习：

\- Handbook: Wallet — 终于把「钱包不是装币的口袋，而是私钥管理工具 + 签名入口」这句话读懂了。地址、助记词、派生路径之间的关系也串起来了一点。

\- 实操：装了 MetaMask，创建了一个全新钱包（助记词抄在纸上、没存电子设备），切到 Sepolia 测试网，领了一点测试 ETH，发了一笔自转账，再到 Sepolia Etherscan 上把昨天学的 6 个字段重新读了一遍 — 概念第一次有了「手感」。

\- 产出：daily/[2026-05-20.md](http://2026-05-20.md) 已 commit 到学习仓库。

最大的认知变化：

\- 钱包 ≠ 账户。一组助记词可以派生出无数个地址，MetaMask 只是这条派生链路的 UI。

卡点：

\- 派生路径（m/44'/60'/0'/0/0 这种）每一段到底代表什么，还需要再读一遍。

明日：

\- Wallet 续 — Seed phrase / Keystore / 派生路径的细节。

\- 想搞清楚：为什么同一组助记词，在 MetaMask 和 Rabby 里能恢复出同一组地址（背后是 BIP39 + BIP44 这套标准在起作用）。

🔗 [https://github.com/peanuut98/ai-web3-school-cohort-0/blob/main/daily/2026-05-20.md](https://github.com/peanuut98/ai-web3-school-cohort-0/blob/main/daily/2026-05-20.md)

\`\`\`
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->



Day 2 · 2026-05-19 · @peanuut98

今日学习：

\- Handbook: Cryptography — 第一次把「私钥签名、公钥验证、地址是公钥的一段 hash」这条链路串起来。

\- 实验：用 SHA-256 工具算了 hello / Hello / hello(带空格) 三个字符串，直观感受到 1bit 输入差异 → 完全不同的 hash（雪崩效应）。

\- 产出：daily/[2026-05-19.md](http://2026-05-19.md) 已 commit 到学习仓库。

卡点：

\- 还不太清楚「签名」在链上到底是怎么被验证的（节点拿到 tx 后具体做了哪几步）。

明日：

\- 读 Wallet 章节，搞清楚钱包 ≠ 私钥本身，而是私钥的管理工具。

🔗 [https://github.com/peanuut98/ai-web3-school-cohort-0/blob/main/daily/2026-05-19.md](https://github.com/peanuut98/ai-web3-school-cohort-0/blob/main/daily/2026-05-19.md)

![截屏2026-05-19 23.12.25.png](https://raw.githubusercontent.com/IntensiveCoLearning/AI-Web3-School/main/assets/peanuut98/images/2026-05-19-1779203675061-__2026-05-19_23.12.25.png)
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->





Day 1 · 2026-05-18 · @peanuut98

今日学习：

\- Handbook: Network — 第一次系统理解 block / consensus / L2 / RPC，最有共鸣的是 RPC 就是「与链对话的入口」。

\- 实验：在 Etherscan 翻了一笔交易，认出了 Block#/Timestamp/From/To/Value/Gas Used 这些字段。

\- 产出：daily/[2026-05-18.md](http://2026-05-18.md) 已 commit 到学习仓库。

卡点：

\- 还没完全分清 L1 finality 和 L2 finality 的差异，先记着。

明日：

\- 读 Cryptography 章节（公私钥），自己跑一遍 SHA-256 直觉实验。

🔗 [https://github.com/peanuut98/ai-web3-school-cohort-0/blob/main/daily/2026-05-18.md](https://github.com/peanuut98/ai-web3-school-cohort-0/blob/main/daily/2026-05-18.md)
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
