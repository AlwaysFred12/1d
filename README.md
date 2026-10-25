# 1D

> One day, starts now.

个人资源小站。三个板块：**1D Tool**（现成能用的网页工具）、**资讯 News**（还没上线的清单）、**Personal App**（自己设计开发的 iPhone App）。另有一篇独立的 **CodeX 使用教程**。

整站是纯静态、零依赖的单文件 HTML —— 没有构建步骤、没有前端框架、没有任何外部资源请求，克隆下来直接就能跑。

---

## 在线地址

| | 地址 |
| --- | --- |
| 主站（国内） | https://1d-tools.app.workbuddy.host/ |
| CodeX 教程 | https://1d-tools.app.workbuddy.host/codex/ |
| GitHub Pages | https://alwaysfred12.github.io/1d/ |

站点自带设备分流：窄屏（< 700px）自动加载手机版，宽屏加载桌面版。也可以强制指定：

- `?mobile` / `?desktop` —— 强制切换版本
- `#home` / `#tools` / `#news` / `#apps` —— 直接落到某个板块

---

## 目录结构

```
.
├── index.html            # 入口分流页（窄屏 → mobile.html，否则 → desktop.html；hash 原样透传）
├── desktop.html          # 主站桌面版（1440 画布，四个整屏横向排开）
├── mobile.html           # 主站手机版（真机重排，不是缩放的桌面版）
├── about.html            # 关于 1D
├── legal.html            # 版权声明与免责声明
├── tutorial-codex.html   # 旧地址跳转存根（/tutorial-codex.html → /codex/）
├── codex/
│   ├── index.html        # CodeX 教程分流页
│   ├── desktop.html      # CodeX 教程 · 桌面版
│   └── mobile.html       # CodeX 教程 · 手机版
├── .nojekyll             # 关掉 GitHub Pages 的 Jekyll 处理
└── README.md
```

---

## 本地预览

直接双击 `index.html` 就能看。若要模拟真实服务环境：

```bash
python3 -m http.server 8000
# 打开 http://127.0.0.1:8000/
```

---

## 部署到 GitHub Pages

仓库根目录就是站点根目录，不需要任何构建。

1. 推到 GitHub 后，进入仓库 **Settings → Pages**
2. **Source** 选 `Deploy from a branch`
3. **Branch** 选 `main`，目录选 `/ (root)`，保存
4. 等一两分钟，访问 `https://<用户名>.github.io/<仓库名>/`

根目录的 `.nojekyll` 会让 Pages 跳过 Jekyll 处理（这个站不需要它，跳过更快也不会误改文件）。

> 换了域名不影响站内链接：所有互链都是**相对路径**，放在仓库根或子路径下都能正常工作。

---

## 技术说明

- **单文件自包含**：样式、脚本、图标、字体全部内联，`src` / `<link href>` / `@import` 对外的请求数为 **0**。断网也能完整显示。
- **字体自托管**：中文用子集化后的 woff2 以 base64 内联（全站 23 条 `@font-face`），不依赖 Google Fonts 之类的境外 CDN。
- **无横向滚动**：桌面版用 `transform: scale()` 按视口等比缩放固定 1440 画布。
- **手机版是独立排版**，不是桌面版的缩放。
- 没有 `package.json`、没有 node_modules、没有构建产物 —— 改完 HTML 存盘即生效。

---

## 更新

日常改版在作者本地的工作目录进行，改完重新装配（改写互链为 ASCII 文件名、补内联 favicon）后覆盖本目录，再 commit 即可。也可以直接改这里的 HTML —— 四个页面的互链都是相对路径，不会因为改名而断。

---

## 版权

站内原创内容（文案、版式、代码）著作权归作者所有，未经许可请勿转载或再发布。收录的第三方工具各自遵循其原始许可，本站仅作索引与说明，不主张任何权利。

详见 [legal.html](legal.html)。
