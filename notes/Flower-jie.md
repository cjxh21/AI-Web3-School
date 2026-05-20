---
timezone: UTC+8
---

# Flower-jie

**GitHub ID:** Flower-jie

**Telegram:** @flower

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-20
<!-- DAILY_CHECKIN_2026-05-20_START -->
# **第三天学习笔记（进阶扩展）**

**日期：2026年5月20日**

* * *

## **一、大语言模型：检索增强生成（RAG）与智能体（Agent）**

### **1\. 检索增强生成（RAG）**

-   **背景**：LLM 的训练数据有截止时间，且无法访问私有知识库。RAG 解决“知识截止”和“幻觉”问题。
    
-   **工作流程**：
    
    1.  用户提问。
        
    2.  将问题向量化（embedding）。
        
    3.  在向量数据库中检索相关文档（知识库）。
        
    4.  将检索到的文档与原始问题一起拼接到提示中。
        
    5.  LLM 基于“问题 + 检索到的上下文”生成答案。
        
-   **优点**：
    
    -   可引用最新或私有信息。
        
    -   减少模型编造答案（幻觉）。
        
    -   方便更新知识库（无需重新训练模型）。
        
-   **典型技术栈**：LangChain、LlamaIndex、Chroma/Pinecone、OpenAI Embeddings。
    

### **2\. 智能体（Agent）**

-   **概念**：LLM 作为“大脑”，不仅能聊天，还能**自主决策、调用工具、执行多步任务**。
    
-   **核心组件**：
    
    -   **推理引擎**：LLM 分析目标，分解步骤。
        
    -   **工具集**：API、代码执行器、搜索引擎、数据库等。
        
    -   **记忆**：短期（对话历史）和长期（向量数据库）。
        
-   **工作流程（ReAct 模式）**：  
    **思考 → 行动 → 观察** 循环。
    
-   **示例**：用户问“巴黎今天天气如何？帮我订一个室内活动”。Agent 会：
    
    1.  调用天气 API 获取天气。
        
    2.  根据天气推荐室内活动。
        
    3.  调用预订 API。
        
-   **框架**：LangChain Agents、AutoGPT、BabyAGI、Semantic Kernel。
    

* * *

## **二、OpenAI API 高级：多模态与音频流**

### **1\. 多模态模型：GPT-4 with Vision**

-   **能力**：接受**图像**输入，理解图像内容并回答相关问题。
    
-   **API 调用**：
    
    python
    
    ```
    response = client.chat.completions.create(
        model="gpt-4-vision-preview",
        messages=[
            {
                "role": "user",
                "content": [
                    {"type": "text", "text": "图中有什么？"},
                    {"type": "image_url", "image_url": {"url": "https://example.com/pic.jpg"}}
                ]
            }
        ]
    )
    ```
    
-   **限制**：不支持物体定位或精确图像编辑；费用高于纯文本模型。
    

### **2\. 音频生成（Text-to-Speech，TTS）**

-   **端点**：`/audio/speech`
    
-   **功能**：将文本转为自然语音，支持多种声音（alloy、echo、fable、onyx、nova、shimmer）。
    
-   **示例**：
    
    python
    
    ```
    from openai import OpenAI
    client = OpenAI()
    response = client.audio.speech.create(
        model="tts-1",
        voice="nova",
        input="你好，这是第三天学习笔记。"
    )
    response.stream_to_file("output.mp3")
    ```
    
-   **应用**：有声内容、语音助手、无障碍体验。
    

### **3\. 可解释性与结构化输出增强**

-   **JSON 模式更严格**：使用 `response_format={"type": "json_object"}` 结合提示保证输出合法 JSON。
    
-   **函数调用自动并行**：模型可一次性调用多个函数，在复杂任务中减少往返次数。
    

* * *

## **三、以太坊：Layer 2、跨链与账户抽象**

### **1\. Layer 2 扩容方案**

-   **为什么需要 L2**：以太坊主网拥堵、Gas 高。
    
