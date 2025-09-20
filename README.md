# CheckMultiLog
多种Windows日志分析、web日志分析，支持IIS日志、Apache日志、 Nginx 日志、 Tomcat日志 、Jetty日志、通用json（常见字段）安全分析。

## 一、支持的日志格式

### WEB日志
- IIS W3C
- NCSA（Apache / Nginx / Tomcat / Jetty）
- HAProxy
- AWS ALB/ELB
- 通用 JSON access log
- Unknown 未识别但包含 IP、时间、URI、User-Agent 信息的日志

### Windows日志
- Security日志
- 应用程序日志
- 系统日志
- SYSMON日志

Web日志分析演示
![食用实例](/demo.gif)

Windows日志分析演示
![食用实例](/demo2.gif)


> **说明**：免费版仅开放 **IIS W3C** 与 **NCSA(IIS)**；授权版解锁全部格式。

---

## 二、内置分析规则种类
- **WebShell 检测**：冰蝎、哥斯拉、Neo-reGeorg 等
- **漏洞利用**：Shiro、Log4Shell、Spring4Shell、ThinkPHP、PHPUnit
- **弱口令/敏感接口**：K8s API/Docker API 未授权、IndexOf 目录列举
- **数据外带**：大 Base64 参数、Token/Session 泄露、归档批量下载
- **扫描识别**：xray、fscan、sqlmap、WPScan、Nuclei
- **通用攻击**：SQLi、XSS、路径遍历、恶意上传绕过、命令执行

> 规则来自 `AttackRules.ini`，采用正则表达式匹配 URL、Header、参数、请求体等。

---

## 三、报告输出优势
- 自动生成 **HTML 报告**，结构化展示攻击事件、Top IP、Top 规则
- 逐条高亮命中规则，保留原始日志行，便于取证与复盘
- 可折叠详情与清晰排版，适合审计输出与汇报
- 统计聚合：按 IP、规则、时间维度形成热点视图
- 可动态自定义搜索及排除事件、IP、规则等白名单优化


---

### 未来更新
- 支持 Windows、Linux 操作系统日志  
- 用户群反馈特定日志（WAF、其他类型 Web 日志、防火墙日志）

### 2025.9.18 - 更新
- 新增windows日志分析功能-授权通用 、支持三大日志+sysmon。windows分析报告建议“windows日志分析”选项卡点击查看打开
