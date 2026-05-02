# 檀谷爵士音乐节 Photo Essay 设计计划

## 概述

将檀谷爵士音乐节的摄影素材制作为一个杂志风格的 photo essay 页面，作为个人博客新增的 `journal/` 分类下的第一篇内容。

**定位**: 简约清新的图文 editorial，不是相册，不是幻灯片——是一篇有叙事节奏的视觉文章。

## 目录结构

```
journal/
└── tanko-jazz-fest/
    ├── index.html          # Photo essay 页面
    ├── styles.css          # 杂志风格样式
    └── images/             # Web 优化后的照片（JPEG, ~1200px 宽）
        ├── poster.jpg       ← IMG_4885.HEIC  活动海报
        ├── tanko-gate.jpg   ← IMG_4928.HEIC  TANKO 标识+水景
        ├── lake.jpg         ← IMG_4927.HEIC  湖面远景
        ├── art-wall.jpg     ← IMG_4889.HEIC  潮流艺术墙
        ├── graffiti.jpg     ← IMG_4890.HEIC  街头涂鸦
        ├── rabbit.jpg       ← IMG_4922.HEIC  兔子雕塑
        ├── blossoms.jpg     ← IMG_4925.HEIC  花树
        ├── wristband.jpg    ← IMG_4914.HEIC  手环特写
        ├── stage-wide.jpg   ← IMG_4916.HEIC  舞台全景
        ├── performer.jpg    ← IMG_4911.HEIC  乐手特写
        ├── crowd.jpg        ← IMG_4897.HEIC  草坪观众
        ├── food.jpg         ← IMG_4896.HEIC  松露薯条+咖啡
        └── sign.jpg         ← IMG_4926.HEIC  "于山间舞动生活"
```

**精选 13 张**，按叙事线组织：入场 → 园区探索 → 演出 → 生活 → 收尾。

## 视觉设计

### 风格: 杂志 Editorial

- **背景**: 纯白 `#fafafa`（区别于 landing page 的深色，形成反差）
- **文字**: 深灰 `#1a1a1a`（标题）/ `#666` （正文）/ `#999`（图注）
- **字体**: 衬线标题（`'Playfair Display'` 或 `'Noto Serif SC'`）+ 无衬线正文（`Inter`）
- **色彩点缀**: 无——让照片本身的色彩说话
- **间距**: 大量留白，图片之间 40-60px 间距

### 页面布局

```
┌─────────────────────────────────────────┐
│                                         │
│     檀谷 × DEFACTTO                     │
│     爵士艺术生活节                        │
│     Jazz & Art Life Fest                │
│     ─────────                           │
│     2026.05.02 · 北京 · 檀谷             │
│                                         │
├─────────────────────────────────────────┤  ← Hero: 海报图 poster.jpg (全宽)
│           [poster.jpg 全宽]              │
│                                         │
├─────────────────────────────────────────┤
│                                         │
│  § 入场                                  │
│                                         │
│  ┌─────────────┐  ┌─────────────┐       │  ← 双列
│  │ tanko-gate  │  │   lake      │       │
│  └─────────────┘  └─────────────┘       │
│  引言文字: 西山脚下...                     │
│                                         │
├─────────────────────────────────────────┤
│                                         │
│  § 园区                                  │
│                                         │
│  ┌─────────────────────────────────┐    │  ← 大图
│  │       art-wall.jpg              │    │
│  └─────────────────────────────────┘    │
│  ┌────┐  ┌────┐  ┌────┐               │  ← 三列小图
│  │grff│  │rbt │  │blsm│               │
│  └────┘  └────┘  └────┘               │
│                                         │
├─────────────────────────────────────────┤
│                                         │
│  § 舞台                                  │
│                                         │
│  ┌─────────────────────────────────┐    │  ← 大图
│  │      stage-wide.jpg             │    │
│  └─────────────────────────────────┘    │
│  短文: 彩色灯光下...                      │
│  ┌─────────────┐  ┌─────────────┐       │  ← 双列
│  │  performer  │  │  wristband  │       │
│  └─────────────┘  └─────────────┘       │
│                                         │
├─────────────────────────────────────────┤
│                                         │
│  § 生活                                  │
│                                         │
│  ┌────────┐  ┌────────────────────┐     │  ← 1:2 比例
│  │  food  │  │     crowd          │     │
│  └────────┘  └────────────────────┘     │
│                                         │
├─────────────────────────────────────────┤
│                                         │
│      [sign.jpg 全宽]                     │  ← 结尾图
│      "于山间舞动生活，摇摆身心"             │
│                                         │
│             ───                          │
│     © 2026 maodf                        │
│                                         │
└─────────────────────────────────────────┘
```

