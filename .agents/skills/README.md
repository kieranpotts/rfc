# Agent skills

Skills available to agents in this repository are:

- **[Draft RFC](./draft-rfc/):**
  Scaffolds a new RFC, ready for the user to complete.

- **[Propose RFC](./propose-rfc/):**
  Handles the `DRAFT` → `PROPOSED` transition.

- **[Accept RFC](./accept-rfc/):**
  Handles the `PROPOSED` → `ACCEPTED` transition.

- **[Implement RFC](./implement-rfc/):**
  Handles the `ACCEPTED` → `IMPLEMENTED` transition.

- **[Reject RFC](./reject-rfc/):**
  Handles the `PROPOSED` → `REJECTED` transition.

- **[Supersede RFC](./supersede-rfc/):**
  Handles the `IMPLEMENTED` → `SUPERSEDED` transition.

## Compatibility

Agent harnesses are converging on the `./.agents/skills/` path for dynamic
retrieval of project-specific skills. This is compatible with the Agent Skills
convention — see https://agentskills.io/.

As of May 2026, OpenAI Codex, GitHub Copilot, Gemini CLI, Google Antigravity,
OpenCode, and Pi will auto-discover these skills, but Claude Code and Cursor
will not.

You will require workarounds for incompatible harnesses. For Claude Code, you
can simply symlink this directory from `.claude/skills/`. Cursor requires more
effort to transpile these skills into its native "rules" format.
