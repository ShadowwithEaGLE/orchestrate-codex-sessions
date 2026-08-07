# Quality Gates and Evidence Matrix

## Contents

1. Work-unit decision examples
2. Stage gates
3. Evidence matrix
4. Defects and environment blockers
5. Common failure modes

## Work-unit decision examples

| Scenario | Choice | Reason |
|---|---|---|
| Small fix in a known file | Level 0 | The primary task must read the exact code; handoff adds no value |
| Trace three independent call paths across a large repository | Level 1 | Scouting can run in parallel and compress results into `file:line` evidence |
| Build a compact static prototype plus investigate current state and acceptance | Level 1 | Subagents scout while the primary task retains sole implementation ownership |
| Core, UI, packaging, and QA have explicit dependencies | Level 2, serial | Durable ownership and stage gates are required |
| Two modules can be edited independently in separate worktrees | Level 2, parallel | Delivery ownership and filesystems are isolated |
| Two tasks share a checkout and modify the same file | Serial | Visible tasks do not provide file isolation |

Do not split work unless you can identify the risk, context load, or elapsed time the split reduces.

## Stage gates

### Core → UI

- Data models and public interfaces exist.
- The product, target, types, and build entry point required by UI are available.
- Normal, boundary, and corrupt inputs have real checks.
- Core changed only its owned scope.
- Unrunnable checks and raw environment errors are recorded.

### UI → Package/QA

- UI uses only accepted interfaces.
- Every user-requested visible category, state, and detail has an Acceptance criterion.
- The build passes; accessibility basics and error states are checked.
- Truncation, placeholders, or totals do not replace requested detail.

### Package/QA → Final

- Release and packaged artifacts come from accepted source.
- Program output is cross-checked against real data.
- The user-visible entry point, runtime state, and operating instructions are explicit.
- QA remained read-only; every defect went through Repair and original-QA verification.
- No unverified item is reported as passed.

## Evidence matrix

| Dimension | Minimum evidence | What cannot replace it |
|---|---|---|
| Scope | Actual changed files compared with ownership | A task claiming “I changed only these files” |
| Logic | Fixture, self-check, or regression-check output | Code review alone |
| Build | Actual Debug or Release command and exit result | Code that appears syntactically correct |
| Packaging | Artifact path, generation command, and source consistency | A successful Release build alone |
| Real data | Independent cross-check against an authoritative source | Mock or sample data |
| Visible UI | Screenshot, visible browser or app check, or explicit human acceptance | A running process |
| Runtime | Evidence for launch, refresh, exit, process, or port as applicable | Generated files |
| Security boundary | Network, permission, sensitive-data, daemon, and publishing state | Absence of observed errors |
| Unverified items | Raw blocker, affected scope, and still-confirmed boundary | A vague “environment issue” |

## Defects and environment blockers

Use three mutually exclusive outcomes:

- `PASS`: Direct evidence supports the Acceptance criterion.
- `DEFECT`: Product behavior violates the expectation with a reproducible scenario and impact.
- `ENV BLOCK`: The environment prevents verification; this does not imply product success or failure.

A DEFECT report must include:

1. A tight `file:line` reference or user-visible location;
2. Reproduction scenario;
3. Actual and expected behavior;
4. Impact;
5. Suggested minimum ownership scope without crossing the boundary to fix it.

An environment blocker must include:

1. Raw error;
2. Safe checks already attempted;
3. Blocked Acceptance criteria;
4. Evidence that still remains valid.

## Common failure modes

- **Narrowing the request:** A screenshot requires category detail, but delivery shows only a total. Give every visible element its own Acceptance criterion.
- **Orchestrator edits delegated code:** The primary task and implementation task modify the same scope. Preserve single ownership.
- **A subagent becomes a long-lived branch:** Work needs repeated user decisions but remains internal scouting. Promote it to a visible task.
- **Visible tasks are mistaken for isolation:** Tasks write concurrently in a shared checkout. Serialize or use separate worktrees.
- **QA fixes opportunistically:** Discovery, repair, and verification become one step. Create a minimal Repair task, then return to original QA.
- **Self-declared completion passes the gate:** Actual scope and command evidence are missing. The primary task must verify the gate.
- **Environment errors are hidden:** A shim, `0 tests`, or a permission bypass manufactures green. Preserve the raw failure and unverified scope.
- **The user cannot find the artifact:** Delivery reports only file generation. Provide the entry point, location, current runtime state, and opening instructions.
