# SlowSprings 个人网站

基于 slowsprings.com 的个人展示网站初版。

## 结构

- `index.html` — 单文件网站（HTML + CSS + JS 全部内嵌），包含：
  - Hero 首屏（一句话介绍 + 行动按钮）
  - About 关于我（介绍文字 + 个人卡片）
  - Projects 精选项目（3 个项目卡片）
  - Skills 技能（三组技能卡）
  - Experience 经历时间线
  - Contact 联系方式
- 响应式设计，手机 / 平板 / 桌面均可正常浏览
- 已做基础 SEO（title / description / Open Graph）
- 滚动淡入动画，支持 prefers-reduced-motion

## 如何修改内容

打开 `index.html`，搜索以下占位符并替换：

1. `[中国资产管理]`、`[读书跑步旅游]` — About 段落
2. SlowSprings、`[职业投资人]`、`中国 · 北京` — 个人卡片
3. 三个项目卡片的标题、描述、标签和 `href="#"` 链接
4. 技能列表和时间线经历
5. `hi@slowsprings.com` 和社交链接

所有需要替换的位置都有 \`\` 注释标记。

## 本地预览

双击 index.html 即可在浏览器打开；或：

```bash
cd slowsprings-site
python3 -m http.server 8080
# 访问 http://localhost:8080
```

## 部署

- **Vercel / Netlify**：把文件夹拖进控制台即可部署
- **GitHub Pages**：推到 GitHub 仓库，Settings → Pages 开启
- **CloudStudio**：国内访问友好，一键部署静态站点
- 域名注册后，在平台绑定 slowsprings.com 即可
