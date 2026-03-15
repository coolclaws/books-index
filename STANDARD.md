# AI 源码解析电子书制作标准

_最后更新：2026-03-16_

---

## 一、项目选择标准

**适合做的项目：**
- 开源、Python 或 Rust 为主、代码量适中（不超过 10 万行）
- GitHub Stars > 5k，且有持续更新
- 在 AI 技术栈中有明确定位（Agent 框架 / 向量库 / 推理引擎 / 应用工具）
- 核心抽象清晰，有值得深读的架构设计

**优先选择标准：**
1. 受众广（与其他书互补，组成完整技术栈）
2. 代码可读性强（有助于源码引用）
3. 设计哲学有特点（能写出"为什么这么设计"）

---

## 二、命名规范

| 项目 | 书名格式 | 域名格式 | GitHub Repo |
|------|---------|---------|-------------|
| LangGraph | LangGraph 源码解析 | langgraph-book.myhubs.dev | coolclaws/langgraph-book |
| CrewAI | CrewAI 源码解析 | crewai-book.myhubs.dev | coolclaws/crewai-book |

**规则：**
- Repo 名：`{项目名小写}-book`
- 域名：`{项目名小写}-book.myhubs.dev`
- 书名：`{项目名} 源码解析`
- 副标题：一句话说清楚项目定位

---

## 三、目录结构

```
{project}-book/
├── .github/
│   └── workflows/
│       └── deploy.yml        # GitHub Actions 自动部署
├── .vitepress/
│   └── config.ts             # VitePress 配置
├── chapters/
│   ├── 01-overview.md
│   ├── 02-repo-structure.md
│   ├── ...
│   ├── appendix-a-reading-path.md
│   ├── appendix-b-type-reference.md
│   └── appendix-c-glossary.md
├── public/
│   ├── logo.png              # 项目真实 logo（GitHub org 头像，128px）
│   ├── favicon.svg           # 可选
│   └── icons/                # 章节内图标（如有）
├── .gitignore
├── CNAME                     # {project}-book.myhubs.dev
├── contents.md               # 完整目录页
├── index.md                  # 首页（VitePress home layout）
└── package.json
```

---

## 四、章节数量参考

| 项目规模 | 建议章节数 | 附录 |
|---------|-----------|------|
| 小型（< 2万行） | 12–15 章 | 3 附录 |
| 中型（2–5万行） | 16–20 章 | 3 附录 |
| 大型（5万行+） | 20–26 章 | 3 附录 |

**标准章节结构（以中型项目为例）：**
1. 第一部分：宏观认知（2章）— 概览 + Repo 结构
2. 第二部分：核心抽象（3–4章）— 最重要的类/接口
3. 第三部分：执行引擎（3–4章）— 运行时机制
4. 第四部分：持久化/存储（2–3章）— 状态管理
5. 第五部分：高级特性（2–3章）— 扩展点
6. 第六部分：生态与集成（1–2章）— 外部接口
7. 附录 A：推荐阅读路径
8. 附录 B：核心类型速查
9. 附录 C：名词解释（Glossary）

---

## 五、写作风格要求

### 5.1 每章内容
- **字数**：1500–2500 字
- **代码引用**：必须标注文件路径和行数
  - Python：`# 文件: module/file.py L123-145`
  - Rust：`// 文件: src/module/file.rs`
- **每章开头**：一句话引言（用 blockquote `>`）
- **每章结尾**：一段"本章小结"

### 5.2 排版规范
- 中英文之间加空格（"Python 函数"，不是"Python函数"）
- 使用中文标点（，。：；""）
- H2 → H3 → 正文，正文段落不超过 5 行就换段
- 对比类信息用表格（不超过 5 列）

### 5.3 内容深度
- 不只是"这个函数做了什么"，要说"为什么这么设计"
- 引用真实源码片段（不编造）
- 指出设计的取舍和局限性

---

## 六、VitePress 配置模板

### 颜色主题选择（各书品牌色）
| 书 | 主色 |
|----|------|
| LangGraph | `#38b2ac`（teal） |
| CrewAI | `#f59e0b`（amber） |
| AG2/AutoGen | `#6366f1`（indigo） |
| Pydantic AI | `#e92063`（red） |
| Mem0 | `#10b981`（green） |
| Chroma | `#f97316`（orange） |
| Qdrant | `#dc244c`（dark red） |
| DeerFlow | `#8b5cf6`（purple） |
| OpenCode | `#0ea5e9`（sky） |
| OpenClaw | `#06b6d4`（cyan） |

