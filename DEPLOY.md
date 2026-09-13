# SlowSprings 上线指南（GitHub + Vercel 方案）

## 前置条件

- 阿里云实名认证已通过（域名 Hold 状态解除）
- 注册一个 GitHub 账号（github.com，用邮箱即可）
- 注册一个 Vercel 账号（vercel.com，推荐点 "Continue with GitHub" 直接用 GitHub 登录）

## 第一步：推送代码到 GitHub（约 3 分钟）

1. 打开 https://github.com/new
2. Repository name 填 `slowsprings-site`，选 Private 或 Public 均可（Vercel 都支持），点 Create repository
3. 页面会显示一串命令，在终端执行（把 `你的用户名` 换成你的）：

```bash
cd /Users/xushi/WorkBuddy/2026-09-11-09-13-30/slowsprings-site
git remote add origin https://github.com/你的用户名/slowsprings-site.git
git branch -M main
git push -u origin main
```

4. 首次 push 会弹出登录窗口，按提示用浏览器授权即可

## 第二步：Vercel 导入部署（约 3 分钟）

1. 打开 https://vercel.com/new
2. 列表里点 `slowsprings-site` 仓库的 Import（首次需先点授权 GitHub）
3. 所有设置保持默认，直接点 Deploy
4. 等约 1 分钟，完成后获得临时地址 `slowsprings-site-xxx.vercel.app`，先确认能打开

## 第三步：绑定域名（约 5 分钟 + 等待生效）

1. Vercel 项目页 → Settings → Domains → 输入 `slowsprings.com` → Add
2. Vercel 会提示需要添加的 DNS 记录，内容是：
   - `A` 记录：`@` → `76.76.21.21`
   - `CNAME` 记录：`www` → `cname.vercel-dns.com`
3. 打开阿里云域名控制台 https://dc.console.aliyun.com
   → 找到 slowsprings.com → 解析 → 添加记录：

   | 记录类型 | 主机记录 | 记录值 |
   |---------|---------|--------|
   | A | @ | 76.76.21.21 |
   | CNAME | www | cname.vercel-dns.com |

4. 回到 Vercel，等待检测通过（通常 10 分钟到 1 小时）
5. 生效后 https://slowsprings.com 自动带 HTTPS 证书

## 之后的日常更新

改完 index.html 后：

```bash
cd /Users/xushi/WorkBuddy/2026-09-11-09-13-30/slowsprings-site
git add -A && git commit -m "更新内容"
git push
```

Vercel 检测到 push 会自动重新部署，约 1 分钟生效。

## 常见问题

- **域名打不开**：先查阿里云实名状态（必须解除 Hold）；再查 DNS 记录是否填对
- **Vercel 检测不到解析**：TTL 默认即可，别改；解析全球生效最长 48 小时，但一般 1 小时内
- **www 打不开但主域可以**：确认 CNAME 那条记录加上了
