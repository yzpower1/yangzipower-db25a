# Yangzi Power 独立站部署指南

## 你的网站会是什么样

```
用户访问 yangzipower.com        → 看到完整的B2B官网
你访问 yangzipower.com/admin    → 登录后可视化编辑网站内容
改了产品/价格/文案 → 保存 → 3秒自动发布到线上
```

无服务器、零维护、不会被黑。

---

## 一次性部署（约 15 分钟，只需做一次）

### Step 1 — 创建 GitHub 仓库
1. 打开 https://github.com 注册/登录
2. 点击右上角 **+** → **New repository**
3. 仓库名填 `yangzipower`，选 **Public**，点 **Create repository**
4. 把本地 `yzpower-website` 文件夹里所有文件上传到这个仓库
   - 可以直接拖拽文件到 GitHub 网页上
   - 也可以下载 GitHub Desktop 客户端，一次同步

### Step 2 — 部署到 Netlify
1. 打开 https://app.netlify.com → 用 GitHub 账号登录
2. 点击 **Add new site** → **Import an existing project** → 选 GitHub
3. 找到刚才创建的 `yangzipower` 仓库 → 点 **Deploy site**
4. 等 1-2 分钟，Netlify 给你一个临时域名如 `xxx.netlify.app`

### Step 3 — 开启 CMS 后台
1. 在 Netlify 进入你的站点 → **Site settings**
2. 左侧点 **Identity** → 点击 **Enable Identity**
3. 往下滚到 **Registration** → 改为 **Invite only**（只允许你自己登录）
4. 左侧点 **Services** → **Git Gateway** → 点击 **Enable Git Gateway**

### Step 4 — 绑定域名 yangzipower.com
1. Netlify → **Domain management** → **Add custom domain** → 输入 `yangzipower.com`
2. 去你的域名管理（Cloudflare）修改 DNS：

| 类型 | 名称 | 值 |
|------|------|-----|
| CNAME | `@` | `你的站点名.netlify.app` |
| CNAME | `www` | `你的站点名.netlify.app` |

3. 等 DNS 生效后，Netlify 自动签发 HTTPS 证书

### Step 5 — 创建你的管理员账号
1. 在 Netlify → **Identity** 页面
2. 点 **Invite users** → 输入你的邮箱
3. 去邮箱收确认邮件，点链接设置密码
4. 访问 `https://yangzipower.com/admin` → 用刚才的邮箱+密码登录

### Step 6 — 配置询盘接收（2分钟）
1. 打开 https://formspree.io → 用邮箱注册
2. 点 **+ New Form** → 表单名填 `yangzipower`
3. 目标邮箱填 `yangzip45@gmail.com`
4. 创建后复制 Form ID（一串字母数字，如 `xabcd123`）
5. 在 GitHub 仓库里打开 `index.html`，搜索 `YOUR_FORM_ID`，替换为你的 ID
6. 保存 → Netlify 自动重新部署（1分钟）

> 不配 Formspree 也能用：客户提交表单时会自动打开邮件客户端，预填好询盘内容，点发送即可。Formspree 只是让体验更流畅。

---

## 日常使用：怎么改网站内容

1. 浏览器打开 `https://yangzipower.com/admin`
2. 登录（你的邮箱+密码）
3. 左边菜单选要改的内容：

| 菜单 | 能改什么 |
|------|----------|
| **Products** | 添加/修改/删除产品，改价格、型号、规格 |
| **Site Settings** | 改品牌名、联系方式、公司信息 |
| **About Page** | 改公司介绍文字、亮点 |
| **Product Categories** | 改品类名称和描述 |

4. 改完点右上角 **Publish** → 选择 **Publish now**
5. 等 10 秒，网站上就更新了

> 添加产品图片：在 CMS 里点产品 → Image 字段 → 上传图片 → 保存

---

## 费用

| 项目 | 费用 |
|------|------|
| GitHub | 免费 |
| Netlify | 免费（100GB 带宽/月，够用） |
| HTTPS 证书 | 自动免费 |
| 域名 yangzipower.com | 你自己买的，续费 ~$10/年 |

---

## 需要帮助？

部署中遇到问题，截图发给我。