### config.ts 关键配置
```ts
export default defineConfig({
  title: '{项目名} 源码解析',
  description: '...',
  lang: 'zh-CN',
  base: '/',                          // 自定义域名用 /，不加子路径

  themeConfig: {
    logo: { src: '/logo.png', alt: '{项目名}' },  // 真实项目 logo
    nav: [
      { text: '开始阅读', link: '/chapters/01-overview' },
      { text: '目录', link: '/contents' },
      { text: 'GitHub', link: 'https://github.com/coolclaws/{repo}' },
    ],
    // sidebar: [...],
    outline: { level: [2, 3], label: '本页目录' },
    search: { provider: 'local' },
    footer: {
      message: '基于 MIT 协议发布',
      copyright: 'Copyright © 2025-present',
    },
  },
  markdown: { lineNumbers: true },
})
```

---

## 七、Logo 获取方式

使用项目的 **GitHub 组织头像**（真实 logo，不自制）：

```bash
# 下载 128px PNG
curl -sL "https://github.com/{org}.png?size=128" -o public/logo.png
```

| 项目 | GitHub Org |
|------|-----------|
| LangGraph | langchain-ai |
| CrewAI | crewAIInc |
| AG2 | ag2ai |
| Pydantic AI | pydantic |
| Mem0 | mem0ai |
| Chroma | chroma-core |
| Qdrant | qdrant |
| DeerFlow | bytedance |
| OpenCode | sst |
| OpenClaw | openclaw |

---

## 八、GitHub Actions 部署文件

统一使用以下 `.github/workflows/deploy.yml`（无需修改，直接复制）：

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - uses: actions/setup-node@v4
        with:
          node-version: 22
          cache: npm
      - uses: actions/configure-pages@v4
      - run: npm ci
      - run: npm run docs:build
      - uses: actions/upload-pages-artifact@v3
        with:
          path: .vitepress/dist

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/deploy-pages@v4
        id: deployment
```

---

## 九、封面 Feature Icon 规范

VitePress 首页（`index.md`）的 features 区域必须使用自定义 SVG，**禁止使用 emoji**。

### 9.1 为什么不用 emoji

- Emoji 在不同操作系统/浏览器渲染差异大，外观不可控
- 无法与书的品牌色联动（SVG 可以直接使用 `fill` 颜色）
- 在暗色模式下对比度差，影响可读性

### 9.2 Icon 格式要求

- 格式：SVG，存放在 `public/icons/` 目录
- 尺寸：`viewBox="0 0 48 48"` 统一规格
- 颜色：使用书的主题色（与 `config.ts` 中的 `--vp-c-brand` 一致）
- 风格：简洁线条/填充混合，语义清晰（不要纯抽象图形）
- 数量：通常 4 个 feature 对应 4 个 icon

### 9.3 index.md 写法

```yaml
features:
  - icon:
      src: /icons/overview.svg     # ✅ 自定义 SVG
    title: 架构概览
    details: 项目定位、整体设计...

  # ❌ 禁止这样写
  - icon: 🚀
    title: 高性能
```

### 9.4 Icon 设计参考

每个分类的常用图形语义：

| 场景 | 推荐图形 |
|------|---------|
| 架构/宏观 | 矩形连线图、层次方块 |
| 调度/批处理 | 横向堆叠矩形 |
| 内存/缓存 | 带引脚的矩形、环形 |
| 编译/优化 | 六边形 + 齿轮 |
| 分布式 | 多节点连线图 |
| 性能/速度 | 折线图、闪电 |
| API/接口 | 代码框 + 勾选 |
| 模型定义 | 多层矩形堆叠 |
| 训练/微调 | 下降曲线 + 刻度 |
| 向量/嵌入 | 坐标轴 + 点集 |

### 9.5 SVG 模板

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48" fill="none">
  <!-- 用书的主题色，如 #0ea5e9 -->
  <rect x="8" y="8" width="32" height="32" rx="4" stroke="#0ea5e9" stroke-width="2"/>
  <circle cx="24" cy="24" r="6" fill="#0ea5e9"/>
</svg>
```

---

## 十、.gitignore 标准

```
.DS_Store
node_modules/
*.swp
*.swo
*~
.vitepress/cache/
```

---

## 十一、完整发布流程

1. **创建目录结构**（参考第三节）
2. **写内容**（用 Claude Code agent 生成，参考 prompt 模板）
3. **本地验证**：`npm install && npm run docs:build`
4. **创建 GitHub Repo**：
   ```bash
   curl -s -X POST "https://api.github.com/user/repos" \
     -H "Authorization: token $GH_TOKEN" \
     -H "Content-Type: application/json" \
     -d '{"name":"{name}-book","private":false,"auto_init":false}'
   ```
5. **push 代码**（记得加 .gitignore，不提交 node_modules）：
   ```bash
   git init && git add . && git commit -m "init: ..."
   git branch -M main && git push -u origin main
   ```
