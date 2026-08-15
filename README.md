# SDUBeamer

山东大学 Beamer 幻灯片模板 | Shandong University Beamer Theme

## 项目简介

山东大学学位论文答辩幻灯片 Beamer 主题。

## 支持的类型

- 本科生毕业设计答辩
- 硕士研究生答辩
- 博士研究生答辩

## 快速开始

```latex
\documentclass{beamer}
\usepackage[color=blue]{sdubeamer}   % 可选 blue(默认)/red/cyan/green/purple

\begin{document}

\title{答辩标题}
\author{姓名}
\institute{山东大学 XXX 学院}
\date{2025年6月}

\begin{frame}
  \titlepage
\end{frame}

\section{第一部分}
\begin{frame}
  \sectionpage
\end{frame}

\begin{frame}{章节标题}
  内容
\end{frame}

\end{document}
```

## 相关仓库

本项目属于山东大学 LaTeX 方案的一部分，各仓库分工如下。完整的仓库关系见 [REPOSITORIES.md](REPOSITORIES.md)。

| 仓库 | 角色 | 说明 |
|------|------|------|
| [sdutex](https://cnb.cool/h1s97x/sdutex) | 核心包 | 论文核心代码（`sduthesis.cls` 等） |
| [sduthesis](https://cnb.cool/h1s97x/sduthesis) | 论文模板 | 可直接使用的毕业论文模板 |
| [sdubeamer](https://cnb.cool/h1s97x/sdubeamer) | 幻灯片模板 | 本仓库 - 答辩 Beamer 主题 |

## 许可证

本项目采用 [LaTeX Project Public License v1.3c](LICENSE)（LPPL v1.3+）。

详见 [LICENSE](LICENSE) 文件。
