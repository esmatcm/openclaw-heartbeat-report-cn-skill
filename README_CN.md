# openclaw-heartbeat-report-cn-skill

这是一个中文 AgentSkill，用来根据本地真实文件说明和汇报 OpenClaw 的心跳规则、任务态回报规则、BLOCKED 模板、以及完成态门禁。

## 仓库内容

- `openclaw-heartbeat-report-cn/`：技能源码
- `openclaw-heartbeat-report-cn.skill`：已打包技能文件

## 这个技能能做什么

- 从真实本地文件读取心跳规则
- 生成中文工程师报告 / SOP / checklist
- 区分 runtime heartbeat 与 active-task cadence
- 输出固定格式的 BLOCKED / 异常回报模板
- 遇到规则冲突时显式指出，而不是混成一句话

## 安装方式

```bash
openclaw skills install ./openclaw-heartbeat-report-cn.skill
```