6. **开启 GitHub Pages + 设置自定义域名**（两步缺一不可）：
   ```bash
   # Step 1: 开启 Pages（workflow 模式）
   curl -s -X POST "https://api.github.com/repos/coolclaws/{name}-book/pages" \
     -H "Authorization: token $GH_TOKEN" \
     -H "Content-Type: application/json" \
     -d '{"build_type":"workflow"}'

   # Step 2: 设置 custom domain（⚠️ 必须显式设置，否则自定义域名 404）
   curl -s -X PUT "https://api.github.com/repos/coolclaws/{name}-book/pages" \
     -H "Authorization: token $GH_TOKEN" \
     -H "Content-Type: application/json" \
     -d '{"cname":"{name}-book.myhubs.dev"}'

   # Step 3: 触发首次 workflow 部署
   curl -s -X POST "https://api.github.com/repos/coolclaws/{name}-book/actions/workflows/deploy.yml/dispatches" \
     -H "Authorization: token $GH_TOKEN" \
     -H "Content-Type: application/json" \
     -d '{"ref":"main"}'
   ```
   > **注意**：即使 `public/CNAME` 文件存在，GitHub Pages 也不会自动读取并生效。
   > 必须通过 API PUT `/pages` 的 `cname` 字段显式绑定，custom domain 才会正常解析。

7. **添加 Cloudflare DNS CNAME**：
   - Zone ID：`605d32215ab6096167efff4f4dcd86fa`
   - Token：在 `/Users/claw/models/cryptosurf/.env.local` 的 `CLOUDFLARE_API_TOKEN`
   ```bash
   curl -s -X POST "https://api.cloudflare.com/client/v4/zones/$CF_ZONE/dns_records" \
     -H "Authorization: Bearer $CF_TOKEN" \
     -H "Content-Type: application/json" \
     -d '{"type":"CNAME","name":"{name}-book","content":"coolclaws.github.io","ttl":1,"proxied":true}'
   ```
8. **更新 books.myhubs.dev 索引页**：
   - 编辑 `/tmp/books-index/index.html`
   - 加入新卡片（参考现有格式）
   - commit & push → coolclaws/books-index

---

## 十二、Agent Prompt 模板

生成新书时，Claude Code agent 的 prompt 参考以下结构：

```
你是一个技术电子书作者。请为 {项目名}（{org}/{repo}）创建一本完整的中文源码解析电子书，
使用 VitePress 构建，风格与 /tmp/langgraph-book/ 完全一致。

书名：{项目名} 源码解析
副标题：{一句话定位}
颜色主题：{品牌色十六进制}
CNAME：{name}-book.myhubs.dev

章节结构：[按第四节规范列出]

写作要求：[按第五节规范列出]

完成后：
1. npm install
2. npm run docs:build（验证构建）
3. openclaw system event --text "Done: {name}-book 创建完成" --mode now
```

---

## 十三、当前书库

### 应用框架与工具链
| 书名 | 域名 | Repo | Stars |
|------|------|------|-------|
| OpenClaw 源码解析 | openclaw-book.myhubs.dev | coolclaws/openclaw-book | 314.6k |
| DeerFlow 源码解析 | deerflow-book.myhubs.dev | coolclaws/deerflow-book | 30.8k |
| OpenCode 源码解析 | opencode-book.myhubs.dev | coolclaws/opencode-book | 122.6k |

### Agent 编排框架
| 书名 | 域名 | Repo | Stars |
|------|------|------|-------|
| LangGraph 源码解析 | langgraph-book.myhubs.dev | coolclaws/langgraph-book | 26.4k |
| CrewAI 源码解析 | crewai-book.myhubs.dev | coolclaws/crewai-book | 46.1k |
| AG2 源码解析 | autogen-book.myhubs.dev | coolclaws/autogen-book | 4.3k |
| Pydantic AI 源码解析 | pydantic-ai-book.myhubs.dev | coolclaws/pydantic-ai-book | 15.5k |

### 记忆与向量数据层
| 书名 | 域名 | Repo | Stars |
|------|------|------|-------|
| Mem0 源码解析 | mem0-book.myhubs.dev | coolclaws/mem0-book | 49.9k |
| Chroma 源码解析 | chroma-book.myhubs.dev | coolclaws/chroma-book | 26.6k |
| Qdrant 源码解析 | qdrant-book.myhubs.dev | coolclaws/qdrant-book | 29.6k |

### 推理引擎
| 书名 | 域名 | Repo | Stars |
|------|------|------|-------|
| vLLM 源码解析 | vllm-book.myhubs.dev | coolclaws/vllm-book | 73.2k |
| SGLang 源码解析 | sglang-book.myhubs.dev | coolclaws/sglang-book | 24.5k |
| Mini-SGLang 源码解析 | mini-sglang-book.myhubs.dev | coolclaws/mini-sglang-book | 3.7k |
| TensorRT-LLM 源码解析 | trtllm-book.myhubs.dev | coolclaws/trtllm-book | 13.1k |
| llama.cpp 源码解析 | llamacpp-book.myhubs.dev | coolclaws/llamacpp-book | 98k |
| MLX 源码解析 | mlx-book.myhubs.dev | coolclaws/mlx-book | 24.5k |
| MLX-LM 源码解析 | mlx-lm-book.myhubs.dev | coolclaws/mlx-lm-book | 4k |
