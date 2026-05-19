---
timezone: UTC+8
---

# Havensky-stack

**GitHub ID:** Havensky-stack

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->
**  
Hermes Agent配置全流程跟进以及答疑**

一、前置环境

1. 支持系统：Linux、MacOS、Windows WSL2

2. 必备依赖：git、curl、tmux（后台保活）

3. 模型选择：OpenRouter（新手）、Ollama（本地）、百炼（国内）

二、安装部署

1\. 一键安装

2\. 验证安装

默认安装目录： ~/.hermes/ 

三、初始化配置

1. 交互式初始化（推荐）

按需选择模型、填写API密钥、设置回复模式

2\. 配置常用命令

四、网关&多平台接入

\- 支持飞书、钉钉、Telegram等平台

\-  hermes skills config  可开关、精简技能，避免指令超限

五、服务运行

1. 前台调试： hermes start 

2. 后台稳定运行（tmux）

六、高频报错答疑

1. Ollama连接失败：执行  ollama serve  启动本地模型服务

2. 机器人不回复：检查网关状态、密钥有效性、回复模式配置

3. 面板打不开：放行9100端口，监听地址改为0.0.0.0

4. 配置不生效：修改配置后必须重启网关

5. Telegram指令超限：禁用多余技能后重启网关

七、核心运维命令

\- 技能管理： hermes skills config 

\- 日志查看： tail -f ~/.hermes/logs/ 

\- 配置校验： hermes config check 

\- 服务重启： hermes gateway restart
<!-- DAILY_CHECKIN_2026-05-19_END -->
<!-- Content_END -->
