# Codex 多 Session 总管

`orchestrate-codex-sessions` 是一个 Codex Skill，用第一性原理选择主任务、会话内 subagent 和可见独立任务，并通过所有权、阶段闸门、独立 QA、Repair 与证据闭环管理复杂开发工作。

## 安装

在 Codex 新任务中输入：

```text
请用 $skill-installer 安装：
https://github.com/ShadowwithEaGLE/orchestrate-codex-sessions/tree/main/skills/orchestrate-codex-sessions
```

安装完成后，下一轮任务即可使用。

## 使用

显式调用：

```text
$orchestrate-codex-sessions 总管实施：在这个项目中拆分 Core、UI、Package 和独立 QA。
```

也可使用隐式触发词：

- `总管实施`
- `编排完成`
- `多 Session`
- `项目总管`
- `独立 QA`

技能会先选择最低可行级别：主任务直接完成、主任务加 subagent，或可见多任务编排。它不会仅为形式拆分简单工作。

## 内容

```text
skills/orchestrate-codex-sessions/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── gates-and-evidence.md
    └── templates.md
```

## 边界

- 可见独立任务只在用户明确授权时创建。
- 外部写入、发布、推送、权限变更和破坏性操作仍需单独授权。
- 缺少任务、subagent、wait 或 worktree 工具时，技能会保留真实边界并降级执行。

## License

尚未选择开源许可证。
