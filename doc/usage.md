# 使用指南

本指南介绍 SDUBeamer 的使用方法，包括基本用法、字体依赖、可选参数与常用排版元素。

## 快速上手

在导言区加载模板：

```latex
\documentclass[aspectratio=169]{beamer}
\usepackage[color=blue, degree=master]{sdubeamer}
```

一个最简可编译文档：

```latex
\documentclass[aspectratio=169]{beamer}
\usepackage[color=blue]{sdubeamer}

\title{答辩标题}
\author{姓名}
\institute{山东大学 XXX 学院}
\date{2025年6月}

\begin{document}
\begin{frame}
  \titlepage
\end{frame}

\section{引言}
\begin{frame}{章节内容}
  正文内容
\end{frame}
\end{document}
```

编译方式（推荐）：

```bash
TEXINPUTS=..:$TEXINPUTS xelatex main.tex   # 在项目根目录执行
xelatex main.tex                            # 建议执行两遍以解决交叉引用
```

## 字体依赖

模板默认基于 `ctex` 的 **fandol 字体集**，随 TeX Live 完整版内置，**跨平台免安装**，开箱即用。

如需使用系统自带字体集，可通过 `fontset` 选项覆盖：

| fontset 值 | 适用系统 | 说明 |
|-----------|---------|------|
| `fandol`（默认） | 全平台 | 免安装，随 TeX Live 内置 |
| `windows` | Windows | 使用系统宋体/黑体等 |
| `mac` | macOS | 使用苹方/宋体等 |
| `ubuntu` | Linux | 使用思源/文泉驿等 |

```latex
\usepackage[fontset=windows]{sdubeamer}  % Windows 系统自带字体
\usepackage[fontset=mac]{sdubeamer}      % macOS 系统自带字体
```

> ⚠️ 由于依赖 `xeCJK`/`ctex`，**必须使用 `xelatex` 编译**，不能使用 `pdflatex`。

## 可选参数说明

模板通过 `\usepackage[选项1, 选项2]{sdubeamer}` 传入配置，支持以下参数：

| 参数 | 默认值 | 可选值 | 说明 |
|------|--------|--------|------|
| `chinese` | `true` | `true` / `false` | 是否启用中文支持（`false` 为纯英文场景） |
| `fontset` | `fandol` | `fandol` / `windows` / `mac` / `ubuntu` | `ctex` 字体集 |
| `color` | `blue` | `blue` / `red` / `cyan` / `green` / `purple` | 主题色 |
| `school` | `山东大学` | 任意字符串 | 页脚显示的学校名 |
| `enname` | `Shandong University` | 任意字符串 | 封面页英文校名 |
| `logo` | `assets/sdu-logo.jpg` | 文件路径 | 封面页校徽文件路径 |
| `degree` | `master` | `undergrad` / `master` / `doctor` | 答辩类型 |

### 使用示例

```latex
% 关闭中文支持（纯英文场景）
\usepackage[chinese=false]{sdubeamer}

% 自定义主题色
\usepackage[color=green]{sdubeamer}

% 自定义页脚学校名
\usepackage[school=山东大学 数学学院]{sdubeamer}

% 自定义封面英文校名
\usepackage[enname=School of Mathematics, Shandong University]{sdubeamer}

% 自定义校徽文件路径
\usepackage[logo=assets/my-logo.png]{sdubeamer}

% 指定答辩类型
\usepackage[degree=doctor]{sdubeamer}
```

## 常用排版元素

### 标题页

```latex
\title{论文标题}
\subtitle{副标题}
\author{张三}
\institute{山东大学 计算机科学与技术学院}
\date{2025 年 6 月}
\begin{frame}
  \titlepage
\end{frame}
```

封面页自动展示校徽、学校中英文全称、学位类型（依据 `degree` 选项）、论文标题、作者、学院与日期。

### 章节页

```latex
\section{第一章}
\begin{frame}
  \sectionpage
\end{frame}
```

章节页会显示当前章节名，页眉左侧同步显示章节名。

### 页脚学校名

默认页脚学校名为「山东大学」，可通过 `school` 选项设置，也可在正文中临时覆盖：

```latex
\sdufooter{山东大学 XX 学院}
```

### 列表 / 彩色块 / 图注 / 超链接

模板已内置 SDU 品牌色排版：

- **列表**：`itemize` / `enumerate` 逐级采用 `sdu@primary`/`sdu@secondary`/`sdu@accent` 递进配色。
- **彩色块**：`block`/`alertblock`/`exampleblock` 标题使用实心底，正文为浅色底；`theorem` 标题采用 SDU 主色。
- **图/表标题**：`caption` 名称用 SDU 主色加粗。
- **超链接**：链接 / 聚焦 / 引用分别采用辅助色与强调色，`colorlinks` 已开启。

```latex
\begin{block}{普通块}
  正文内容
\end{block}

\begin{alertblock}{警示块}
  需要强调的内容
\end{alertblock}

\begin{exampleblock}{示例块}
  示例或结论
\end{exampleblock}
```

### 分栏

```latex
\begin{columns}
  \begin{column}{0.48\textwidth}
    左侧内容
  \end{column}
  \begin{column}{0.48\textwidth}
    右侧内容
  \end{column}
\end{columns}
```

## 完整示例

完整的可编译示例见 [`examples/demo.tex`](../examples/demo.tex)，覆盖标题页、章节页、内容帧、分栏、列表、数学公式、代码块、引用、表格等常见元素。
