# openclaw-heartbeat-report-cn-skill

Chinese AgentSkill for auditing, explaining, and reporting the current OpenClaw heartbeat / task-reporting rules from real local files.

## Included

- `openclaw-heartbeat-report-cn/` — skill source
- `openclaw-heartbeat-report-cn.skill` — packaged distributable skill

## What this skill is for

- explain local heartbeat settings from actual files
- report heartbeat cadence and task-reporting gates
- output fixed Chinese report / BLOCKED / abnormal formats
- distinguish runtime heartbeat facts vs active-task reporting rules
- surface conflicts between `HEARTBEAT.md`, `AGENTS.md`, and runtime status instead of hiding them

## Local rule sources the skill is designed to read

- `AGENTS.md`
- `HEARTBEAT.md`
- `config/main_session_task_rules.yaml`
- `references/main-session-task-mode.md`
- `references/main-session-task-card.md`

## Install the packaged skill

```bash
openclaw skills install ./openclaw-heartbeat-report-cn.skill
```
