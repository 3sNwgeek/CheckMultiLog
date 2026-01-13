# CheckMultiLog
多种web日志分析，支持IIS日志、Apache日志、 Nginx 日志、 Tomcat日志 、Jetty日志、通用json（常见字段）安全分析。

![食用实例](/demo.gif)

### 一、支持的日志格式
- IIS W3C
- NCSA（Apache / Nginx / Tomcat / Jetty）
- HAProxy
- AWS ALB/ELB
- 通用 JSON access log
- Unknown 未识别但包含 IP、时间、URI、User-Agent 信息的日志
- windows操作系统日志、Linux操作系统日志
> **说明**：免费版仅开放 **IIS W3C** 与 **NCSA(IIS)**；授权版解锁全部格式。

---

### 二、内置分析规则种类
- **WebShell 检测**：冰蝎、哥斯拉、Neo-reGeorg 等
- **漏洞利用**：Shiro、Log4Shell、Spring4Shell、ThinkPHP、PHPUnit
- **弱口令/敏感接口**：K8s API/Docker API 未授权、IndexOf 目录列举
- **数据外带**：大 Base64 参数、Token/Session 泄露、归档批量下载
- **扫描识别**：xray、fscan、sqlmap、WPScan、Nuclei
- **通用攻击**：SQLi、XSS、路径遍历、恶意上传绕过、命令执行
- **入侵溯源**：根据系统日志分析攻击者攻击操作
> 规则来自 `AttackRules.ini`，采用正则表达式匹配 URL、Header、参数、请求体等。

---

### 三、报告输出优势
- 自动生成 **HTML 报告**，结构化展示攻击事件、Top IP、Top 规则
- 逐条高亮命中规则，保留原始日志行，便于取证与复盘
- 可折叠详情与清晰排版，适合审计输出与汇报
- 统计聚合：按 IP、规则、时间维度形成热点视图
- 可动态自定义搜索及排除事件、IP、规则等白名单优化

```
=====================================================================================================
```

## 2025.9.18 - 更新
- 新增windows日志分析功能-授权通用 、支持三大日志+sysmon。windows分析报告建议本地浏览器打开
```
=====================================================================================================
```
## 2026.1.13 - 更新
- 新增linux日志分析功能-免费使用 。
- ## 功能特性

- ## 核心功能
- 🔍 **多类型日志分析**：支持系统日志、安全日志、Web日志、邮件日志等多种类型
- 🚀 **高效检测**：采用并行处理和批量命令执行，提高检测速度
- 📊 **直观报告**：生成美观的 HTML 报告，包含统计卡片、时间线分析、攻击流程可视化
- 🎯 **ATT&CK 框架支持**：基于 MITRE ATT&CK 框架生成攻击流程分析报告
- 📝 **自定义规则**：支持 JSON 格式自定义检测规则
- 🔐 **安全连接**：使用 SSH 协议安全连接目标服务器

- ## 检测能力
- 暴力破解检测
- 可疑 IP 识别
- 登录失败/成功统计
- 系统错误分析
- Web 攻击检测（SQL注入、XSS、Webshell等）
- 异常进程检测
- 系统服务异常检测
- 网络连接异常检测

## 支持的自动收集日志类型

- **系统日志**：/var/log/syslog, /var/log/messages
- **安全日志**：/var/log/auth.log, /var/log/secure
- **Web 日志**：Apache、Nginx 访问日志和错误日志
- **邮件日志**：Postfix、Sendmail 日志
- **防火墙日志**：iptables、firewalld 日志
- **SSH 日志**：SSH 服务日志
- **应用日志**：MySQL、Redis 等应用日志


## 分析模式

### logs 模式

- 仅分析系统日志文件
- 检测速度快，资源消耗少
- 适合快速初步分析

### full 模式

- 全面检查系统，包括：
  - 日志文件分析
  - 系统进程检测
  - 网络连接检测
  - 系统服务检测
  - 异常文件检测
  - 安全配置检查
- 检测全面，资源消耗较大
- 适合深入分析和应急响应

## 自定义规则

### 规则文件格式（JSON）

```json
{
  "rules": [
    {
      "id": "rule_001",
      "name": "暴力破解检测",
      "description": "检测连续失败的登录尝试",
      "pattern": "Failed password",
      "severity": "critical",
      "log_type": "auth",
      "threshold": 5,
      "time_window": 3600
    },
    {
      "id": "rule_002",
      "name": "Webshell 检测",
      "description": "检测可疑的 Web 请求",
      "pattern": "cmd=|exec|system|passthru|eval",
      "severity": "critical",
      "log_type": "web_access",
      "threshold": 1,
      "time_window": 3600
    }
  ]
}
```

### 规则字段说明

- **id**：规则唯一标识符
- **name**：规则名称
- **description**：规则描述
- **pattern**：检测正则表达式
- **severity**：严重程度（critical、warning、normal）
- **log_type**：适用的日志类型
- **threshold**：阈值
- **time_window**：时间窗口（秒）

## ATT&CK 攻击流程分析

### 功能说明

- 基于 MITRE ATT&CK 框架生成攻击流程分析报告
- 支持战术和技术的关联分析
- 生成可视化的攻击路径
- 支持 HTML 和 JSON 两种输出格式

### 支持的 ATT&CK 战术

- 侦察
- 资源开发
- 初始访问
- 执行
- 持久化
- 权限提升
- 防御规避
- 凭证访问
- 发现
- 横向移动
- 收集
- 命令与控制
- 数据渗漏
- 影响


### 报告内容

1. **分析摘要**：总览检测结果
2. **ATT&CK 攻击流程分析**：基于 ATT&CK 框架的攻击流程可视化
3. **日志分析详细结果**：按日志类型分类显示检测结果
4. **系统检查结果**：仅在 full 模式下显示

