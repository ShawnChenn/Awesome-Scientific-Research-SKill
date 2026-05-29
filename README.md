# Awesome-Scientific-Research-SKill

A Collection of Reliable Skills for facilitating scientific research.

---

## Table of Contents

1. [Research-Paper-Writing-Skills](#1-research-paper-writing-skills)
2. [figures4papers](#2-figures4papers)
3. [awesome-ai-research-writing](#3-awesome-ai-research-writing)
4. [nature-skills](#4-nature-skills)

---

## 1. Research-Paper-Writing-Skills

来源仓库：`https://github.com/Master-cai/Research-Paper-Writing-Skills`

假设当前目录在该仓库根目录，并且已拉取到本地（包含 `research-paper-writing/` 文件夹）。

### 1) Codex

将 skill 复制到 `$CODEX_HOME/skills/`：

```bash
mkdir -p "$CODEX_HOME/skills"
cp -R research-paper-writing "$CODEX_HOME/skills/"
```

### 2) Claude Code (CC)

可选全局安装或项目级安装。

全局安装：

```bash
mkdir -p "$HOME/.claude/skills"
cp -R research-paper-writing "$HOME/.claude/skills/"
```

项目级安装：

```bash
mkdir -p .claude/skills
cp -R research-paper-writing .claude/skills/
```

### 3) Gemini

将 skill 复制到 Gemini skills 目录：

```bash
mkdir -p "$HOME/.gemini/skills"
cp -R research-paper-writing "$HOME/.gemini/skills/"
```

### 使用场景（简要）

`research-paper-writing` 主要用于 ML/CV/NLP 论文写作与改写，典型场景包括：

- 改写或起草 `Abstract / Introduction / Method / Experiments / Conclusion`
- 优化段落衔接与论证逻辑
- 检查 claim-evidence 对齐
- 投稿前自检（审稿人视角）

示例提示词：

- Codex：`Use $research-paper-writing to improve my paper's Introduction.`
- Claude Code：`Please use the research-paper-writing skill to rewrite my Abstract with clearer claim-evidence alignment.`
- Gemini：`Use research-paper-writing to revise the Experiments section and strengthen ablation discussion.`

> 说明：以上安装命令来自该仓库 README，默认是 Unix shell（macOS/Linux）写法。

---

## 2. figures4papers（Scientific Figure Making Skill）

来源仓库：`https://github.com/ChenLiu-1996/figures4papers`

该仓库的 skill 目录是：`scientific-figure-making/`。

### 方式 A：免安装（路径引用，推荐）

打开该仓库后，在提示词中直接引用：

- `scientific-figure-making/SKILL.md`
- `scientific-figure-making/references/design-theory.md`
- `scientific-figure-making/references/api.md`

示例提示词：

`Create a publication-quality figure script and follow scientific-figure-making/SKILL.md + references/design-theory.md + references/api.md.`

### 方式 B：安装为本地 skill（软链接）

在 `figures4papers` 仓库根目录执行：

```bash
# Cursor
mkdir -p ~/.cursor/skills
ln -s "$(pwd)/scientific-figure-making" ~/.cursor/skills/scientific-figure-making

# Claude Code
mkdir -p ~/.claude/skills
ln -s "$(pwd)/scientific-figure-making" ~/.claude/skills/scientific-figure-making

# Codex
mkdir -p ~/.codex/skills
ln -s "$(pwd)/scientific-figure-making" ~/.codex/skills/scientific-figure-making
```

完成后重启或刷新 agent 的 skill 列表。

### 使用场景（简要）

- 论文图表脚本生成与改写（柱状图/折线图/热力图/雷达图等）
- 统一论文风格（配色、字号、导出规范）
- 复用仓库中的通用绘图模式（如 `apply_publication_style`、`finalize_figure`）

---

## 3. awesome-ai-research-writing（Prompt + Skills 指南）

来源仓库：`https://github.com/Leey21/awesome-ai-research-writing`

该仓库定位是**写作 Prompt 集合 + Agent Skills 使用教程**，不是单一 skill 包。

### 使用方式 A：直接使用 Prompt（零安装）

适合快速上手：直接从仓库复制对应场景的 Prompt 使用，例如：

- 中英互译（LaTeX / Word）
- 英文/中文润色
- 逻辑检查、去 AI 味
- 图表标题、实验分析、Reviewer 视角审稿

### 使用方式 B：按其教程安装 OpenSkills 生态技能

仓库给出的典型命令：

```bash
# 检查 OpenSkills
npx openskills --version

# （可选）全局安装
npm i -g openskills
openskills --version

# 安装 skill 仓库（示例）
npx openskills install zechenzhangAGI/AI-research-SKILLs
npx openskills install anthropics/skills
```

安装后可在 `.claude/skills/`（以及部分工具的 `.cursor/skills/`）中被发现并调用。

### 使用场景（简要）

- 论文写作全流程：起稿、改写、引用、投稿前 checklist
- 文本人类化润色（减少 AI 痕迹）
- Word 模板填充/修订、协作式文档迭代

---

## 4. nature-skills（Nature 论文学术表达与科研绘图）

来源仓库：`https://github.com/Yuan1z0825/nature-skills`

该仓库包含了 9 个以 `SKILL.md` 为核心、针对 Nature 级高影响因子期刊打磨的学术与绘图技能包。

### 1) Codex（本地与插件市场安装）

- **方式 A (插件市场)：**
  1. 打开 Codex Desktop，添加自定义 marketplace；
  2. 源仓库填入 `https://github.com/Yuan1z0825/nature-skills.git`，分支设为 `main`；
  3. 在 Marketplace 搜索 `nature-skills` 插件并安装。
- **方式 B (本地手动复制)：**
  先 clone 仓库，随后在本地运行：
  ```bash
  mkdir -p ~/.codex/skills
  # 复制全部 skills/nature-* 目录到本地 skills 文件夹
  for d in skills/nature-*; do cp -R "$d" ~/.codex/skills/; done
  ```

### 2) Claude Code（插件市场与 subagent 安装）

- **方式 A (插件注册安装，最简推荐)：**
  ```bash
  # 1. 注册市场
  /plugin marketplace add https://github.com/Yuan1z0825/nature-skills
  # 2. 安装插件
  /plugin install nature-skills
  # 3. 重启插件
  /reload-plugins
  ```
- **方式 B (作为独立 subagent 运行)：**
  直接把某个具体 skill（如 `nature-reader`）的 `SKILL.md` 拷贝并作为 subagent 配置：
  ```bash
  mkdir -p ~/.claude/agents
  cp skills/nature-reader/SKILL.md ~/.claude/agents/nature-reader.md
  ```

### 3) 核心 Skills 功能与使用场景

| Skill 目录/名称 | 状态 | 功能简述 & 触发场景 |
| :--- | :--- | :--- |
| `nature-figure` | Stable | 绘制符合 Nature 标准的多面板图（正确字体、出版色、无冗余）|
| `nature-polishing` | Stable | 将学术草稿/中译英转换为优雅地道的 Nature 风格（句子≤30字、时态校准）|
| `nature-writing` | Draft | 针对 Abstract, Intro, Methods 模块化生成论文段落与逻辑线 |
| `nature-citation` | Beta | 严格检索 Crossref 并生成 RIS/ENW/Zotero 等引文文件 |
| `nature-reader` | Beta | 生成支持双语对照、图文定位与锚点还原的 Markdown 全文阅读器 |
| `nature-response` | Beta | 自动起草、核对 point-by-point 审稿意见回复信 (Rebuttal) |
| `nature-academic-search` | Beta | 结合本地 MCP 检索并处理 PubMed/CrossRef/arXiv 的文献 |
| `nature-data` | Draft | 构建、审核符合 FAIR 原则的数据可用性声明（Data Availability）|
| `nature-paper2ppt` | Beta | 从论文或阅读笔记自动提取并制作中文 Journal Club PPTX 演示幻灯片 |

> 说明：以上命令与流程基于该仓库 README 的 OpenSkills 教程内容，命令为 Unix shell（macOS/Linux）风格。