# 常见问题（FAQ）

## 编译报错

### 1. 使用 `pdflatex` 编译报错

模板依赖 `ctex`/`xeCJK` 支持中文，**不能**使用 `pdflatex` 或 `latex` 引擎。

**解决**：改用 `xelatex` 编译：

```bash
xelatex main.tex
xelatex main.tex   # 建议执行两遍
```

### 2. 提示找不到 `sdubeamer.sty`

模板宏包未被编译程序找到。**解决**：

- 确认 `sdubeamer.sty` 与你的 `.tex` 文件在同一目录，或已通过 `TEXINPUTS` 指定搜索路径：
  ```bash
  TEXINPUTS=..:$TEXINPUTS xelatex main.tex
  ```
- 若模板在子目录（如 `src/`），将对应目录加入 `TEXINPUTS`：
  ```bash
  TEXINPUTS=src/:$TEXINPUTS xelatex main.tex
  ```

### 3. 提示缺少 `ctex` 或 `xeCJK` 宏包

请安装/更新 TeX 发行版：

- **TeX Live**：使用完整版安装（含 `ctex`），或运行 `tlmgr install ctex xeCJK fandol`。
- **MiKTeX**：在包管理器中安装 `ctex`、`xeCJK` 包。

### 4. 提示缺少中文字体（fontspec / fandol）

默认使用 `fandol` 字体集（随 TeX Live 完整版内置）。若缺失：

- **TeX Live 完整版**：fandol 已内置，无需处理。
- **其他发行版**：安装 `fandol` 字体包，或改用系统字体集：
  ```latex
  \usepackage[fontset=windows]{sdubeamer}  % Windows
  \usepackage[fontset=mac]{sdubeamer}      % macOS
  ```

### 5. 编译后页码显示异常或交叉引用错误

Beamer 模板内部含交叉引用，**需要执行两遍**编译：

```bash
xelatex main.tex
xelatex main.tex
```

或使用 `latexmk` 自动处理：

```bash
latexmk -xelatex -cd main.tex
```

## 使用问题

### 6. 封面页没有显示校徽

封面页默认从 `assets/sdu-logo.jpg` 加载校徽。若未显示：

- 确认 `assets/` 目录与 `sdu-logo.jpg` 存在，且编译时能被找到（`TEXINPUTS`）。
- 或通过 `logo` 选项指定校徽路径：
  ```latex
  \usepackage[logo=path/to/logo.png]{sdubeamer}
  ```

### 7. 想更换校徽

直接替换 `assets/sdu-logo.jpg` 即可（保持文件名不变），无需修改代码。

### 8. 想自定义页脚学校名

- 通过 `school` 选项全局设置：
  ```latex
  \usepackage[school=山东大学 数学学院]{sdubeamer}
  ```
- 或在正文中临时覆盖：
  ```latex
  \sdufooter{山东大学 XX 学院}
  ```

### 9. 中文段落中英文与中文间距问题

模板已基于 `ctex` 自动处理中西文间距。若仍出现间距异常，请确认使用 `xelatex` 编译，且 `ctex` 版本较新。

### 10. 在线平台（Overleaf / TeXPage）编译提示缺少宏包

在线平台默认使用完整 TeX Live，通常无需额外安装。若提示缺少包，可在项目设置中「切换编译器」为 `XeLaTeX`，并确认模板文件位置。

## 其他

### 11. 如何参与贡献？

请阅读 [CONTRIBUTING.md](../CONTRIBUTING.md) 了解贡献流程。

### 12. 如何报告问题或建议新功能？

请使用仓库的 [Issue 模板](https://cnb.cool/h1s97x/sdubeamer/-/issues/new) 提交：

- Bug 报告：使用 **Bug Report** 模板
- 新功能建议：使用 **Feature Request** 模板

### 13. 模板有版本号吗？

有。请查看仓库 [Releases](https://cnb.cool/h1s97x/sdubeamer/-/releases) 页面获取最新版本标签。
