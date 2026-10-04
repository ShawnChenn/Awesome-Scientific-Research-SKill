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
7. [paper-prereview](#7-paper-prereview-tou-gao-qian-zi-cha-skill)
8. [paper-rebuttal](#8-paper-rebuttaltou-gao-hou-fan-bo-skill)
9. [edit-banana](#9-edit-bananajie-tu-zhuan-ke-bian-ji-drawio)
10. [ppt-master](#10-ppt-masterwendang-zhuan-ppt)
11. [ai-figure-prompt-handbook](#11-ai-figure-prompt-handbookke-yan-tu-ti-shi-ci-shou-ce)
12. [drawio-diagram-builder](#12-drawio-diagram-builder-drawio-tu-gou-jian-qi)
13. [research-media-card](#13-research-media-cardke-yan-mei-ti-ka-pian)
14. [anti-defensive-writing](#14-anti-defensive-writingqiang-hua-xue-zhu-wen-ben)
15. [ccf-figure](#15-ccf-figureding-hui-ji-ke-pai-ji-ke-yan-pei-tu)
16. [academic-figure-skill](#16-academic-figure-skillxue-shu-ke-yan-pei-tu-skill)
17. [scipilot-figure-skill](#17-scipilot-figure-skillke-yan-ke-yan-pei-tu-copilot)
18. [paper-framework-figure-studio-pro](#18-paper-framework-figure-studio-prolun-wen-jia-gou-tu-gong-zuo-shi)
19. [CCFA-Skills](#19-ccfa-skillsccf-a-lun-wen-ji-neng-jia-zu)
20. [vivid-figures-skill](#20-vivid-figures-skillsheng-dong-shu-ju-tu-ke-yan-hui-tu-pei-fang-ku)

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

## 5. humanizer（去除 AI 写作痕迹 · 中文增强版）

来源仓库：`https://github.com/blader/humanizer`（英文版） + `https://github.com/op7418/Humanizer-zh`（汉化增强）
本地化改造：`skills/humanizer/`（本仓库内置，含 24 模式中文适配 + 个性注入 + 质量评分）

基于 Wikipedia "Signs of AI writing" 指南，融合 Humanizer-zh 汉化增强，消除 AI 生成文本的痕迹，
使其更自然、更有人味。在原有 5 类检测基础上新增：核心规则速查、**个性与灵魂注入**（6 条原则）、
快速检查清单（10 项）、多维度质量评分（/50）。支持中英文输入，中文语境特殊适配。

### 安装

```bash
# 方式 A：从本仓库直接复制（推荐，含中文增强）
mkdir -p ~/.claude/skills
cp -R skills/humanizer ~/.claude/skills/

# 方式 B：一键安装 Humanizer-zh
npx skills add https://github.com/op7418/Humanizer-zh.git

# 方式 C：克隆英文原版
git clone https://github.com/blader/humanizer.git ~/.claude/skills/humanizer
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

### 检测的 24 种 AI 特征模式（中文适配）

| 类别 | 模式 | 中文特定警告词 |
| :--- | :--- | :--- |
| 内容模式（6种） | 意义夸大、名人效应、-ing 肤浅分析、广告式语言、模糊归因、模板化挑战段 | 标志着、见证了、作为……的证明、令人叹为观止 |
| 语言模式（6种） | AI 词汇、回避系动词、否定排比、三段式过度、同义词循环、虚假范围 | 此外、至关重要、强调、格局、充满活力、深入探讨 |
| 风格模式（6种） | 破折号滥用、粗体过度、内联标题列表、标题大小写、emoji、弯引号 | —— 连用、🚀💡✅ 装饰 |
| 交流模式（3种） | 聊天机器人话术、知识截止日期免责、谄媚语气 | 希望这对您有帮助、当然！好问题！ |
| 填充词/修饰（3种） | 填充短语、过度限定、万能积极结论 | 值得注意的是、未来看起来光明 |

### 🆕 质量评分体系（/50）

| 维度 | 评估 |
| :--- | :--- |
| 直接性 /10 | 直接陈述事实还是绕圈宣告？ |
| 节奏 /10 | 句子长短是否交错？ |
| 信任度 /10 | 是否尊重读者智慧？ |
| 真实性 /10 | 听起来像真人说话吗？ |
| 精炼度 /10 | 还有可删减的内容吗？ |

45-50 ✅ 优秀 / 35-44 ⚠️ 良好 / <35 ❌ 需重新修订

### 使用场景（简要）

- 将 AI 生成文本转换为自然人类写作风格（含中文语境优化）
- 个人声纹匹配（提供自己写作样本使输出符合个人习惯）
- 批量文档/博客/技术文章的 AI 特征检测与修正
- 团队写作前统一文本风格
- 输出附带多维度质量评分，量化改写效果

> 说明：本 skill 融合 blader/humanizer（英文原版 30 模式）和 op7418/Humanizer-zh（汉化版 24 模式 + 个性注入 + 质量评分），取两者之长。

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

## 7. Paper-PreReview（投稿前自查 Skill）

来源仓库：`https://github.com/xf686/Meet-Reviewer-2`
本地化改造：`skills/paper-prereview/`（本仓库内置，聚焦 Mode A 投稿前红队）

基于 Meet-Reviewer-2 的方法论，提取并改造为**你自己的投稿前检查 skill**。模拟一个有分歧的
审稿小组（R1 拥护者 / R2 方法怀疑论者 / R3·AC 新意鹰派），由 AC 综合预测结局
（Reject / Borderline / Accept），输出按"影响 × 成本"排序的修补清单。每条弱点必须钉到
具体位置并过 ACL **H1–H17 公正性防火墙**，绝不脑补缺陷。

### 安装

```bash
# 复制到 Claude Code 全局 skills
mkdir -p ~/.claude/skills
cp -R skills/paper-prereview ~/.claude/skills/

# 或作为插件（指向本仓库）
# /plugin marketplace add <本仓库地址>
# /plugin install paper-prereview
```

### 核心机制

| 机制 | 说明 |
| :--- | :--- |
| 三人格审稿小组 | R1 拥护者校准强弱、R2 专攻 soundness、R3·AC 卡 novelty |
| 证据契约 | 每条 weakness 钉到 `[§x / 图y / 表z / 第n段]`，定位不到标 `⚠ MISSING` |
| H1–H17 防火墙 | 对照 ACL 不正当批评黑名单过滤，命中即删除或降级 |
| 三色分级 | 🔴 实质 / 🟡 误读风险 / 🟢 打磨 |
| 修补清单 | 按"影响 × 成本"排序，标注 `✅ deadline内 / ⏳ 需新实验 / 🛟 写进 limitations` |

### 使用方式

```text
# 基础：投稿前自查自己的草稿
Red-team my draft before I submit: ~/papers/mypaper/main.tex

# 指定会议 sharpen 面板
Red-team this for NeurIPS, and add a reproducibility-stickler reviewer.

# 中文
投稿前帮我 red-team 这份草稿：~/papers/mypaper/main.tex
```

输入支持：`.pdf` / `.tex` / `.md` / arXiv 链接 / 粘贴文本。
产物输出到 `prereview/<paper-slug>.md`（含模拟结局预测 + 共识弱点 + 修补清单）。

### 使用场景（简要）

- 投稿前本地红队草稿，预测审稿意见与结局
- 按影响×成本排序生成可执行的修补清单
- 指定会议（NeurIPS/ICLR/ACL）适配对应评分量表
- 检查 claim-evidence 对齐、baseline 充分性、ablation 完整性

---

## 8. Paper-Rebuttal（投稿后反驳 Skill）

来源仓库：`https://github.com/xiongqi123123/awesome-rebuttal`
本地化改造：`skills/paper-rebuttal/`（本仓库内置，技能优先架构 + 分层原子能力）

基于 awesome-rebuttal 的方法论，提取并改造为**你自己的投稿后反驳 skill**。覆盖全生命周期：
工作区初始化 → 评审理解 → 策略规划 → 实验分类（Triage）→ 格式感知起草 →
提交前安全门禁 → 压力测试 → 多轮讨论处理。各阶段结构化记忆持久化在
`<rebuttal-workspace>/.paper-rebuttal/`。

### 安装

```bash
# 复制到 Claude Code 全局 skills
mkdir -p ~/.claude/skills
cp -R skills/paper-rebuttal ~/.claude/skills/

# 或作为插件（指向本仓库）
# /plugin marketplace add <本仓库地址>
# /plugin install paper-rebuttal
```

### 核心能力（七阶段）

| 阶段 | 能力 | 产物 |
| :--- | :--- | :--- |
| 1 评审理解 | 原子关注点账本 + 跨审稿人聚类 | `concern_ledger.json` |
| 2 策略规划 | 姿态矩阵 + 优先级 + AC 决策事实 | `strategy_matrix.json` |
| 3 实验分类 | 必须做 / 高价值 / 不推荐 / 不可行 | 写入策略矩阵 |
| 4 起草 | 单页 PDF / OpenReview / 全局 / 混合 / MD+LaTeX | `drafts/` |
| 5 安全门禁 | 无支撑声明 / 伪造 / 权限 / 敌对 / 匿名泄漏 | 5 项检查表 |
| 6 压力测试 | 重构审稿人 / 独立审稿人 / AC 模拟 | 加固清单 |
| 7 多轮讨论 | 跟进判定 + 一致性维护 | 讨论轮次回应 |

### 使用方式

```text
# 初始化工作区
Use Paper-Rebuttal to initialize this rebuttal workspace.

# 评审分析 + 策略
Use Paper-Rebuttal: the reviews are in Reference/. Build the concern analysis and a strategy plan.

# 起草单页 PDF
Use Paper-Rebuttal to draft a one-page PDF rebuttal from the approved strategy.

# 提交前压力测试
Use Paper-Rebuttal to rehearse the rebuttal: simulate the reviewers and AC, and tell me what to harden.

# 讨论期处理
Use Paper-Rebuttal: here is Reviewer 2's follow-up reply — help me decide whether and how to respond.
```

内置单页 LaTeX 模板：`skills/paper-rebuttal/assets/one-page-rebuttal-template/rebuttal.tex`。

### 使用场景（简要）

- 收到审稿意见后规范化拆解原子关注点、聚类共识弱点
- 规划反驳姿态（接受修补 / 澄清 / 温和反驳 / 暂不处理）与优先级
- 补实验分类（Triage），避免盲目跑无用实验
- 按会议格式起草 rebuttal，提交前过安全门禁防翻车
- 多轮讨论期判定是否回应、保持一致性

---

> **⚠️ 以下为辅助工作工具，非 Skills 插件。** 记录于此供参考，无需安装为 skill，直接按仓库说明使用即可。

---

## 9. Edit Banana（截图转可编辑 Draw.io）

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

## 10. PPT Master（文档转PPT）

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

## 11. ai-figure-prompt-handbook（科研图提示词手册）

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

## 12. drawio-diagram-builder（Draw.io 图构建器）

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

## 13. research-media-card（科研媒体卡片）

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

---

## 14. anti-defensive-writing（强化学术文本 · 去除防御性写作）

来源仓库：`https://github.com/Kiterlin/anti-defensive-writing`

一个 Codex skill，用于**识别并修订防御性写作（defensive writing）**——即在学术或专业文本中过度预判反驳、边界情况、读者误解或审稿人质疑，导致文字更长、更弱、焦点涣散。让论证更直接、精确、claim-forward，同时保留必要的 scope、方法局限与法律/伦理边界。

### 安装

```bash
# 方式 A：克隆后复制到 Codex skills（推荐，可先审阅内容）
git clone https://github.com/Kiterlin/anti-defensive-writing.git
mkdir -p ~/.codex/skills
cp -R anti-defensive-writing ~/.codex/skills/

# 方式 B：Claude Code 全局安装
mkdir -p ~/.claude/skills
cp -R anti-defensive-writing ~/.claude/skills/
```

> 注意：仓库 README 另提供 `curl ... | sh` 一键安装脚本，但会直接执行远程脚本，存在安全风险。建议优先使用上面的手动 clone + 复制方式，先审阅内容再安装。

### 核心能力

| 能力 | 说明 |
| :--- | :--- |
| 防御性写作检测 | 定位反复申明"本文不声称…"、贡献段以局限开头、滥用模糊 hedges（`may`/`could`/`potentially`）、冗长但无增益的 caveat |
| 文本强化改写 | 将论证改为 direct、precise、claim-forward，同时保留必要 scope 与方法局限 |
| 适用场景 | 论文、摘要、proposal、基金申请、专业报告、技术/产品说明文案 |

### 使用场景（简要）

- 论文投稿前去除防御性话术，让贡献更突出
- 摘要/引言中删减无增益的 hedging 与 caveat
- proposal / grant 文本强化论证力度但保持严谨
- 技术报告与产品说明中消除"过度保护论点"的冗长表达

示例提示词：

- Codex：`Use anti-defensive-writing to revise my paper's Introduction and remove hedging that weakens the contribution.`
- Claude Code：`Please use anti-defensive-writing to strengthen this abstract and make the claims more direct.`

> 说明：本 skill 由 Kiterlin 维护，MIT License，GitHub Topics 含 `academic-writing` / `agent-skill` / `codex-skill` / `editing` / `writing`。

---

## 15. CCF-Figure（顶会级科研配图）

来源仓库：`https://github.com/Deepshare-Official/CCF-Figure`

一个面向 AI / 计算机科学研究的 skill，用于从论文内容生成符合顶会视觉标准的出版级科研配图（NeurIPS / ICML / ICLR / CVPR / ACL / Nature MI / IEEE TPAMI 等）。核心理念是**先分类论文类型，再自动选取最优图结构**，而非机械套用"左输入→中模型→右输出"的通用模板。

### 安装

```bash
# Claude Code（用户级，所有项目可用）
git clone https://github.com/Deepshare-Official/CCF-Figure ~/.claude/skills/ccf-figure

# Claude Code（项目级）
git clone https://github.com/Deepshare-Official/CCF-Figure .claude/skills/ccf-figure

# Codex（用户级）
git clone https://github.com/Deepshare-Official/CCF-Figure ~/.agents/skills/ccf-figure

# Codex（项目级）
git clone https://github.com/Deepshare-Official/CCF-Figure .agents/skills/ccf-figure
```

### 核心能力

| 能力 | 说明 |
| :--- | :--- |
| 论文类型自动分类 | 识别 7 类论文：method、mechanism/analysis、benchmark/evaluation、scaling-law/trend、robotics/embodied-AI、interdisciplinary、survey |
| 图结构自动选择 | 从 11 种图结构中匹配最佳布局 |
| 完整提示词库 | 中英文双语 prompt 模板，可直接复制使用 |
| 5 类失败模式预防 | 内置自检清单，规避常见 AI 配图错误 |
| 迭代协议 | 标准化修订流程，最多 3 轮 |

### 使用场景（简要）

- 根据论文类型生成 method / benchmark / scaling-law 等顶会级配图
- 替代通用模板，按论文语义自动选图结构
- 中英文 prompt 辅助在 Claude Code / Codex 中出图
- 规避 AI 配图常见失败模式（自检清单）

示例提示词：

- Claude Code：`Use ccf-figure to generate a publication-ready method figure for my NeurIPS paper.`
- Codex：`Please use ccf-figure to create a benchmark/evaluation figure that matches top-venue visual standards.`

> 说明：本 skill 由 Deepshare-Official（深度之眼）维护，MIT License，GitHub Topics 含 `AI Research Tools` / `Scientific Figure Generation` / `Claude Code Skills` / `Codex Skills` / `Prompt Engineering`。

---

## 16. academic-figure-skill（学术科研配图 Skill）

来源仓库：`https://github.com/TingxiYu/academic-figure-skill`

一个面向 AI 编程助手（Claude Code / Codex / Cursor / GitHub Copilot）的 Skill 包，让其能够**自主生成符合顶刊（Nature / Cell / Science）标准的出版级科研配图**。核心理念是**"问题驱动，而非模板驱动"**——每张图都从科学问题出发，走完 **8 步闭环工作流**，最终交付：

- 矢量 **PDF** 主文件（用于投稿）
- **300 dpi PNG** 预览图
- 统计报告 + QA 报告

### 安装

```bash
# Claude Code（全局）
mkdir -p ~/ai-skills
cd ~/ai-skills
git clone https://github.com/TingxiYu/academic-figure-skill.git
cp -r academic-figure-skill ~/.claude/skills/

# Codex
git clone https://github.com/TingxiYu/academic-figure-skill.git
cd academic-figure-skill
mkdir -p ~/.codex/skills/academic-figure-skill
cp -r SKILL.md references/ scripts/ assets/ install/codex/* ~/.codex/skills/academic-figure-skill/

# Cursor（写入 .cursorrules）
git clone https://github.com/TingxiYu/academic-figure-skill.git
cp academic-figure-skill/install/cursor/.cursorrules <your-project>/.cursorrules

# GitHub Copilot（写入 .github 指令）
git clone https://github.com/TingxiYu/academic-figure-skill.git
mkdir -p <your-project>/.github
cp academic-figure-skill/install/copilot/copilot-instructions.md <your-project>/.github/
```

### 8 步工作流

1. **用户意图解析** – 澄清研究问题
2. **原型分类** – 4 种范式（定量网格 / 示意主导 / 图像+定量 / 非对称混合）
3. **图表论证** – 面板方案设计，与用户确认
4. **环境检测** – 检查 Python / R 运行环境
5. **风格注入** – 排版 + 配色基准
6. **资产检索** – 扫描 `assets/figures/<type>/` 复用生产脚本
7. **渲染生成** – 原生运行匹配脚本（Copy-First 规则）或继承参数
8. **质量校验** – 4 轮 QA 协议（30+ 检查项）后交付

### 核心能力

| 能力 | 说明 |
| :--- | :--- |
| 原型分类 | 4 种范式自动驱动布局与 hero-panel 策略 |
| 29 种图类型 | 热力图、火山图、柱状、散点、箱线、PCA、RDA、雷达、桑基、AUROC、ridge、violin 等，每种含 `.py`/`.R` 脚本 |
| Copy-First 规则 | 原生运行既有生产脚本（Python→`.py`，R→`.R`），不翻译不降质 |
| 跨类型继承 | 无匹配脚本时借用相近图类型的视觉参数（配色/比例/逻辑）|
| 多语言混排 | R 面板经 Cairo→PNG；Python `compose.py` 按物理尺寸拼多面板 |
| 4 轮 QA 协议 | Pass 0 反模式 → Pass 1 代码合规 → Pass 2 视觉逻辑 → Pass 3 渲染核验（30+ 检查）|
| 数据校验门 | 渲染前每面板预检（如火山图需 ≥10 个差异基因）|
| 期刊配色体系 | Nature（冷蓝）/ Cell（暖色）/ Science（灰）；色盲友好 |
| 审稿人模拟 | 5 维批评，区分 must-fix 与建议项 |

### 使用场景（简要）

- 从数据出发生成 CNS 级科研配图，几乎无需手动调参
- 火山图（差异表达）、AUROC 曲线（分类评估）、PCA（群体结构）、桑基（通路流）、3D 热力图（多因子互作）等
- R + Python 混合多面板复杂补充图组装
- 投稿前用 4 轮 QA 与审稿人模拟自查图表质量

示例提示词：

- Claude Code：`Use academic-figure-skill to draw a Nature-style volcano plot from data.csv.`
- Codex：`Please use academic-figure-skill to create a multipanel figure combining PCA and heatmap.`

> 说明：本 skill 由 TingxiYu 维护，Apache-2.0 License，仓库约 246 stars，覆盖 29 种图表类型与 8 步闭环工作流。

---

## 17. scipilot-figure-skill（科研配图 Copilot）

来源仓库：`https://github.com/Haojae/scipilot-figure-skill`

SciPilot Skills 家族第二成员，面向 **Claude Code / Codex / Cursor** 的科研数据可视化顾问。核心理念是**"先思考，后绘图（thinks first, plots second）"**——不立即出图，而是先对你的数据做 profiling，再帮你选对最能支撑研究论点的图。

### 安装

```bash
git clone https://github.com/Haojae/scipilot-figure-skill.git \
          ~/.claude/skills/scipilot-figure-skill
pip install -r ~/.claude/skills/scipilot-figure-skill/requirements.txt
```

### 8 步工作流

理解 → 数据 profiling → 选图 → 核对期刊规范 → 风格注入 → 绘图 → 自检 → 导出。

### 核心能力

| 能力 | 说明 |
| :--- | :--- |
| 数据 profiling 优先 | 绘图前先做 EDA，并询问"这张图要支撑什么结论"（列类型 / 样本量 / 分布 / 离群 / 相关）|
| 选图决策框架 | 按数据形态 + 意图推荐图类型（`chart_selection.md`）|
| 主动拦截坏实践 | 拒绝 n<10/组的均值柱状图（改箱线+散点）、双 Y 轴误导相关、饼图/3D、jet 配色等（15 项陷阱见 `viz_pitfalls.md`）|
| 期刊规范 | 列宽、字号、DPI、字体按目标期刊设定（`journal_specs.md`，含 Nature/Science/IEEE/Elsevier/PNAS 及中文期刊）|
| CJK 字体自动配置 | 依次回退 Noto Sans CJK SC > Source Han Sans SC > SimHei > Microsoft YaHei，修复减号/中文"豆腐块"|
| V2.1 视觉自检循环 | 渲染 PNG 后程序化审计（`visual_qa`）捕获缺字/裁切/重叠，AI 再读图查图例遮挡、面板对齐、灰度辨识，循环直到干净 |
| 五条硬规则 | 终尺寸渲染不缩放；优先矢量（PDF/SVG/EPS，不用 JPEG）；色盲安全配色（Okabe-Ito）；可读字号（7–9 pt，最小 6 pt）；误差须在 caption 说明（SD/SEM/CI + n + 检验）|
| 出版级导出 | 多格式、终尺寸输出、灰度预览（`export_figure.py`）|

### 使用场景（简要）

- 只给裸 CSV：skill 先 profiling、问清论点，推荐图类型与替代方案，确认后再绘
- 请求不合适图表：如"3 组各 5 样本用均值柱"被拦截并改为箱线+散点叠加
- 多面板合图：Nature 双栏 Figure 1 含 PCA / loss / 混淆矩阵 / 生存曲线四面板，统一字体配色，`add_panel_labels` 对齐 a/b/c/d
- 统计比较：带显著性标注的箱线图，绘前确认 n、检验方法、多重校正
- CLI 直接使用：`profile_data.py` / `setup_style.py` / `export_figure.py` / `check_figure.py`

示例提示词：

- Claude Code：`Use scipilot-figure-skill to profile data.csv and recommend a figure that supports my claim.`
- Codex：`Please use scipilot-figure-skill to build a multi-panel Nature-style figure from these results.`

> 说明：本 skill 由 Haojae 维护，MIT License（© 2026），版本 v2.1.0，仓库约 1.9k stars；基于 matplotlib + seaborn + SciencePlots（静态）与 plotly（交互），强调"先分析后绘图"与坏实践主动拦截。

---

## 18. paper-framework-figure-studio-pro（论文架构图多轮协同工作室）

来源仓库：`https://github.com/c-narcissus/paper-framework-figure-studio-pro`

一个面向 AI 编程助手（主要 ChatGPT Web，含历史 Codex 版本）的**提示词式 skill 包**，用于自动化起草计算机科学论文的**架构图 / 方法总览图 / pipeline 流程图 / agent 工作流图**。它不一次出最终图，而是通过**人机协同（human-in-the-loop）工作流**产出多个可审计的候选草稿，供作者筛选、对比、手改、定稿。当前 `main` 分支为 **v3.2.15f**。

### 获取与安装

```bash
# 克隆整个仓库（含 skill 压缩包、示例、文档）
git clone https://github.com/c-narcissus/paper-framework-figure-studio-pro.git
```

或直接下载仓库 `main` 分支的 skill 压缩包（无系统级安装，由 LLM 作为参考 skill 读取）：

- `paper-framework-figure-studio-pro-v3.2.15f-skill.zip`（ChatGPT Web 用）
- `paper-framework-figure-studio-pro-v3.2.15c-skill.zip`（旧版，含 Codex 兼容的线稿风格）

示例用法提示词：

> "请严格遵循 `sources/paper-framework-figure-studio-pro-v3.2.15f-skill.zip` 内 skill 的人机协同工作流步骤，为 `sources/semiDFL.pdf` 绘制一张图。"

### S0–S5 分阶段工作流

| 阶段 | 类型 | 内容 |
| :--- | :--- | :--- |
| S0 | 文本 | 抽取论文事实、算法、模块、箭头、风险 |
| S1 | 文本+提示词准备 | 诊断图类型、读者路径，准备可审计提示词包 |
| S2 | 仅图像 | 第一轮全局探索候选（v3.2.15f 默认 C01–C04）|
| S3 | 文本 | 评审候选、建立问题台账、记录偏好 |
| S4 | 文本+提示词准备 | 正式候选矩阵与 S5 提示词包 |
| S5 | 仅图像/终端 | 第二轮正式候选（默认 F01–F02），工作流结束，人工定稿 |

### 核心能力

| 能力 | 说明 |
| :--- | :--- |
| 提示词契约系统 | 生成前审计结构化规格（语义图、视觉渲染图、可见文本白名单、线承载变量、负向约束）|
| 两轮发散-收敛 | 先广域探索，后聚焦正式候选 |
| 严格检查点治理 | 每阶段检查点可重建，不完整则触发修复或重做 |
| 风格控制 | 默认正式出版风；可在 S1/S4 注入 `ACM/IEEE/AAAI 双栏线稿示意图` 表面风格 |
| 仅参考图输出 | 产出 PNG 候选（生成提示词存于子文件夹）供手绘复刻；非默认可编辑 SVG/PPT |
| 中断可恢复 | 通过检查点 zip 或重跑上一步提示词续作 |

### 使用场景（简要）

- CS 研究者需要论文方法总览 / 架构 / pipeline 图
- 生成多样化草稿以避免"空白页瘫痪"并对比视觉策略
- 经 S5 后风格转换满足 IEEE/Nature/PLOS/Wiley 线稿规范
- 通过让 AI 从本地知识推断 skill 构建流程，扩展到非 CS 领域
- 适配 ChatGPT Web（chat / work 模式）；历史 Codex 用旧版 zip；Cursor/subagents 版本规划中

> 说明：本 skill 由 c-narcissus 维护，MIT-0（MIT No Attribution）License，当前版本 v3.2.15f（约 66 commits）；以多轮协同产出可审计候选图为特色，最终图为参考 PNG，需人工复刻为可编辑稿件。

---

## 19. CCFA-Skills（CCF-A 论文技能族）

来源仓库：`https://github.com/mikubaka88/CCFA-Skills`

面向 **CCF-A 类论文**写作的 **AI 代理技能族**（共 17 个模块化技能），适配 Claude Code、Codex、Cursor、Gemini CLI 等。它把论文写作视为一条**"研究故事线"**，覆盖**从构思到投稿**的全生命周期：不是单一庞大 Prompt，而是分工明确的技能各司其职（检索忠实于来源、审稿独立于写作），任务在技能间传递时保留研究问题、证据与结论之间的关联。

### 安装

```bash
# Codex 一行安装
npx skills add mikubaka88/CCFA-Skills --global --agent codex --skill '*' --yes --copy

# 标准克隆（Claude Code / Cursor / Gemini CLI 等按各自 skills 目录复制）
git clone https://github.com/mikubaka88/CCFA-Skills.git
```

### 17 个核心技能（按研究阶段）

| 阶段 | 技能 | 用途 |
| :--- | :--- | :--- |
| 协调 | `ccf-common` | 共享规则、基于证据的处理、隐私 |
| 进程 | `ccf-pipeline-orchestrator` | 目标、里程碑、下一步行动 |
| 启动 | `ccf-project-scaffolder` | 论文目录 / 模板设置 |
| 构思 | `ccf-idea-reviewer` / `ccf-idea-optimizer` | 评估构思价值；把模糊想法发展为问题与方法 |
| 文献 | `ccf-literature-searcher` / `ccf-literature-monitor` | 检索相关工作、基准、基线；跟踪新论文 |
| 实验 | `ccf-experiment-designer` | 主实验、消融实验、鲁棒性 |
| 完整性 | `ccf-integrity-auditor` | 验证声明、数字、引用 |
| 评审 | `ccf-paper-reviewer` | 独立同行评审式评估、版本对比、录用就绪度 |
| 写作 | `ccf-paper-writer` / `ccf-humanization` | 起草/润色；移除防御性或机械化语言 |
| 反驳 | `ccf-rebuttal-writer` | 反驳意见、回复信、修订记录 |
| 绘图 | `ccf-visual-composer` | 可复现图表、方法/架构图、可编辑 SVG/PDF/PPTX |
| 投稿 | `ccf-submission-checker` | 模板、页数、匿名性、PDF 检查 |
| 学习 | `ccf-paper-to-exemplar` | 从你提供的模范论文提取写作模式 |
| 维护 | `ccf-skill-forger` | 改进技能本身 |

### 使用场景（简要）

- 对 3 个论文构思排名并指出可能被拒稿的原因
- 检索近 3 年特定主题的相关工作
- 设计实验且不编造结果
- 以 CVPR 风格重写方法部分
- 生成方法架构图（可编辑 PPTX 选项）
- 最新适配（2026-09）：ICLR 2027 准则——匿名性、页数限制、年度模板、AI 使用声明检查

### 红线保证

- 不伪造实验结果、引用、模块或会议规则
- 隐私：仅在授权后读取私有论文/外部搜索所需的最低限度信息
- 用户可禁用任何技能，其余技能尊重该选择
- 自动评分必须披露其度量与不确定性

> 说明：本 skill 族由 mikubaka88 维护，MIT License，版本 v0.10.0（约 60 commits），仓库约 2.9k stars / 125 forks；提供英文、简繁中文三语 README，覆盖构思→文献→实验→写作→审稿→反驳→投稿全流程。

---

## 20. vivid-figures-skill（生动数据图 · 科研绘图配方库）

来源仓库：`https://github.com/yjz211/vivid-figures-skill`

一句话定位：**把数据交给 AI，让它帮你选图、画图、检查，再交付图片和绘图源码**。面向论文、数学建模和实验报告的科研绘图 Skill，采用 Agent Skills 开放规范（根目录 `SKILL.md` 为标准 YAML 元数据 + Markdown 正文，其他文件按相对路径加载）。

### 安装

```bash
# 克隆仓库
git clone https://github.com/yjz211/vivid-figures-skill.git

# Claude Code 全局安装
mkdir -p ~/.claude/skills
cp -R vivid-figures-skill ~/.claude/skills/

# Codex 全局安装
mkdir -p ~/.codex/skills
cp -R vivid-figures-skill ~/.codex/skills/

# 安装 Python 依赖
pip install -r vivid-figures-skill/requirements.txt
```

环境要求：Python 3.10+；可选 Node.js 22.6+（用于完整图集规划）；普通数据图**无需配置图像生成 API Key**。具体安装命令以仓库内《安装指南》为准。

### 核心能力

| 能力 | 说明 |
| :--- | :--- |
| 143 个图表配方 | 146 张模板说明卡与预览：108 个原配方 + 32 个截图恢复模板 + 三维分组渐变柱状图、多Y轴渐变直方图、立体方块相关性热图等 |
| 3 套完整组合模板 | SEM 与两套 SHAP 组合图，可直接整图复用 |
| 七套配色 | 珊瑚青绿、橄榄杏棕（默认）、蓝粉浅彩、蓝天绿地、柔绿森林、粉彩少女、海洋清风，支持自定义；配色由单一 JSON 色板提供 |
| 统一模板检索 | 全部说明卡可按用途、结构和数据要求搜索、按标签筛选，下载后可在浏览器打开图文目录 |
| 全流程交付 | 读取数据 → 选择配方 → 执行绘图 → 查看结果 → 按需修复；在任务目录 `figures/` 下输出 PNG（预览）、PDF（排版）与可继续修改的绘图源码 |
| 防简化机制 | 强制先读取完整配方并以配方代码为起点适配数据；渐变、透明度层次和关键图形元素必须保留，不能随意简化成纯色或轮廓 |
| 数据诚实 | 数据不支持某元素（如无重复试验数据）时须说明调整原因，不凭空补置信带 |

### 使用方式

在对话中指明使用 `vivid-figures-skill`，可直接描述需求或指定图型（山脊图、雨云图、热力图等）：

```text
用 vivid-figures-skill 读取 results.csv，比较不同方法的得分分布。
用珊瑚青绿配色。图型你来选，输出 PNG、PDF 和绘图源码。

用 vivid-figures-skill 给这份实验结果画一组论文配图。
用珊瑚青绿配色。保留模板的渐变和层次，不要随意简化。

继续修改刚才的图：图例移到上方，字号稍微加大。
沿用已经选好的风格和配色，保留其他设计。
```

同一任务的补图/修图会自动沿用已选配色与风格。

### 使用场景（简要）

- Excel / CSV / JSON 数据快速出图：读懂字段、自动选型
- 实验结果与模型对比：性能对比、误差分布、收敛曲线、置信区间
- 空间坐标、曲面或工程数据：三维曲面、轨迹、地图或工程图
- 方法说明与关系：流程图、技术路线图、精确几何图
- 已有图与绘图源码：调整颜色、文字、间距或布局，保留原模板设计

> 说明：本 skill 由 yjz211 维护（约 433 stars / 29 forks），**仅限个人、非商业使用**，未经书面许可禁止二次开发及商业使用；项目配置使用 `.vivid/` 目录。