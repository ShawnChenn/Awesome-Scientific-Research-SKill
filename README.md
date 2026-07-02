# Awesome-Scientific-Research-SKill

A Collection of Reliable Skills for facilitating scientific research.

---

## Table of Contents

1. [Research-Paper-Writing-Skills](#1-research-paper-writing-skills)
2. [figures4papers](#2-figures4papers)
3. [awesome-ai-research-writing](#3-awesome-ai-research-writing)
4. [nature-skills](#4-nature-skills)
5. [humanizer](#5-humanizer)
6. [gpt-image-2-skill](#6-gpt-image-2-skill)
7. [edit-banana](#7-edit-bananajie-tu-zhuan-ke-bian-ji-drawio)
8. [ppt-master](#8-ppt-masterwendang-zhuan-ppt)
9. [ai-figure-prompt-handbook](#9-ai-figure-prompt-handbookke-yan-tu-ti-shi-ci-shou-ce)
10. [drawio-diagram-builder](#10-drawio-diagram-builder-drawio-tu-gou-jian-qi)
11. [research-media-card](#11-research-media-cardke-yan-mei-ti-ka-pian)

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

---

## 5. humanizer（去除 AI 写作痕迹）

来源仓库：`https://github.com/blader/humanizer`

该 skill 基于 Wikipedia "Signs of AI writing" 指南，可消除 AI 生成文本的痕迹，使其更自然。

### 安装

```bash
# Claude Code
mkdir -p ~/.claude/skills
git clone https://github.com/blader/humanizer.git ~/.claude/skills/humanizer

# OpenCode（也兼容 ~/.claude/skills/）
mkdir -p ~/.config/opencode/skills
git clone https://github.com/blader/humanizer.git ~/.config/opencode/skills/humanizer
```

### 使用方式

**基础用法：**
```
/humanizer

[paste your text here]
```

**声纹校准（匹配个人写作风格）：**
```
/humanizer

Here's a sample of my writing for voice matching:
[paste 2-3 paragraphs of your own writing]

Now humanize this text:
[paste AI text to humanize]
```

### 检测的 30 种 AI 特征模式

| 类别 | 模式数量 | 示例 |
| :--- | :--- | :--- |
| 内容模式 | 6 种 | 显著性夸大、名人效应、虚假挑战 |
| 语言模式 | 7 种 | AI 词汇、回避系动词、规则三 |
| 风格模式 | 8 种 | 破折号滥用、标题大小写、emoji 使用 |
| 沟通模式 | 3 种 | 聊天机器人话术、截断免责声明 |
| 填充词/修饰 | 4 种 | 冗余短语、过度修饰、泛泛结论 |

### 使用场景（简要）

- 将 AI 生成文本转换为自然人类写作风格
- 个人声纹匹配（提供自己写作样本使输出符合个人习惯）
- 批量文档/博客/技术文章的 AI 特征检测与修正
- 团队写作前统一文本风格

> 说明：以上安装命令来自该仓库 README，默认是 Unix shell（macOS/Linux）写法。

---

## 6. GPT-Image-2-Skill（AI 图像生成 Skill + 提示词画廊）

来源仓库：`https://github.com/wuyoscar/gpt_image_2_skill`

OpenAI GPT Image 2 的提示词画廊 + 智能体技能 + CLI 工具三合一，覆盖 20+ 类别（科研论文配图、UI 模拟、摄影修图、动漫漫画、品牌设计等）。

### 安装

**Claude Code（插件市场，最简推荐）：**
```bash
/plugin marketplace add wuyoscar/gpt_image_2_skill
/plugin install gpt-image@wuyoscar-skills
```

**Codex：**
```bash
# 方式 A：使用内置安装器，输入技能文件夹 URL
# https://github.com/wuyoscar/gpt_image_2_skill/tree/main/skills/gpt-image

# 方式 B：手动复制
mkdir -p ~/.codex/skills
cp -R skills/gpt-image ~/.codex/skills/
```

**跨平台（npx）：**
```bash
npx --yes skills@latest add wuyoscar/gpt_image_2_skill --skill gpt-image --agent codex --copy
npx --yes skills@latest add wuyoscar/gpt_image_2_skill --skill gpt-image --agent openclaw --copy
```

**CLI 独立使用：**
```bash
# 直接运行
uvx --from git+https://github.com/wuyoscar/gpt_image_2_skill gpt-image -p "a cat astronaut"

# 或安装到 PATH
uv tool install git+https://github.com/wuyoscar/gpt_image_2_skill
gpt-image -p "a cat astronaut"
```

> API Key 读取顺序：环境变量 `OPENAI_API_KEY` → `.env` → `~/.env`

### 核心功能

| 功能 | 说明 |
| :--- | :--- |
| 文本→图像 | `gpt-image-2` 模型生成 |
| 文本+参考图→图像 | 支持多参考图输入编辑 |
| 遮罩修复（Inpaint） | 不透明区域保留，透明区域重新生成 |
| 提示词画廊 | 20+ 类别精选提示词（科研图、UI、动漫、摄影等） |
| CLI 工具 | 命令行直接生图，支持 size/quality/background 等参数 |

### 使用场景（简要）

- 科研论文配图（架构图、热力图、桑基图、缩放定律图等，Nature/NeurIPS 风格）
- UI/UX 设计稿、移动端 App 模拟
- 海报与排版（杂志封面、宣传海报）
- 参考图风格迁移、遮罩修复、多图融合编辑
- 品牌识别系统展示板

---

> **⚠️ 以下为辅助工作工具，非 Skills 插件。** 记录于此供参考，无需安装为 skill，直接按仓库说明使用即可。

---

## 7. Edit Banana（截图转可编辑 Draw.io）

来源仓库：`https://github.com/bit-datalab/edit-banana`

将静态图表（流程图、架构图、科学公式等）转换为可编辑的 Draw.io（XML）格式，支持 1:1 还原布局、颜色、线条样式。

### 安装

```bash
git clone https://github.com/BIT-DataLab/Edit-Banana.git
cd Edit-Banana
pip install -r requirements.txt
bash scripts/setup_sam3.sh          # 安装 SAM3 分割模型
sudo apt install tesseract-ocr tesseract-ocr-chi-sim   # OCR 引擎
cp config/config.yaml.example config/config.yaml
# 编辑 config.yaml 配置模型路径
```

### 核心功能

| 功能 | 说明 |
| :--- | :--- |
| SAM3 精确分割 | 微调 Segment Anything Model 3 分割图表元素 |
| 多模态 VLM 引导 | 多轮 VLM 扫描保证高保真重建 |
| OCR 文字识别 | 本地 Tesseract + Pix2Text 数学公式转 LaTeX |
| 1:1 样式还原 | 布局、颜色、线条粗细、虚线等全部保留 |

### 使用场景（简要）

- 将论文/报告中截图的流程图、架构图转为 Draw.io 可编辑文件
- 科学公式图片识别并导出为 LaTeX
- 技术原理图修复与模板替换

> 在线体验：https://www.editbanana.net/

---

## 8. PPT Master（文档转PPT）

来源仓库：`https://github.com/hugohe3/ppt-master`

支持 PDF、DOCX、URL、Markdown 等文档直接转换为原生可编辑 PPTX（真实 DrawingML 形状，非图片），内置模板复制、动画、TTS 语音旁白、多格式输出。

### 安装

```bash
git clone https://github.com/hugohe3/ppt-master.git
cd ppt-master
pip install -r requirements.txt
# Windows 用户参考仓库 Windows 安装指南额外配置 PATH
```

### 核心功能

| 功能 | 说明 |
| :--- | :--- |
| 原生可编辑 | 生成的幻灯片为真实 DrawingML 形状，可逐元素编辑 |
| 多格式输入 | PDF、DOCX、URL、Markdown 直接转 PPT |
| 模板复制 | 导入任意 .pptx 作为模板，提取布局/颜色/字体 |
| 实时预览编辑 | localhost:5050 浏览器预览，点击元素标注修改 |
| 动画与过渡 | 真实 OOXML 动画，自动级联进入 |
| 语音旁白/克隆 | 支持 ElevenLabs/MiniMax/Qwen/CosyVoice 克隆声音 |
| 多画布输出 | PPT 16:9、小红书、微信等 10+ 画布格式 |

### 使用场景（简要）

- 论文/报告 PDF 转可编辑幻灯片
- 品牌模板批量生成（客户/公司现有 PPT 作为模板）
- 自动生成数据报告、季度总结演示
- 制作带语音旁白的培训视频

---

## 9. ai-figure-prompt-handbook（科研图提示词手册）

来源：本地自建 skill（`~/.codex/skills/ai-figure-prompt-handbook/`）

为学术论文设计 publication-quality 图片提供标准化提示词模板与视觉规范。覆盖 framework、motivation、comparison、pipeline、poster、media card 等多种图类型。

### 1) Codex

```bash
mkdir -p ~/.codex/skills
cp -R ai-figure-prompt-handbook ~/.codex/skills/
```

### 2) Claude Code

```bash
mkdir -p ~/.claude/skills
cp -R ai-figure-prompt-handbook ~/.claude/skills/
```

### 3) Gemini

```bash
mkdir -p ~/.gemini/skills
cp -R ai-figure-prompt-handbook ~/.gemini/skills/
```

### 核心功能

| 功能 | 说明 |
| :--- | :--- |
| 图类型自动识别 | 根据用户请求自动匹配 figure type（framework / motivation / comparison / pipeline / poster 等）|
| 标准化提示词输出 | 输出包含 Figure Prompt、Layout Notes、Text Labels、Style Constraints 四段式结构 |
| 视觉规范体系 | 内置 Color System、Icon Library、Layout Patterns、Typography、Prompt Templates 五套参考资产 |
| draw.io 联动 | 对 paper framework / motivation / comparison / pipeline 图默认生成可编辑 `.drawio` 文件 |
| 参考样例库 | 包含 motivation-comparison、pipeline-framework、architecture、poster 等多组样例图片 |

### 使用场景（简要）

- 论文 framework / motivation / comparison / pipeline 图的提示词设计
- 学术 poster 与 research media card 的视觉规范制定
- 为 AI 图像工具（DALL-E、Midjourney 等）生成精准的学术图提示词

示例提示词：

- Codex：`Use ai-figure-prompt-handbook to design a motivation figure for my paper on federated learning.`
- Claude Code：`Please use ai-figure-prompt-handbook to create a comparison figure for my paper.`
- Gemini：`Use ai-figure-prompt-handbook to generate a pipeline figure prompt for my training method.`

> 说明：本 skill 为本地自建，目录内包含 `references/samples/` 参考样例图片。

---

## 10. drawio-diagram-builder（Draw.io 图构建器）

来源：本地自建 skill（`~/.codex/skills/drawio-diagram-builder/`）

通过直接编写 draw.io XML 创建、编辑和迭代科研图表，支持从参考图复现到高保真架构图的全流程。

### 1) Codex

```bash
mkdir -p ~/.codex/skills
cp -R drawio-diagram-builder ~/.codex/skills/
```

### 2) Claude Code

```bash
mkdir -p ~/.claude/skills
cp -R drawio-diagram-builder ~/.claude/skills/
```

### 3) Gemini

```bash
mkdir -p ~/.gemini/skills
cp -R drawio-diagram-builder ~/.gemini/skills/
```

### 核心功能

| 功能 | 说明 |
| :--- | :--- |
| XML 直接建模 | 直接编写 `.drawio` XML，精确控制 mxGeometry 位置与样式 |
| 参考图复现 | 从截图/参考图出发，通过坐标清点 → 布局网格 → 资产清单 → 缺陷日志四步流程复现 |
| 迭代式修正 | 渲染截图 → 检查缺陷 → 批量修正 → 重复直到图表干净 |
| 科研风格 | 支持 publication-style 输出，保持可编辑性 |

### 使用场景（简要）

- 论文方法图、架构图、流程图的 draw.io 可编辑版本
- 参考已有论文图的精确复现
- 文字溢出、箭头、间距、图标、对齐等问题的迭代修复

示例提示词：

- Codex：`Use drawio-diagram-builder to create a system architecture diagram for my paper.`
- Claude Code：`Please use drawio-diagram-builder to replicate this reference figure as an editable draw.io file.`
- Gemini：`Use drawio-diagram-builder to fix the text overflow and alignment issues in my diagram.`

> 说明：本 skill 为本地自建。目录内 `references/samples/` 用于存放 draw.io 输出截图样例，用户可自行添加参考图。

---

## 11. research-media-card（科研媒体卡片）

来源：本地自建 skill（`~/.codex/skills/research-media-card/`）

将论文转化为面向大众的 editorial 风格信息图卡片，不直接绘制 pipeline，而是用视觉故事传递科研成果。

### 1) Codex

```bash
mkdir -p ~/.codex/skills
cp -R research-media-card ~/.codex/skills/
```

### 2) Claude Code

```bash
mkdir -p ~/.claude/skills
cp -R research-media-card ~/.claude/skills/
```

### 3) Gemini

```bash
mkdir -p ~/.gemini/skills
cp -R research-media-card ~/.gemini/skills/
```

### 核心功能

| 功能 | 说明 |
| :--- | :--- |
| 视觉叙事 | 将论文重新组织为 5-8 张卡片的完整故事线（title → takeaway → background → insight → method → evidence）|
| 非专业读者友好 | 面向 broad audience，10-20 秒内传达核心 idea |
| 卡片式编辑布局 | 温暖、现代、杂志风美学，柔和语义色、留白图标、短标签 |
| 内置参考资产 | Layout Patterns、Color System、Icon Library、Typography、Prompt Templates |
| 示例样例 | 包含 research-media-card-01/02 参考样例图片 |

### 使用场景（简要）

- 论文的社交媒体传播卡片（Twitter / 微信 / 小红书等）
- 科研成果的大众传播信息图
- Journal Club / 学术分享的 teaser card

示例提示词：

- Codex：`Use research-media-card to create a media card for my paper on large language model reasoning.`
- Claude Code：`Please use research-media-card to design a science communication card for my federated learning paper.`
- Gemini：`Use research-media-card to translate my paper into a visual story card.`

> 说明：本 skill 为本地自建，目录内包含 `references/examples/` 参考样例图片。