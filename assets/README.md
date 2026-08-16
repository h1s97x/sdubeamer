# 资源目录

本目录存放 SDUBeamer 模板所需的外部资源文件。

## `sdu-logo.jpg`

山东大学校徽（JPEG 格式）。

> 模板封面页会自动从 `assets/sdu-logo.jpg` 加载校徽。如需更换，将新的校徽文件命名为 `sdu-logo.jpg` 替换本文件即可，无需修改代码。

### 使用说明

1. 校徽文件默认放在本目录，命名为 `sdu-logo.jpg`
2. 模板封面页通过 `\includegraphics` 加载该文件
3. 若需要更换为其他格式（如 `.pdf` / `.png`），可修改 `logo` 选项指定文件路径：
   ```latex
   \usepackage[logo=assets/my-logo.png]{sdubeamer}
   ```

### 模板中的引用方式

封面页模板通过以下方式引用校徽：

```latex
\includegraphics[height=2.5cm]{assets/sdu-logo.jpg}
```

编译时需要将仓库根目录加入 `TEXINPUTS`，例如：

```bash
cd examples && TEXINPUTS=..:$TEXINPUTS xelatex demo.tex
```
