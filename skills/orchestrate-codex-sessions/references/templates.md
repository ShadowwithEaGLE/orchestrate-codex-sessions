# 编排模板

只读取和复制当前任务需要的模板。删除无关占位符，不为单一用途增加抽象。

## 派发前路由声明

```text
工作单元：...
级别：Level 0 / Level 1 / Level 2
侧边栏可见：是 / 否
执行载体：主任务 / spawn_agent / 可见任务
创建工具：当前准确工具名 / 无
模型：工具接受的 ID / 已核验的继承默认值 / 无
推理档位：支持档位 / 已核验的继承默认值 / 无
模型与档位依据：用户选择 / 当前工具 schema / OpenCodex 只读状态
所有权：主任务 / 独立交付任务
Depends on：无 / ...
初始状态：ready / blocked / pending
模式 / 修改范围：实施 / 侦察 / 独立 QA；准确可写文件或无
完成证据：...
```

## 项目级 AGENTS.md

```markdown
# Project Contract

## Product Goal
- 最终用户可见结果：...
- 数据来源与关键口径：...

## Global Boundaries
- 项目根目录：...
- 禁止修改：...
- 隐私、联网、权限、依赖、后台进程和发布边界：...
- 未经授权不得提交、推送或发布。

## Shared Rules
- 开始前阅读本文件。
- 只修改分配给自己的文件。
- 不回退或重构其他任务的工作。
- 发现上游问题只报告，不越权修复。
- 完成时列出修改文件、验证命令、实际结果和遗留问题。

## Ownership

### Core
- Owns: ...
- Must not edit: ...
- Prerequisites: ...
- Deliverables: ...
- Verification: ...

### UI
- Owns: ...
- Must not edit: ...
- Prerequisites: Core 闸门通过
- Deliverables: ...
- Verification: ...

### Package & QA
- Owns: 打包、真实数据、可见 UI、运行与安全验收
- Must not edit: Core/UI 实现
- Prerequisites: 可运行产物
- Deliverables: QA 报告和最终产物
- Verification: ...

## Acceptance
- 用户可见：...
- 数据正确性：...
- 构建与运行：...
- 安全与隐私：...
- 未验证项必须显式报告。
```

## Level 1 subagent 任务书

```text
执行【明确目录、模块或资料范围】内的临时子任务。

模式：边界明确的实施 / 只读侦察 / 独立 QA
允许修改：【实施的准确文件】/ 侦察或 QA 为无
输入与前置条件：【现有文件或已验收上游产物】
有限步骤与验收检查：【必须执行的动作及可运行检查】
首批输入 / 检查点：【真实有界输入 / 首个产物】
下次进度核对 / 纠偏条件：【可观察阶段证据 / 偏离】
宿主 shell / 允许读取：【实际 shell / 准确文件；无关代理日志禁止】
主任务保持最终交付所有权。

任务与验收：
【一个边界明确的实施结果或可独立回答的审查问题】
实施任务必须实际修改分配文件并运行检查，不得只返回建议。

返回：
1. 结论；
2. file:line、符号名、关键原文或来源链接；
3. 修改文件与产物、实际检查命令/结果及相关风险；
4. 未确认项。

不要扩展到相邻问题，不要修改未授权文件，不要输出大段原始日志。
若发现需要跨轮次状态、用户直接介入、独立所有权、正式交接或长期恢复，立即停止并返回：当前发现、已生成产物、升级原因和建议下一步。
```

## Level 2 可见性检查点

```text
目标任务：...
创建结果：READY / PENDING / FAILED
请求模型 / 档位：...
实际模型 / 档位：... / 未验证
thread ID：...
client ID（如有）：...
任务列表核对：标题 / 项目 / 环境 / 状态
内容抽查：PASS / FAIL / 尚不可读
决定：START / WAIT / STOP
```

## 可见实现任务书

