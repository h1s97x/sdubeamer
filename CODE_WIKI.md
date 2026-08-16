# SDUBeamer Code Wiki

> 山东大学 Beamer 幻灯片模板 | Shandong University Beamer Theme Code Wiki

---

## 目录

1. [项目概览](#1-项目概览)
2. [项目整体架构](#2-项目整体架构)
3. [目录结构说明](#3-目录结构说明)
4. [核心模块与关键代码](#4-核心模块与关键代码)
5. [配置选项与参数系统](#5-配置选项与参数系统)
6. [依赖关系分析](#6-依赖关系分析)
7. [项目运行与编译](#7-项目运行与编译)
8. [CI/CD 与发布流程](#8-cicd-与发布流程)
9. [仓库生态与关联项目](#9-仓库生态与关联项目)
10. [贡献指南与开发规范](#10-贡献指南与开发规范)
11. [版本历史](#11-版本历史)
12. [常见问题排错](#12-常见问题排错)

---

## 1. 项目概览

### 1.1 项目定位

**SDUBeamer** 是面向山东大学学位论文答辩场景的 Beamer 幻灯片主题模板。它提供标准化的学术视觉风格（校徽、品牌色、页眉页脚等），支持本科、硕士、博士三种答辩类型，内置中文支持（基于 ctex），跨平台免安装即可编译。

### 1.2 核心特性

| 特性 | 说明 |
|------|------|
| **学位类型支持** | 本科生毕业设计答辩 / 硕士研究生答辩 / 博士研究生答辩 |
| **中文支持** | 基于 `ctex` + `xeCJK`，默认 `fandol` 字体集（跨平台免安装） |
| **主题色系统** | 5 套可选品牌色：blue(默认) / red / cyan / green / purple |
| **定制页面模板** | 封面页（校徽+校名+学位类型+标题）、章节页独立设计 |
| **视觉元素定制** | 页眉、页脚、列表、彩色块、图注、超链接统一品牌配色 |
| **编译方式** | 必须使用 `xelatex` 引擎，支持 `latexmk` 自动化 |

### 1.3 技术栈

- **语言**: LaTeX (LaTeX2e)
- **文档类**: Beamer
- **核心依赖**: ctex, xeCJK, graphicx, expl3, l3keys2e
- **编程范式**: LaTeX3 (expl3) + 传统 LaTeX2e 混合
- **许可证**: LPPL v1.3c (LaTeX Project Public License)

---

## 2. 项目整体架构

### 2.1 架构总览

SDUBeamer 采用**单宏包架构**，所有功能集中在一个 `.sty` 文件中，通过模块化的代码分节组织。

```
用户文档 (.tex)
    │
    ▼
┌──────────────────────────────────────────────────┐
│                sdubeamer.sty (核心宏包)           │
│  ┌────────────┐ ┌────────────┐ ┌───────────────┐ │
│  │ 选项解析   │ │ 中文支持   │ │ 颜色定义系统  │ │
│  │ (l3keys)   │ │ (ctex)     │ │ (5套主题色)   │ │
│  └────────────┘ └────────────┘ └───────────────┘ │
│  ┌────────────┐ ┌────────────┐ ┌───────────────┐ │
│  │ Beamer主题 │ │ 封面页模板 │ │ 章节页模板    │ │
│  │ 基础设置   │ │            │ │               │ │
│  └────────────┘ └────────────┘ └───────────────┘ │
│  ┌────────────┐ ┌────────────┐ ┌───────────────┐ │
│  │ 页眉模板   │ │ 页脚模板   │ │ 帧标题模板    │ │
│  └────────────┘ └────────────┘ └───────────────┘ │
│  ┌────────────┐ ┌────────────┐ ┌───────────────┐ │
│  │ 列表样式   │ │ 块/定理    │ │ 图注/超链接   │ │
│  └────────────┘ └────────────┘ └───────────────┘ │
└──────────────────────────────────────────────────┘
    │
    ▼
外部资源: assets/sdu-logo.jpg (校徽)
```

### 2.2 执行流程

1. **加载阶段**: `\usepackage[options]{sdubeamer}` 触发宏包加载
2. **选项解析**: 使用 LaTeX3 `\DeclareKeys` 解析 7 个配置参数
3. **中文初始化**: 若 `chinese=true`，加载 ctex 宏包并配置字体集
4. **颜色系统**: 根据 `color` 选项定义 `sdu@primary`/`secondary`/`accent` 三色
5. **Beamer 主题设置**: 基础主题 (default + seahorse + professionalfonts)
6. **模板注册**: 注册封面页、章节页、页眉、页脚、帧标题等自定义模板
7. **样式定制**: 列表、彩色块、定理、图注、超链接的品牌色样式

---

## 3. 目录结构说明

```
/workspace/
├── src/                          # 核心源码目录
│   └── sdubeamer.sty             # Beamer 主题宏包（唯一核心代码文件）
│
├── examples/                     # 示例目录
│   └── demo.tex                  # 完整可编译示例，覆盖所有常用元素
│
├── doc/                          # 用户文档目录
│   ├── installation.md           # 安装说明（4种安装方式 + 环境要求）
│   ├── usage.md                  # 使用指南（参数/字体/排版元素）
│   └── faq.md                    # 常见问题（编译报错 + 使用问题）
│
├── assets/                       # 外部资源目录
│   ├── README.md                 # 资源使用说明
│   └── sdu-logo.jpg              # 山东大学校徽（封面页使用）
│
├── .cnb.yml                      # CNB 平台 CI/CD 流水线配置
├── .cnb/
│   └── web_trigger.yml           # CNB Web 手动触发按钮配置
│
├── .github/                      # GitHub 平台配置
│   ├── workflows/
│   │   └── sync-cnb.yml          # GitHub → CNB 反向同步 Workflow
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.yml        # Bug 报告模板
│   │   └── feature_request.yml   # 功能建议模板
│   ├── PULL_REQUEST_TEMPLATE.md  # PR 模板
│   └── CODEOWNERS                # 代码所有者配置
│
├── README.md                     # 项目首页说明
├── REPOSITORIES.md               # 关联仓库关系说明
├── CONTRIBUTING.md               # 贡献指南
├── CHANGELOG.md                  # 版本变更记录
└── LICENSE                       # LPPL v1.3c 许可证
```

---

## 4. 核心模块与关键代码

所有核心代码位于 [sdubeamer.sty](file:///workspace/src/sdubeamer.sty)，共约 347 行，按功能分为 12 个逻辑模块。

### 4.1 模块一：宏包声明与基础依赖加载

**位置**: [sdubeamer.sty#L1-L12](file:///workspace/src/sdubeamer.sty#L1-L12)

```latex
\NeedsTeXFormat{LaTeX2e}[1995/12/01]
\ProvidesPackage{sdubeamer}[2024/12/01 Shandong University Beamer Theme]

\RequirePackage{expl3}       % LaTeX3 编程层
\RequirePackage{l3keys2e}    % 选项解析（\ProcessKeyOptions）
\RequirePackage{graphicx}    % 图片加载（校徽）
\ExplSyntaxOn                % 进入 LaTeX3 语法模式
```

**设计说明**:
- 使用 `LaTeX3 (expl3)` 进行现代 LaTeX 编程，提供强大的键值选项系统
- `l3keys2e` 提供 `\ProcessKeyOptions`，显式加载消除对 beamer 的隐式依赖
- `graphicx` 用于封面页加载校徽图片

### 4.2 模块二：选项解析系统（核心配置入口）

**位置**: [sdubeamer.sty#L14-L47](file:///workspace/src/sdubeamer.sty#L14-L47)

使用 LaTeX3 `\DeclareKeys` 定义 7 个配置参数：

| 选项名 | 类型 | 内部变量 | 默认值 | 说明 |
|--------|------|----------|--------|------|
| `color` | tl (token list) | `\l_@@_color_tl` | `blue` | 主题色 |
| `chinese` | bool | `\l_@@_chinese_bool` | `true` | 是否启用中文支持 |
| `fontset` | tl | `\l_@@_fontset_tl` | `fandol` | ctex 字体集 |
| `school` | tl | `\l_@@_school_tl` | `山东大学` | 页脚学校名 |
| `enname` | tl | `\l_@@_enname_tl` | `Shandong~University` | 封面英文校名 |
| `logo` | tl | `\l_@@_logo_tl` | `assets/sdu-logo.jpg` | 校徽文件路径 |
| `degree` | tl | `\l_@@_degree_tl` | `master` | 答辩类型 |

**关键桥接命令**（将 expl3 变量暴露给传统 LaTeX2e 上下文）：

```latex
\tl_set_eq:NN \sdufootertext \l_@@_school_tl   % 页脚学校名
\tl_set_eq:NN \sduenname    \l_@@_enname_tl    % 英文校名
\tl_set_eq:NN \sdulogopath  \l_@@_logo_tl      % 校徽路径
\tl_set_eq:NN \sdudegreetype \l_@@_degree_tl   % 答辩类型
```

### 4.3 模块三：中文支持（ctex / xeCJK）

**位置**: [sdubeamer.sty#L53-L59](file:///workspace/src/sdubeamer.sty#L53-L59)

```latex
\bool_if:NT \l_@@_chinese_bool
  {
    \tl_set:Nx \l_tmpa_tl { fontset = \l_@@_fontset_tl }
    \exp_args:NV \PassOptionsToPackage \l_tmpa_tl { ctex }
    \RequirePackage[UTF8]{ctex}
  }
```

**实现原理**:
1. 条件判断：仅当 `chinese=true` 时执行
2. 动态构造选项：将 `fontset` 值拼接为 `fontset=xxx` 字符串
3. 传递选项：使用 `\PassOptionsToPackage` 在加载前将选项传给 ctex
4. 加载宏包：以 UTF8 编码加载 `ctex`，自动引入 xeCJK 中文支持

### 4.4 模块四：颜色定义系统

**位置**: [sdubeamer.sty#L66-L98](file:///workspace/src/sdubeamer.sty#L66-L98)

使用 `\str_case:Vn` 实现 5 套主题色切换，每套定义 3 个颜色变量：

| 颜色变量 | 语义 | blue (默认) RGB |
|----------|------|-----------------|
| `sdu@primary` | 主色（标题、结构、页脚线） | `0, 82, 147` (SDU官方蓝) |
| `sdu@secondary` | 辅助色（二级列表、超链接） | `0, 123, 182` |
| `sdu@accent` | 强调色（三级列表、警示块、引用） | `230, 126, 34` |

**5 套主题色完整定义**:

| color 值 | primary | secondary | accent |
|----------|---------|-----------|--------|
| `blue` | (0,82,147) 深SDU蓝 | (0,123,182) 浅蓝 | (230,126,34) 橙 |
| `red` | (155,20,20) 深红 | (200,60,60) 亮红 | (255,140,0) 橙 |
| `cyan` | (0,130,130) 深青 | (0,170,170) 亮青 | (255,165,0) 橙 |
| `green` | (20,120,40) 深绿 | (40,160,60) 亮绿 | (255,165,0) 橙 |
| `purple` | (110,30,130) 深紫 | (150,60,170) 亮紫 | (255,140,0) 橙 |

**兜底机制**: 未知 `color` 值时回退到默认 blue 配色。

### 4.5 模块五：Beamer 基础主题设置

**位置**: [sdubeamer.sty#L104-L129](file:///workspace/src/sdubeamer.sty#L104-L129)

```latex
\mode<presentation>
\usetheme{default}          % 基础主题
\usecolortheme{seahorse}    % 配色底版（后续被自定义覆盖）
\usefonttheme{professionalfonts}  % 专业字体
```

**Beamer 颜色映射**（关键设计）:

| Beamer 颜色名 | 映射到 | 用途 |
|---------------|--------|------|
| `title page` | fg=white, bg=sdu@primary | 封面页底色 |
| `frametitle` | fg=sdu@primary, bg=white | 帧标题 |
| `structure` | fg=sdu@primary | 结构元素（目录、TOC 等） |
| `footline` | fg=sdu@secondary, bg=white | 页脚文字 |
| `headline` | fg=sdu@primary, bg=white | 页眉文字 |
| `page number` | fg=sdu@primary, bg=white | 页码 |
| `footer school` | fg=sdu@secondary, bg=white | 页脚校名 |

**字体大小映射**:
- `title`: `\LARGE` + `\bfseries`
- `subtitle`: `\large`
- `author`: `\normalsize`
- `institute`: `\small`
- `footline` / `page number`: `\footnotesize`
- `headline`: `\scriptsize`

### 4.6 模块六：封面页（Title Page）模板

**位置**: [sdubeamer.sty#L136-L191](file:///workspace/src/sdubeamer.sty#L136-L191)

**学位类型文案映射** (`\sdu@degreetext`):

| degree 值 | 显示文案 |
|-----------|----------|
| `undergrad` | 本科毕业论文答辩 |
| `master` (默认) | 硕士学位论文答辩 |
| `doctor` | 博士学位论文答辩 |

**用户自定义命令**:
- `\sdudegree{自定义文案}` — 临时覆盖学位类型
- `\sduennamecmd{自定义英文名}` — 临时覆盖英文校名

**封面页布局结构**（垂直居中）:

```
┌─────────────────────────────────┐
│                                 │
│       [校徽 2.5cm 高]           │  ← 不存在则用主题色方块占位
│                                 │
│     山东大学 (主色 加粗)         │
│   Shandong University (辅助色)  │
│                                 │
│    硕士学位论文答辩 (强调色)     │
│                                 │
│    ───── 主色分隔线 ─────       │
│                                 │
│       论文标题 (LARGE+主色)     │
│       副标题                    │
│                                 │
│       作者姓名                  │
│       学院名称                  │
│       日期                      │
│                                 │
└─────────────────────────────────┘
```

### 4.7 模块七：章节页（Section Page）模板

**位置**: [sdubeamer.sty#L197-L205](file:///workspace/src/sdubeamer.sty#L197-L205)

简洁的居中布局：顶部 2cm 留白 + `\LARGE\bfseries` 章节名。

### 4.8 模块八：帧标题（Frametitle）模板

**位置**: [sdubeamer.sty#L211-L217](file:///workspace/src/sdubeamer.sty#L211-L217)

```latex
\setbeamertemplate{frametitle}{
  \nointerlineskip
  \begin{beamercolorbox}[wd=\paperwidth,ht=2.5ex,dp=1ex]{frametitle}
    \hspace*{0.5cm}
    \Large\bfseries\insertframetitle
  \end{beamercolorbox}
}
```

设计：通栏宽度 `\paperwidth`，左侧 0.5cm 缩进，`\Large\bfseries` 主色文字。

### 4.9 模块九：页眉（Headline）模板

**位置**: [sdubeamer.sty#L225-L239](file:///workspace/src/sdubeamer.sty#L225-L239)

**结构**:
1. 上方 beamercolorbox：左侧 0.6cm 缩进 + `\insertsectionhead`（当前章节名）
2. 下方 1pt 粗主色细线（`structure` 颜色，即 sdu@primary）

使用 `\nointerlineskip` 消除两段之间的垂直间距，使细线紧贴页眉文字。

### 4.10 模块十：页脚（Footline）模板

**位置**: [sdubeamer.sty#L246-L264](file:///workspace/src/sdubeamer.sty#L246-L264)

**结构**（与页眉镜像对称）:
1. 上方 1pt 主色细线
2. 下方 beamercolorbox：
   - 左侧 0.6cm 缩进 + `\sdufootertext`（页脚学校名，辅助色）
   - 右侧 `\insertframenumber{}/\inserttotalframenumber`（当前帧/总帧数，主色）
   - 右侧 0.6cm 缩进

**运行时覆盖命令**:
```latex
\newcommand\sdufooter[1]{\def\sdufootertext{#1}}
```
允许用户在正文中任意位置临时修改页脚校名。

### 4.11 模块十一：列表（Itemize / Enumerate）样式

**位置**: [sdubeamer.sty#L272-L288](file:///workspace/src/sdubeamer.sty#L272-L288)

**Itemize（无序列表）三级递进**:

| 层级 | 符号 | 颜色 |
|------|------|------|
| 一级 (item) | `$\blacktriangleright$` 黑三角 | sdu@primary |
| 二级 (subitem) | `$\bullet$` 实心圆点 | sdu@secondary |
| 三级 (subsubitem) | `$-$` 短横线 | sdu@accent |

**Enumerate（有序列表）三级递进**:

| 层级 | 编号格式 | 颜色 |
|------|----------|------|
| 一级 | `1.` | sdu@primary |
| 二级 | `1.` | sdu@secondary |
| 三级 | `1.` | sdu@accent |

同时设置 `item projected` 背景（圆角编号块）：bg=sdu@primary, fg=white。

### 4.12 模块十二：块/定理/图注/超链接样式

**位置**: [sdubeamer.sty#L295-L340](file:///workspace/src/sdubeamer.sty#L295-L340)

**彩色块 (Block) 配色**:

| 块类型 | 标题背景/文字 | 正文背景 |
|--------|--------------|----------|
| 普通 block | 主色实心底 / 白字 | 主色 10% 透明底 |
| alertblock | 强调色实心底 / 白字 | 强调色 15% 透明底 |
| exampleblock | 辅助色实心底 / 白字 | 辅助色 12% 透明底 |

**定理类**:
- `theorem title`: fg=主色, bg=主色 8% 透明底
- `theorem body`: fg=黑色
- 覆盖 theorem/lemma/corollary 等全部定理环境

**强调文本**:
- `example text`: fg=辅助色
- `alerted text`: fg=强调色

**图注 (Caption)**:
- `caption name`（"图/表"前缀）：主色 + `\small\bfseries`
- `caption`（正文说明）：黑色 + `\small`

**超链接配色** (`\hypersetup`):
- `linkcolor` (内部交叉引用) = sdu@primary
- `urlcolor` (URL 链接) = sdu@secondary
- `citecolor` (参考文献引用) = sdu@accent
- `anchorcolor` (锚点) = sdu@accent
- `colorlinks=true`（启用彩色链接，非方框）

**导航符号**: `\setbeamertemplate{navigation symbols}{}` — 完全禁用 Beamer 默认右下角导航图标，保持简洁。

---

## 5. 配置选项与参数系统

### 5.1 完整参数表

| 参数 | 类型 | 默认值 | 可选值 | 作用域 | 说明 |
|------|------|--------|--------|--------|------|
| `chinese` | bool | `true` | `true`/`false` | 加载时 | 是否接入 ctex 中文排版 |
| `fontset` | string | `fandol` | `fandol`/`windows`/`mac`/`ubuntu` | 加载时 | ctex 字体集选择 |
| `color` | string | `blue` | `blue`/`red`/`cyan`/`green`/`purple` | 加载时 | 主题色三元组切换 |
| `school` | string | `山东大学` | 任意字符串 | 加载时 | 页脚显示的学校名 |
| `enname` | string | `Shandong University` | 任意字符串 | 加载时 | 封面页英文校名 |
| `logo` | path | `assets/sdu-logo.jpg` | 任意图片路径 | 加载时 | 封面页校徽文件 |
| `degree` | enum | `master` | `undergrad`/`master`/`doctor` | 加载时 | 答辩类型文案 |

### 5.2 运行时可覆盖命令（正文级）

| 命令 | 签名 | 等效加载时选项 | 说明 |
|------|------|---------------|------|
| `\sdufooter{name}` | 单参数 | `school=name` | 临时覆盖页脚学校名 |
| `\sdudegree{text}` | 单参数 | `degree=自定义` | 临时覆盖学位类型文案 |
| `\sduennamecmd{name}` | 单参数 | `enname=name` | 临时覆盖英文校名 |

### 5.3 颜色变量（可在用户文档中直接引用）

```latex
\textcolor{sdu@primary}{主色文字}
\textcolor{sdu@secondary}{辅助色文字}
\textcolor{sdu@accent}{强调色文字}
```

常见用法：代码高亮关键字着色（见 demo.tex 中 listings 配置）。

---

## 6. 依赖关系分析

### 6.1 外部 LaTeX 宏包依赖

| 宏包 | 用途 | 引入方式 | 必选 |
|------|------|----------|------|
| `expl3` | LaTeX3 编程层 | `\RequirePackage` | ✅ |
| `l3keys2e` | LaTeX3 选项解析 | `\RequirePackage` | ✅ |
| `graphicx` | 图片加载（校徽） | `\RequirePackage` | ✅ |
| `ctex` | 中文排版 + 字体集 | 条件 `\RequirePackage` (chinese=true) | 条件 |
| `xeCJK` | XeLaTeX 中文支持 | 由 ctex 间接引入 | 条件 |
| `beamer` | 幻灯片文档类 | 用户文档 `\documentclass` | ✅ (用户侧) |
| `hyperref` | 超链接 | 由 beamer 间接引入 | 间接 |

### 6.2 字体依赖

| fontset 值 | 字体集 | 来源 | 跨平台 |
|-----------|--------|------|--------|
| `fandol` (默认) | Fandol 字体 | TeX Live 完整版内置 | ✅ 免安装 |
| `windows` | 宋体/黑体/微软雅黑等 | Windows 系统自带 | ❌ 仅 Windows |
| `mac` | 苹方/宋体等 | macOS 系统自带 | ❌ 仅 macOS |
| `ubuntu` | 思源/文泉驿等 | Ubuntu 系统自带 | ❌ 仅 Linux |

### 6.3 编译引擎依赖矩阵

| 引擎 | 支持中文 | 兼容模板 | 推荐 |
|------|---------|---------|------|
| `xelatex` | ✅ (xeCJK) | ✅ 完全兼容 | ✅ 首选推荐 |
| `lualatex` | ✅ (LuaTeX-ja) | ⚠️ 未经测试 | 不推荐 |
| `pdflatex` | ❌ (无 xeCJK) | ❌ 不兼容 | 禁止使用 |
| `latex` (dvi) | ❌ | ❌ 不兼容 | 禁止使用 |

### 6.4 内部依赖关系图

```
用户文档 .tex
  │
  ├── \documentclass{beamer}
  │     └── beamer.cls (外部)
  │           ├── hyperref.sty
  │           └── xcolor.sty
  │
  └── \usepackage{sdubeamer}
        │
        ├── expl3.sty ─────────────────┐
        ├── l3keys2e.sty               │ (LaTeX3 编程层)
        │                               │
        ├── graphicx.sty               │
        │                               │
        ├── [chinese=true] ──► ctex.sty ──► xeCJK.sty
        │                               │   └── fontspec.sty
        │                               │
        ├── 颜色定义 (sdu@primary/secondary/accent)
        │
        ├── Beamer 基础主题设置 (default + seahorse + professionalfonts)
        │
        ├── 模板注册 (title page / section page / headline / footline / frametitle)
        │
        └── 样式定制 (列表 / 块 / 定理 / 图注 / 超链接)
```

---

## 7. 项目运行与编译

### 7.1 环境要求

| 组件 | 要求 | 推荐版本 |
|------|------|---------|
| TeX 发行版 | 含 ctex + fandol | TeX Live 2023+ 完整版 |
| 编译引擎 | xelatex（必须） | XeTeX 3.1415926+ |
| 可选工具 | latexmk | latexmk 4.7+ |

### 7.2 本地编译示例（从仓库根目录）

**方式 A：直接 xelatex（推荐上手）**
```bash
cd examples
# 将上级目录(含 assets/) 和 src/ 加入 TEXINPUTS 搜索路径
TEXINPUTS=..:../src:$TEXINPUTS xelatex -interaction=nonstopmode demo.tex
TEXINPUTS=..:../src:$TEXINPUTS xelatex -interaction=nonstopmode demo.tex  # 第二遍解引用
```

**方式 B：latexmk（自动化多遍）**
```bash
latexmk -xelatex -cd examples/demo.tex
```

**方式 C：从根目录指定输出目录**
```bash
xelatex -output-directory=examples examples/demo.tex
```

编译产物：`examples/demo.pdf`

### 7.3 用户项目编译

将 `src/sdubeamer.sty` 和 `assets/sdu-logo.jpg` 放置在用户项目目录下：

```
my-project/
├── main.tex
├── sdubeamer.sty
└── assets/
    └── sdu-logo.jpg
```

编译：
```bash
xelatex main.tex
xelatex main.tex
```

### 7.4 安装方式速查

| 方式 | 操作 | 适用场景 |
|------|------|---------|
| 直接复制 | 下载 `sdubeamer.sty` + `sdu-logo.jpg` 到项目目录 | 快速上手，小型项目 |
| Release 附件 | 从 Releases 下载完整发布包解压 | 正式项目，含完整文档 |
| 克隆仓库 | `git clone` + TEXINPUTS 配置 | 参与开发，调试模板 |
| 在线平台 | Overleaf/TeXPage 上传整个目录 | 无需本地 TeX 环境 |

### 7.5 编译验证脚本（CI 同款）

```bash
set -e
cd examples
TEXINPUTS=..:../src:$TEXINPUTS xelatex -interaction=nonstopmode -halt-on-error demo.tex
TEXINPUTS=..:../src:$TEXINPUTS xelatex -interaction=nonstopmode -halt-on-error demo.tex
test -f demo.pdf
ls -lh demo.pdf
```

---

## 8. CI/CD 与发布流程

### 8.1 流水线总览（.cnb.yml）

配置文件：[.cnb.yml](file:///workspace/.cnb.yml)

CNB 平台流水线覆盖 4 类事件：

| 触发事件 | 流水线任务 |
|---------|-----------|
| `push` (main 分支) | ① 同步到 GitHub（rebase 模式）② TeX Live 编译验证 |
| `pull_request` | ① PR 自动分配处理人 + 审查人 ② TeX Live 编译验证（质量门禁） |
| `tag_push` (v*) | ① 创建 Release ② 上传附件（sty/examples/assets/doc/LICENSE/README） |
| `issue.open` | 自动分配 Issue 处理人 |
| `web_trigger_sync_github` (手动) | 手动同步当前分支到 GitHub |
| `web_trigger_pull_from_github` (手动) | 手动从 GitHub 拉取回 CNB |

### 8.2 双向同步闭环

```
  CNB 仓库 (主)                    GitHub 仓库 (镜像)
  ┌─────────────┐                 ┌──────────────┐
  │             │  push main      │              │
  │  .cnb.yml   │ ─────────────►  │  (git-sync)  │
  │  sync-to-github  (rebase)     │              │
  │             │                 │              │
  │             │  GitHub Actions │              │
  │  (git-sync) │ ◄─────────────  │ sync-cnb.yml │
  │             │  (防环判断)      │  直接改代码时 │
  └─────────────┘                 └──────────────┘
```

**防同步环关键逻辑**（GitHub → CNB 方向）:
- Workflow 条件：`github.event.head_commit.committer.email != 'git-sync@plugin.local'`
- 由 CNB 侧 git-sync 插件推送的提交，其 committer 邮箱固定为 `git-sync@plugin.local`
- 此类提交在 GitHub 侧被跳过，不会反向回灌
- 仅当用户直接在 GitHub 修改代码时才触发反向同步

### 8.3 编译验证任务

可复用的 YAML 锚点 `&texlive-compile`：
- Docker 镜像：`ghcr.io/xu-cheng/texlive-full:latest`（完整 TeX Live）
- 执行两遍 xelatex 解决交叉引用
- `test -f demo.pdf` 校验产物存在
- 同时用于 `push` 和 `pull_request` 事件，构成质量门禁

### 8.4 自动发布流程

打 tag `v*` 触发：
1. `git:release` 内置任务创建 Release，描述从 `README.md` 读取
2. `cnbcool/attachments` 插件上传以下附件：
   - `src/sdubeamer.sty`
   - `examples/`（含 demo.tex）
   - `assets/`（含校徽）
   - `doc/`（安装/使用/FAQ 文档）
   - `LICENSE`、`README.md`、`CHANGELOG.md`、`CONTRIBUTING.md`

### 8.5 PR / Issue 自动分配

| 事件 | 分配目标 | 机制 |
|------|---------|------|
| PR 创建 | h1s97x (assignee) + 随机仓库成员 (reviewer) | `git:reviewer` 内置任务 |
| Issue 创建 | h1s97x | `cnbcool/cnb-cli` 插件 + `cnb issues add-assignees` |

---

## 9. 仓库生态与关联项目

### 9.1 生态总览

SDUBeamer 是山东大学 LaTeX 方案的三大仓库之一：

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

### 9.2 三仓库定位

| 仓库 | 角色 | 交付物 | 面向用户 |
|------|------|--------|---------|
| **sdutex** | 核心包（底层） | `sduthesis.cls`, `sdutex.sty`, `sduthesis.bst` | 开发者/维护者 |
| **sduthesis** | 论文模板 | 可直接编译的毕业论文模板 | 论文作者（最常用） |
| **sdubeamer**（本仓库） | 幻灯片模板 | `src/sdubeamer.sty` | 答辩/汇报用户 |

### 9.3 SDUBeamer 的独立性

与 sduthesis 不同，**sdubeamer 不直接依赖 sdutex** 核心包。它是一个独立宏包，仅通过品牌视觉风格（配色、校名、校徽）与整体方案保持一致。

**设计取舍**：
- 优势：单文件分发，易于安装使用，无额外依赖
- 劣势：与 sduthesis 的品牌视觉元素无法共享代码（当前通过人工保持一致）

---

## 10. 贡献指南与开发规范

### 10.1 开发工作流

```
Fork & Clone
    │
    ▼
git checkout -b feat/xxx        # 新建功能分支
    │
    ▼
修改 src/sdubeamer.sty / doc/
    │
    ▼
本地编译验证 examples/demo.tex  ← 必须通过！
    │
    ▼
git commit (Conventional Commits)
    │
    ▼
Push & 创建 PR
    │
    ▼
CI 编译验证通过 + Reviewer 审查
    │
    ▼
合并到 main
```

### 10.2 提交信息规范（Conventional Commits）

| 类型前缀 | 用途 | 示例 |
|---------|------|------|
| `feat:` | 新功能 | `feat: 新增 purple 主题色` |
| `fix:` | Bug 修复 | `fix: 修复页脚页码在 16:9 下错位` |
| `docs:` | 文档更新 | `docs: 补充 FAQ 第 14 条` |
| `refactor:` | 代码重构 | `refactor: 抽取颜色定义为独立函数` |
| `chore:` | 杂项 | `chore: 更新 .gitignore` |
| `ci:` | CI/CD 变更 | `ci: 优化编译验证步骤` |

### 10.3 代码风格约定

**.sty 文件**:
- 使用 `%% === 模块名 ===` 分节注释
- LaTeX3 语法用 `\ExplSyntaxOn` / `\ExplSyntaxOff` 包裹
- 内部变量使用 `\l_@@_xxx_tl` / `\l_@@_xxx_bool` 命名（`@@` 自动替换为宏包名前缀）
- 暴露给用户的命令前缀统一为 `\sdu`

**Markdown 文档**:
- 中文文档使用统一的技术文档语气
- 参数/命令名用 `` `code` `` 标记
- 新增选项必须同步更新 `doc/usage.md` 中的参数表格

### 10.4 PR 质量门禁（自动）

- [ ] TeX Live 编译验证通过（xelatex 两遍无报错）
- [ ] `examples/demo.pdf` 成功生成
- [ ] Reviewer 至少 1 人审批

### 10.5 向后兼容原则

- 新增选项必须设置合理默认值（保持现有用户配置不变）
- 修改已有模板时避免破坏用户自定义命令接口
- 颜色命名 `sdu@primary/secondary/accent` 视为稳定 API，不随意变更

### 10.6 发布流程（维护者）

1. 确认 main 分支 CI 全绿
2. 创建语义化版本标签：
   ```bash
   git tag v1.1.0
   git push origin v1.1.0
   ```
3. CNB 流水线自动创建 Release 并上传附件
4. 在 CHANGELOG.md 中补版本记录

---

## 11. 版本历史

完整记录见 [CHANGELOG.md](file:///workspace/CHANGELOG.md)。

### v1.0.0 (2026-08-16) — 首个正式版

**新增**:
- SDUBeamer Beamer 主题宏包 `sdubeamer.sty`
- 支持 undergrad / master / doctor 三种答辩类型
- 基于 ctex 的中文支持（fandol 字体集跨平台免安装）
- 5 套主题色：blue / red / cyan / green / purple
- 自定义模板：封面页（校徽+校名+学位类型）、章节页、页眉、页脚、帧标题
- 定制样式：三级列表递进配色、block/alertblock/exampleblock、theorem、caption、hyperlink
- 可编译示例 `examples/demo.tex`
- 文档：installation.md / usage.md / faq.md / CONTRIBUTING.md / CHANGELOG.md
- CNB 流水线：GitHub 双向同步、PR/Issue 自动分配、Tag 自动发布 Release、编译验证门禁

### Unreleased (开发中)

**变更**:
- 目录结构优化：拆分 src/ examples/ doc/ assets/
- `sdubeamer.sty` 从根目录移至 `src/`

---

## 12. 常见问题排错

详细 FAQ 见 [doc/faq.md](file:///workspace/doc/faq.md)，此处列出核心排错要点。

### 12.1 编译类问题

| 现象 | 根因 | 解决方案 |
|------|------|---------|
| `pdflatex` 编译含中文时报 xeCJK 相关错 | 模板依赖 xeCJK，仅支持 XeLaTeX | 改用 `xelatex` 编译 |
| 提示找不到 `sdubeamer.sty` | 宏包不在 TEXINPUTS 搜索路径 | 将 sty 所在目录加入 `TEXINPUTS=path:$TEXINPUTS`，或直接放项目根目录 |
| 缺少 `ctex` / `xeCJK` / `fandol` | TeX 发行版不完整 | TeX Live 完整版，或 `tlmgr install ctex xeCJK fandol` |
| 交叉引用/页码/目录不对 | 只编译了一遍 | 执行第二遍 `xelatex`，或用 `latexmk -xelatex` |
| Overleaf/TeXPage 编译失败 | 编译器选错（默认 pdflatex） | 项目设置中切换编译器为 **XeLaTeX** |

### 12.2 显示类问题

| 现象 | 根因 | 解决方案 |
|------|------|---------|
| 封面页无校徽，显示彩色方块 | 校徽文件路径错误或未找到 | 检查 `assets/sdu-logo.jpg` 存在，或用 `logo=path` 指定路径 |
| 页脚校名需要改为学院名 | 默认显示"山东大学" | `\usepackage[school=山东大学 XX学院]{sdubeamer}` 或正文 `\sdufooter{...}` |
| 中西文间距异常 | 未用 xelatex，或 ctex 版本过旧 | 确认使用 xelatex，更新 ctex 宏包 |
| 列表/块颜色与文档不符 | 颜色变量可能被用户代码覆盖 | 检查用户代码中是否重定义了 beamer 颜色 |

### 12.3 自定义扩展速查

```latex
% 1. 更换主题色（加载时）
\usepackage[color=green]{sdubeamer}

% 2. 自定义页脚校名（正文任意位置）
\sdufooter{山东大学 数学与统计学院}

% 3. 自定义学位类型文案
\sdudegree{博士后出站答辩}

% 4. 自定义校徽路径
\usepackage[logo=figures/my-custom-logo.png]{sdubeamer}

% 5. 关闭中文（纯英文场景，可使用 pdflatex）
\usepackage[chinese=false]{sdubeamer}

% 6. 在用户代码中复用品牌色
\textcolor{sdu@primary}{主色强调}
\colorbox{sdu@primary!15}{浅色背景块}
```

---

## 附录 A：关键代码行数统计

| 文件 | 行数 | 角色 |
|------|------|------|
| `src/sdubeamer.sty` | 347 | 核心宏包（全部功能） |
| `examples/demo.tex` | 215 | 完整可编译示例 |
| `doc/installation.md` | 80 | 安装文档 |
| `doc/usage.md` | 174 | 使用指南 |
| `doc/faq.md` | 112 | 常见问题 |
| `.cnb.yml` | 162 | CI/CD 流水线配置 |
| `.github/workflows/sync-cnb.yml` | 62 | GitHub→CNB 反向同步 |
| **合计核心代码** | **~1152** | |

## 附录 B：对外稳定接口（API）

以下接口视为稳定，用户文档可安全依赖，版本升级时保证向后兼容：

1. **加载选项**: `chinese`, `fontset`, `color`, `school`, `enname`, `logo`, `degree`
2. **运行时命令**: `\sdufooter{}`, `\sdudegree{}`, `\sduennamecmd{}`
3. **颜色变量**: `sdu@primary`, `sdu@secondary`, `sdu@accent`
4. **Beamer 模板名**: `title page [sdu]`, `section page [sdu]`, `headline [sdu]`, `footline [sdu]`
5. **桥接命令**: `\sdufootertext`, `\sduenname`, `\sdulogopath`, `\sdudegreetype`

---

*本文档基于 SDUBeamer v1.0.0 生成，最后更新：2026-08-16*
