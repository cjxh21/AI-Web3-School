---
timezone: UTC+8
---

# yichen-bear

**GitHub ID:** yichen-bear

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-21
<!-- DAILY_CHECKIN_2026-05-21_START -->
**「Transformers 能做什麼？ (Transformers, what can they do?)」**。

它主要介紹了 Hugging Face 的核心工具 `pipeline()` 函數，並展示如何用它來輕鬆操作各種自然語言處理（NLP）、語音、以及電腦視覺（CV）的任務。

以下為該頁面的核心重點整理：

### 1\. `pipeline()` 的核心概念與運作流程

`pipeline()` 是 Hugging Face `transformers` 庫中最頂層、最易用的 API。當你把一段文字丟給 `pipeline` 時，它在背後其實自動執行了**三個主要步驟**：

1.  **預處理 (Preprocessing)**：將人類看得懂的文字，轉換成模型能理解的格式（Token）。
    
2.  **模型預測 (Model Pass)**：將預處理後的輸入傳給模型進行計算。
    
3.  **後處理 (Post-processing)**：將模型輸出的數字（Predictions）轉換成人類看得懂的結果。
    

### 2\. 經典的 NLP 任務範例

網頁中介紹了幾種最常見的文字處理 pipeline 應用：

-   **情感分析 (Sentiment Analysis)**：
    
    -   **功能**：判斷一段文字是正面的還是負面的。
        
    -   _範例_：輸入 "I've been waiting for a HuggingFace course my whole life." $\\rightarrow$ 輸出 `POSITIVE` (信心度 99.9%)。
        
-   **零樣本分類 (Zero-shot Classification)**：
    
    -   **功能**：對**未標籤**的文字進行分類。你可以自行決定任何想分類的標籤（Labels），模型不需要重新訓練就能直接分類。
        
    -   _應用場景_：現實中缺乏標籤數據、需要靈活分類時。
        
-   **文字生成 (Text Generation)**：
    
    -   **功能**：給予一段初始提示（Prompt），讓模型自動續寫接下來的句子。
        
-   **遮罩填空 (Fill-Mask)**：
    
    -   **功能**：給予一個帶有 `<mask>`（遮罩）的句子，讓模型預測被蓋住的字詞是什麼。
        
-   **命名實體識別 (NER - Named Entity Recognition)**：
    
    -   **功能**：找出文本中的實體，並將其分類。例如區分出哪些字是「人名（PER）」、「組織名（ORG）」或「地點（LOC）」。
        
-   **問答系統 (Question Answering)**：
    
    -   **功能**：給予一段「上下文（Context）」與一個「問題」，模型會直接從上下文中抽取出正確答案。
        
-   **文本摘要 (Summarization)**：
    
    -   **功能**：將長篇文章縮短，同時保留核心重點。
        
-   **機器翻譯 (Translation)**：
    
    -   **功能**：將一種語言轉換成另一種語言（如法文轉英文）。
        

### 3\. 多模態（跨領域）的應用擴展

除了文字（NLP）之外，`pipeline()` 也能應用在語音和影像上：

-   **影像 Pipeline (Image pipelines)**：
    
    -   `image-to-text`：看圖說故事（產生影像的文字描述）。
        
    -   `image-classification`：影像分類（辨識圖中物體是什麼）。
        
    -   `object-detection`：物件偵測（在圖像中定位並標出物體位置）。
        
-   **語音 Pipeline (Audio pipelines)**：
    
    -   `automatic-speech-recognition`：自動語音辨識（語音轉文字）。
        
    -   `audio-classification`：語音分類。
        
    -   `text-to-speech`：文字轉語音（讓電腦說話）。
        

### 💡 總結

這一節的重點在於讓學習者明白：**你不需要知道模型背後複雜的數學與架構，只要呼叫** `pipeline()` **並指定任務名稱，就能直接將當前最頂尖的 AI 模型應用在文字、語音與影像處理上。**
<!-- DAILY_CHECKIN_2026-05-21_END -->

# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->

### What is a Large Language Model? 影片觀看

LLM是模型判斷下一個生成的文字是甚麼，藉由大量的文章資料訓練調整超級多的參數，讓下一個生成的文字越來越順暢合理
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->


因為我是AI和Web3兩者的初學者，所以我今天先了解模塊A的核心知識點

### 一、 大模型基礎與控制參數

-   **Token**：大模型處理文字的基本單位，大約一個英文單字或一個中文字。
    
-   **MaaS (Model as a Service)**：模型即服務。指開發者不需要自己購買硬體，直接透過 API 密鑰，按照使用的 Token 數量付費調用雲端模型。
    
-   **Context Window (上下文窗口)**：模型單次對話能容納的最高訊息量，可以理解為模型的短期工作記憶體。
    
-   **System Instruction (系統指令)**：在對話開始前幫模型設定的根本規則，用於定義模型的角色、語氣和行為邊界，優先級高於一般提示詞。
    
-   **Temperature (溫度)**：控制模型輸出隨機性的參數。設定越接近 0，回答越精準嚴謹；設定越接近 1，回答越具創意與隨機性。
    

* * *

### 二、 開發模式的三個演進階段

-   **Prompt (提示詞)**：最基礎的一問一答模式。模型被動回應，下一步的決策完全由人類主導。
    
-   **Workflow (工作流)**：將任務拆解為固定步驟的自動化流程。路徑是提前寫死的，大模型在其中只負責特定節點的處理。
    
-   **Agent (智能體)**：人類只給定最終目標，由大模型自己思考、規劃步驟，並根據中間結果動態決定要調用哪些工具。
    

* * *

### 三、 Agent 核心技術組件

-   **State (狀態管理)**：在複雜的長流程中，用來紀錄當前進度與資料的共享資料結構，讓不同的執行節點可以讀寫同一個狀態。
    
-   **Tool Calling (工具調用)**：模型將自己的意圖轉化為結構化的數據格式（通常是 JSON），讓外部程式能夠幫它執行查資料、發送郵件等具體動作。
    
-   **MCP (Model Context Protocol)**：大模型上下文協議。一種讓大模型與外部工具、資料源進行標準化連接的統一協議。
    
-   **Skills (技能集)**：將高層次的指令或常用動作打包成可複用的模組，讓 Agent 能夠動態發現並重複使用。
    
-   **Tracing (鏈路追蹤)**：紀錄 Agent 每一步思考與執行細節的日誌系統，主要用於開發時的排錯與行為視覺化。
    
-   **Guardrails (護欄)**：在輸入和輸出端設置的硬性檢查規則，只要發現不合規的內容或越權行為就會強制中斷。
    
-   **Handoff (控制權移交)**：在多 Agent 系統中，當一個子任務完成或超出能力範圍時，將主導權移交給另一個 Agent 的機制。
    

* * *

### 四、 風險與防範機制

-   **Hallucination (幻覺)**：模型以極其自信的語氣編造出錯誤的事實、不存在的論文或網址連結。
    
-   **Reasoning Drift (推理漂移)**：在長文本或多輪對話中，模型後期的邏輯鏈條斷裂，導致最終結論偏離了一開始的前提。
    
-   **Human-in-the-loop (人工介入)**：在高風險或合規要求高的操作節點（如涉及資金、敏感數據變更），強制加入人類審核的卡點。
    

* * *

核心的評估準則可以總結為：流程固定、合規要求高的場景優先使用傳統腳本或 Workflow；目標開放、需要走一步看一步的複雜場景才考慮 Agent。
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
