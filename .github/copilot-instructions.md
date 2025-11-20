# Commit 规范指南

本项目遵循约定式提交（Conventional Commits）规范，以保持提交历史的清晰和一致性。

## 提交消息格式

```text
<type>: <subject>

[optional body]
```

### Type（类型）

提交类型必须是以下之一：

- **feat**: 新功能（feature）
- **ci**: CI/CD 配置和脚本的变更
- **docs**: 文档变更
- **chore**: 构建过程或辅助工具的变更，不影响源代码

### Subject（主题）

- 使用中文简要描述变更内容
- 不超过 50 个字符
- 不以句号结尾
- 使用祈使句，例如："添加"而不是"添加了"

### Body（正文）

可选的详细描述，用于说明：

- 变更的具体内容
- 变更的原因
- 与之前行为的对比

正文应该：

- 使用项目符号列表（-）
- 每条说明一个要点
- 简洁明了

## 示例

### 基础示例（仅主题）

```text
chore: 重命名 lint 为 test
```

```text
chore: 删除 hadolint 的 lint 检查
```

### 完整示例（包含正文）

```text
ci: 添加 Dockerfile 检查和测试工作流
- 使用 Hadolint 进行 Dockerfile 语法检查
- 在 PR 和推送时自动构建测试镜像
- 验证关键工具（Node.js、Git、Zsh）是否正确安装
- 仅在 Dockerfile 或工作流文件变更时触发
```

```text
feat: 初始化开发容器项目
- 添加基于 Ubuntu 22.04 的 Dockerfile
- 集成 zsh + oh-my-zsh
- 安装 nvm 和 Node.js 22
- 添加项目文档 README.md
- 配置 GitHub Actions 自动构建和发布镜像
- 添加 .gitignore 文件
```

```text
docs: 更新 README，添加 Dev Container 使用说明
- 补充配合 VS Code Dev Containers 插件使用的说明
- 添加 .devcontainer/devcontainer.json 配置示例
- 强调 CI/CD 加速和节省费用的优势
- 优化使用方法章节结构
```

## 最佳实践

1. **提交粒度**：每个提交应该是一个逻辑上完整的变更单元
2. **原子性**：一次提交只做一件事
3. **可读性**：提交信息应该让其他开发者快速理解变更内容
4. **正文使用**：当变更较复杂或需要解释时，添加正文说明
5. **语言一致性**：本项目统一使用中文编写提交信息

## Type 使用场景

- `feat`: 添加新功能、新特性
- `ci`: 修改 GitHub Actions 工作流、Docker 构建配置等
- `docs`: 更新 README、添加文档、修改注释等
- `chore`: 重命名文件、删除无用代码、调整项目结构等

## 不推荐的做法

❌ 提交信息过于简单

```text
update
fix bug
修改
```

❌ 混合多种类型的变更

```text
feat: 添加新功能并修复 bug 还更新了文档
```

❌ 提交信息与实际变更不符

```text
docs: 更新文档
（实际修改了代码）
```

## 版本标记

重要版本可以使用 Git tag 进行标记：

```bash
git tag -a 1.0.0-beta.1 -m "发布 beta 版本"
```

格式：`<major>.<minor>.<patch>[-<pre-release>]`