-   **常见 L2 类型**：
    
    -   **乐观 Rollup**（Optimism、Arbitrum）：假设交易有效，提供挑战期；费用低，兼容性好。
        
    -   **零知识 Rollup**（zkSync、Starknet）：使用有效性证明，安全性高，提现快。
        
    -   **状态通道**（如闪电网络的思想）：适合高频小额支付。
        
-   **用户体验**：用户将资产桥接到 L2，交易费降低 10-100 倍。
    

### **2\. 跨链互操作性**

-   **桥（Bridge）**：锁定源链资产，在目标链铸造包裹资产（如 WETH）。
    
-   **主要桥协议**：Hop、Across、Stargate（基于 LayerZero）。
    
-   **风险**：桥漏洞是主要安全事件来源（如 Ronin 桥被盗）。建议使用经过审计、大额锁仓的桥。
    

### **3\. 账户抽象（EIP-4337）**

-   **目标**：让合约账户拥有外部账户的能力，摆脱硬编码私钥的限制。
    
-   **实现方式**：引入 **UserOperation** 交易类型，用户通过“入口点合约”提交。
    
-   **好处**：
    
    -   社交恢复（使用多个守护者找回账户）。
        
    -   批量交易（一次签名执行多个操作）。
        
    -   赞助交易（第三方支付 gas）。
        
    -   无 gas 代付（用户可用 ERC-20 支付）。
        
-   **现状**：已上线以太坊主网，钱包如 Safe（原 Gnosis Safe）开始支持。
    

### **4\. 去中心化身份（DID）与 ENS**

-   **ENS（Ethereum Name Service）**：将 `xxx.eth` 域名映射到地址，也可存储头像、邮箱等。
    
-   **使用**：通过 `ethers.js` 解析 `name` 或 `address`。
    
-   **去中心化身份**：将身份信息（凭证、认证）上链，由用户自己控制。
<!-- DAILY_CHECKIN_2026-05-20_END -->

# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->

# **第二天学习笔记（扩展篇）**

**日期：2026年5月19日**

* * *

## **一、大语言模型进阶：评估与微调**

### **1\. 模型评估**

-   **困惑度（Perplexity）**：衡量模型对测试集预测的“惊讶程度”，越低越好。
    
-   **任务特定指标**：
    
    -   分类任务：准确率、F1 分数
        
    -   生成任务：BLEU（机器翻译）、ROUGE（摘要）、BERTScore
        
-   **人工评估**：流畅度、相关性、无害性（尤其对于对话系统）。
    

### **2\. 微调（Fine-tuning）**

-   **概念**：在预训练模型基础上，用特定领域的小规模标注数据继续训练，使模型适配特定任务。
    
-   **与提示工程的区别**：
    
    -   提示工程：不改变模型参数，通过输入设计引导输出。
        
    -   微调：改变模型参数，永久学习新知识或风格。
        
-   **典型流程**：
    
    1.  准备带标注的数据集（如“问题-答案”对）。
        
    2.  调用 OpenAI 微调 API 或使用开源框架（如 Hugging Face PEFT、LoRA）。
        
    3.  上传数据，启动微调作业，获得专属模型。
        
-   **成本与收益**：微调需要额外计算资源和数据准备，但能显著提升特定任务的准确率。
    

### **3\. 参数高效微调（PEFT）**

-   **LoRA（Low-Rank Adaptation）**：只更新原模型参数的极小子集（低秩矩阵），大幅降低显存需求。
    
-   **QLoRA**：结合量化（4-bit）与 LoRA，可在单张消费级 GPU 上微调数十亿参数模型。
    

### **4\. 模型量化**

-   将模型权重从 32 位浮点数压缩为 8 位或 4 位整数。
    
-   作用：减少显存占用、加快推理速度，但可能轻微损失精度。
    
-   常见方法：GPTQ、AWQ、GGUF（用于 llama.cpp）。
    

* * *

## **二、OpenAI API 高级用法与系统集成**

### **1\. 流式输出（Streaming）**

-   普通调用：模型生成完整回复后一次性返回。
    
-   流式调用：设置 `stream=True`，逐步返回 token，提升用户体验（像 ChatGPT 打字效果）。
    
