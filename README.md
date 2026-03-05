# Project Template

Claude Code 自主项目引擎。3 个 Skill 覆盖产品全生命周期：建设 → 评审 → 算法审计。

---

## 快速开始（3 步）

### Step 1：从模板创建新项目

```bash
gh repo create my-new-project --template Bruce-Kang1994/project-template --clone --private
cd my-new-project
```

> 也可以在 GitHub 页面点 **"Use this template"** → **"Create a new repository"**

### Step 2：配置权限（首次使用需要，之后不用）

在项目根目录创建 `.claude/settings.json`：

```bash
mkdir -p .claude
cat > .claude/settings.json << 'EOF'
{
  "permissions": {
    "allow": [
      "Read",
      "Write",
      "Edit",
      "Glob",
      "Grep",
      "Bash(npm run *)",
      "Bash(npx *)",
      "Bash(git *)",
      "Bash(ls *)",
      "Bash(mkdir *)",
      "Bash(cd *)",
      "Bash(cat *)",
      "Bash(cp *)",
      "Bash(mv *)"
    ]
  }
}
EOF
```

> 这个文件已被 `.gitignore` 排除，不会提交到 GitHub，只在你本地生效。

### Step 3：启动 Claude Code，说出你的 idea

```bash
claude
```

然后直接告诉它你想做什么，比如：

```
我想做一个 AI 简历分析工具，用户上传简历，AI 给出评分和改进建议。
```

```
I want to build a habit tracker app where users log daily habits and see streaks.
```

```
帮我做一个 SaaS 定价计算器，输入成本和用户量，自动推荐定价策略。
```

Claude 会自动开始：竞品调研 → 写 PRD → 选技术栈 → 开发 → 测试 → 部署。
中间不需要你反复确认，最后给你一个可访问的 URL。

---

## 它会自动做什么？

| 阶段 | Claude 自动执行的内容 |
|------|----------------------|
| 调研 | 搜索 3-5 个竞品，找差异化空间 |
| 需求 | 写轻量 PRD（`docs/PRD.md`），砍到 3-5 个核心功能 |
| 架构 | 选技术栈，初始化项目，建 `CLAUDE.md` |
| 开发 | 按优先级逐个实现功能，每个功能自测后提交 |
| 打磨 | 端到端走查，加 OG 标签 / 错误处理 / 移动端适配 |
| 部署 | 部署到 Vercel，输出可访问的 URL |

## 什么时候会问你？

只有这几种情况 Claude 会暂停询问：

- 需要 API Key（比如 OpenAI Key、Supabase URL）
- 需要付费服务的账号配置
- 涉及域名、定价等商业决策

以下全部自主决定：技术栈、UI 设计、配色、文件结构、数据库设计、API 设计、文案内容。

---

## 模板里包含什么

```
project-template/
  .claude/
    skills/
      solo-ship/
        SKILL.md           <-- 自主开发引擎（idea -> 部署全流程）
      product-review/
        SKILL.md           <-- 全方位产品评审（品牌/功能/逻辑/UI/竞品/执行计划）
      algorithm-audit/
        SKILL.md           <-- 算法模型审计（框架对标/BARS/权重/分层/原型系统）
  .gitignore               <-- 排除 settings.json、node_modules、.env 等
  README.md                <-- 你正在看的这个文件
```

### 三个 Skill 的关系

| Skill | 什么时候用 | 触发方式 |
|-------|----------|---------|
| **solo-ship** | 从零开始建产品 | "I want to build..." |
| **product-review** | 产品建完后做全方位评审 | "Review this product" |
| **algorithm-audit** | 产品包含评分/排名/分类算法时 | "Audit the algorithm" |

`solo-ship` 在 Phase 4（打磨）结束后会提示你运行另外两个 skill 做深度审计。

## 常见问题

**Q: 我能自定义技术栈吗？**
可以。在描述 idea 时加上要求，比如"用 Python + FastAPI 做后端"，Claude 会遵守。

**Q: 部署一定是 Vercel 吗？**
默认是 Vercel（对 Next.js 最友好）。如果你想用别的（Railway、Fly.io），告诉 Claude 即可。

**Q: 一个项目能跑多久？**
取决于复杂度。一个简单的 MVP（3-5 个功能）通常一个对话 session 内可以完成。

**Q: 我中途想改方向怎么办？**
直接告诉 Claude，比如"停一下，我想把目标用户改成..."，它会调整。

---

## License

MIT
