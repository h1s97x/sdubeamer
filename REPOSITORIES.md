# 仓库关系总览

本页梳理 `h1s97x` 名下与山东大学 LaTeX 方案相关的仓库及其协作关系，便于快速定位所需代码。

## 仓库一览

| 仓库 | 角色 | 主要交付物 | 典型用途 |
|------|------|-----------|----------|
| [**sdutex**](https://cnb.cool/h1s97x/sdutex) | 核心包 | `sduthesis.cls`、`sdutex.sty`、`sduthesis.bst` | 底层核心代码，供上层模板复用 |
| [**sduthesis**](https://cnb.cool/h1s97x/sduthesis) | 论文模板 | 可直接编译的毕业论文模板 | 本科 / 硕士 / 博士论文写作 |
| [**sdubeamer**](https://cnb.cool/h1s97x/sdubeamer) | 幻灯片模板 | `src/sdubeamer.sty` | 答辩 / 会议 / 汇报 Beamer 幻灯片 |

## 关系结构

```
            ┌─────────────────────────────────────┐
            │            sdutex (核心包)            │
            │   sduthesis.cls · sdutex.sty · bst   │
            │        —— 公共核心代码仓库 ——          │
            └───────────────┬─────────────────────┘
                            │ 提供核心能力
              ┌─────────────┴─────────────┐
              ▼                           ▼
┌───────────────────────┐   ┌───────────────────────┐
│   sduthesis (论文模板)  │   │   sdubeamer (幻灯片)    │
│  基于核心包构建的完整模板  │   │  独立的 Beamer 主题     │
│  内核 + 模块插件化架构    │   │  复用山大学术视觉风格    │
└───────────────────────┘   └───────────────────────┘
```

## 各仓库定位说明

### sdutex —— 核心包（底层）

山东大学 LaTeX 方案的**核心代码仓库**，沉淀可复用的基础能力：

- `sduthesis.cls` —— 学位论文文档类
- `sdutex.sty` —— 工具宏包（通用排版辅助）
- `sduthesis.bst` —— 参考文献样式（GB/T 7714-2015）

它不面向最终用户直接使用，而是作为**公共基础层**，被上层模板引用。

### sduthesis —— 论文模板（面向用户）

基于 `sdutex` 核心包构建的**可直接使用的毕业论文模板**，采用“内核 + 模块”插件化架构：

- 通过 `\SDUSetup{}` 集中配置论文信息与样式
- 通过模块（`undergraduate` / `master` / `blindreview`）支持不同学位类型与盲审
- 一键导入 Overleaf / TeXPage 在线编译

对普通论文作者而言，这是**最常用的入口仓库**。

### sdubeamer —— 幻灯片模板（面向用户）

独立维护的 **Beamer 幻灯片主题**，用于学位论文答辩、学术会议、工作汇报等场景：

- 提供 `src/sdubeamer.sty` 宏包，`\usepackage{sdubeamer}` 即可使用
- 复用山东大学校色（`sdu@primary` 等）与学术视觉风格
- 与论文模板（sduthesis）共享品牌视觉，形成完整“论文 + 答辩”方案

## 使用建议

| 需求场景 | 应使用仓库 |
|----------|-----------|
| 写作毕业论文（本科/硕士/博士） | `sduthesis` |
| 开发/维护论文核心排版能力 | `sdutex` |
| 制作答辩/会议 Beamer 幻灯片 | `sdubeamer` |

## 命名说明

> 曾误写作 `sduttex`，本仓库正式名称为 **`sdutex`**（SDUT + eX，无多余 `t`）。

## 许可证

各仓库均采用 [LaTeX Project Public License (LPPL)](https://www.latex-project.org/lppl/) 协议发布。