-   示例：
    
    python
    
    ```
    response = client.chat.completions.create(
        model="gpt-4",
        messages=[{"role": "user", "content": "写一首诗"}],
        stream=True
    )
    for chunk in response:
        if chunk.choices[0].delta.content:
            print(chunk.choices[0].delta.content, end="")
    ```
    

### **2\. 异步调用（Async）**

-   适用于高并发场景（如同时处理多个用户请求）。
    
-   使用 `async` 和 `await` + OpenAI 异步客户端。
    
-   示例：
    
    python
    
    ```
    import asyncio
    from openai import AsyncOpenAI
    
    async def get_response():
        client = AsyncOpenAI(api_key="...")
        response = await client.chat.completions.create(...)
        return response
    
    asyncio.run(get_response())
    ```
    

### **3\. 批量处理与成本优化**

-   **批处理 API**（OpenAI Batch API）：将多个请求打包一次性提交，价格折扣 50%，但结果异步返回（通常 24 小时内）。
    
-   **缓存语义相同请求**：对于 FAQ 等重复查询，使用嵌入相似度缓存结果，减少 API 调用。
    

### **4\. 安全与合规**

-   **内容过滤级别**：通过 `moderation` 端点或设置 `max_tokens` 限制风险输出。
    
-   **数据保留**：OpenAI API 默认不存储请求数据，但企业可签订数据保护协议。
    
-   **API Key 轮换**：定期生成新密钥，并使用密钥管理服务（如 AWS KMS、Vault）。
    

* * *

## **三、以太坊进阶：智能合约开发基础**

### **1\. 智能合约是什么**

-   存储在以太坊上的**不可更改的程序**，在满足条件时自动执行预设逻辑。
    
-   常用语言：**Solidity**（语法类似 JavaScript）。
    

### **2\. 一个简单的 Solidity 合约示例**