```text
你负责【唯一职责】。

项目：...
开始前：
1. 阅读项目级 AGENTS.md；
2. 核对上游交付物和当前工作区状态；
3. 前置条件缺失时只报告，不越权修改。

所有权：
- 允许修改：...
- 禁止修改：...

必须完成：
- ...

必须验证：
- 命令：...
- 场景：正常、边界、失败路径、真实数据或可见 UI 等。

完成回复：
- 修改文件；
- 验证命令及实际结果；
- 未验证项和原因；
- 遗留风险。

你不是代码库中的唯一工作者。不要回退他人的修改；适配当前工作区状态。
```

## 只读 QA 任务书

```text
你只负责【打包/真实数据/可见 UI/运行/安全】验收。

禁止修改 Core、UI、测试或构建逻辑；禁止创建 shim、绕过权限或伪造通过。

逐项返回：
- Acceptance 项；
- 证据和实际结果；
- PASS / DEFECT / ENV BLOCK；
- DEFECT 必须含 file:line、复现场景、期望行为和影响；
- ENV BLOCK 必须含原始错误、受影响范围和仍可确认的边界。
```

## Repair 任务书

```text
只修复以下已确认根因：
【缺陷、复现、期望行为】

允许修改：...
禁止修改：其他任何文件或行为。

要求：
1. 先复现；
2. 在共享根因处做最小修改；
3. 留下一个能防止回归的最小检查；
4. 不重构相邻代码，不增加依赖，不提交。

完成时返回修改文件、精确改动、验证结果和剩余限制。
```

## Windows shell 写法

在 PowerShell 中直接使用，不再套一层 `powershell -Command`。`input.json` 是 UTF-8 数据，不是可执行代码。单引号 here-string 保留代码内引号与 JavaScript 模板表达式；较长代码保存到获授权的 `.py`/`.js` 文件，再把文件路径交给解释器。Bash 的 `<<EOF` 不是 PowerShell 语法。核对 `$LASTEXITCODE` 与真实输出；只读范围可用 stdin 避免写辅助文件。

```powershell
@'
import json
from pathlib import Path
for row in json.loads(Path("input.json").read_text(encoding="utf-8")):
    print(f"{row['name']}:{row['records']}")
'@ | python -
if ($LASTEXITCODE -ne 0) { throw "Python execution failed" }
```

```powershell
@'
const fs = require('node:fs');
const rows = JSON.parse(fs.readFileSync('input.json', 'utf8'));
for (const row of rows) console.log(`${row.name}:${row.records}`);
'@ | node -
if ($LASTEXITCODE -ne 0) { throw "Node execution failed" }
```

旧编码 shell 中通过管道传代码时保持代码为 ASCII，从 UTF-8 数据文件读取中文业务名称。代码本身需中文常量时，使用 UTF-8 脚本文件或明确设置管道编码。

## 简短监听状态

每个工作单元在工作上下文中保留一条，持久交接需要时才落盘。这些是跟踪字段，不是工具参数或虚构的运行时状态；不支持的可选字段可省略。

```text
工作单元：真实 ID / 执行载体 / 适用时的 host
Depends on：尚未满足的依赖或无
游标：工具支持时最后返回的 cursor
最近进展：时间 / 工具活动或产物证据
阻塞：无 / 证据与所需决策
原生门：当前接受 / 明确拒绝或缺失 / 结果未知
阶段：输入子集 / 预期产物 / 已验收部分
纠偏：实际偏离 / 向原代理输入或确认停止后重派 / 下一结果
回退：首选模型调用证据 / 另一模型证据 / 最终保底门 / 下个获授权路由
交付状态：执行中或已结束 / 报告缺失或已返回 / 验收待定、通过或失败
下一动作：工作 / 等待 / 诊断 / 补收报告 / 验收 / 交接 / 释放
```

## 主任务闸门回复

```text
阶段：...
范围核对：PASS / FAIL
接口与产物：PASS / FAIL
验证证据：...
未验证项：...
决定：NEXT / REPAIR / ENV BLOCK
下一步唯一动作：...
```
