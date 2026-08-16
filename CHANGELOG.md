# Changelog

本项目遵循 [语义化版本](https://semver.org/lang/zh-CN/)（Semantic Versioning）。所有显著的变更都会记录在本文件中。

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.0.0/)。

## [Unreleased]

### 新增

- 目录结构优化：拆分 `src/`、`examples/`、`doc/`、`assets/` 目录
- 新增 `doc/installation.md`（安装说明）
- 新增 `doc/usage.md`（使用指南）
- 新增 `doc/faq.md`（常见问题）
- 新增 `CONTRIBUTING.md`（贡献指南）
- 新增 `CHANGELOG.md`（版本记录）

### 变更

- `sdubeamer.sty` 从仓库根目录移至 `src/` 目录
- 更新 README 以反映新的目录结构与安装方式
- 更新 CI / Release 附件中的模板路径引用

---

## [1.0.0] - 2026-08-16

首个正式发布版本。

### 新增

- SDUBeamer Beamer 幻灯片主题宏包 `sdubeamer.sty`
- 支持本科 / 硕士 / 博士答辩场景
- 基于 `ctex` 的中文支持（`fandol` 字体集跨平台免安装）
- 内置山东大学视觉识别：校徽封面、品牌色页眉/页脚、列表/彩色块/图注/超链接配色
- 可编译示例 `examples/demo.tex`
- CNB 流水线（`.cnb.yml`）：GitHub 双向同步、PR/Issue 自动分配、Tag 自动发布 Release