solidity

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleStorage {
    uint256 public storedData;

    function set(uint256 x) public {
        storedData = x;
    }

    function get() public view returns (uint256) {
        return storedData;
    }
}
```

### **3\. 部署与交互**

-   **开发环境**：Remix IDE（浏览器）、Hardhat、Foundry。
    
-   **部署工具**：使用 `ethers.js` 或 `web3.js` 调用合约。
    
-   **Gas 费用**：每执行一次合约操作（写入）需支付 ETH 作为燃料。
    

### **4\. 代币标准**

-   **ERC-20**：同质化代币（如 USDC、DAI）。
    
-   **ERC-721**：非同质化代币（NFT）。
    
-   **ERC-1155**：混合标准（可包含同质化与非同质化）。
    

### **5\. 账户与合约交互的风险**

-   **重入攻击**：合约在更新状态前再次调用自身（可通过检查-生效-交互模式或互斥锁防范）。
    
-   **整数溢出**：使用 SafeMath 库或 Solidity 8+ 内置检查。
    
-   **Gas 限制**：无限循环或复杂计算可能导致交易失败。
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->



# **今日学习笔记汇总**

**日期：2026年5月18日**

* * *

## **一、大语言模型（LLM）的工作原理**

### **1\. 核心机制**

-   LLM 是一个复杂的数学函数，根据输入文本**预测下一个词的概率分布**。
    
-   通过反复执行“输入已有文本 → 预测下一个词 → 追加到文本”的过程，自动生成完整回复。
    
-   模型本身是确定性的，但为了让输出更自然，会**随机选择概率稍低的词**，因此每次回答可能不同。
    

### **2\. 训练方式（预训练）**

-   从互联网抓取海量文本（例如 GPT-3 的训练文本，一个人 24/7 不间断阅读需要 **2600 多年**）。
    
-   模型内部有数百亿个**参数（权重）**，初始随机 → 输出乱码。
    
-   通过**反向传播算法**，根据真实文本不断微调参数，使预测越来越准。
    

### **3\. 计算规模**

-   训练最大的 LLM，即使每秒执行 10 亿次加法/乘法，也需要 **超过 1 亿年**。
    
-   必须依赖 **GPU** 进行大规模并行计算。
    

### **4\. Transformer 架构（2017 年提出）**

-   **关键创新**：不逐词顺序阅读，而是**并行处理整个文本**。
    
-   **注意力机制（Attention）**：让每个词的数值向量根据上下文相互“交流”（例如区分 river bank 和 bank account）。
    
-   配合**前馈神经网络**，存储更多语言模式。
    

### **5\. 与人类对齐（RLHF）**

-   预训练只是补全互联网文本，不保证成为好助手。
    
-   使用**基于人类反馈的强化学习（RLHF）**：人工标注错误回答，进一步微调模型，使其更符合用户偏好。
    

### **6\. 局限性**

-   模型行为是数百亿参数**涌现**的结果，难以精确解释某个预测的原因。
    

* * *

## **二、OpenAI API 与实用 AI 开发课程**

### **（一）OpenAI API 基础**

-   **API**：应用程序编程接口，像“餐厅服务员”传递请求并返回结果。
    
-   **OpenAI API**：以编程方式调用 GPT、Whisper 等模型，不限于 ChatGPT。
    
-   **主要端点**：
    
    -   `/chat/completions` – 聊天补全
        
    -   `/embeddings` – 生成文本向量
        
    -   `/moderations` – 内容审核
        
    -   `/audio/transcriptions` & `/audio/translations` – 语音转文字 / 翻译
        
-   **认证与费用**：使用 API Key，费用基于模型和 token 数量。
    

### **（二）聊天补全详解**

-   **消息角色**：
    
    -   `system`：设定助手行为（如“你是友好客服”）
        
    -   `user`：用户输入
        
    -   `assistant`：模型回复
        
-   **温度（temperature）**：0（确定）~ 2（随机）
    
-   **最大令牌数（max\_tokens）**：限制回复长度
    

### **（三）函数调用（Function Calling）**

-   让模型输出**结构化的 JSON**，便于与外部系统集成。
    
-   应用：从非结构化文本提取字段、并行调用多个函数、调用外部 API（如博物馆推荐）。
    

### **（四）嵌入（Embeddings）与向量数据库**

-   **嵌入**：将文本映射为 1536 维向量，语义相似的文本在向量空间中距离更近。
    
-   **应用**：
    
    -   语义搜索（搜索“电脑”返回“新技术产品”文章）
        
    -   推荐系统（根据用户历史取向量均值推荐）
        
    -   零样本分类（与类别描述向量比较距离）
        
-   **向量数据库（以 Chroma 为例）**：
    
    -   高效存储和查询大规模向量。
        
    -   支持元数据过滤（如只查“电影”类型、2020 年后上映）。
        
    -   自动嵌入，支持增删改查。
        

### **（五）提示工程核心技巧**

1.  **使用明确的动作动词**（写、总结、分类），避免模糊词（理解、思考）。
    
2.  **提供详细指令**（长度、格式、风格、受众）。
    
3.  **使用分隔符**（如三重反引号 \`\`\`）区分指令与输入。
    
4.  **少样本提示（Few-shot）**：给出示例让模型学习输出格式。
    
5.  **思维链（Chain-of-Thought）**：要求展示推理步骤，提高复杂问题准确率。
    
6.  **多步提示（Multi-step）**：分解任务（如先改错别字，再改语气）。
    
7.  **迭代优化**：根据输出反复修改提示。
    

### **（六）生产环境最佳实践**

1.  **错误处理**：try/except 捕获认证错误、速率限制；使用 `tenacity` 库指数退避重试。
    
2.  **速率限制**：控制请求频率，批处理输入，减少 token 数。
    
3.  **内容审核**：moderation 端点检测暴力、仇恨等内容，可自定义阈值。
    
4.  **对抗性测试**：用刁钻输入（讽刺、反转情绪）测试鲁棒性。
    
5.  **安全建议**：
    
    1.  API Key 存在环境变量，不提交到仓库。
        
    2.  使用用户 ID 标记请求，便于审计。
        

### 设置“护栏”（guardrails）限制模型回答领域。
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
