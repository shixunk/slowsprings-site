# SlowSprings 慢泉 · 网站

投资与生活的公开备忘。线上地址：https://slowsprings.com

- **作者**：Matt（碳基 SlowSprings）& 硅基 SlowSprings
- **slogan**：The river of riches runs deep and slow
- **公众号**：慢泉 SlowMoney
- **托管**：GitHub `shixunk/slowsprings-site` → Vercel 自动部署

---

## 目录结构

```
slowsprings-site/
├── index.html                    首页（关于 / 栏目 / 在做什么 / 轨迹 / 联系）
├── assets/
│   ├── style.css                 共享样式表 ← 全站配色、导航、页脚、正文排版都在这里
│   ├── logo.svg                  圆形品牌标志（导航 / favicon / 头像）
│   └── hero-river.svg            首屏河流插图
├── memos/
│   ├── index.html                全部备忘（归档列表，按时间倒序）
│   └── 001-why-slowsprings.html  第 0 期 · 发刊词
├── DEPLOY.md                     首次上线用的部署指南（已完成，留作备份）
└── README.md                     本文件
```

**关键约定**：`style.css` 是唯一的样式来源。改配色、字体、间距只改这一个文件，首页和所有文章页同时生效。

---

## 怎么新增一篇备忘（核心流程）

### 1. 新建文章页

在 `memos/` 下新建文件，命名规则 `序号-英文短名.html`，例如：

```
memos/002-2026-w39.html     第 1 期周度投资备忘
memos/003-reading-dalio.html 读书笔记
```

复制 `memos/001-why-slowsprings.html` 作为模板，改这几处：

| 位置 | 改什么 |
|------|--------|
| `<title>` | 文章标题 |
| `meta description` | 一句话摘要（给搜索引擎和分享卡片用） |
| `meta og:url` | 改成这篇文章的完整网址 |
| `<span class="section-tag">` | 栏目名：投资备忘 / 读书笔记 / 旅游跑步 / 宏观大类资产 |
| `<h1 class="article-title">` | 文章标题 |
| `.article-meta` | 日期 + 作者 |
| `.prose` 里的内容 | 正文 |

正文用这些标签，样式已经配好：

```html
<h2>小节标题</h2>
<p>段落</p>
<ul><li>无序列表</li></ul>
<ol><li>有序列表</li></ol>
<blockquote><p>想强调的一句话</p></blockquote>
<hr />                       <!-- 分隔线 -->
<p class="muted">脚注小字</p>
<table>...</table>            <!-- 数据表格 -->
```

### 2. 在归档页登记

打开 `memos/index.html`，在 `.memo-list` 里**最上面**加一条（倒序排列）：

```html
<a class="memo-item" href="002-2026-w39.html">
  <div class="memo-date">2026-09-20 · 投资备忘</div>
  <div class="memo-title">2026 W39 · 中国资产周记</div>
  <div class="memo-desc">一句话摘要，写清楚这一期主要判断什么。</div>
</a>
```

**这一步不能省** —— 静态网站没有数据库，不登记就不会出现在网站上。

### 3. 推送上线

```bash
cd slowsprings-site
git add .
git commit -m "Memo 002: 2026 W39 周记"
git push
```

Vercel 检测到 `main` 分支更新后自动重新部署，约 30 秒后 slowsprings.com 就是新版。

---

## 本地预览

```bash
cd slowsprings-site
python3 -m http.server 8080
# 浏览器打开 http://localhost:8080
```

> 直接双击 `index.html` 也能看首页，但文章页之间的相对链接在 `file://` 协议下可能不正常，建议用上面的本地服务。

---

## 常用改动位置速查

| 想改什么 | 改哪里 |
|---------|--------|
| 全站配色 / 字体 / 间距 | `assets/style.css` 顶部的 `:root` 变量 |
| 全站导航、页脚 | `assets/style.css`（`nav` / `footer` 段）—— **注意两处页面都有 HTML，样式在共享表** |
| 首页自我介绍 | `index.html` → `#about` 区块 |
| 首页四个栏目卡片文案 | `index.html` → `#columns` 区块 |
| 轨迹时间线 | `index.html` → `#experience` 区块（第 2、3 条目前是占位） |
| 联系方式 | `index.html` → `#contact` 区块 |
| 导航栏链接 | 每个页面 `<nav>` 里各改一次（首页 `#about`，子页 `../index.html#about`） |

---

## 设计规范

| 项 | 值 |
|----|-----|
| 主色 | `#0f6e56` 深绿（`--accent`） |
| 深色 | `#085041`（`--accent-dark`） |
| 浅色底 | `#e1f5ee`（`--accent-light`） |
| 页面底色 | `#faf9f6`（`--bg`） |
| 卡片底 | `#ffffff`（`--surface`） |
| 边框 | `#e5e3dc`（`--border`） |
| 圆角 | 14px（`--radius`） |
| 内容宽 | 960px（`--max-w`）；正文阅读宽 720px（`--read-w`） |

配色与「河流深且缓」的意象一致：深绿为主，米白为底，克制、留白多。
