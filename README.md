# First Principles Skill Builder

You ask for a skill, or you have one that only works on one machine. This plugin
helps the Hermes agent build or fix it so it works with the tools, hardware,
subscriptions and permissions you actually have, and says exactly what is missing
when it cannot. You give the goal; the agent finds the resources, drafts, checks,
corrects and reports.

**At a glance**

- **Install:** `hermes plugins install flabanabba8/first-principles-skill-builder`, then `hermes plugins enable first-principles-skill-builder`.
- **Needs:** Hermes 0.22 or later. No keys or extra tools; the reasoning is done by your Hermes agent.
- **Internet:** Nothing: the plugin makes no network or model calls of its own.
- **Limits:** Linux is the only platform checked. It helps the agent write and check skills; it cannot guarantee a skill works on machines it has not seen, and installing a skill needs your approval.
- **Credits:** No third-party code or data is bundled. Licence: GPL-3.0-or-later.
- **AI assistance:** Written with AI coding assistants (Anthropic Claude and OpenAI Codex agents) under the maintainer's direction; what was actually tested is listed in VERIFICATION.md.

The method is a registered skill, `first-principles-skill-builder`: establish the
goal and acceptance checks, discover resources before recommending, write the
workflow with discovery, setup, authorization, acceptance and a degraded mode for each
capability, then test it against three contrasting cases (limited CPU and offline;
capable GPU with cached models; a hosted service you explicitly chose). Reasoning is
done by the host agent. The plugin adds five deterministic helpers and no model call.

- `skillbuilder_resources`: CPU, RAM, free disk, NVIDIA GPU (via nvidia-smi), versions
  of common executables, cached model names, and the host's registered tools and
  skills. Names only: no model is loaded, no credential or account store is read.
- `skillbuilder_save`: save a draft SKILL.md as a new numbered revision in the plugin
  data folder. Earlier revisions are never overwritten.
- `skillbuilder_check`: one result per check, with offending lines: frontmatter,
  description quality, size, personal paths, mandatory provider ids, acceptance,
  degraded mode, retired workflows, harness neutrality, side effects without
  approval, referenced files and tools, and which contrasting cases are recorded.
- `skillbuilder_case`: record the agent's walk-through of one contrasting case for a
  revision, with a verdict (works, degraded, blocked).
- `skillbuilder_install`: install a clean, fully walked-through revision into your
  skills folder. It always asks a person to confirm, refuses failing checks, missing
  cases and overwrites.

It is not a scaffold generator and does not bring back the retired generic
write-a-skill, scaffold, explain or find-skills wrappers; drafts that depend on them
fail the check and cannot be installed.

Limits: the checks are structural lint (regular expressions), not a judgment that a
skill works; the walk-throughs are reasoning, not execution; GPU detection covers
NVIDIA only; host tool names are read from the Hermes registry when reachable.
The bundled `llmwiki/` has the task guide with a worked example, resource decisions,
failure diagnosis, exact schemas and provenance.
