# iPeng AI 官网落地页（ipengai-landing）

芃芃科技 · iPeng AI 的品牌与产品主站。它以公司/品牌身份对外展示旗下 AI 产品、产品实验与研发理念，不以创始人个人展示为主页主叙事。

线上地址：<https://ipengai.cn>

## 定位：品牌主站 + 产品页面 / 产品应用

主域名 `ipengai.cn` 是**品牌与产品汇总门户**：负责建立 iPeng AI 的品牌认知、展示产品矩阵并把用户导向对应产品；同时承接有真实需求的 C 端个人与 B 端团队，提供 AI 产品共创入口。内容型产品和销售页可放主域名子路径；具备独立功能的产品应用使用二级域名：

| 地址 | 产品 | 状态 |
|---------|------|------|
| `huma.ipengai.cn` | Huma AI Writer —— 英文论文/报告的 AI 痕迹检测、段落诊断与自然化改写 | 已上线 |
| `ipengai.cn/agentteam/` | AgentTeam —— 一人公司 AI Agent 团队搭建模板包 | 首发销售页，¥49；自动交付链接待接入 |
| …（后续产品） | 按产品形态选择主域子路径或二级域名 | - |

淘宝、小红书等渠道是**宣传渠道**，不是主站的一部分，也不归本仓库管。

## 技术栈

- 纯静态 HTML，**无构建工具**：样式、脚本全部内联在 `index.html` 一个文件里
- 任意静态托管即可部署（Vercel / Cloudflare Pages / OSS+CDN 等）
- 依赖：无

## 项目结构

```
ipengai-landing/
├── index.html      # 单页落地页（内联 CSS/JS），全部页面内容都在这里
├── agentteam/      # AgentTeam 模板包独立销售页 + 产品封面
├── blog/           # 博客文章（静态 html）+ blog/index.html 博客索引
├── sitemap.xml     # SEO Sitemap（新增文章后需同步）
└── .gitignore      # 忽略 .workbuddy/ 与 .DS_Store
```

`.workbuddy/` 是内部工作记忆目录，不提交。

## 页面结构

单页内通过锚点导航：

- `#home` 首屏 Hero ——「好用的 AI 产品」品牌主张；右侧卡片集成面向 C/B 端的 AI 产品共创入口
- `#tools` 产品矩阵 —— Huma AI Writer / AgentTeam
- `#projects` 产品方法 —— 真实问题 / 简单可用 / 结果交付 / 反馈生长
- `#writing` 产品知识与研发札记
- `#about` 关于 + 联系（GitHub、邮箱）

## 视觉主题

当前主题为 **HiPilot 暖色系**：暖纸米色底 `#faf9f6` + 陶土橙 `#c96442` 强调 + 暖墨 `#141413` 文字，参考 HiPilot 官网配色重构。

- 颜色令牌集中在两处 `:root`（首部基础令牌 + 底部「策略层」覆盖），改主题只动这两处
- 深色细节：页脚为暖深色带收尾；Hero 粒子、背景符号、灯晕等动效均为暖色调
- 老版本为「暗黑科技风」（深蓝黑 `#070b12` + 酸绿 `#B8F36B`），已废弃

## 本地预览

```bash
cd ipengai-landing
python3 -m http.server 8000
# 打开 http://localhost:8000
```

无需 `npm install`，改完刷新即生效。

## 维护要点

1. **新增博客文章**：把文章 html 放进 `blog/`，文件名用 URL 安全的命名（避免 `%`/空格，历史踩过坑），然后在 `blog/index.html` 索引和首页 `#writing` 区块登记，最后更新 `sitemap.xml`（中文文件名需 URL 编码）。
2. **上线新产品**：内容型产品/销售页可放主域子路径；独立产品应用开二级域名。主站产品卡直接指向对应地址。
3. **SEO**：`index.html` 头部已含百度站点验证、Open Graph、Schema.org Organization；页脚有 ICP 备案（京ICP备2026033653号）与公安备案，改动时勿删。
4. 改完 `git add` + commit + push 到 `main` 即完成发布（远端：`git@github.com:ipengai/ipengai-landing.git`）。

### AgentTeam 支付与交付

- 销售页：`agentteam/index.html`。
- 产品封面：`agentteam/assets/product-cover.png`。
- 交付目标是第三方数字内容平台的自动发货：用户打开商品收银台，使用支付宝或微信支付，完成后直接进入资料下载页，不再发送付款截图或等待人工邮件。
- 当前销售页已按自动交付流程设计，但正式商品链接尚未接入；获得平台商品 URL 后，将 `agentteam/index.html` 购买按钮替换为该 URL，并把按钮文案改为“立即购买并下载”。
- 首发版 ZIP 保存在内部项目目录，商品创建时上传到交付平台。
- **不要把付费 ZIP 直接放进静态站目录**；静态文件无法做可靠的付费权限校验，公开路径会被直接下载。

## 内容归属原则

- `ipengai.cn` 只保留公司动态、跨产品观点、AI 产品研发与产品矩阵内容。
- Huma 的使用指南、检测原理、案例与关键词内容，长期应迁移到 `huma.ipengai.cn` 的知识库。
- 迁移前先在 Huma 建立文章路由和 sitemap，再为主站旧 URL 配置永久重定向；在这两个条件完成前，不直接删除或搬走现有文章，避免损失已经积累的搜索收录。

## 相关项目

- [aigc-humanizer-en](../aigc-humanizer-en/) —— Huma AI Writer 服务本体（检测 + 改写 + 支付），部署在 `huma.ipengai.cn`
