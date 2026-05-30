# 灵感便签 · Cloudflare Pages 共享版

## 功能
- 所有设备打开同一个 Cloudflare Pages 链接，读取同一份云端便签
- 查看模式：双击 / 双触复制
- 编辑模式：添加、删除、修改、保存
- 保存后写入 Cloudflare Workers KV
- 自动保证只有一个 `#新点子`，并且必须保留一个
- 15 秒轮询同步云端数据；编辑模式下不会自动刷新覆盖当前输入

## 文件结构

```
/
├── index.html
├── functions/
│   └── api/
│       └── notes.js
└── wrangler.toml
```

## Cloudflare Pages 部署步骤

### 1. 创建 KV
Cloudflare Dashboard → Workers & Pages → KV → Create namespace  
建议命名：`inspiration_notes_kv`

### 2. 部署 Pages 项目
因为使用了 Pages Functions，建议通过 GitHub 仓库或 Wrangler 部署，不建议只用 Dashboard 的 Direct Upload。

### 3. 绑定 KV
进入 Pages 项目：

Settings → Bindings → Add binding → KV namespace

- Variable name：`NOTES_KV`
- KV namespace：选择你创建的 `inspiration_notes_kv`

Production 和 Preview 环境都建议绑定。

### 4. 重新部署
绑定后重新部署一次，访问 Pages 链接即可。

## 注意
这是轻量共享便签，不是强实时协作文档。多人同时编辑并保存时，后保存的人会覆盖前一次保存。
如果你需要像 Google Docs 那样多人同时编辑不互相覆盖，应升级为 Durable Objects / D1 版本。
