# GLA 16th 大会横幅 · GitHub Pages 图床

零成本、永久有效的邮件图片托管骨架。目录内已含：

| 文件 | 说明 |
|---|---|
| `gla-16th-conference-banner.jpg` | 高清版 2400×800，471 KB，推荐（二维码清晰） |
| `gla-16th-conference-banner-1600.jpg` | 轻量版 1600×533，207 KB |
| `index.html` | 落地页，自动生成图片直链与可复制的邮件 HTML 片段 |
| `.nojekyll` | 跳过 Jekyll 构建，避免静态文件被过滤 |
| `CNAME.example` | 自定义域名示例，按需改名使用 |

## 部署步骤

1. 在 GitHub 新建**公开**仓库，例如 `gla-email-assets`（免费版 Pages 不支持私有仓库）。
2. 把本目录全部文件复制到仓库根目录。
3. 本地初始化并推送：
   ```bash
   git init
   git add .
   git commit -m "Add GLA 16th conference email banner"
   git branch -M main
   git remote add origin https://github.com/<USER>/gla-email-assets.git
   git push -u origin main
   ```
4. 仓库 **Settings → Pages → Build and deployment**：Source 选 `Deploy from a branch`，Branch 选 `main` / `(root)`，保存。
5. 等 1–2 分钟，打开 `https://<USER>.github.io/gla-email-assets/` 确认落地页与图片显示正常。
6. （推荐）绑定自有域名：DNS 添加 CNAME `img.glafamily.com → <USER>.github.io`；把 `CNAME.example` 改名为 `CNAME` 并写入 `img.glafamily.com`；在 Pages 设置里填入自定义域名并勾选 **Enforce HTTPS**。
7. 用 curl 验证直链返回的是图片而不是 HTML：
   ```bash
   curl -sS -I "https://img.glafamily.com/gla-16th-conference-banner.jpg"
   # 期望：HTTP/2 200 + content-type: image/jpeg
   ```
8. 发测试邮件到 Gmail、Outlook、QQ 邮箱、企业微信邮箱各验一次，确认图片不被屏蔽、二维码可扫。

## 最终图片 URL

| 场景 | URL |
|---|---|
| 不绑域名 | `https://<USER>.github.io/gla-email-assets/gla-16th-conference-banner.jpg` |
| 绑定自有域名（推荐） | `https://img.glafamily.com/gla-16th-conference-banner.jpg` |

邮件 HTML 片段：

```html
<img src="https://img.glafamily.com/gla-16th-conference-banner.jpg"
     width="600" height="200"
     alt="The 16th GLA Global Logistics Conference | 6-9 May 2027 | Shenzhen, China"
     style="display:block;width:100%;max-width:600px;height:auto;border:0;" />
```

## 为什么用 Pages 而不是 raw 链接

实测 `raw.githubusercontent.com` 的响应头：

- `content-type: image/png` —— 类型正确，但
- `cache-control: max-age=300` —— 仅缓存 5 分钟
- `content-security-policy: default-src 'none'; ... sandbox`
- `x-frame-options: deny`
- 请求落到 `japaneast` 节点，境内无直连节点

它是给人查看源码用的，带速率限制，不是为生产图片托管设计的。GitHub Pages 才是官方静态托管通道，缓存与稳定性都好得多；jsDelivr（`https://cdn.jsdelivr.net/gh/<USER>/<REPO>@main/...`）也可作为 CDN 前端，但域名信誉对邮件不如自有域名。

## 政策与限制（务必知悉）

依据 GitHub 可接受使用政策（2026-11 查阅）：

- **第 9 条 过度带宽使用**：带宽明显高于同类用户时，GitHub 可暂停账户、限制文件托管，甚至提前通知后删除仓库。单张横幅 471 KB、3000 人各加载一次约 1.5 GB，远低于 100 GB/月软限制，正常用量没问题。
- **第 10 条 GitHub 上的广告**：内容不应「侧重于广告或促销」。纯图床仓库属灰区，因此本目录保留了 `index.html` 项目说明页，请把仓库当作一个正常的「邮件素材项目」维护，不要只扔图片。
- 单文件上限 100 MB，仓库建议 1 GB 以内 —— 当前完全够用。
- 仓库公开：对外横幅本就是公开物料，但不要放入任何内部或未发布素材。

## 国内送达提醒

GitHub Pages 服务器在境外，绑定自定义域名只解决品牌与信誉，**不解决境内速度**。若这封邮件面向国内外大量会员正式群发，更稳的是把同一批文件上传到腾讯云 COS / 阿里云 OSS + 国内 CDN，或直接放到 `www.glafamily.com` 官网目录，再替换 URL 即可，本目录的文件命名可直接复用。

## 维护约定

- 图片 URL 一旦写进邮件，不要改文件名、不要删仓库、不要下线 Pages。
- 需要换图时，用**新文件名**上传并更新模板，保留旧文件至少到该轮邮件生命周期结束。

---

GLA Global Logistics Alliance · www.glafamily.com
