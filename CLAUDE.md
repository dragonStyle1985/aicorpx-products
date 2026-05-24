# AICorpX Products Landing Page

落地页：https://aicorpx.predict-future.com
源码仓库：GitHub Pages 自动部署（push main 即生效）

## 配色方案

- CSS 变量定义在 `:root` 中，主色 `#7c3aed`（紫），强调 `#2563eb`（蓝）
- 支持 dark mode（`@media (prefers-color-scheme: dark)`）
- 卡片图标背景色在产品 JS 数据中逐项指定

## Grid 布局规则

所有 Grid 使用固定列数 + 媒体查询，不允许 `auto-fill`（避免半行空位）：

| 区域 | 桌面 | ≤1024px | ≤640px |
|---|---|---|---|
| 核心产品 `.grid` | 3列 | 2列 | 1列 |
| 更多能力 `.services-grid` | 4列 | 2列 | 1列 |
| 为什么选我们 `.why-grid` | 2列 | 2列 | 1列 |
| FAQ `.faq-grid` | 2列 | 2列 | 1列 |

- 如果卡片数不能整除列数，补卡片或用 `why-grid` 这种固定列数布局
- 服务卡片文字长度尽量控制在 28-40 字，保持视觉平衡

## 页面结构

Hero → 数据统计(Stats) → 核心产品(Products, JS渲染) → 更多能力(Services) → 为什么选我们(Why Us) → FAQ → CTA → Footer

## 产品卡片数据

定义在 JS 数组 `products` 中，每个条目含：
- `name`, `tagline`, `icon`, `iconBg`, `features`(string[]), `price`, `target`

添加新产品时必须同时：
1. 在 `products` 数组中添加条目
2. 在 `renderProducts()` 底部更新表单下拉框（`document.getElementById('formProduct')` 的 options）

## 询盘表单

- API 端点：`const API_ENDPOINT = 'https://predict-future.com/api/inquiry'`
- 字段：product_name（下拉预填）、name（必填）、contact（必填）、message
- 提交失败时降级显示微信公众号和邮箱联系信息
- 后端在 `Personal-Life-Assistant/operations/inquiry_api.py`

## 部署

```bash
git add -A && git commit -m "..." && git push
```

GitHub Pages 自动部署，通常 1-2 分钟生效。
