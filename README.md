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

将仓库克隆到 Codex 的用户级 Skills 目录：

```bash
git clone https://github.com/jyx0919/resume-deep-dive-skill.git ~/.codex/skills/resume-deep-dive
```

安装后可以这样开始：

```text
使用 $resume-deep-dive。我会提供目标岗位 JD 和初始简历，请从第一阶段开始。
```

### Codex：项目级安装

如果只想在某个项目中使用，可将 Skill 放在项目内：

```bash
git clone https://github.com/jyx0919/resume-deep-dive-skill.git .codex/skills/resume-deep-dive
```

### 其他支持 Agent Skills 的 AI 工具

本仓库的核心是符合 Agent Skills 结构的 `SKILL.md`。请根据目标工具的官方文档，将整个 Skill 文件夹复制或注册到它的 Skill/Capability 目录。`agents/openai.yaml` 是 OpenAI/Codex 的可选界面配置；其他工具可以忽略它。

不同工具的自动发现、附件读取、PDF/DOCX 处理和长期对话能力可能不同，因此不能保证所有阶段在所有 AI 产品中具有完全一致的体验。

### 不支持 Agent Skills 的普通 AI

可以上传或粘贴 `SKILL.md`，再提供目标 JD 和初始简历，并明确要求 AI 按文件中的五阶段工作流执行。此方式可以复用核心方法，但通常不具备自动发现和自动调用能力。

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
