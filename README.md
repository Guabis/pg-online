---
AIGC:
    Label: "1"
    ContentProducer: 001191440300708461136T1XGW3
    ProduceID: fa90a3ce7c42f36245ef4460c02dcf39_90a1c07ace8911f193fe525400638852
    ReservedCode1: WN8aBeQPUNt71k32CcNcws8hhefr0En1AjcuvkQ0x1iHWfc60s03GmC1rYJO7MFDana5XQ4gGbPE84KH0s0j6+YUjwn4wVwGnMA0wdrYdEqRUgVRkxz5biEBiQ1HyexPxVdjp1a1FY6ehpvPGZkkitDF+v8bmPyesIByOlqyl0gJUqqN0mw71crREU8=
    ContentPropagator: 001191440300708461136T1XGW3
    PropagateID: fa90a3ce7c42f36245ef4460c02dcf39_90a1c07ace8911f193fe525400638852
    ReservedCode2: WN8aBeQPUNt71k32CcNcws8hhefr0En1AjcuvkQ0x1iHWfc60s03GmC1rYJO7MFDana5XQ4gGbPE84KH0s0j6+YUjwn4wVwGnMA0wdrYdEqRUgVRkxz5biEBiQ1HyexPxVdjp1a1FY6ehpvPGZkkitDF+v8bmPyesIByOlqyl0gJUqqN0mw71crREU8=
---

# pg 在线订阅发布目录

本目录基于 `pg.20261016-1049.zip` 改造而来，可直接上传 GitHub 仓库后通过 jsDelivr 生成在线订阅链接。目录结构保持与原包相对路径一致（`jsm.json` + `pg.jar` + `js/` + `lib/`），确保 jar 与 JS 相对路径引用有效。

## 目录结构

```
pg/
├── jsm.json          # 主配置（已改造）
├── pg.jar            # 影视TV专用jar（spider: ./pg.jar）
├── pg.jar.md5
├── README.md         # 本文件
└── README.txt        # 原包说明（保留）
    ├── js/           # 31 个 DrPy JS 源
    └── lib/          # 运行库 / 网盘模板 / 分享库
```

## 订阅链接构造（Gitee raw 直链）

上传后订阅地址为：

```
https://gitee.com/<你的Gitee用户名>/<仓库名>/raw/<分支名>/pg/jsm.json
```

- `<你的Gitee用户名>` / `<仓库名>` / `<分支名>`：替换为实际仓库信息（分支默认 `master`）
- Gitee raw 直链无需实名、无需开通 Pages，播放器导入即可解析
- 如需更稳定的 CORS 与正确 Content-Type，可开通 Gitee Pages 后用 `https://<用户名>.gitee.io/<仓库名>/pg/jsm.json`（需实名认证）

## 上传步骤

1. 在 Gitee 新建仓库（如 `pg-online`），将本目录内容整体放在 `pg/` 子目录（或直接放仓库根目录，订阅链接相应调整）
2. 推送到默认分支（`master`），或直接网页上传
3. 访问 `https://gitee.com/<user>/<repo>/raw/<branch>/pg/jsm.json` 验证返回 JSON
4. 在影视TV / OK影视 中"订阅配置"粘贴上述链接导入
5. 后续修改文件即时生效，无需刷新 CDN 缓存；如遇播放器缓存旧配置，重新导入订阅即可

## 本次改造修改点

1. **删除依赖本机 tgsearch 的站点**（3 个）：
   - `TGDouban`（豆瓣 TG 搜索）
   - `TGYunPanLocal`（本地 TG 网盘搜索）
   - `TGYunPan`（TG群组搜索，含 `tgsearch_url: http://127.0.0.1:10199` 与私有 `./lib/tokenm.json` 引用）
2. **删除失效的本地直播源**（24 个）：所有指向 `127.0.0.1:35456`、`192.168.101.2:35455` 的直播条目（最强国内直播系列、肥羊直播系列、五星体育、BJYD 等）
3. **直播源去重**：FMM.txt 重复条目合并
4. **清除空 lives 条目** 1 个
5. **补齐缺失关键文件**：
   - `lib/alistjar.json` ← 由 `lib/alistjar.example.json` 复制
   - `js/alist.json` ← 新建空 JSON（`[]`）
   - `lib/ytblive.m3u` ← 新建占位 m3u
6. **私有文件不托管**：`lib/tokenm.json`（用户私有 token）及原包缺失的站点凭证（`woniu.txt`、`yiso.txt`、`4kzn.txt`、`huamucang.txt`、`guanying.txt`、`hdhive.txt`、`hdhaven.txt`、`webdav.json`、`sambashare.txt`、`panta.txt`、`qianfan.txt`、`pikpakclass.json.txt.gz` 等）不发布、不补造，对应站点需用户本地放置同名文件后方可使用

## 自测结果

- `jsm.json` JSON 合法 ✅
- 残留检查：`127.0.0.1:35456` = 0，`192.168.x.x` = 0，`127.0.0.1:10199` = 0 ✅
- 相对路径引用文件缺失 = 0（除上述私有凭证文件）✅
- 关键文件存在：`jsm.json` / `pg.jar` / `js/alist.json` / `lib/alistjar.json` / `lib/ytblive.m3u` ✅

## 已知说明

- 配置中保留 `http://127.0.0.1:10079/...` 共 34 处：这是影视TV 播放器内置的本地代理端口（DLNA / 转发代理），播放器导入订阅后会在本机自动启动，**不是失效地址**，无需替换
- `lib/tgsearch.json` 为公开搜索配置（无 token），已保留
*（内容由AI生成，仅供参考）*
