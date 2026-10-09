# Request to Feishu Workflow

A Codex skill for turning a repeatable request into a reviewable workflow:

1. clarify the request;
2. find or reuse specialist skills;
3. produce a sample;
4. create and verify a Feishu document;
5. optionally create a safe recurring automation.

The skill is an orchestration layer. It relies on available specialist capabilities such as `find-skills`, `agent-browser`, `lark-doc`, `lark-shared`, and Codex automation tools.

## Install

Install the repository with the skills CLI, or copy the `request-to-feishu-workflow` directory into your user skills directory:

```text
~/.codex/skills/request-to-feishu-workflow/
```

The skill does not install other skills, create documents, or schedule automations by itself. Those actions still require the user authorization required by the host environment.

## Example requests

- “找一个技能收集本周 AI 动态，先生成飞书样例，再决定是否每周运行。”
- “把这套论文阅读流程整理成飞书周报，并从下周开始每周生成新文档。”
- “先找合适的资料 skill，再把结果写入飞书，暂时不要设定时任务。”

## Structure

- `SKILL.md`: routing and workflow rules;
- `references/research-selection.md`: selecting and combining research skills;
- `references/feishu-schedule.md`: Feishu document and automation state rules;
- `agents/openai.yaml`: optional UI metadata.
