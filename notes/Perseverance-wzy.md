---
timezone: UTC+8
---

# Perseverance-wzy

**GitHub ID:** Perseverance-wzy

**Telegram:** 

## Self-introduction

AI x Web3 School

## Notes

<!-- Content_START -->
# 2026-05-19
<!-- DAILY_CHECKIN_2026-05-19_START -->
# 以太坊账户（Accounts）笔记

## 一、账户概述

-   以太坊账户：拥有 ETH 余额、可在链上发送消息的实体。
    
-   两类账户：**外部账户（EOA）**、**合约账户**。
    
-   共同点：均可收发 ETH / 代币、与智能合约交互。
    

* * *

## 二、两类账户对比

### 1\. 外部账户（EOA，用户账户）

-   由**私钥**控制，无需部署成本，免费创建。
    
-   可**主动发起交易**（转账、调用合约）。
    
-   交易：EOA ↔ EOA 只能是 ETH / 代币转账。
    
-   组成：**公钥 + 私钥**加密对。
    

### 2\. 合约账户（智能合约）

-   由**代码逻辑**控制，**无私钥**。
    
-   创建需要 Gas（占用链上存储）。
    
-   只能**被动响应交易**（收到消息后执行代码）。
    
-   可执行复杂逻辑：转账、发代币、创建新合约等。
    

* * *

## 三、账户的四个核心字段

1.  **nonce**：
    
    -   EOA：已发送交易计数；
        
    -   合约：已创建合约计数；
        
    -   防重放攻击：同一 nonce 仅执行一次。
        
2.  **balance**：账户余额，单位 **wei**（1 ETH = 10¹⁸ wei）。
    
3.  **codeHash**：
    
    -   EOA：空字符串哈希；
        
    -   合约：EVM 代码哈希（不可修改）。
        
4.  **storageRoot**：
    
    -   账户存储的默克尔 Patricia 树根哈希；
        
    -   合约状态数据存在这里，EOA 默认为空。
        

* * *

## 四、外部账户与密钥对

-   **私钥**：64 位十六进制字符串，账户控制权核心，**必须保密**。
    
-   **公钥**：由私钥通过椭圆曲线算法生成。
    
-   **地址**：公钥 Keccak-256 哈希后取**最后 20 字节**，前缀 `0x`，共 42 字符。
    
-   逻辑：私钥 → 签名交易 → 网络验证公钥 → 确认交易合法。
    

* * *

## 五、账户创建

1.  **EOA**：随机生成私钥 → 推导公钥 → 生成地址；常用工具：Geth/Clef、钱包（MetaMask）、web3 库。
    
2.  **合约地址**：由**创建者地址 + nonce** 计算生成，部署时确定。
    

* * *

## 六、验证者密钥（PoS）

-   以太坊升级为权益证明（PoS）后引入 **BLS 密钥**。
    
-   用于标识验证者，支持密钥聚合，降低共识带宽和最低质押门槛。
<!-- DAILY_CHECKIN_2026-05-19_END -->

# 2026-05-18
<!-- DAILY_CHECKIN_2026-05-18_START -->

## 一、前期准备

1.  电脑开启**CPU虚拟化**（任务管理器-性能-CPU查看已启用）
    
2.  D盘新建文件夹：`D:\\\\WSL`
    
3.  关闭电脑360/管家，避免拦截权限
    

* * *

# 第一步：管理员PowerShell开启WSL2功能

1.  右键开始菜单 → **Windows终端(管理员)** / PowerShell管理员
    
2.  依次执行两行命令
    

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

1.  **立刻重启电脑**（不重启必报错）
    

## 第二步：安装WSL2内核+设定默认WSL2

1.  浏览器搜索下载：`wsl_update_x64.msi` 微软官方内核包，双击安装
    
2.  管理员PowerShell执行
    

```powershell
wsl --set-default-version 2
```

## 第三步：手动把Ubuntu22.04安装到D盘（核心！不占C盘）

1.  先在D盘建好文件夹
    

```powershell
mkdir D:\\\\WSL\\\\Ubuntu
```

1.  下载Ubuntu22.04镜像到D盘
    

