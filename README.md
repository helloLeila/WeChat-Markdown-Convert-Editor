# WeChat Markdown Convert Editor

微信公众号 Markdown 编辑器：在本机编写和预览文章，复制公众号格式，或配置公众号凭证后同步为微信草稿。

## 本地启动

需要 Node.js 18 或更新版本：

```bash
npm install
npm start
```

浏览器打开 http://127.0.0.1:3210/。没有配置公众号凭证时，仍可使用 Markdown 编辑、预览和复制功能。

如需同步微信草稿，在编辑器的“设置”中配置公众号 AppID 和 AppSecret，然后测试连接。也可以通过 `WECHAT_APP_ID` 和 `WECHAT_APP_SECRET` 环境变量提供凭证。AppSecret 只提交给本机服务端，不会写入浏览器 localStorage；不要提交到 Git。

## 常用命令

```bash
npm run dev       # 启动本地编辑器
npm run build     # 构建编辑器资源
npm test          # 运行测试
npm run check     # 检查关键 JavaScript 文件语法
```

## Docker Compose

```bash
cp .env.example .env.local
# 按需编辑 .env.local；公网部署应启用登录并配置强密码和会话密钥。
docker compose --env-file .env.local up --build
```

服务默认监听 `http://127.0.0.1:3210/`。持久化配置保存在 `data/`，不要提交该目录或 `.env.local`。

容器内配置目录默认为 `/data/config`，由 `OPEN_WECHAT_EDITOR_CONFIG_DIR` 控制；Compose 将主机上的 `./data` 挂载到容器 `/data`。基础镜像可通过 `NODE_BASE_IMAGE` 配置；Docker Hub 访问较慢时，可使用 `docker.m.daocloud.io/library/node:20-bookworm-slim`。

服务器部署脚本：

```bash
bash scripts/deploy-wechat-editor.sh
```

部署脚本会从本仓库的 `main` 分支拉取代码。公网使用时应设置编辑器登录认证，并通过 HTTPS 反向代理提供服务。

## 设计与配置

- [编辑器状态与设计](docs/wechat-editor-status-and-design.md)
- [公众号配置与同步设计](docs/superpowers/specs/2026-08-20-wechat-sync-config-design.md)
- [编辑器设计](docs/superpowers/specs/2026-07-13-open-wechat-editor-design.md)

## 安全

不要将 AppSecret、登录密码、会话密钥或 `.env.local` 提交到仓库。公网部署必须启用登录认证，并使用 HTTPS。
