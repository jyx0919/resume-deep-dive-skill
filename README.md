# Resume Deep Dive Skill｜求职简历深挖

一个以证据为基础的求职简历工作流。它不会在拿到简历后立即改写，而是先分析目标岗位、识别证据缺口，再通过逐轮 STAR 访谈补充事实，最后在用户确认后生成针对目标岗位的简历。

An evidence-first workflow for tailoring a resume to a specific job description. It maps role requirements, interviews the candidate for missing evidence, proposes line-by-line revisions, reviews the result from a recruiter’s perspective, and only generates the final resume after confirmation.

## 它解决什么问题

常见的简历优化容易出现三个问题：为了匹配 JD 而补写不存在的能力、只润色措辞却没有补足证据、过早生成最终稿导致重要信息被遗漏。

本 Skill 将简历优化拆成五个有明确门槛的阶段：

1. **JD 能力与证据映射**：提炼岗位最看重的 5–8 项能力，区分硬性要求、核心职责与加分项，并输出“JD要求｜我的对应经历｜证据是否充分｜需要补充什么”表格。
2. **STAR 逐项采访**：每轮只问 1–2 个问题，逐步补齐背景、任务、行动与结果。
3. **逐条修改对照**：按照“原文｜修改后｜为什么这样改”展示建议，等待用户确认。
4. **招聘经理 30 秒审阅**：判断候选人定位、竞争力证据、筛选风险、冗余内容、未被证明的能力与关键词匹配情况。
5. **生成最终版简历**：仅在用户明确确认后，使用已经核实的信息成稿。

## 核心原则

- 不虚构经历、数据、职责、技能、证书或成果。
- 数字无法确认时，不估算；改用可核验的交付、采用、覆盖范围、流程变化或用户反馈证明结果。
- 区分个人完成、共同完成、在指导下完成与团队成果。
- 区分计划、原型、内部测试、真实用户测试和正式上线。
- 信息没有补充完整前，不生成最终版简历。
- 真实能力缺口会被直接指出，而不是通过包装掩盖。

## 适用场景

适合：

- 已有目标 JD 和初始简历，希望进行针对性优化；
- 经历真实但表达不清楚，不知道哪些信息值得补充；
- 希望用面试式追问梳理项目、实习或工作成果；
- 希望检查修改后的简历能否通过招聘经理的快速筛选。

不适合：

- 没有目标岗位，只想获得泛化职业建议；
- 希望生成虚构经历或无法核实的数据；
- 只需要排版、美化或翻译简历。

## 安装与使用

### Codex：用户级安装

用户级安装表示：安装一次后，可以在 Codex 的不同对话和项目中继续使用这个 Skill。

最简单的安装方式，是把 `SKILL.md` 下载下来并交给 Codex 安装，不需要自己操作终端或寻找隐藏文件夹。

#### 第一步：下载 `SKILL.md`

1. 打开仓库中的 [`SKILL.md`](SKILL.md)；
2. 点击页面右上方的下载按钮，或点击 **Raw** 后保存文件；
3. 确认下载得到的文件名是 `SKILL.md`。

#### 第二步：让 Codex 安装

打开 Codex，新建一个对话，上传刚才下载的 `SKILL.md`，然后发送：

```text
请把我上传的 SKILL.md 安装为用户级 Codex Skill。
Skill 名称为 resume-deep-dive，请保存到用户级 Skills 目录，保持文件内容不变。
安装完成后，请告诉我保存路径，并确认是否可以通过 $resume-deep-dive 调用。
```

Codex 会将文件保存到类似下面的位置：

```text
~/.codex/skills/resume-deep-dive/SKILL.md
```

如果 Codex 请求写入本地文件的权限，请先确认目标路径是 `resume-deep-dive` 的用户级 Skills 目录，再允许操作。

只下载和安装 `SKILL.md` 就可以运行完整的简历工作流。仓库中的 `agents/openai.yaml` 主要用于显示名称、默认提示词等可选界面配置，不影响核心流程。

#### 第三步：新建对话并开始使用

安装完成后，新建一个 Codex 对话。如果暂时没有显示，可以重新打开 Codex，然后上传：

- 目标岗位 JD，可以是图片、PDF 或文字；
- 初始简历，建议使用 PDF、DOCX 或纯文本。

