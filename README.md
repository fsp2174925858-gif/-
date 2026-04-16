# 今天吃什么 · 转盘

一个纯前端的「自定义选项 + 大转盘随机选」小工具，适合决定午饭、聚餐吃什么。无需后端数据库，打开网页就能用。

---

## 功能一览

| 功能 | 说明 |
|------|------|
| 转盘抽奖 | 至少 2 个有效选项时可点击「开始转！」，指针停在某一扇区 |
| 编辑选项 | 添加、删除；「填入示例」「清空」快捷操作 |
| 本机记忆 | 选项保存在浏览器 `localStorage`，刷新不丢（每人、每浏览器各自一份） |
| 分享链接 | 「复制分享链接」会把当前选项编码进 URL，发给朋友打开即看到同一组候选 |
| 手机适配 | 安全区、触控区域、小屏转盘缩放等 |
| 中英文界面 | 右上角 **English** / **中文** 切换；语言会记在浏览器里。分享链接里会带上 `lang=`，对方打开时界面语言与你复制时一致 |

**选项里的竖线**：分享链接用 `|` 分隔多项；若某项里写了 `|`，复制时会自动替换成 `·`，避免弄乱链接。

**英文界面直达**：在地址后加 `?lang=en`（例如 `https://你的域名.vercel.app/?lang=en`），首次打开会切到英文（并写入本机语言偏好）；`?lang=zh` 同理。

---

## 使用前准备（按你想用的方式选做）

### 只想自己电脑上玩

- 安装任意现代浏览器（Chrome、Edge、Firefox、Safari 等）。
- 双击打开项目里的 `index.html`，或把文件拖进浏览器窗口。

### 想同一 WiFi 下用手机访问（局域网预览）

1. 电脑安装 **[Node.js](https://nodejs.org/)**（带 `npm` 即可，LTS 版本推荐）。
2. 在本项目根目录（与 `package.json` 同级）打开终端，执行：

   ```bash
   npm run preview
   ```

3. 终端里会显示本地访问地址（默认监听 **3333** 端口）。在同一 WiFi 下，用手机浏览器访问：

   ```text
   http://你的电脑局域网IP:3333
   ```

   **查电脑 IP（Windows）**：PowerShell 或 CMD 里执行 `ipconfig`，看「无线局域网适配器 WLAN」或「以太网」下的 **IPv4 地址**。

4. **若 PowerShell 报错** `running scripts is disabled`：不要用 `npm` 这条在 PowerShell 里跑，可改用 **CMD** 执行 `npm run preview`，或先调整执行策略（以管理员 PowerShell 执行 `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` 后再试）。

### 想让朋友用手机点链接就能用（公网）

需要：**GitHub 账号**（免费） + **Vercel 账号**（个人免费档通常够用） + 把本项目放到 GitHub 上的一个仓库里。

下面分步说明。

---

## 第一步：注册并登录 GitHub

1. 打开 [https://github.com](https://github.com) ，用邮箱注册账号。
2. 登录后，右上角 **「+」→ New repository**。
3. 填写 **Repository name**（例如 `food-wheel`），选 **Public**，勾选 **Add a README** 可选可不选，点 **Create repository**。
4. 按 GitHub 页面提示，把本文件夹里的文件推上去（网页上传、GitHub Desktop、或命令行 `git` 均可）。  
   **注意**：仓库根目录下要能直接看到 `index.html`（不要多包一层空文件夹），这样部署最简单。

若你还不熟悉 Git，可使用 GitHub 网页：**Add file → Upload files**，把 `index.html`、`package.json`、`README.md` 拖进去后 **Commit**。

---

## 第二步：注册并登录 Vercel

1. 打开 [https://vercel.com](https://vercel.com) ，用 **Continue with GitHub** 授权登录（推荐，后面导入仓库一步完成）。
2. 按提示验证邮箱等，直到进入 Vercel 控制台（Dashboard）。

**费用说明**：个人小项目、静态页面一般落在 **Hobby 免费套餐** 内即可；具体额度以 [Vercel Pricing](https://vercel.com/pricing) 官网为准。

---

## 第三步：把 GitHub 仓库部署到 Vercel

1. 在 Vercel 控制台点 **Add New… → Project**（或 **New Project**）。
2. **Import** 你在第一步里放本项目代码的 GitHub 仓库。若列表里没有，点 **Adjust GitHub App Permissions** 给对应仓库授权。
3. **Configure Project** 里重点检查：

   - **Framework Preset**：选 **Other**，或保持自动检测（纯静态通常没问题）。
   - **Root Directory**：默认 **`.`**（仓库根目录），除非你故意把网页放在子文件夹。
   - **Build Command**：**留空**（本项目没有 `npm run build`）。
   - **Output Directory**：**留空** 或 **`.`**（根目录已有 `index.html` 即可被托管）。

4. 点 **Deploy**。等待一分钟左右，出现 **Congratulations** 后，页面会给出 **Production** 地址，形如：

   ```text
   https://你的项目名-xxx.vercel.app
   ```

5. 复制该 **HTTPS** 链接，通过微信、QQ、短信等发给朋友即可在手机上打开。

以后你改了 `index.html` 并 **push 到 GitHub**，Vercel 会自动重新部署（默认已开启），无需每次手动上传。

---

## 分享给朋友时的两种用法

### 1. 直接发站点链接

把 Vercel 给你的 `https://....vercel.app` 发出去。朋友打开后可以自己改选项；每个人浏览器里保存的列表互不影响。

### 2. 发「带固定选项」的链接

1. 你在页面上把候选（例如火锅、烧烤、日料…）编辑好，保证至少 **2** 项。
2. 点页面上的 **「复制分享链接（带当前选项）」**。
3. 把复制下来的完整链接发给朋友。对方打开后会加载这组选项（地址栏里的 `list` 参数会被页面处理掉，避免链接过长）。

---

## 可选：不用 Vercel 的同类服务

思路相同：**把包含 `index.html` 的仓库或文件夹交给平台托管**。

- [Netlify](https://www.netlify.com/)：Drop 拖拽部署或连接 GitHub。
- [Cloudflare Pages](https://pages.cloudflare.com/)：连接 Git 仓库，构建设置里同样无需复杂构建命令。

---

## 本地项目结构

```text
s1/
├── index.html      # 页面 + 样式 + 逻辑（单页应用）
├── package.json    # 仅含 npm run preview（局域网静态服务）
└── README.md       # 本说明
```

---

## 常见问题

**Q：朋友打开链接是白的或 404？**  
到 Vercel 该项目 → **Deployments** → 点最新一条看 **Build** 是否成功；确认仓库根目录有 `index.html`。

**Q：复制分享链接失败？**  
非 HTTPS 或部分内置浏览器可能限制剪贴板。可部署到 Vercel（HTTPS）后再试；或手动复制地址栏完整 URL。

**Q：我想下线，不再让别人访问？**  
登录 Vercel → 进入该项目 → **Settings → Delete Project**。

**Q：能绑定自己的域名吗？**  
可以。在 Vercel 该项目 **Settings → Domains** 按说明添加域名并在域名 DNS 处配置解析。

---

## 许可证

本项目可按你的需要自由使用与修改；若二次分发，建议保留对原作者的说明（可选）。

祝你和朋友们吃得开心。
