# Request to Feishu Workflow

## 中文版

一个把“提出需求 → 找到或复用 skills → 先出样例 → 写入飞书 → 可选定时任务”串起来的 Codex skill。

### 适用场景

1. 需要先找资料、研究或浏览器 skill，再生成一份可审核的样例。
2. 需要把完整结果写入新的飞书文档，并回查确认内容。
3. 需要按固定时间创建新的飞书文档，而不是覆盖旧文档。
4. 需要先看样例，再决定是否启用定时任务。

### 工作流程

1. 明确主题、受众、资料范围、输出格式、飞书位置和时间要求。
2. 使用 `find-skills` 和 skills.sh 选择合适的研究 skill；优先复用已安装的 skill。
3. 先生成短样例，保留来源、发布日期、URL，并区分事实、推断和未知项。
4. 按 `lark-doc` 工作流创建并验证飞书文档。
5. 启用前逐项确认四个关卡：用户认可周报样例格式；来源可靠且范围可接受；用户确认飞书文档在手机端可读；首次运行日期、周期、时区、报告位置和通知/链接接收方式均正确。任一项未确认，定时任务保持关闭。未来开始日期使用有起始边界的计划。

### 依赖与来源仓库

- [`agent-browser`](https://github.com/vercel-labs/agent-browser)：浏览器自动化 CLI；其 Codex skill 位于 [`skills/agent-browser`](https://github.com/vercel-labs/agent-browser/tree/main/skills/agent-browser)。
- [`lark-doc`](https://github.com/larksuite/cli/tree/main/skills/lark-doc)：飞书 / Lark 云文档操作 skill；所属官方仓库是 [`larksuite/cli`](https://github.com/larksuite/cli)。
- `find-skills`、`lark-shared` 和 Codex 定时任务能力：由运行环境提供，按需复用，不在本仓库复制实现手册。

这些链接用于查阅来源和版本；本 skill 不会自动安装依赖。

### 示例请求

- “关注本周 AI 发展。先找合适的资料 skill，优先官方和一手来源；先生成一份中文飞书样例，标注事实、推断和未知项，暂时不要设定时任务。”
- “每周五上午 08:00（Asia/Shanghai）收集 AI 行业动态，从我指定的首次日期开始，每次创建新的飞书文档；完整报告只放飞书，聊天只返回状态和链接。启用前先让我确认样例格式、来源可靠性、手机端可读性、首次运行时间和通知方式。”
- “我有一篇植物保护论文。先提炼主旨、病原、寄主、传播、诊断、防治和易混点，再生成 3～5 道自测题，最后创建飞书复习文档。”

### 安装

使用 skills CLI 安装本仓库，或把 `request-to-feishu-workflow` 目录复制到：

```text
~/.codex/skills/request-to-feishu-workflow/
```

本 skill 不会自行安装其他 skills、创建飞书文档或启用定时任务；这些操作仍需按照运行环境的授权规则执行。

### 目录

- `SKILL.md`：路由和工作流程规则；
- `references/research-selection.md`：研究 skill 的选择与证据记录；
- `references/feishu-schedule.md`：飞书文档和定时任务状态；
- `agents/openai.yaml`：可选的 Codex 界面元数据。

---

## English version

A Codex skill that turns “request → skill discovery or reuse → reviewed sample → Feishu document → optional schedule” into one repeatable workflow.

### When to use it

1. You need a research, browser, or domain skill before producing a reviewable sample.
2. You need the full result written to a new Feishu document and verified afterwards.
3. You need each run to create a new Feishu document instead of overwriting an old one.
4. You want to review a sample before enabling a recurring task.

### Workflow

1. Define the subject, audience, source scope, output format, Feishu destination, and timing.
2. Use `find-skills` and skills.sh to select a suitable research skill; reuse installed skills first.
3. Produce a short sample with sources, publication dates, URLs, and explicit fact/inference/unknown labels.
4. Create and verify the Feishu document through the `lark-doc` workflow.
5. Before enabling, confirm four checkpoints: the user approves the sample format; the sources are reliable and the source scope is accepted; the user confirms the Feishu document is readable in the mobile app; and the first-run date, recurrence, timezone, report destination, and notification or link delivery method are correct. Keep the task disabled while any item remains unconfirmed. Preserve a future start date with an anchored schedule.

### Dependency and source repositories

- [`agent-browser`](https://github.com/vercel-labs/agent-browser): browser automation CLI; its Codex skill is under [`skills/agent-browser`](https://github.com/vercel-labs/agent-browser/tree/main/skills/agent-browser).
- [`lark-doc`](https://github.com/larksuite/cli/tree/main/skills/lark-doc): Feishu / Lark document skill; the official parent repository is [`larksuite/cli`](https://github.com/larksuite/cli).
- `find-skills`, `lark-shared`, and Codex scheduling: provided by the host environment and reused as needed rather than copied into this repository.

These links are for source and version lookup. This skill does not install dependencies automatically.

### Example requests

- “Track this week’s AI developments. Find a suitable research skill first, prioritize official and primary sources, create a Chinese Feishu sample, label facts, inferences, and unknowns, and do not schedule it yet.”
- “Every Friday at 08:00 Asia/Shanghai, collect AI industry updates from the specified first-run date, create a new Feishu document for each run, keep the full report in Feishu, and return only a short status and link in chat. Before enabling the schedule, let me confirm the sample format, source reliability, mobile readability, first-run time, and notification method.”
- “I have a plant-protection paper. Extract the main claim, pathogen, host, transmission, diagnosis, control, and confusing points; generate 3–5 self-test questions; then create a Feishu study document.”

### Installation

Install this repository with the skills CLI, or copy the `request-to-feishu-workflow` directory to:

```text
~/.codex/skills/request-to-feishu-workflow/
```

The skill does not install other skills, create Feishu documents, or enable recurring tasks by itself; those mutations still follow the authorization rules of the host environment.

### Structure

- `SKILL.md`: routing and workflow rules;
- `references/research-selection.md`: research-skill selection and evidence handling;
- `references/feishu-schedule.md`: Feishu and scheduling states;
- `agents/openai.yaml`: optional Codex UI metadata.