发送以下指令：

```text
使用 $resume-deep-dive。我会提供目标岗位 JD 和初始简历，请从第一阶段开始。
```

正常情况下，Codex 会先分析岗位要求并输出“JD要求｜我的对应经历｜证据是否充分｜需要补充什么”表格，而不是直接修改简历。

如果没有自动调用，可以再发送一次更明确的指令：

```text
请明确调用 $resume-deep-dive，并严格按照 SKILL.md 的五阶段工作流执行。现在只进行第一阶段，不要生成最终版简历。
```

#### 后续如何继续

Skill 会按照五个阶段逐步进行，你不需要一次提供所有信息：

1. 查看第一阶段的能力与证据表；
2. 回答 AI 每轮提出的 1–2 个 STAR 问题；
3. 不知道准确数字时直接说明“无法核实”，不要估算；
4. 审核“原文｜修改后｜为什么这样改”的逐条建议；
5. 修改完成后，让 AI 进行招聘经理 30 秒审阅；
6. 只有确认前面内容无误后，再同意生成最终版简历。

如果 AI 提前生成了最终版，可以发送：

```text
请停止生成最终版简历，回到当前阶段。信息没有补充完整、修改建议没有经过我确认前，不要进入下一阶段。
```

如果 Codex 无法直接安装上传的文件，再使用终端备用方式：

```bash
git clone https://github.com/jyx0919/resume-deep-dive-skill.git ~/.codex/skills/resume-deep-dive
```

### Codex：项目级安装

项目级安装表示：这个 Skill 只在当前项目或文件夹中使用，不会自动出现在其他项目里。适合希望把求职材料与 Skill 放在同一个独立目录中的用户。

同样可以把下载好的 `SKILL.md` 上传给 Codex，然后发送：

```text
请把我上传的 SKILL.md 安装到当前项目中。
Skill 名称为 resume-deep-dive，请保存为 .codex/skills/resume-deep-dive/SKILL.md，保持文件内容不变。
安装完成后，请告诉我保存路径，并确认是否可以通过 $resume-deep-dive 调用。
```

如果希望使用终端安装，先进入目标项目目录，再运行：

```bash
git clone https://github.com/jyx0919/resume-deep-dive-skill.git .codex/skills/resume-deep-dive
```

安装后的目录结构应当是：

```text
当前项目/
└── .codex/
    └── skills/
        └── resume-deep-dive/
            └── SKILL.md
```

然后用 Codex 打开这个项目，新建对话，上传目标 JD 和初始简历，并发送：

```text
使用 $resume-deep-dive。我会提供目标岗位 JD 和初始简历，请从第一阶段开始。
```

如果你不确定用户级和项目级应该选哪一个：

- 希望以后在多个求职对话中都能使用：选择用户级安装；
- 只希望当前项目读取这个 Skill：选择项目级安装；
- 两种方式的工作流相同，只是 Skill 的可用范围不同。

### 其他支持 Agent Skills 的 AI 工具

本仓库的核心是符合 Agent Skills 结构的 `SKILL.md`。是否能够原生安装主要取决于你使用的 AI 工具，而不是某个具体模型名称。

以下工具的官方文档已说明支持 Agent Skills：

| 工具 | 安装位置或命令 | 调用方式 |
| --- | --- | --- |
| Cursor | 将文件夹放入 `~/.cursor/skills/resume-deep-dive/` 或项目的 `.cursor/skills/resume-deep-dive/` | 在 Agent 对话中输入 `/`，搜索 `resume-deep-dive` |
| Claude Code | 将文件夹放入 `~/.claude/skills/resume-deep-dive/` | 输入 `/resume-deep-dive` |
| Gemini CLI | `gemini skills install https://github.com/jyx0919/resume-deep-dive-skill` | 先用 `/skills list` 检查，再明确要求使用 `resume-deep-dive` |

手动安装到这些工具时，需要建立 `resume-deep-dive` 文件夹并将 `SKILL.md` 放在其中；也可以直接复制整个仓库。其中：

- `SKILL.md` 是所有工具需要读取的核心工作流；
- `agents/openai.yaml` 是 OpenAI/Codex 的可选界面配置，其他工具可以忽略；
- 不同工具的自动发现、附件读取、PDF/DOCX 处理和长期对话能力可能不同。

