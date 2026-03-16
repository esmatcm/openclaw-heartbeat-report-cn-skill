# OpenClaw 心跳回报中文规范 Skill / OpenClaw Heartbeat Report CN Skill

把 **OpenClaw 心跳规则、任务态回报规则、BLOCKED 模板、完成态门禁** 整理成一份可复用、可发布的中文 AgentSkill。

这份仓库重点解决的是：

- 心跳规则散落在不同本地文件里
- 运行态 heartbeat 与 active-task cadence 容易混淆
- 想要工程师可直接使用的中文报告格式
- 遇到规则冲突时需要明确指出，而不是模糊带过

## 核心能力

- 从真实本地文件读取心跳与回报规则
- 输出中文工程师报告 / SOP / checklist
- 区分 runtime heartbeat、active-task cadence、final completion gate
- 输出固定格式的异常回报与 BLOCKED 模板
- 当 `HEARTBEAT.md`、`AGENTS.md`、运行态信息冲突时，明确列出差异

## 适用场景

适合以下需求：

- 整理当前 OpenClaw 心跳配置
- 生成“每次回报”的标准中文格式
- 输出 BLOCKED 模板
- 解释 `HEARTBEAT_OK` 规则
- 给工程师、维护者、操作者直接看的心跳规范说明

## 仓库结构

```text
openclaw-heartbeat-report-cn/
  SKILL.md
openclaw-heartbeat-report-cn.skill
```

## 安装方式

```bash
openclaw skills install ./openclaw-heartbeat-report-cn.skill
```

---

This repository packages a Chinese AgentSkill for explaining and reporting OpenClaw heartbeat rules from real local files.

It is designed for cases where you need:

- exact heartbeat/reporting rules from local configuration
- a structured Chinese engineer-facing report
- clear distinction between runtime heartbeat and active-task reporting cadence
- fixed abnormal / BLOCKED templates
- explicit conflict reporting when local rule files disagree

## Core capabilities

- read heartbeat and reporting rules from real local files
- generate Chinese SOP / checklist / engineering reports
- distinguish runtime heartbeat, active-task cadence, and completion gates
- produce fixed abnormal-report and BLOCKED templates
- surface file/runtime conflicts instead of hiding them

## Use cases

Use this skill when you need to:

- audit current OpenClaw heartbeat settings
- generate fixed Chinese progress-report formats
- output a BLOCKED template
- explain `HEARTBEAT_OK` behavior
- hand the heartbeat/reporting rules directly to engineers or operators

## Repository layout

```text
openclaw-heartbeat-report-cn/
  SKILL.md
openclaw-heartbeat-report-cn.skill
```

## Install

```bash
openclaw skills install ./openclaw-heartbeat-report-cn.skill
```
