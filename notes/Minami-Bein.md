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
# 🔧 技术问题修复 + 📝 学习笔记模板

## 一、先解决你的 Chrome 报错

你的错误是典型的 **容器/虚拟机沙盒权限问题**。直接加 `--no-sandbox` 参数：

```python
# Playwright 示例
browser = playwright.chromium.launch(
    args=['--no-sandbox', '--disable-setuid-sandbox']
)

# Selenium 示例
options.add_argument('--no-sandbox')
options.add_argument('--disable-dev-shm-usage')  # 防止共享内存问题
```

---

## 二、✨ 今日学习笔记模板（已帮你填好示例框架）

---

# 🏷️ [行动代号/第1天]｜Chrome 自动化抓包从入门到跑路

## 💡 今日硬核充能 · 知识卡片

* **[无头浏览器(Headless)]** ｜ 📌 一句话大白话翻译：看不见的 Chrome，没有图形界面但能执行所有 JS
* **[沙盒(Sandbox)]** ｜ 📌 一句话大白话翻译：Chrome 的保镖，把网页代码关在笼子里运行，防止搞破坏

---

## 🗺️ 一图流人肉拆解 · 丝滑流转路径

* 🟢 **第一步｜搞事情**：[Playwright] 发起了 [访问网页请求]
* 🟡 **第二步｜过安检**：[Chrome 检测沙盒环境] 进行了 [安全验证]
* 🟠 **第三步｜盖章确认**：如果沙盒不可用 → 报错退出
* 🔴 **最终状态**：进程崩溃，报 "No usable sandbox!"

---

## ✍️ 搞钱/搞事新灵感 · 深度输出

### 📄 正在憋的大招/爆款草稿：
* **暂定 Title**：《浏览器自动化踩坑实录：为什么 Chrome 死活不肯启动》
* **核心内容剧透**：
  * **痛点**：在 Docker/Ubuntu 23.10+ 跑爬虫/测试，Chrome 动不动就罢工
  * **解法**：加 `--no-sandbox` 三连，让 Chrome 在 CI 服务器上乖乖干活！

---

## 🛠️ 避坑指南 · Handbook 纠错本

* ⚠️ **吐槽/优化点**：Chrome 报错信息全是英文术语，小白根本看不懂！
* 🔄 **我的更正版**：记住这句咒语 → `--no-sandbox --disable-setuid-sandbox --disable-dev-shm-usage`，已加入我的个人知识库。

---

## 💡 今日代码实战

```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(
        headless=True,
        args=[
            '--no-sandbox',                      # 关闭沙盒
            '--disable-setuid-sandbox',         # 禁用 setuid 沙盒
            '--disable-dev-shm-usage',           # 避免共享内存问题
        ]
    )
    page = browser.new_page()
    page.goto("https://example.com")
    print(page.title())
```

---

需要我帮你把某个具体技术点深挖成这种格式吗？ 🎯
<!-- DAILY_CHECKIN_2026-05-21_END -->
<!-- Content_END -->
