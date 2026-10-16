# FileBrowser Quantum - LazyCat App

[FileBrowser Quantum](https://github.com/gtsteffaniak/filebrowser)（Web 文件浏览器，v2 "Quantum" 稳定版）的懒猫微服（LazyCat）打包。

## 模式

- **镜像模式（mirror）**：`ghcr.io/gtsteffaniak/filebrowser` 镜像经 `ghcr.1ms.run` 加速器拉取，`require_digest_match: true` 校验镜像内容与上游一致。
- **自动跟随上游**：每日检查上游 `N.N.N-stable` tag（`channel: stable`，版本号剥掉 `-stable` 后缀），发现新版本自动更新版本号与镜像、构建 LPK、发布商店。
- **喵喵商店发布**：仅私有商店（MiaoMiao private store），不发布官方商店。

## 说明

- 挂载：`/lzcapp/run/mnt/home` → `/srv/home`（用户家目录，可写）、`/lzcapp/run/mnt/media` → `/srv/media`（只读）
- 数据卷：`/lzcapp/var/filebrowser` → `/home/filebrowser/data`（SQLite 数据库 + config.yaml）
- **首次启动**：admin 密码随机生成并打印在容器日志里（首次登录需重置密码）；可在 `config.yaml` 里设置 `auth.adminPassword`
- 添加更多文件源：编辑 `/home/filebrowser/data/config.yaml` 的 `sources` 列表
- 健康检查 `/health`（端口 80）

## 所需 Secrets

| Secret | 说明 |
| --- | --- |
| `APPSTORE_URL` / `APPSTORE_TOKEN` | 喵喵商店 API 地址与发布令牌 |
| `APP_ID` | 可选 |
| `PRIVATE_STORE_GROUP_CODES` | 可选，私有分组码 |

## 许可

Apache-2.0（上游）
