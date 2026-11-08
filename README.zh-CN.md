# dbfox

本地 SQL、数据库浏览与迁移工作台。

[English](README.md) · [官网](https://richardgvin.github.io/dbfox-site/) · [下载](https://github.com/richardgvin/dbfox/releases) · [安装说明](docs/installation.md)

![dbfox SQL 工作台](https://richardgvin.github.io/dbfox-site/assets/workspace.jpg)

浏览数据库对象、执行 SQL、查看结果并审阅迁移计划。各数据库的支持范围不同，
请参阅官网能力表。迁移执行需要人工审阅；MCP 工具只读或生成建议。
dbfox 在本地运行，不是托管数据库服务。

## 安装

从 [Releases](https://github.com/richardgvin/dbfox/releases) 下载已发布版本。
首个版本发布前，尚无可用的公共安装包。

- Windows x64：MSI 安装包，或包含服务端、CLI 与网页界面的独立 ZIP。
- Docker：Linux amd64 的 server/web 镜像及固定版本的 Compose ZIP。
- MCP：单独下载 Windows x64 包，内含 `dbfox-mcp.exe`。
- 首批不提供 macOS、Linux 桌面版和 ARM64 安装包。

首发 Windows 程序**未签名**，系统可能提示未知发布者或 SmartScreen 警告。
请用发行版的 `SHA256SUMS` 核对 SHA-256，并遵守所在组织的安装策略。
安装 MSI 不会安装或配置独立 MCP 包。

使用 Docker 时，下载并解压该版本的 Compose ZIP：

```sh
cp .env.example .env
docker compose pull
docker compose up -d --wait
```

访问 `http://127.0.0.1:8080`。仓库中的模板需要填写发行版的版本和 digest；
下载包已经填写。升级前必须备份数据目录及 `secret.key`。

## 使用文档

- [Windows 安装与独立运行](docs/installation.md)
- [Docker、存储与外部驱动](docs/docker.md)
- [MCP 配置与权限](docs/mcp.md)
- [备份、升级与恢复](docs/upgrade.md)

## 反馈与更新

安装问题、缺陷及功能请求请提交到 [Issues](https://github.com/richardgvin/dbfox/issues)。
发送日志前，请脱敏连接串、主机名、用户名、密码及业务数据。
安全问题使用 [SECURITY.md](SECURITY.md) 中的私密渠道。

[在 GitHub 上 Star](https://github.com/richardgvin/dbfox)。订阅版本通知，请选择本仓库
的 **Watch → Custom → Releases**。下载不要求 Star，也不要求登录 GitHub。

## 许可

dbfox 二进制沿用 [MIT](LICENSE)，允许再分发和修改。本仓库保存使用文档与部署配置，
不包含产品源码或构建历史。各发行版的依赖许可见[第三方声明](THIRD_PARTY_NOTICES.md)。
