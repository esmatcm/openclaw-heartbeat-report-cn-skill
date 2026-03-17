---
name: openclaw-heartbeat-report-cn
description: Generate exact Chinese reports and SOPs for the current OpenClaw heartbeat, heartbeat prompt, reporting rules, BLOCKED template, HEARTBEAT_OK behavior, active-task gates, final-report requirements, and sleep/wake token-burn control. Use when the user asks to整理心跳配置、列出每次回报格式、输出BLOCKED模板、整理HEARTBEAT_OK规则、审计是否空转烧token、解释sleep/wake哨兵机制、做成工程师报告/SOP/checklist, or wants the local heartbeat/reporting setup explained from actual files and runtime facts.
---

# OpenClaw Heartbeat Report（中文心跳与回报规范）

Produce a configuration-first Chinese report or SOP for the current OpenClaw setup.
Lead with exact configured values from local files, then add runtime-observed facts when needed.
Do not paraphrase concrete settings into vague summaries.

## Read these sources first

Resolve all paths from the current workspace root. Read the exact local files below before answering when they exist:
- `AGENTS.md`
- `HEARTBEAT.md`
- `config/main_session_task_rules.yaml` when the user asks about active-task gates, completion gates, or task heartbeat cadence
- `references/main-session-task-mode.md` when the user asks about how the main session should report progress or completion
- `references/main-session-task-card.md` when the user asks for fixed output format, task cards, or exact report templates
- `memory/executor-heartbeat-guard.json` when the user asks whether the system is sleeping, how sleep/wake works, or whether token burn has been stopped
- `memory/active-task-state.json` when the user asks whether there is a real active task, whether the tracked task changed, or why the heartbeat should wake or sleep
- `MEMORY.md` only when the user asks about long-term reporting preferences or remembered reporting conventions and the current context is a private/main session

When the user asks about current timing, scheduler cadence, or "actual" runtime behavior, prefer exact local evidence in this order:
1. `HEARTBEAT.md` hard rules if they state a fixed interval
2. `config/main_session_task_rules.yaml` for active-task cadence and completion gates
3. runtime-observed cron/job facts
4. current session/system heartbeat prompt text if present
5. local OpenClaw status or docs only when needed

Always distinguish between:
- runtime/system heartbeat cadence
- active-task reporting cadence
- dormant sentinel cadence
- final completion gate conditions

If local files and runtime/status facts differ, report both explicitly and do not collapse them into one number.

Do not invent cron jobs, scheduler IDs, or tool names that are not available in the current environment.
If an exact runtime scheduler value is not locally available, say so plainly and separate:
- file-defined heartbeat rules
- runtime-observed scheduler facts

## Sleep / Wake token-burn audit rules

When the user asks whether OpenClaw is still wasting tokens, whether an idle executor is still polling, or asks for a token-burn stop SOP, explicitly inspect and report these layers separately:
1. active/high-frequency heartbeat job
2. dormant/low-frequency sentinel job
3. guard file state (`active` vs `sleeping`)
4. active task state fingerprint source
5. background process/session facts
6. OS-process-vs-session-record mismatch if present

Use a fingerprint built from `status`, `task_id`, `next_step`, `updated_at`, and `last_output_at` when the local task state file exposes those fields.

If the user asks for a stop-burn SOP, require the report to cover:
- how to detect continuous polling
- how to disable the high-frequency heartbeat
- how to add or enable a low-frequency dormant sentinel
- how to store shared sleep/wake state in a guard file
- how to define wake-by-fingerprint-change rather than wake-by-field-existence
- how to validate that false wake conditions were removed
- how to distinguish a stale session record from a real OS process

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

When the user asks for a token-burn / sleep-wake audit or SOP, use this order:
1. 当前是否存在高频持续轮询
2. 当前 active heartbeat / dormant sentinel 状态
3. 当前 guard 文件与 active-task-state 证据
4. 当前 sleep / wake 判定逻辑
5. 当前是否已止血
6. 验收清单
7. 可直接执行的 SOP

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

### Token-burn stop acceptance summary

```text
- active heartbeat：<enabled / disabled>
- dormant sentinel：<enabled / disabled>
- guard mode：<active / sleeping / unknown>
- wake 条件：<fingerprint changed / other>
- false wake 已移除：<yes / no>
- session / OS 进程判定：<stale session / real running process / unknown>
- 最终结论：<已止血 / 未止血 / 证据不足>
```

## Wording rules

- Use Chinese labels even when the underlying keys are English.
- Preserve exact technical identifiers verbatim when they exist, for example:
  - `HEARTBEAT_OK`
  - `execution_done`
  - `browser_validation_passed`
  - `final_report_generated`
  - `RUNNING / BLOCKED / COMPLETED`
  - `active heartbeat`
  - `dormant sentinel`
  - `sleepFingerprint`
- If the user asks for a “报告”, produce a ready-to-send report, not loose notes.
- If the user asks for “给工程师直接看”, keep it structured, exact, and path-based.
- If the user asks for “SOP”, make it executable by another operator; do not return only retrospective notes.

## Local interpretation rules

- Treat `HEARTBEAT.md` as the primary local hard-rule file for heartbeat behavior.
- Treat `AGENTS.md` as the policy/context file that may add proactive heartbeat behavior, active-task requirements, and reporting style.
- Treat `config/main_session_task_rules.yaml` as the machine-readable rule source for active-task cadence and gate checks.
- Treat `references/main-session-task-card.md` as the preferred fixed-format contract when the user asks for exact report wording.
- Treat `memory/executor-heartbeat-guard.json` as the current sleep/wake state source when present.
- Treat `memory/active-task-state.json` as the current tracked task evidence source when present.
- For report channel, use the current session/channel context when available; otherwise say the channel could not be confirmed from local files alone.
- Distinguish clearly between:
  - heartbeat acknowledgment rules
  - active-task progress reporting rules
  - dormant sentinel / sleep-wake control rules
  - final completion gate rules
- If `HEARTBEAT.md`, `AGENTS.md`, guard/state files, and runtime/status facts are partially inconsistent, explicitly call out the conflict instead of pretending there is one unified source of truth.

## Do not do these

- Do not invent a heartbeat interval when the file already states one.
- Do not say “大概几分钟一次” when an exact value exists.
- Do not omit the exact rule file path.
- Do not replace fixed templates with prose summaries.
- Do not infer from old chats when the current files can be read directly.
- Do not claim token burn is stopped unless high-frequency polling was actually disabled or proven absent.
- Do not treat `next_step` merely being non-empty as sufficient evidence to wake a sleeping executor.

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
- guard/sleep-wake state when relevant
- active-vs-dormant cadence distinction when relevant
- final acceptance conclusion when the task is a token-burn audit
