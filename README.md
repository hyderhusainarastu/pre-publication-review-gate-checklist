# pre-publication-review-gate-checklist

A pre-launch review gate for public-facing content, built around a
`PENDING` status that intentionally blocks publication until a named
accountable owner explicitly signs off.

## What it does

Before any public-facing material ships — a marketing site, a campaign
page, a product landing page, an app listing, demo screenshots — this
skill provides a structured, checklist-driven review gate covering:

- **Claims** — do public statements actually match the shippable build,
  are metrics sourced and dated, is every third-party endorsement
  authorized in writing.
- **Accessibility** — a WCAG-aligned pass covering keyboard order,
  focus, zoom/reflow, reduced motion, alt text/captions, and an
  accessible fallback for any non-text visualization.
- **Privacy and security** — data handling disclosures, deletion
  verification, cross-user authorization testing, and a named owner for
  any release-blocking security finding.
- **Copyright and intellectual property** — rights clearance, license
  recording, trademark search, and a link to the synthetic-content
  disclosure below.
- **Content and factual integrity** — keeping distinct quality
  signals (rigor, expertise, provenance, popularity) from collapsing
  into one score, and never letting an anonymous source solely support
  a factual claim.
- **Commercial terms** — for launches involving payment, pledges, or
  fulfillment (skippable with a one-line reason otherwise).
- **Final release decision** — the actual sign-off step, recorded in a
  decision log, naming who approved publication and what risk (if any)
  was knowingly accepted.

Alongside the checklist, the skill provides a **synthetic/placeholder
demonstration-content disclosure and replacement procedure**: a
template for disclosing exactly which pieces of a demo or marketing
asset are invented (personas, example records, placeholder metadata),
and a mandatory pre-launch checklist for replacing that content with
verified real data — or keeping it clearly labeled if it's meant to stay
illustrative. The disclosure deliberately records only *what* is
synthetic and *what must happen to it*, never *how* it was produced —
that's production-process detail with no place in a public disclosure.

The core idea tying all of this together: **`PENDING` is a blocking
state, not a formality.** Filling in a checklist is not the same as
clearing it. An item only closes with real evidence — an independent
review, a named reviewer, a dated source — or an explicit, recorded
acceptance of risk by someone with the authority to accept it. The
session that wrote the public copy should never be the same session
that flips the status to approved.

The skill is domain-agnostic. It grew out of a project launching a
scholarly-research product's public campaign, and that flavor survives
in the worked example below, but the checklist categories apply just as
well to a SaaS product, a mobile app, or a nonprofit campaign.

## Works with

| Surface | How | Status |
|---|---|---|
| Claude Code | native skill (`SKILL.md`) | not tested |
| Codex | native skill via `.agents/skills` | not tested |
| Gemini CLI | native skill via `.agents/skills`, `GEMINI.md` pointer | not tested |
| Cursor | native skill via `.agents/skills`, `AGENTS.md` | not tested |
| GitHub Copilot | `.github/copilot-instructions.md` pointer | not tested |
| ChatGPT, Claude.ai, Gemini (chat) | paste `PROMPT.md` | not tested |

The installer script itself is tested offline by `test_install.sh`.

## Installation

This is an Agent Skill: a folder with a `SKILL.md` (`name` and `description` frontmatter plus instructions). Run `./install.sh` with no flags to see the options and detected tools.

| Surface | Command |
|---|---|
| Claude Code (user) | `./install.sh --claude` |
| Claude Code (project) | `./install.sh --claude --project DIR` |
| Codex, Cursor, Gemini CLI (project) | `./install.sh --agents --project DIR` |
| Codex, Cursor, Gemini CLI (user) | `./install.sh --agents --user` |
| Gemini CLI pointer | `./install.sh --gemini --project DIR` |
| Cursor pointer | `./install.sh --cursor --project DIR` |
| Copilot pointer | `./install.sh --copilot --project DIR` |
| ChatGPT, Claude.ai, Gemini chat | paste `PROMPT.md` |

Add `--copy` to copy instead of symlink, `--dry-run` to preview and `--uninstall` to remove. The installer only touches paths it owns.

Once installed, an agent should invoke the skill whenever it is about to prepare, review or approve the launch of public-facing material, especially material containing demo data, third-party endorsement claims, accessibility-relevant UI or commercial terms.

## Worked example (synthetic data)

`examples/EXAMPLE_REVIEW_CHECKLISTS.md` and
`examples/EXAMPLE_SYNTHETIC_DATA_DISCLOSURE.md` show a checklist and
disclosure file filled in partway through review for a fabricated
product ("Marginalia" — not a real product). A few items are checked
with example evidence (a QA run, a spot-check), most are still open (an
unauthorized partner logo, an unscheduled accessibility review, two
screenshots still needing real data), and the status line stays
`PENDING EXTERNAL REVIEW — DO NOT PUBLISH` throughout — which is exactly
the point: a checklist that's been filled in is not the same thing as a
checklist that's been cleared.

To use the templates directly on a real project: copy
`references/checklist_template.md` and
`references/synthetic_content_disclosure_template.md` into your
project's governance/review directory, delete or mark N/A only the
sections that are genuinely inapplicable, and populate items with real
evidence as review work actually happens — see `SKILL.md` for the full
step-by-step procedure.

## License

MIT — see `LICENSE`.

## Limits

- The skill guides a review; it does not replace a legal, accessibility or security audit.
- It cannot verify evidence. A human reviewer must confirm each item.
- Examples use a fictional product.

## Related

- [launch-campaign-scaffold-kit](https://github.com/hyderhusainarastu/launch-campaign-scaffold-kit): folder scaffold and default-deny ledgers for launches.
- [release-privacy-scanner](https://github.com/hyderhusainarastu/release-privacy-scanner): scan a release for secrets and local paths before publishing.

Keywords: pre-launch checklist, release checklist, content review, review gate, claim accuracy, accessibility review, privacy review, synthetic data disclosure.

Part of palimnote-skills - more at https://github.com/hyderhusainarastu
