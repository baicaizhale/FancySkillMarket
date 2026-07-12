# FancySkillMarket

> 此仓库的所有 skill 均与 codex、ClaudeCode 等不兼容，专门为 FancyHelper 服务。

Minecraft 服务器管理员专用 Claude Code Skill 市场。基于 Cloudflare Workers 部署的静态站点。

## 项目结构

```
FancySkillMarket/
├── .claude/                  # Claude Code 项目配置
├── <skill-name>/             # 每个 Skill 独立目录
│   └── skill.md              # Skill 内容文件（Markdown + frontmatter）
├── _headers                  # Cloudflare Pages 响应头配置
├── index.html                # 市场首页
├── manifest.json             # Skill 清单（名称与版本）
├── wrangler.jsonc            # Cloudflare Workers 配置
└── README.md                 # 本文件
```

## 什么是 Skill？

Skill 是 Claude Code 的功能扩展，定义了一组触发词和对应的知识内容。当用户在对话中提到触发词时，Claude Code 会自动加载对应的 Skill 内容来增强回答能力。

这个项目中的 Skill 专注于 **Minecraft 服务器管理插件** 的使用指南，例如 CoreProtect、LuckPerms、WorldEdit 等。

## 如何创建一个新的 Skill

### 1. 创建 Skill 目录与文件

在项目根目录下创建一个新目录，目录名即为 Skill 的标识符（使用小写字母和连字符）。在其中创建 `skill.md` 文件：

```
mkdir <skill-name>
```

### 2. 编写 Frontmatter

`skill.md` 必须以 YAML frontmatter 开头，定义 Skill 的元数据：

```yaml
---
name: "<skill-name>"
description: "简短描述，说明此 Skill 的用途"
triggers:
  - "触发词1"
  - "触发词2"
  - "触发词3"
auto_trigger: true
source: "<目录名>"
author: "FancyHelper Team"
version: "1.0.0"
categories:
  - "分类1"
  - "分类2"
---
```

| 字段 | 说明 |
|------|------|
| `name` | Skill 名称，应与目录名一致 |
| `description` | 一行简短描述，在市场上展示 |
| `triggers` | 触发词列表，用户在对话中提到这些词时会自动加载此 Skill |
| `auto_trigger` | 是否允许自动触发，通常设为 `true` |
| `source` | 源码目录名 |
| `author` | 作者信息 |
| `version` | 语义化版本号 |
| `categories` | 分类标签，用于组织 Skill |

### 3. 编写 Skill 内容

Frontmatter 之后，使用 Markdown 编写 Skill 的具体知识内容。内容应清晰、结构化，便于 Claude Code 理解和使用。

参考现有 Skill（如 [coreprotect/skill.md](coreprotect/skill.md)）的写法：

- 使用 `##` 二级标题划分章节
- 命令和代码示例使用代码块
- 表格用于展示参数说明
- 保持内容聚焦，只包含与此 Skill 相关的信息

### 4. 注册到 Manifest

在 `manifest.json` 的 `skills` 对象中添加新条目：

```json
{
  "skills": {
    "<skill-name>": { "version": "1.0.0" }
  }
}
```

## 开发规范

### 命名规范

- 目录名使用小写字母和连字符：`coreprotect`、`house-builder`、`nbt-format`
- 触发词应覆盖中英文常用关键词
- 版本号遵循 [SemVer](https://semver.org/) 规范

### 内容规范

- **准确性**：确保所有命令、参数和说明经过验证
- **版本说明**：如果内容依赖特定版本（如 Minecraft 版本），在文中明确标注
- **安全提示**：危险操作（如回档、删除）必须附带注意事项
- **示例丰富**：提供足够的实际使用示例
- **保持聚焦**：每个 Skill 只关注一个插件或一个主题

### 发布流程

1. 创建 Skill 目录和 `skill.md`
2. 更新 `manifest.json` 添加版本号
3. 提交 PR 合并到 `main` 分支
4. Cloudflare Workers 自动部署（基于项目配置自动生效）

## 本地开发

项目使用 Cloudflare Workers 部署为静态站点，无构建步骤。

```bash
# 安装依赖（首次）
npm install

# 本地预览
npx wrangler pages dev .

# 部署
npx wrangler pages deploy .
```

## 部署架构

项目通过 Cloudflare Workers + Pages 部署：

- **静态资源**：`index.html`、`manifest.json`、各 Skill 的 `skill.md` 作为静态文件托管
- **响应头**：`_headers` 确保 `.md` 文件以 `text/plain` 而非 `text/html` 返回，避免浏览器渲染 Markdown
- **首页**：`index.html` 从 `manifest.json` 读取 Skill 列表并生成导航页面

## License

本项目基于 [The Unlicense](LICENSE) 开源，属于公共领域。
