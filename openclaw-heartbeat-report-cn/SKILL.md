---
name: openclaw-heartbeat-report-cn
description: Generate an exact Chinese report for the current OpenClaw heartbeat, heartbeat prompt, reporting rules, BLOCKED template, HEARTBEAT_OK behavior, active-task gates, and final-report requirements. Use when the user asks to整理心跳配置、列出每次回报格式、输出BLOCKED模板、整理HEARTBEAT_OK规则、做成工程师报告/SOP/checklist, or wants the local heartbeat/reporting setup explained from actual files.
---

# OpenClaw Heartbeat Report（中文心跳与回报规范）

Produce a configuration-first Chinese report for this local OpenClaw setup.
Lead with exact configured values from local files, then give the fixed report formats.
Do not paraphrase concrete settings into vague summaries.

## Read these sources first

Read the exact local files below before answering:
- `/Users/kuo/.openclaw/workspace/AGENTS.md`
- `/Users/kuo/.openclaw/workspace/HEARTBEAT.md`
- `/Users/kuo/.openclaw/workspace/config/main_session_task_rules.yaml` when the user asks about active-task gates, completion gates, or task heartbeat cadence
- `/Users/kuo/.openclaw/workspace/references/main-session-task-mode.md` when the user asks about how the main session should report progress or completion
- `/Users/kuo/.openclaw/workspace/references/main-session-task-card.md` when the user asks for fixed output format, task cards, or exact report templates
- `/Users/kuo/.openclaw/workspace/MEMORY.md` only when the user asks about long-term reporting preferences or remembered reporting conventions

When the user asks about the current time, schedule timing, or "actual" runtime timing, prefer exact local evidence in this order:
1. `HEARTBEAT.md` hard rules if they state a fixed interval
2. `config/main_session_task_rules.yaml` for active-task cadence and completion gates
3. current session/system heartbeat prompt text if present
4. local OpenClaw status or docs only when needed

Always distinguish between:
- runtime/system heartbeat cadence (for example main-session periodic heartbeat)
- active-task reporting cadence
- final completion gate conditions

If local files and runtime/status facts differ, report both explicitly and do not collapse them into one number.

Do not invent cron jobs, scheduler IDs, or tool names that are not available in the current environment.
If an exact runtime scheduler value is not locally available, say so plainly and separate:
- file-defined heartbeat rules
- runtime-observed scheduler facts

## Report order

When the user asks for a machine-default heartbeat/rule report, use this order:
1. 当前本地 OpenClaw 心跳设置
2. 心跳执行时读取的规则文件
3. 当前 heartbeat 规则本体
4. 当前“每次回报”的硬规则
5. 当前允许使用的任务状态
6. 当前“必须回报”的触发条件
7. 当前固定回报格式
8. 当前本地回报通道设置
9. 一句话总结

## Fixed formats to include

### Non-trivial task opening report

```text
- 状态：RUNNING
- task_id：<任务ID>
- 当前步骤：<当前在做什么>
- 已完成项：
  1. ...
  2. ...
- 证据：
  - <文件 / 命令输出 / 页面结果 / diff 摘要>
- 问题 / 风险：
  - ...
- 下一步：
  1. ...
  2. ...
```

### Heartbeat abnormal report

```text
- 状态：
- 当前任务：
- 已完成项：
- 发现问题：
- 恢复动作：
- 当前结果：
- 下一步：
```

### BLOCKED report

```text
- 当前状态：BLOCKED
- 当前任务：
- 阻塞原因：
- 卡住位置：
- 已尝试动作：
- 需要的最小外部信息：
- 建议下一步：
```

## Wording rules

- Use Chinese labels even when the underlying keys are English.
- Preserve exact technical identifiers verbatim when they exist, for example:
  - `HEARTBEAT_OK`
  - `execution_done`
  - `browser_validation_passed`
  - `final_report_generated`
  - `RUNNING / BLOCKED / COMPLETED`
- If the user asks for a “报告”, produce a ready-to-send report, not loose notes.
- If the user asks for “给工程师直接看”, keep it structured, exact, and path-based.

## Local interpretation rules

- Treat `HEARTBEAT.md` as the primary local hard-rule file for heartbeat behavior.
- Treat `AGENTS.md` as the policy/context file that may add proactive heartbeat behavior, active-task requirements, and reporting style.
- Treat `config/main_session_task_rules.yaml` as the machine-readable rule source for active-task cadence and gate checks.
- Treat `references/main-session-task-card.md` as the preferred fixed-format contract when the user asks for exact report wording.
- For report channel, use the current session/channel context when available; otherwise say the channel could not be confirmed from local files alone.
- Distinguish clearly between:
  - heartbeat acknowledgment rules
  - active-task progress reporting rules
  - final completion gate rules
- If `HEARTBEAT.md`, `AGENTS.md`, and runtime/status facts are partially inconsistent, explicitly call out the conflict instead of pretending there is one unified source of truth.

## Do not do these

- Do not invent a heartbeat interval when the file already states one.
- Do not say “大概几分钟一次” when an exact value exists.
- Do not omit the exact rule file path.
- Do not replace fixed templates with prose summaries.
- Do not infer from old chats when the current files can be read directly.

## Output checklist

Before sending, verify the report includes:
- exact heartbeat interval when locally known
- exact heartbeat prompt text when available
- exact rule file path
- fixed required report fields
- allowed task states when explicitly defined
- heartbeat abnormal format
- BLOCKED format
- main reporting channel when confirmable
