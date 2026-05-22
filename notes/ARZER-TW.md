---
timezone: UTC+8
---

# james_1022

**GitHub ID:** ARZER-TW

**Telegram:** @Lain_1022

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-22
<!-- DAILY_CHECKIN_2026-05-22_START -->
學習了**Hermes Agent** 的入門概述  
  

## 核心定位

Hermes 是一個**自我改進的 AI Agent**。它與傳統無狀態 Agent 框架最大的差異在於：**閉合了學習循環**。傳統 Agent 執行完任務就遺忘，而 Hermes 會觀察自身表現、把可複用流程提取成技能、持久化知識，並隨時間加深對使用者的理解。它可運行在任何模型（透過 OpenRouter、NVIDIA NIM 等 25+ 提供商），並存在於 CLI、Telegram、Discord、Slack、WhatsApp、Signal 等任何平台。

## 關鍵特性

主打的 **40+ 內建工具**（終端、瀏覽器、檔案、網頁搜尋、圖像生成、任務委派）、**持久記憶**（多提供商記憶系統 + FTS5 跨會話搜尋）、**多平台網關**（單一進程服務 10+ 平台）、**7 種終端後端**（Local、Docker、SSH、Modal 等含無伺服器持久化方案）、**子 Agent 委派**、**Cron 排程**、**插件系統**與 **MCP 整合**。

## 自我改進循環（最關鍵的架構）

這套循環跨三個時間維度運作：

-   **會話內**：處理複雜任務時提取流程存成技能（`~/.hermes/skills/` 帶 YAML frontmatter 的 Markdown），立即注入系統提示詞讓 Agent 變聰明。
    
-   **跨會話**：記憶管理器在輪次前預取、輪次後同步；用 SQLite FTS5 搜尋過往對話；`USER.md` 持續累積使用者偏好。
    
-   **後台**：Agent 閒置超過閾值（預設 2 小時）且距上次整理超過一週時，**整理器（curator）** 會 fork 一個 AIAgent 來審查技能——可置頂、歸檔、整合，但**絕不自動刪除**（歸檔可復原），且使用輔助 client 以避免干擾主會話的提示詞快取。
    

## 值得注意的工程設計

**三層系統提示詞**（為了提示詞快取最佳化）：

-   **穩定層**：身份（SOUL.md）、工具指導、技能提示——每會話建一次，維持位元組級一致以保持快取熱度
    
-   **上下文層**：呼叫方的 system\_message + 工作目錄下的上下文檔（AGENTS.md 等）
    
-   **易變層**：記憶快照、USER.md、時間戳等——每輪重建、不快取
    

另外，**工具註冊與暴露是刻意分離的**：工具透過 `registry.register()` 自動發現，但只有出現在 `toolsets.py` 工具集中的工具才會真正暴露給 Agent。對話循環本身是**完全同步**的 while 迴圈，而自我改進機制（記憶同步、技能提取、整理器）都是**輪次後的鉤子**，絕不阻塞主迴圈。

## 安裝

Linux/macOS/WSL2 一行指令即可：

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

* * *

整體來看，Hermes 的賣點不是工具數量，而是那套**無人干預的閉合學習循環**——技能會被自動提取、改進、後台整理，配合持久記憶與可插拔上下文引擎，理論上越用越好。
<!-- DAILY_CHECKIN_2026-05-22_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->

打卡，基本上把第一週的內容都看完了。都是些較為基礎的內容。把任務一跟任務二完成了。
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->


打卡，今天是共學第一天，差點忘記打卡，趕在截止時間前打個卡
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
