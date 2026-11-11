# Verification

## 2026-11-10 first version (0.1.0), offline only

- Unit tests (`tests/test_builder.py`, 13 tests, also run with ResourceWarning as an
  error) cover every helper:
  - lint: a deliberately bad draft (`tests/fixtures/bad.md`) fails description quality,
    personal paths, mandatory provider id, acceptance, degraded mode and missing
    referenced files, and warns on host-specific files, side
    effects without approval and an unregistered tool name, with the right line
    numbers; the improved revision (`tests/fixtures/good.md`) has no failures or
    warnings; retired workflow references and names fail (`tests/test_retired_policy.py`); hedged versus mandatory provider ids; size limit; frontmatter and name
    mismatch.
  - revisions and cases: revisions are numbered and never overwritten; cases are
    stored per revision and the missing ones reported; invalid names, cases,
    verdicts, short walk-throughs and unknown revisions are rejected.
  - install: refused for a failing draft, for missing cases and for an existing
    skill; succeeds for a clean walked-through revision into a temporary folder.
  - resources: bounded output, extra executable names are located but not run,
    invalid names ignored, model cache optional.
  - registration: five tools, additionalProperties false, skill registered, the
    install tool requires approval through pre_tool_call, and an end-to-end flow
    through the registered handlers (with the data folder redirected to a temp dir).
- Hermes admission: `hermes_cli.plugin_validate.validate_plugin_dir` result is in
  `maintenance/skill-builder-plugin-20261110/admission.json`; the workflow preflight
  in `preflight.json` next to it.

## Not verified

- A real skill-building session in Hermes, and the on-screen approval prompt for
  `skillbuilder_install`; the default Hermes data and skills folders were not written.
- Resource discovery on other platforms (macOS, Windows), AMD/Intel/Apple GPUs, and
  against a host whose tool registry is not importable (covered only by the
  `skipped` path in tests).
- Whether skills built with it perform well; the checks are structure, not quality.
- No network, model, install or publication was used.

## 2026-11-10 first live Hermes run and fixes (still 0.1.0)

- A real Hermes session (owned runtime, run kept in the maintainer's private evidence folder) built a
  skill for turning meeting recordings into searchable notes: revision 1 failed the
  degraded-mode check, revision 2 passed after the agent added a missing-recognizer
  mode; three contrasting cases recorded per revision; nothing installed.
- Defects found and fixed in source: passing check rows repeated the requirement text
  ("needs observable acceptance checks") as their detail; `skillbuilder_check` with no
  name or text returned the raw error `'name'`; `skillbuilder_resources` reported the
  CPU model, the GPU model and home-directory names inside version strings (now: CPU
  count, GPU vendor and memory only, home user names scrubbed). Three tests added
  (`LiveRunFindings`).
- Still not verified: the install approval prompt on screen; quality of any built skill.
