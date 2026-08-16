# 贡献指南（CONTRIBUTING）

感谢你愿意为 SDUBeamer 贡献代码或文档！请遵循以下流程。

## 目录结构

```
├── src/                    # 模板宏包源码
│   └── sdubeamer.sty       # 核心 Beamer 主题宏包
├── examples/               # 可编译示例
│   └── demo.tex
├── doc/                    # 文档
│   ├── installation.md     # 安装说明
│   ├── usage.md            # 使用指南（字体/参数/排版）
│   └── faq.md              # 常见问题
├── assets/                 # 外部资源（校徽等）
│   └── sdu-logo.jpg
├── .cnb.yml                # CNB 流水线配置
├── .github/                # GitHub/CNB 平台配置
│   ├── ISSUE_TEMPLATE/     # Issue 模板
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── CODEOWNERS
├── README.md               # 项目首页
├── REPOSITORIES.md         # 仓库关系说明
└── LICENSE                 # LPPL v1.3c
```

## 如何贡献

### 1. 报告 Bug / 建议功能

- 请先搜索 [Issues](https://cnb.cool/h1s97x/sdubeamer/-/issues) 确认没有重复问题。
- 报告 Bug 使用 **Bug Report** 模板，尽量提供最小可复现示例与环境信息。
- 建议功能使用 **Feature Request** 模板。

### 2. 提交代码

推荐流程：

1. **Fork 仓库** 并克隆到本地。
2. 基于 `main` 新建功能分支：
   ```bash
   git checkout -b feat/xxx
   ```
3. 进行修改，**保持改动聚焦**（一个 PR 解决一个问题）。
4. 提交前本地验证：
   - 修改 `src/sdubeamer.sty` 后，务必用 `xelatex` 编译 `examples/demo.tex` 确认无报错。
   - 示例仍可正常编译。
5. 提交并推送分支，然后创建 Pull Request。

### 3. 提交信息规范

推荐使用约定式提交（Conventional Commits）：

| 类型 | 用途 | 示例 |
|------|------|------|
| `feat` | 新功能 | `feat: 新增 XX 主题色` |
| `fix` | 修复 | `fix: 修复页脚页码错位` |
| `docs` | 文档 | `docs: 补充常见问题` |
| `refactor` | 重构 | `refactor: 重构封面页布局` |
| `chore` | 杂项 | `chore: 更新流水线配置` |
| `ci` | CI | `ci: 优化同步任务` |

### 4. Pull Request 要求

- 关联相关 Issue（如 `Closes #12`）。
- 勾选 PR 模板中的检查清单。
- 修改 `.sty` 时需保证 `xelatex` 编译通过。
- 行为变化时同步更新 README 与 `doc/` 文档。

### 5. 代码风格

- `.sty`：保持与现有宏包一致的分节注释与缩进风格。
- Markdown：保持中文文档一致的语气与格式。
- 涉及新选项时，需同步补充 `doc/usage.md` 中的参数表格。

## 开发注意事项

- **中文支持**：模板基于 `ctex`，修改后务必用 `xelatex` 验证中文场景。
- **跨平台**：默认字体为 `fandol`（跨平台免安装），新增依赖需评估兼容性。
- **向后兼容**：新增选项应有合理默认值，避免破坏现有用户配置。

## 发布流程（维护者）

1. 合并待发布改动到 `main`。
2. 创建版本标签（如 `v1.0.0`），遵循 [语义化版本](https://semver.org/lang/zh-CN/)：
   - 破坏性变更：`v2.0.0`
   - 新增向后兼容功能：`v1.1.0`
   - Bug 修复：`v1.0.1`
3. 打 tag 后，CNB 流水线（`.cnb.yml` 中 `tag_push`）会自动创建 Release 并上传模板附件。

## 行为准则

- 保持友善与专业，尊重他人。
- 关注技术问题本身，避免无关讨论。