```powershell
curl -L -o D:\\\\WSL\\\\ubuntu-22.04-root.tar.xz <https://cloud-images.ubuntu.com/jammy/current/jammy-server-cloudimg-amd64-wsl.rootfs.tar.gz>
```

1.  导入系统至D盘（最重要）
    

```powershell
wsl --import Ubuntu D:\\\\WSL\\\\Ubuntu D:\\\\WSL\\\\ubuntu-22.04-root.tar.xz
```

1.  查看是否安装成功
    

```powershell
wsl -l -v
```

**显示Ubuntu 版本2 即为成功**

## 第四步：进入WSL创建日常普通用户

1.  进入刚装好的Ubuntu
    

```powershell
wsl -d Ubuntu
```

1.  WSL内执行创建用户（用户名自定义，我用xiaobai）
    

```bash
NEW_USER=xiaobai
useradd -m -s /bin/bash $NEW_USER
passwd $NEW_USER
usermod -aG sudo $NEW_USER
```

1.  设置开机默认登录这个用户
    

```bash
cat > /etc/wsl.conf << EOF
[user]
default=$NEW_USER
EOF
```

1.  输入 `exit` 退出，重新进WSL就是普通用户
    

* * *

# 第二步：WSL内部全网国内加速（必做）

## 1\. 替换Ubuntu阿里软件源

```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
sudo sed -i 's|archive.ubuntu.com|mirrors.aliyun.com|g' /etc/apt/sources.list
sudo sed -i 's|security.ubuntu.com|mirrors.aliyun.com|g' /etc/apt/sources.list
sudo apt update && sudo apt upgrade -y
```

## 2\. 安装Git并配置

```bash
sudo apt install -y git
git config --global user.name "xiaobai"
git config --global user.email "xiaobai@qq.com"
```

* * *

# 第三步：国内镜像加速安装 Hermes Agent

## 1\. 加速一键安装命令（解决GitHub超时）

用**ghproxy镜像代理**执行官方安装脚本

```bash
curl -fsSL <https://mirror.ghproxy.com/https://raw.githubusercontent.com/NousResearch/HermesAgent/main/install.sh> | bash
```

等待自动安装：uv、Python、Node、Playwright全套依赖 **Playwright下载浏览器慢是正常现象，千万别终止！**

## 2\. 刷新环境变量识别hermes命令

```bash
source ~/.bashrc
```

## 3\. 验证安装成功

```bash
hermes --version
```

提示命令不存在就用完整路径：

```bash
~/.local/bin/hermes --version
```

* * *

# 第四步：对接大模型API配置（必须配置才能用）

Hermes无本地模型，只对接线上API

## 方式1：交互式快速配置

```bash
hermes setup
```

依次填写：

1.  选择模型厂商
    
2.  粘贴你的API Key
    
3.  填写代理接口BaseURL
    
4.  填写调用模型名称 回车确认完成
    

## 方式2：手动修改配置文件

```bash
nano ~/.hermes/config.yaml
```

写入格式

```yaml
model:
  default: 模型名
  provider: 厂商名
  base_url: 你的API接口地址
```

保存：Ctrl+O 回车，Ctrl+X退出

* * *

# 第五步：省Token省钱优化（新手必开）

进入Hermes对话界面后直接输入

1.  关闭多Agent并行（最耗Token）
    

```
/config delegation.orchestrator_enabled false
```

1.  减少对话轮数
    

```
/config agent.max_turns 30
```

1.  随时切换轻量模型
    

```
/model 轻量模型名称
```

* * *

# 第六步：日常启动使用

## 启动命令

```bash
hermes
# 或
~/.local/bin/hermes
```

## 常用内置命令

-   `/help` 查看全部功能
    
-   `/model 模型名` 快速切模型
    
-   `/config 参数 值` 修改配置
    

## 已解锁全部Hermes核心能力

1.  四层长效记忆系统
    
2.  AI自动生成实用技能
    
3.  多平台机器人网关
    
4.  任务并行处理
    
5.  本地语音输入Whisper
<!-- DAILY_CHECKIN_2026-05-18_END -->
<!-- Content_END -->