### 图片网格规则

- **全宽大图**: 关键叙事节点（海报、舞台全景、结尾语）
- **双列**: 对称/对比场景（入场两张、乐手+手环）
- **三列**: 同类素材快速浏览（艺术装置三连）
- **1:2 比例**: 主次区分（美食小图 + 草坪大图）
- 所有图片 `border-radius: 4px`，极轻的阴影
- 图注在图片下方，小字居左

### 文字内容

每个 section 配 1-2 句简短文案（中文），不做长篇叙述：

- **入场**: "西山脚下，慢闪公园。五月的风里带着爵士的味道。"
- **园区**: "涂鸦、雕塑、花树。音乐节不只是音乐。"
- **舞台**: "萨克斯、小号、吉他。彩色灯光下，乐手们忘我地演奏。"
- **生活**: "草坪上的咖啡和薯条，远处传来即兴的旋律。"

### 技术实现

- **纯 HTML + CSS**，零 JS
- **CSS Grid** 做图片布局
- **响应式**: 手机全部单列，桌面按上述网格
- **图片优化**: HEIC → JPEG，宽度统一 1200px，质量 82%（估算每张 150-300KB，总量 ~3MB）
- **Lazy loading**: `<img loading="lazy">`
- 页面顶部返回 landing page 的导航链接

## 图片处理流程

使用 ImageMagick 批量转换：

```bash
cd /home/maodf/immich-20260502_175342

# 逐个转换选定的 HEIC 文件为 JPEG，缩放到 1200px 宽
convert IMG_4885.HEIC -resize 1200x -quality 82 poster.jpg
convert IMG_4928.HEIC -resize 1200x -quality 82 tanko-gate.jpg
convert IMG_4927.HEIC -resize 1200x -quality 82 lake.jpg
convert IMG_4889.HEIC -resize 1200x -quality 82 art-wall.jpg
convert IMG_4890.HEIC -resize 1200x -quality 82 graffiti.jpg
convert IMG_4922.HEIC -resize 1200x -quality 82 rabbit.jpg
convert IMG_4925.HEIC -resize 1200x -quality 82 blossoms.jpg
convert IMG_4914.HEIC -resize 1200x -quality 82 wristband.jpg
convert IMG_4916.HEIC -resize 1200x -quality 82 stage-wide.jpg
convert IMG_4911.HEIC -resize 1200x -quality 82 performer.jpg
convert IMG_4897.HEIC -resize 1200x -quality 82 crowd.jpg
convert IMG_4896.HEIC -resize 1200x -quality 82 food.jpg
convert IMG_4926.HEIC -resize 1200x -quality 82 sign.jpg

# 移动到目标目录
mv *.jpg /home/maodf/projects/claude_code_practices/journal/tanko-jazz-fest/images/
```

## Landing Page 更新

在 `index.html` 中新增 "Journal / 记录" section（与现有 "Practices / 实践" 并列），添加新卡片：

```html
<a href="journal/tanko-jazz-fest/" class="card">
  <span class="card-icon">&#127926;</span>
  <h3>檀谷爵士音乐节</h3>
  <p class="card-subtitle">TANKO Jazz & Art Life Fest</p>
  <p class="card-desc">五月西山，爵士与生活。一场音乐节的视觉纪实。</p>
  <time>2026/05/02</time>
</a>
```

## 实施步骤

1. 创建目录 `journal/tanko-jazz-fest/images/`
2. 用 ImageMagick 转换 13 张精选照片（HEIC → JPEG, 1200px, q82）
3. 创建 `journal/tanko-jazz-fest/styles.css`（杂志风格白色主题）
4. 创建 `journal/tanko-jazz-fest/index.html`（图文 editorial 布局）
5. 更新根 `index.html`：新增 "Journal / 记录" section + 卡片
6. 浏览器验证
7. 提交推送
