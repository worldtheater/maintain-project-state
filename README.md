# Maintain Project State

English | [简体中文](README.zh-CN.md)

<img src="assets/icon.png" alt="Maintain Project State" width="128" height="128">

Maintain a concise project snapshot grounded in repository evidence, so coding agents can orient, resume work, and hand off across sessions.

The snapshot records the project's purpose, architecture, conventions, implemented capabilities, active work, risks, decisions, and verification boundaries. Source code, tests, logs, and accepted design documents remain authoritative.

## Compatibility

This skill follows the [Agent Skills format](https://agentskills.io/specification). Its workflow requires access to project files and Git; updates require permission to write the selected state file. Skill discovery, installation locations, and project instruction files depend on the host agent.

The core workflow has no Codex-specific API dependency. `agents/openai.yaml` supplies optional Codex presentation metadata. **Only Codex has been tested; other agents have not been validated.**

## Installation

Repository: [worldtheater/maintain-project-state](https://github.com/worldtheater/maintain-project-state).

For other agents, install the repository's root skill directory using the host's supported Agent Skills mechanism. Include `SKILL.md`, `assets/`, and `LICENSE`; retain `agents/` when using Codex presentation metadata. Do not copy `.git`.

### Codex

Ask Codex:

```text
Use $skill-installer to install maintain-project-state from the root of https://github.com/worldtheater/maintain-project-state.
```

For manual installation, clone the repository and copy `SKILL.md`, `agents/`, `assets/`, and `LICENSE` into either:

- `~/.agents/skills/maintain-project-state/` for personal use.
- `.agents/skills/maintain-project-state/` in the target project for project use.

Start a new conversation after installation. If the skill does not appear, restart Codex. Find it through `/skills` or invoke `$maintain-project-state`. See the [Codex skills documentation](https://developers.openai.com/codex/skills) for supported locations.

## Usage

- “Review the project's current state and relevant evidence without editing files.”
- “Initialize a project-state snapshot for this repository.”
- “Update the project state for a handoff to another session.”

The default path is `.codex/project-state.md` at the project root. It is a configurable file-location convention; user- or project-specified paths take precedence. Share the same state file across agents.

Status queries are read-only. Initialization and maintenance require user or repository authorization. Keep implementation, verification, and uncommitted work distinct. The skill does not authorize automatic commits, pushes, or changes to repository instruction files, and it does not bypass filesystem permissions.

## Updates and verification

Installed skills are local copies and may need explicit reinstallation or updates. Preserve local modifications before replacing them.

[TESTING.md](TESTING.md) records the ten behavior scenarios and GitHub installation checks performed with Codex CLI for the published `v0.1.1` snapshot. Those historical results do not establish compatibility with other agents. This portability and documentation revision has format and document checks; the behavior suite has not been rerun.

The earlier [v0.1.1 source ZIP](https://github.com/worldtheater/maintain-project-state/archive/refs/tags/v0.1.1.zip) remains available as the tested snapshot. Install from the default branch for the current documentation and positioning.

## License

Author: **worldtheater**. Released under the [MIT License](LICENSE); retain the copyright and license notice when redistributing.
