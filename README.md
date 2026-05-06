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
\usepackage{sdubeamer}

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

| 仓库 | 说明 |
|------|------|
| [sduthesis](https://github.com/h1s97x/sduthesis) | 论文模板 |
| [sduttex](https://github.com/h1s97x/sduttex) | 核心包 |
| [sdubeamer](https://github.com/h1s97x/sdubeamer) | 本仓库 - 幻灯片模板 |

## 许可证

LaTeX Project Public License v1.3+
