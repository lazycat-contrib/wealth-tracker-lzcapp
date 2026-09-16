# wealth-tracker-lzcapp（生财有迹）

[生财有迹](https://github.com/nicejade/wealth-tracker)（个人资产分析应用）的懒猫微服（LazyCat）打包。

## 模式

- **镜像模式（mirror delivery）**：manifest 经国内加速器 `docker.1ms.run` 引用上游镜像 `nicejade/wealth-tracker`，不复制到懒猫镜像仓库。
- **自动版本**：上游发布标准 SemVer tag（如 `5.0.0`），`channel: stable` 自动发现更新并升级包版本。
- **仅发布喵喵商店**（MiaoMiao private store）；官方平台不发布。

## 结构

| 文件 | 说明 |
| --- | --- |
| `package.yml` | 包元数据（`community.lazycat.app.wealth-tracker`） |
| `lzc-manifest.yml` | 运行配置（单服务 `wealth-tracker`，端口 8888） |
| `lzc-build.yml` | 构建配置 |
| `icon.png` | 图标 |
| `.github/lazycat-action.yml` | [lazycat-github-action](https://github.com/ca-x/lazycat-github-action) 配置 |

## 自动化

`lazycat.yml` 工作流（配置文件 PR 时 dry-run 验证、每日定时约北京时间 13:37 + 手动触发）自动：

1. 检查上游 `nicejade/wealth-tracker` 新 SemVer tag；
2. 更新包版本与 manifest 中的加速器镜像引用；
3. 构建 LPK、发布 GitHub Release（`<package-id>-v<version>.lpk`）；
4. 发布喵喵商店。

## 所需 Secrets

| Secret | 说明 |
| --- | --- |
| `APPSTORE_URL` | 喵喵商店 API 地址 |
| `APPSTORE_TOKEN` | 喵喵商店发布令牌 |
| `APP_ID` | 可选，喵喵商店应用 ID |
| `PRIVATE_STORE_GROUP_CODES` | 可选，私有分组码 |
