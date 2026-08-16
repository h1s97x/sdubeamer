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
\usepackage[color=blue, degree=master]{sdubeamer}   % 默认已启用中文支持

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

## 页眉 / 页脚

模板内置了定制的页眉与页脚，体现山东大学视觉识别：

- **页眉**：左侧显示当前章节名（`\section`），下方为一条主题色细线。
- **页脚**：顶部为一条主题色细线，左侧显示学校名，右侧显示页码（`当前帧 / 总帧数`）。

## 列表 / 彩色块 / 图注 / 超链接

模板已内置与 SDU 品牌色一致的排版样式：

- **列表**：`itemize`/`enumerate` 各级项目符号与编号逐级采用 `sdu@primary`/`sdu@secondary`/`sdu@accent` 递进配色。
- **彩色块**：`block`/`alertblock`/`exampleblock` 标题使用实心底（主色/强调色/辅助色），正文为浅色底呼应品牌色；`theorem` 等定理标题采用 SDU 主色。
- **图/表标题**：`caption` 名称（“图/表”字样）用 SDU 主色加粗，说明正文为黑色小字。
- **超链接**：链接 / 聚焦 / 引用分别采用辅助色与强调色，`colorlinks` 已开启。

## 页眉 / 页脚

模板内置了定制的页眉与页脚，体现山东大学视觉识别：

- **页眉**：左侧显示当前章节名（`\section`），下方为一条主题色细线。
- **页脚**：顶部为一条主题色细线，左侧显示学校名，右侧显示页码（`当前帧 / 总帧数`）。

页脚学校名默认为「山东大学」，可通过 `school` 选项自定义，或在正文中用 `\sdufooter{}` 临时覆盖：

```latex
% 通过 school 选项设置页脚学校名
\usepackage[school=山东大学 数学学院]{sdubeamer}

% 或在正文中临时覆盖
\sdufooter{山东大学 XX 学院}
```

## 封面页设计

封面页采用**学位论文答辩专用布局**，包含以下元素：

- **校徽**：默认从 `assets/sdu-logo.jpg` 加载（需将仓库根目录加入 `TEXINPUTS`）
- **学校中英文全称**：中文名默认为「山东大学」，英文名默认为「Shandong University」
- **学位类型**：根据 `degree` 选项显示「本科毕业论文答辩 / 硕士学位论文答辩 / 博士学位论文答辩」
- **论文标题**、作者、学院、日期等信息

> ℹ️ 仓库内的 `assets/sdu-logo.jpg` 为山东大学校徽，模板封面页会自动加载。
> 如需更换校徽，直接替换该文件或通过 `logo` 选项指定路径，详见 [`assets/README.md`](assets/README.md)。

## 可选选项

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

% 指定答辩类型（undergrad / master / doctor）
\usepackage[degree=doctor]{sdubeamer}
```

- `chinese`（默认开启）：接入 `ctex` 中文排版
- `fontset`（默认 `fandol`）：指定 `ctex` 字体集
- `color`（默认 `blue`）：主题色，可选 `blue` / `red` / `cyan` / `green` / `purple`
- `school`（默认 `山东大学`）：页脚显示的学校名
- `enname`（默认 `Shandong University`）：封面页英文校名
- `logo`（默认 `assets/sdu-logo.jpg`）：封面页校徽文件路径
- `degree`（默认 `master`）：答辩类型，可选 `undergrad` / `master` / `doctor`

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
