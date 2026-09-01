# is-an.org - 免费二级域名申请

一个纯静态的二级域名申请页面，为开源项目、个人作品和非营利组织提供 `yourname.is-an.org` 免费子域名。

## 工作原理

纯前端 + 邮件：

1. 申请者填写表单（子域名、申请人、邮箱、项目类型、描述、目标 IP/CNAME）
2. 点击「提交申请」后自动打开邮件客户端，申请内容以邮件形式发往 `contact@is-an.org`
3. 管理员收到邮件后人工审核，通过后手动配置 DNS 解析并回复申请者

无需数据库、无需后端服务、无需 API Key。

## 项目结构

```
.
├── index.html   # 申请页面（唯一的文件）
└── README.md
```

## 部署

任意静态托管平台均可，例如：

- **Cloudflare Pages**
- **GitHub Pages**
- **Vercel / Netlify**
- **任意 Nginx / 对象存储静态站点**

### Cloudflare Pages 示例

1. 在 [Cloudflare Dashboard](https://dash.cloudflare.com) 创建 Pages 项目
2. 连接本仓库（或直接上传 `index.html`）
3. 构建设置：Build command 留空，Build output directory 为 `/`
4. 部署后添加自定义域名 `is-an.org` 即可

## 自定义配置

如需修改收件邮箱，编辑 `index.html` 中的 `RECIPIENT` 变量：

```javascript
var RECIPIENT = 'contact@is-an.org';
```

## 注意事项

- 邮件通过 `mailto:` 打开申请者本地邮件客户端发送，不经过服务器
- 页面同时提供「复制申请内容」按钮，便于在网页邮箱中手动粘贴发送
- 审核通过后需要在 Cloudflare DNS 中添加对应子域名的解析记录

## 许可证

MIT
