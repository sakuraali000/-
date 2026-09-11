# 旅行手册 · 部署说明（电脑端操作）

本仓库只有一个文件 `index.html`（单文件、零外部依赖、可离线）。把它发布成任何人可访问的公开网址，全程免费，走 **GitHub + Cloudflare Pages**，push 即上线。

> 本文件只是给你看的部署手册，不是网页内容。发布后它也会跟着上线（无害），你也可以随时删除它，不影响页面。

---

## 仓库结构

```
nordic-trip/            ← 你的仓库名（随意）
├── index.html          ← 旅行手册（唯一要发布的文件）
└── DEPLOY.md           ← 本部署说明（可删）
```

只要根目录有 `index.html`，Cloudflare 就能发布。任何后续改动都只动这个 `index.html`。

---

## 一、首次发布（必须电脑）

### 步骤 1　准备本地文件夹　（电脑）
把 `index.html` 放进一个空文件夹，例如 `nordic-trip/`。

### 步骤 2　在 GitHub 新建空仓库　（必须电脑）
1. 登录 https://github.com （没有就注册，免费）
2. 右上角 **＋ → New repository**
3. Repository name 填 `nordic-trip`（随意）
4. **不要** 勾选 "Add a README" / .gitignore / license（保持空仓库）
5. 点 **Create repository**

### 步骤 3　把文件推上去　（必须电脑）
在终端（Mac 终端 / Windows PowerShell / Git Bash）进入文件夹后执行：

```bash
git init
git add index.html
git commit -m "trip handbook v1"
git branch -M main
git remote add origin https://github.com/你的用户名/nordic-trip.git
git push -u origin main
```

> 嫌命令行麻烦：装 **GitHub Desktop**，登录后把文件夹拖进去，点 Publish → 推送即可。

### 步骤 4　连接 Cloudflare 自动发布　（必须电脑，需授权）
1. 登录 https://dash.cloudflare.com （没有就注册，免费版即可）
2. 左侧 **Workers 和 Pages → 创建 → Pages → 连接到 Git**
3. 授权 GitHub，选中 `nordic-trip` 仓库
4. 构建设置：
   - **Framework preset**：选 `None`
   - **Build command**：**留空**
   - **Build output directory**：填 `/`（根目录）
5. 点 **保存并部署**

约 10–30 秒后，你会得到一个形如 `https://nordic-trip-xxxx.pages.dev` 的**公开网址**——任何人点开就能看，不用登录、不用装 App。

---

## 二、以后每次更新（push 即上线）

我改好新的 `index.html` 给你后，你只需覆盖旧文件并推送：

```bash
git add index.html
git commit -m "update"
git push
```

Cloudflare 会自动重新构建上线，通常十几秒生效。无需再进 Cloudflare 后台。

---

## 三、常见问题

- **打开是空白 / 404**：确认仓库根目录确实有 `index.html`（拼写、大小写都对），且 Build output directory 设为 `/`。
- **改了但页面没变**：Cloudflare 有缓存，等 30 秒刷新；硬刷新 `Ctrl+Shift+R`（Mac `Cmd+Shift+R`）。
- **想换自定义域名**（如 `trip.example.com`）：Cloudflare Pages → 项目 → **自定义域**，按提示加一条 CNAME 解析即可（可选，不必须）。
- **一定要用 Cloudflare Workers 而非 Pages**：Pages 是 Workers 平台的静态站点方案，最省事。若坚持纯 Workers + 静态资源，需加 `wrangler.toml` 配 `assets`，步骤更绕，需要我再给。

---

## 四、隐私提醒

`index.html` 是**公开网址、谁都能看**。请确认里面**没有**填过：
- 机票/订单**确认号、票号**
- 护照/证件号
- 酒店**房间号**

本手册已按此原则制作（确认号、证件号、票号、房间号均未写入）。后续你让我改内容时也请提醒我别加这些。
