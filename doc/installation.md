# 安装说明

SDUBeamer 是一个独立的 Beamer 主题宏包，安装方式灵活，可按需选择以下任意一种。

## 方式一：直接复制（推荐，快速上手）

从仓库下载以下文件到你的项目目录：

```
src/sdubeamer.sty
assets/sdu-logo.jpg
```

然后在你的 `.tex` 文件中引用：

```latex
\documentclass{beamer}
\usepackage[color=blue]{sdubeamer}
\begin{document}
...
\end{document}
```

若将模板放在子目录中，请确保编译时可被 `TEXINPUTS` 找到，例如模板放在 `theme/` 下：

```bash
xelatex -interaction=nonstopmode -shell-escape main.tex
# 或在编译命令中指定 TEXINPUTS
TEXINPUTS=theme/:$TEXINPUTS xelatex main.tex
```

## 方式二：通过 Release 附件安装

从仓库的 [Releases](https://cnb.cool/h1s97x/sdubeamer/-/releases) 页面下载最新发布包（包含 `sdubeamer.sty`、`examples/`、`assets/`、`README.md`、`LICENSE`），解压后按方式一使用即可。

## 方式三：克隆仓库

```bash
git clone https://cnb.cool/h1s97x/sdubeamer.git
cd sdubeamer
```

编译示例：

```bash
cd examples && TEXINPUTS=..:../src:$TEXINPUTS xelatex demo.tex
TEXINPUTS=..:../src:$TEXINPUTS xelatex demo.tex   # 建议执行两遍以解决交叉引用
```

## 方式四：在线平台（Overleaf / TeXPage）

1. 下载本仓库 ZIP 包并解压
2. 在 Overleaf / TeXPage 中「新建项目 → 上传项目」，将解压后的目录上传
3. 将 `src/`、`examples/`、`assets/` 保持在仓库根目录下，确认模板可通过 `TEXINPUTS` 被找到

> 💡 在线平台默认会递归搜索子目录中的宏包，通常无需额外配置。若编译提示找不到 `sdubeamer.sty`，可将 `src/sdubeamer.sty` 复制到项目根目录后再编译。

## 环境要求

- **TeX 发行版**：推荐 [TeX Live 2023+](https://tug.org/texlive/)（完整版内置 `ctex` 与 `fandol` 字体集）；[MiKTeX](https://miktex.org/) 亦可，需联网自动安装缺失宏包。
- **编译引擎**：`xelatex`（必须）。模板依赖 `ctex`/`xeCJK`，**不兼容** `pdflatex` 或 `latex` 引擎。
- **可选工具**：`latexmk`（推荐，用于自动编译多次循环）、`make`（用于自动化脚本）。

## 验证安装

在项目目录下新建 `test.tex`：

```latex
\documentclass{beamer}
\usepackage[color=blue]{sdubeamer}
\begin{document}
\begin{frame}{安装验证}
  \begin{block}{成功}
    如果你能编译出本页，说明 SDUBeamer 已安装成功！
  \end{block}
\end{frame}
\end{document}
```

使用 `xelatex` 编译，若无报错并输出 PDF，则安装成功。
