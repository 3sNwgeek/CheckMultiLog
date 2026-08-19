# WiFi WPA2 握手破解（字典导入）

## 题目背景
分析师截获了办公无线网络的监听抓包（Radiotap + 802.11），包含：

1. SSID 为 `3sNwGeek-Office` 的 Beacon 帧（信道 6，WPA2-PSK/CCMP）；
2. 完整四次握手中的 M1（ANonce）与 M2（SNonce + MIC）；
3. 两帧 CCMP 加密数据帧，内层为 HTTP 请求/响应，响应正文包含 flag。

## 任务
仅依靠抓包与同目录字典，自动完成：

1. 识别 WiFi 网络（SSID/BSSID/信道/加密类型）；
2. 收集四次握手并用字典爆破 PSK（PBKDF2-HMAC-SHA1 + MIC 校验）；
3. 派生 PTK 解密 CCMP 数据帧，还原 HTTP 明文并提取 flag。

## 验证方法（CheckMultiLog）
1. 导入 `wifi_wpa2_handshake.pcap`；
2. 进入“WiFi / WPA2 握手”选项卡，确认识别到 `3sNwGeek-Office`（信道 6、WPA2-PSK · CCMP、M1+M2 已捕获）；
3. 点击“导入字典 / 指定 PSK”，选择同目录 `wifi_dict.txt`，点击“应用并开始破解”；
4. 预期：网络行变为“已破解”并显示 PSK；“TLS / Key Log 解密”视图出现 WPA2-CCMP 已解密会话；Flag 汇总出现：

```
flag{wpa2_handshake_dict_crack_ok}
```

## 真值（出题参考，勿随包发布）
- SSID：`3sNwGeek-Office`（BSSID 12:34:56:78:9a:bc，信道 6）
- PSK：`3sNwGeek@WiFi#2026`
- 加密：WPA2-PSK / AES-CCMP
- flag：`flag{wpa2_handshake_dict_crack_ok}`

## 生成方式
`仓库根/_gen/gen_wifi_wpa2.py`（纯 Python 构造 802.11 帧：Beacon/RSN 标签、EAPOL M1/M2（真实 MIC）、AES-CCM 数据帧；依赖 `pip install cryptography`）。