本项目目前已经在 Codex 中验证完整工作流。Cursor、Claude Code 和 Gemini CLI 虽然支持 Agent Skills 标准，但本项目尚未逐一进行完整的端到端测试，因此不能保证体验完全一致。

关于“哪些模型能用”：

- Codex 中能够调用 Skills 的文本或推理模型可以使用；
- Cursor Agent、Claude Code 和 Gemini CLI 中能够读取 Skills 的模型原则上可以使用；
- 不限定某个 GPT、Claude 或 Gemini 型号，模型名称更新后通常不需要修改 `SKILL.md`；
- 优先选择擅长长文本理解、多轮对话和结构化分析的模型；
- 纯图片、视频或语音生成模型不适合执行这个简历工作流。

### 不支持 Agent Skills 的普通 AI

没有安装 Codex，也没有使用 Cursor、Claude Code 或 Gemini CLI，仍然可以复用这个工作流。例如，可以在支持文件上传和多轮对话的普通 AI 网页或 App 中手动使用。

#### 使用步骤

1. 在 GitHub 仓库中打开 [`SKILL.md`](SKILL.md)；
2. 下载 `SKILL.md`，或复制文件中的全部内容；
3. 在同一个 AI 对话中上传或粘贴 `SKILL.md`；
4. 上传目标岗位 JD 和初始简历；
5. 发送下面的启动指令。

```text
请完整阅读我提供的 SKILL.md，并严格按照其中的五阶段工作流执行。
我已经提供目标岗位 JD 和初始简历，请从第一阶段开始：先分析岗位要求和证据缺口，不要直接修改简历。
没有的信息请写“待补充”，不要编造。
```

如果所用 AI 不支持上传 Markdown 文件，可以把 `SKILL.md` 的全部文字直接粘贴到对话中；如果不支持读取 PDF 或图片，需要将 JD 和简历转成文字后再提供。

需要注意：

- 普通 AI 不会真正“安装”这个 Skill；
- 直接输入 `$resume-deep-dive` 通常不会生效；
- 换一个新对话时，通常需要重新上传或粘贴 `SKILL.md`；
- 部分模型可能跳过阶段或一次提出过多问题，此时需要提醒它严格遵守文件中的阶段门槛；
- 如果工具无法保持较长的多轮上下文，可能会遗漏之前的采访回答，不适合完成整个五阶段流程。

## 推荐输入

开始时提供：

- 完整目标岗位 JD；
- 当前简历，建议使用 PDF、DOCX 或纯文本；
- 目标岗位名称；
- 希望重点解决的问题（可选）。

示例：

```text
使用 $resume-deep-dive 分析我提供的产品运营岗位 JD 和初始简历。
先完成能力与证据映射，不要直接修改简历；没有的信息请标记为“待补充”，不要编造。
```

## 仓库结构

```text
resume-deep-dive-skill/
├── SKILL.md
└── agents/
    └── openai.yaml
```

- `SKILL.md`：完整的五阶段工作流与事实约束。
- `agents/openai.yaml`：OpenAI/Codex 的显示名称、默认提示词和调用策略。

## 隐私提醒

简历和 JD 可能包含姓名、电话、邮箱、公司内部数据等敏感信息。请在公开提问、提交 Issue 或分享测试案例前完成脱敏；不要将个人简历直接提交到本公开仓库。

## English overview

This skill enforces a five-stage resume workflow:

1. Map 5–8 high-impact job requirements to evidence already present in the resume.
2. Interview the candidate with only one or two STAR questions at a time.
3. Present every proposed edit as “original | revision | reason.”
4. Review the revised resume as a hiring manager scanning it for 30 seconds.
5. Generate the final resume only after the candidate confirms the revisions.

The workflow never invents experience or metrics. When a number is unavailable, it looks for other verifiable evidence, such as completion, adoption, scope, process improvement, user feedback, or a clear before-and-after change.

## License

This project is released under the [MIT License](LICENSE).

## Reference

The Skill uses the open Agent Skills structure described in the [OpenAI Skills documentation](https://developers.openai.com/api/docs/guides/tools-skills).
