---
AIGC:
    Label: "1"
    ContentProducer: 001191440300708461136T1XGW3
    ProduceID: fa90a3ce7c42f36245ef4460c02dcf39_07cc612bd65d11f1a97752540064ee0f
    ReservedCode1: LBxnhRD3wl9uwxGKV5SuHczgnEGG20KpS8U6V1IYJDuCo9k0CoqVSl9WHIwRHds5T6Y/bNbc0LDUkPRgXhiBn8grMy0R/X8hDHigNpe+EUhuOhN7rw6PmsuYanv5CUMQczq3Ssac0nIBPtrC5fBrGS53PNHCbNYmqDq7LLdk5uGfyCX75LRFe4qihJU=
    ContentPropagator: 001191440300708461136T1XGW3
    PropagateID: fa90a3ce7c42f36245ef4460c02dcf39_07cc612bd65d11f1a97752540064ee0f
    ReservedCode2: LBxnhRD3wl9uwxGKV5SuHczgnEGG20KpS8U6V1IYJDuCo9k0CoqVSl9WHIwRHds5T6Y/bNbc0LDUkPRgXhiBn8grMy0R/X8hDHigNpe+EUhuOhN7rw6PmsuYanv5CUMQczq3Ssac0nIBPtrC5fBrGS53PNHCbNYmqDq7LLdk5uGfyCX75LRFe4qihJU=
---

# Marvis 定制 TVBox 源包（基于 subscription-release v3.0.124 开源版）

## 文件结构

```
我的源包/
├── marvis_open.json          # 订阅配置（直连 raw.githubusercontent 线路）
├── marvis_open_ghproxy.json  # 订阅配置（gh-proxy.com 国内加速线路）
├── assets/
│   ├── spider_open.txt       # 开源 Spider（jar 文本形式，带 md5 校验）
│   ├── token.json            # 网盘 cookie 配置（空，扫码后自动回填）
│   └── live_iptv.m3u         # 自建直播源
├── README.md                 # 本文件
└── 安全审查报告.md             # 后门/风险审查结果
```

## 一、部署（托管到 GitHub）

1. 把 `assets/` 下三个文件上传到你的 GitHub 仓库（例如 `Guabis/pg-online` 的 `tvbox/` 目录）
2. 确认 `marvis_open.json` 中的 `spider` / `token` / 直播源地址与你的实际托管路径一致：

```
spider: https://raw.githubusercontent.com/Guabis/pg-online/main/tvbox/spider_open.txt;md5;70cc68258967d704c4edcc1e694ed332
token:  https://raw.githubusercontent.com/Guabis/pg-online/main/tvbox/token.json
live:   https://raw.githubusercontent.com/Guabis/pg-online/main/tvbox/live_iptv.m3u
```

> 只要 spider_open.txt 内容不变，MD5 就保持 `70cc68258967d704c4edcc1e694ed332`，TVBox 会做一致性校验。
> 若要加 jsDelivr 线路，把上面的域名换成 `https://cdn.jsdelivr.net/gh/Guabis/pg-online@main/tvbox/...` 即可。

## 二、订阅使用

- 国内线路：`https://gh-proxy.com/https://raw.githubusercontent.com/Guabis/pg-online/main/tvbox/marvis_open.json`
- 直连线路：`https://raw.githubusercontent.com/Guabis/pg-online/main/tvbox/marvis_open.json`

把链接填入 TVBox / 影视仓 / 可视TV 等客户端的「订阅地址」即可。

## 三、定制差异（相对原作者 v3.0.124）

- 采用**开源版** `spider_open.txt`（纯开源 Spider，可审计），不使用私有 `spider.jar`
- 移除全部第三方私有解析站（parses 为空）；需要解析功能时，自行添加可信解析接口
- 移除未知第三方代理域名规则（`cdn.v82u1l.com`）与作者品牌 logo
- 移除不可达的第三方 ext（豆瓣扩展配置）
- 保留 58 个站点、广告拦截列表、公共 DoH、直播源

## 四、网盘加速（可选）

如需夸克/阿里/115 网盘 Range 并发加速，从官方 release 单独下载对应平台 `goproxy` 二进制并校验 MD5 后使用；本包不内置该私有组件。

## 五、更新维护

- 上游出新版时，对比 `spider_open.txt` MD5；内容变化则替换 assets 并同步更新配置中的 md5 值
- 定期复查第三方站点域名是否失效，按需增删 sites
*（内容由AI生成，仅供参考）*
