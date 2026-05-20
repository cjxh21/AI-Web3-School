---
timezone: UTC+8
---

# Bein

**GitHub ID:** Minami-Bein

**Telegram:** 

## Self-introduction

I am‘s Bein.

## Notes

<!-- Content_START -->
# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->
今天深度的学会了 **Hermes 从 0 到 1** 完成构建
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->

Mythos
<!-- DAILY_CHECKIN_2026-05-18_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->
第三天的打卡
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-21
<!-- DAILY_CHECKIN_2026-05-21_START -->
# 🏷️ Day 7｜Chrome沙盒拦路？自动化启动失败的救命稻草

## 💡 今日硬核充能 · 知识卡片

* **沙盒（Sandbox）** ｜ 📌 一句话大白话翻译：Chrome的“安全隔离舱”，把浏览器进程锁在笼子里，防止恶意代码祸害你的整个系统
* **Unprivileged User Namespaces** ｜ 📌 一句话大白话翻译：Linux给普通用户开的“特权小门”，Ubuntu 23.10+把这个门焊死了，Chrome傻眼了
* **SUID Sandbox** ｜ 📌 一句话大白话翻译：老式沙盒保镖，用SetUID机制给浏览器临时开挂，现在很多Linux发行版嫌弃它太危险，直接禁用
* **--no-sandbox参数** ｜ 📌 一句话大白话翻译：跟Chrome说“别装了，不用保镖”，在容器/虚拟机里必须喊这句话

---

## 🗺️ 一图流人肉拆解 · 丝滑流转路径

* 🟢 **第一步｜搞事情**：自动化脚本（比如Selenium/Playwright）试图启动Chrome Headless
* 🟡 **第二步｜过安检**：Chrome检查系统沙盒状态，发现Ubuntu 23.10+的AppArmor把unprivileged user namespaces禁用了
* 🟠 **第三步｜盖章确认**：Chrome举手投降，甩出"No usable sandbox!"报错，进程原地爆炸（exit code: unknown）
* 🔴 **最终状态**：自动化流水线卡死，CI/CD红一片，只能对着屏幕发呆

---

## ✍️ 搞钱/搞事新灵感 · 深度输出

### 📄 正在憋的大招/爆款草稿：
* **暂定 Title**：《自动化脚本在服务器上疯狂报错？99%的人踩了这个坑！》
* **核心内容剧透**：
  * **痛点**：以前大家在Ubuntu 23.10+服务器跑Selenium/Playwright，代码写得美滋滋，一跑起来就"No usable sandbox"，对着错误日志瞪眼3小时
  * **解法**：其实只要给Chrome加上`--no-sandbox --disable-dev-shm-usage`这两个启动参数，或者老老实实配置Docker容器权限，就能闭眼起飞！

---

## 🛠️ 避坑指南 · Handbook 纠错本

* ⚠️ **吐槽/优化点**：Chromium官方文档的报错信息太硬核了，"No usable sandbox!"后面跟一堆链接，Linux小白根本看不懂
* 🔄 **我的更正版**：下次遇到这个报错，先别慌，直接在chrome_options里加这两行：`options.add_argument('--no-sandbox')` 和 `options.add_argument('--disable-dev-shm-usage')`，已加入我的个人知识库，屡试不爽！

#笔记灵感 #搞钱思路 #独立开发 #AI设计 #干货分享 #程序员的日常
<!-- DAILY_CHECKIN_2026-05-21_END -->
<!-- Content_END -->
