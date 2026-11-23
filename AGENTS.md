# pre-publication-review-gate-checklist

A pre-launch review gate for public-facing content. A `PENDING` status blocks publishing until a named owner signs off.

## Using this in your project

- Use the skill (`SKILL.md`) before you prepare, populate, review or approve a launch of public-facing material: a campaign site, landing page, app listing, demo screenshots or promotional copy.
- Invoke it by name (`pre-publication-review-gate-checklist`) or let the agent load it when the task matches the description in `SKILL.md`.
- Copy `references/checklist_template.md` and `references/synthetic_content_disclosure_template.md` into the project's governance or review folder. Fill them in there.
- Keep the status `PENDING` until real evidence exists: an independent review, a named reviewer, a dated source, or a recorded risk acceptance by someone with authority.
- Never set the status to approved in the same session that wrote the public copy. Never invent evidence, reviewers or dates.
- The disclosure records what is synthetic and what must happen to it, never how it was produced.
- It writes only the files you copy it into. Nothing is sent over the network.
- Companions: `launch-campaign-scaffold-kit` (launch folder scaffold and validators) and `release-privacy-scanner` (scan a release for secrets and local paths before publishing).
- Paste version for chat assistants: `PROMPT.md`.

## Working on this repo

- No build step. Test: `bash test_install.sh` (offline).
- Edit `SKILL.md`, `references/` and `examples/`. Examples use fictional data only.
- Do not add real names, venues, paths or credentials.
