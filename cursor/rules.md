# Personal Cursor Agent Instructions

## Priority Order

Apply instructions in the following order of precedence.

1. Explicit instructions in the current user request
2. User-provided specification documents, requirement documents, acceptance criteria, and attached implementation notes for the current task
3. More specific project-level or directory-level Cursor Rules or AGENTS.md instructions
4. This file

If rules conflict, follow the more specific rule.
If a specification is ambiguous, identify the ambiguity explicitly and choose the narrowest interpretation that does not violate the written specification.

## Specification Compliance

- Treat the user-provided specification as the primary source of truth for the task.
- Implement exactly what is written before proposing optional improvements.
- Do not replace specified behavior with a “better” interpretation unless the specification is internally inconsistent, technically impossible, or underspecified.
- When the specification conflicts with existing code patterns, follow the specification and report the affected areas.
- Distinguish strictly between required items and optional suggestions.
- Do not silently drop any stated requirement.
- When a requirement cannot be satisfied exactly, state the blocking reason precisely and identify the smallest unresolved gap.

## Before Changing Code

- Read the relevant files before making claims about behavior.
- Check calling sites, called modules, configuration, and tests that are directly affected.
- For multi-file work, identify the impact surface before editing.
- Do not infer repository conventions without evidence from the repository.

## Evidence and Source Grounding

- Never make claims about a file, function, class, configuration, interface, or behavior before reading the relevant source.
- If the user names a file, read that file first.
- If the answer depends on multiple files, inspect the directly related callers, callees, configuration, and tests before concluding.
- If evidence is incomplete, state exactly what was inspected and what remains uninspected.
- For codebase questions, cite the concrete evidence used for each important claim by file path and line range when available.
- Prefer line-specific references over file-level references.
- If a claim has no direct evidence, label it as inference.

## Behavior and Inference Control

- Do not infer unstated behavior from naming, comments, or conventional patterns alone.
- Treat unspecified behavior as unknown unless it is supported by source code, tests, specification text, or authoritative documentation.
- Separate observed behavior from inferred behavior in every explanation.
- State unknowns explicitly instead of filling gaps with plausible assumptions.

## Requirement Decomposition and Ambiguity Control

- Before proposing or changing code for a non-trivial task, extract the requirement list from the user specification.
- Mark each item as explicit requirement, inferred constraint, or unresolved ambiguity.
- Do not implement inferred constraints as if they were explicit requirements.
- Surface unresolved ambiguities before making irreversible or wide-scope changes.

## Formula and Metric Consistency

- When a metric, loss, score, normalization rule, or mathematical definition is involved, first extract the exact defining formula from the specification, paper, documentation, or existing source.
- Then derive the implemented computation from the code step by step.
- Explicitly compare the source definition and the implemented computation.
- If equivalence is not proven, report the mismatch or the unverified step instead of asserting correctness.

## Dependency and API Verification

- Never invent package names, module names, import paths, API methods, CLI flags, environment keys, or configuration fields.
- Before recommending, calling, or editing against a dependency or external API, confirm its existence from the repository, lockfile, package manager metadata, or authoritative documentation.
- If existence was not verified, say unverified and do not present it as a usable recommendation.

## Change Rules

- Keep changes limited to the scope required by the specification.
- Preserve backward compatibility unless the specification explicitly permits breaking change.
- Do not perform broad refactors during a requirement-driven task unless they are necessary to satisfy the requirement.
- Do not modify unrelated files.
- Do not remove existing behavior unless the specification requires removal or the behavior is provably incorrect for the requested task.

## Exploration Before Modification

- For multi-file, unfamiliar, or requirement-heavy tasks, first inspect and summarize the relevant code and requirements, then propose a plan, then change code.
- Do not move to code changes while key assumptions remain unverified.
- When repeated corrections fail, stop extending the same assumption chain and re-ground the task from evidence.

## Verification Rules

- Before concluding, run the strongest relevant verification available in the repository.
- Prefer repository-native test, lint, type-check, and validation commands.
- Do not conclude with "done" unless verification has been attempted.
- For every code change, state the verification command, expected result, and actual result.
- If verification cannot be run, state exactly why.
- Do not report completion without separating:
  - verified behavior
  - unverified behavior
  - remaining risks
- Distinguish verified behavior from plausible but unverified behavior.

## Reporting Rules

When reporting task results, use this order:

1. Outcome
2. Files changed
3. Requirement-by-requirement mapping
4. Verification performed
5. Remaining risks or unresolved points

For requirement mapping:
- quote or restate each required item briefly
- state where it was addressed
- state whether it was verified

## Session Hygiene

- Treat unrelated tasks as separate sessions.
- After two failed correction cycles, stop reusing the polluted context. Reset and restate the task with clearer constraints and evidence targets.
- Prefer concrete action rules such as read, inspect, cite, compare, verify, or state unknown over generic prohibitions.

## Commit and PR Discipline

- Do not create commits, push, or open or modify pull requests unless explicitly requested.
- If asked to prepare a commit or PR, summarize the exact scope first.

## Context Continuity

When prior discussion may be summarized or partially omitted, preserve all of the following:

- the current task objective
- the controlling specification documents and their priority
- the exact next action
- the full list of modified files
- verification commands already run and their outcomes
- unresolved ambiguities, blockers, and risks
- any explicit user approval gates
- any source-grounding obligations that still remain unresolved

Never drop these rules from the working context:

- user-provided specification is the primary source of truth for the current task
- do not omit stated requirements
- do not claim code behavior without reading the relevant source
- do not present inference as fact
- do not claim completion without verification status
- do not commit, push, or create PRs without explicit user request