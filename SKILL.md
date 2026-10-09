---
name: request-to-feishu-workflow
description: "Turn a request into a reviewable workflow: clarify the goal, discover or reuse skills, produce a sample, publish it to Feishu, and optionally schedule recurring runs. Use when the user wants this end-to-end workflow or a similar repeatable information task."
---

# Request to Feishu workflow

Use this as an orchestration layer. Delegate specialist work to the skills already installed in the environment; do not copy their implementation manuals into this skill.

## When to use

Use this skill when a request combines at least two of these stages:

- finding or selecting a skill for the task;
- collecting current information or processing user-provided material;
- creating a new Feishu document as the deliverable;
- repeating the workflow on a schedule.

For a one-off Feishu document, use `lark-doc` directly. For a plain web search, use the available research or browser capability directly.

## Workflow

### 1. Define the request

Record the subject, audience, source scope, output format, Feishu destination, recurrence, first-run date, time, timezone, and whether the task is one-time or recurring. Ask only for details that change the result or schedule. State reasonable defaults.

Treat “先看看效果”“只是样例” as a sample-only phase. Do not create a recurring automation during that phase.

### 2. Discover and select skills

When the user asks to find a skill, use `find-skills` and inspect the skills.sh leaderboard before recommending or installing anything. Prefer official or actively maintained sources, and do not recommend a skill from a search result alone.

Classify candidate skills by role:

- source research or domain analysis;
- browser interaction;
- document output;
- scheduling or automation.

Choose one primary skill for each needed role and a fallback only where it adds coverage. A research skill found in this step may be used as the primary source collector. Use `agent-browser` to open, verify, or supplement public pages when needed. Reuse installed skills before installing another one; install only after explicit user authorization.

### 3. Produce a sample

Collect only the material needed for the agreed scope. For current information, prefer primary sources and keep publication dates and URLs.

Separate source-supported facts from analysis, inference, and unknowns. Do not fill evidence gaps with plausible wording. Keep the first sample short enough for the user to review on a phone.

### 4. Publish to Feishu

For a new authored document, follow the `lark-doc` creation workflow: presentation decision, draft initialization, XML authoring, draft parse, `docs +create`, and `docs +fetch` verification.

Create a new document for each scheduled run when the user asks for an archive. Do not update an old document unless explicitly requested. Report the document URL and distinguish created, verified, and failed states.

### 5. Schedule after explicit approval

Before writing an automation, restate the recurrence, first-run date, time, timezone, destination, and whether each run creates a new Feishu document.

For a future first-run date, use an anchored schedule or the scheduler’s suggested-create confirmation flow. Do not create an unanchored weekly rule that could run earlier than authorized. If a confirmation card is rendered, label the task as suggested or awaiting confirmation until the tool confirms it is active.

The scheduled prompt should specify the selected research skill, the new-document behavior, the Feishu-only full report, and the short status/link returned to chat.

## Boundaries

- Do not broaden the subject, source scope, cadence, or destination silently.
- Do not install skills, write Feishu documents, send messages, change permissions, or create automations without authorization for that mutation.
- Do not claim a document or automation is complete until the relevant tool confirms it.
- If a write or schedule is rejected, report the exact state and stop at the safe boundary; do not use an unreviewed workaround.
- For finance or other high-stakes topics, provide sourced information and uncertainty, not buy, sell, or pause instructions.

## Handoff format

For a sample, report what was researched, the Feishu URL, source and verification status, and whether scheduling remains disabled.

For a schedule, report the first run, recurrence, timezone, document behavior, and confirmed automation state. Use the state terms `draft`, `suggested`, `awaiting confirmation`, `active`, `paused`, or `failed` accurately.

## Example request patterns / 示例请求

Use these as request shapes, not as fixed topics:

- 中文：关注本周 AI 发展；先找资料 skill，优先官方来源；生成飞书样例，标注事实、推断和未知项；暂时不要设定时任务。
- English: Track this week’s AI developments; find a research skill first, prioritize official sources, create a Feishu sample, label facts, inferences, and unknowns, and do not schedule it yet.
- 中文：每周五 08:00（Asia/Shanghai）从指定日期开始收集动态，每次创建新的飞书文档；先展示任务摘要，确认后再启用。
- English: Starting on the specified date, collect updates every Friday at 08:00 Asia/Shanghai, create a new Feishu document for each run, show the schedule summary first, and enable it only after confirmation.

Read the supporting references only when the corresponding stage is needed:

- [research-selection.md](references/research-selection.md) for choosing and combining research skills;
- [feishu-schedule.md](references/feishu-schedule.md) for document creation and safe scheduling state.
