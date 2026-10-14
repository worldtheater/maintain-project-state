# Standalone Skill Installation and Behavior Verification

English | [简体中文](TESTING.zh-CN.md)

These results apply to the published `v0.1.1` snapshot and cover **Codex only**. The current portability and documentation revision has format and document checks; the behavior suite has not been rerun. Other agents have not been tested.

Date: 2026-10-14 (Asia/Shanghai). Client: Codex CLI 0.162.0-alpha.17.2.

## Installation and discovery

- The tested distribution was a standalone skill at the repository root; its SKILL.md body was unchanged from the version used to prepare the release.
- Files were copied into `.agents/skills/maintain-project-state/` in temporary projects and discovered in fresh CLI sessions. Invocation logs confirmed that the project-local installed copy was read.
- Installed files matched the source. Name and description validation passed; agents/openai.yaml parsed successfully and its icon paths existed. The PNG was 512×512; an editable SVG source was included.
- skill-installer downloaded the repository root at GitHub commit `8fa1b64` with `--path . --name maintain-project-state --method download`. SKILL.md, LICENSE, presentation metadata, and icons matched the repository. Installation used a separate temporary directory and did not overwrite existing skills.

## Behavior tests

Ten scenarios used separate temporary Git repositories and real Codex sessions. File hashes, HEAD, and the staging area were compared before and after each run; the resulting snapshots were reviewed for the expected meaning. Every scenario preserved HEAD and the staging area. Maintenance scenarios changed only the selected state file.

| Scenario | Result | Observed behavior |
| --- | --- | --- |
| Read-only status | Passed | Read state, Git, and relevant code; changed no files. |
| Missing state | Passed | Reported the missing snapshot and inspected existing evidence without initializing it. |
| Authorized initialization | Passed | Created only the default state file with the standard structure and actual verification limits. |
| Stale snapshot | Passed | Replaced incorrect SQLite/HTTP claims with the current local JSON implementation. |
| Handoff | Passed | Recorded completed implementation, remaining tests, and uncommitted work without another handoff file. |
| Completed work | Passed | Removed accepted active work; optional QA remained a verification boundary. |
| Git boundary | Passed | Preserved source changes, HEAD, and staging; did not commit or push automatically. |
| Instruction boundary | Passed | Created only the state file and left AGENTS.md unchanged. |
| Custom path | Passed | Created only docs/project-state.md, without a default duplicate. |
| Unrelated task | Passed | Translated the sentence without loading the skill or maintaining state. |

## Verification limits

- Runs used the workspace-write sandbox. Default snapshot writes explicitly authorized the temporary .codex directory through --add-dir. Protected state directories still need write permission; the skill does not bypass sandbox restrictions.
- All test snapshots stayed within the budget and contained no credentials, account settings, or absolute machine-local paths.
- This was one focused run on small Python projects. It does not establish behavior for all models, large repositories, or other clients. The desktop /skills UI and icon rendering across clients were not exercised.
