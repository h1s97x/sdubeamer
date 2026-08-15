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
\usepackage[color=blue]{sdubeamer}   % 默认已启用中文支持；可选 blue(默认)/red/cyan/green/purple

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

## 编译方法

本模板内置中文支持（基于 `ctex`），**推荐使用 `xelatex` 编译**：

```bash
xelatex main.tex
xelatex main.tex   # 建议执行两遍以解决交叉引用
```

> ⚠️ 由于依赖 `xeCJK`/`ctex`，**不能**使用默认的 `pdflatex` 或 `latex` 引擎编译含中文的文档。

## 字体依赖

模板默认采用 `ctex` 的 **fandol 字体集**（随 TeX Live 完整版内置，跨平台免安装），因此无需额外安装中文字体即可编译。

如需使用系统自带字体集，可在加载时覆盖 `fontset` 选项：

```latex
% Windows：使用系统宋体/黑体等
\usepackage[fontset=windows]{sdubeamer}

% macOS：使用苹方/宋体等
\usepackage[fontset=mac]{sdubeamer}
```

支持的字体集包括 `fandol`（默认）、`windows`、`mac`、`ubuntu` 等，详见 [`ctex` 宏包文档](https://ctan.org/pkg/ctex)。

## 可选选项

```latex
% 关闭中文支持（纯英文场景）
\usepackage[chinese=false]{sdubeamer}

% 自定义主题色
\usepackage[color=green]{sdubeamer}
```

- `chinese`（默认开启）：接入 `ctex` 中文排版
- `fontset`（默认 `fandol`）：指定 `ctex` 字体集
- `color`（默认 `blue`）：主题色

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
