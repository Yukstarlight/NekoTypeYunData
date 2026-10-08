# NekoTypeYunData

NekoType · 云端的**公开数据仓库**（由客户端通过 jsDelivr CDN / GitHub API 读取）。

## 目录结构

```
cloud-data/
  config/notice.json          公告 { active, text, updatedAt }
  config/version.json         版本 { latest, minSupported, downloadUrl, backupUrl, changelog }
  presets/index.json          已审预设索引（列表页数据）
  presets/approved/<id>.json  已审预设完整内容（r ules 等）
  presets/pending/<id>.json   待审预设（管理员审核后移入 approved 并更新 index）
```

## 管理员操作（直接在网页上做，无需后台）

**通过一个预设**：
1. 打开 `cloud-data/presets/pending/<id>.json`，确认内容
2. 把它移动到 `cloud-data/presets/approved/<id>.json`（GitHub 网页支持 Move/Rename）
3. 在 `cloud-data/presets/index.json` 数组里加一条元信息（id / ownerId / name / desc / ruleCount / downloads / updatedAt）
4. 从 pending 目录删除原文件

**驳回**：直接从 `pending/` 删除文件（可在文件里记录原因后移入 `rejected/`）

**下架**：从 `approved/` 删除文件 + 从 `index.json` 移除对应条目

**改公告**：编辑 `cloud-data/config/notice.json` 的 `active` 和 `text`（CDN 缓存 1-5 分钟生效）

**发新版本**：编辑 `cloud-data/config/version.json` 的 `latest` / `downloadUrl` 等
