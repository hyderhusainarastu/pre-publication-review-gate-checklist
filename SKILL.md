---
name: pre-publication-review-gate-checklist
description: "A pre-launch review gate for public-facing content: claim accuracy, accessibility, privacy, copyright, content integrity, commercial-terms, and synthetic/placeholder demonstration-data disclosure and replacement, built around a PENDING status that blocks publication until a named accountable owner explicitly signs off. Invoke this skill whenever an agent is about to prepare, populate, review, or approve the launch of any public-facing material — a marketing or campaign site, a product landing page, an app listing, demo screenshots, promotional copy — especially when that material contains example/demo data, third-party endorsement claims, accessibility-relevant UI, or financial/commercial terms."
---

# Pre-publication review gate checklist

## Why this exists

Public-facing launches fail in predictable, recurring ways: a demo
screenshot with fabricated data ships as if it were real; a claim about
what the product does outruns what the current build actually does; an
accessibility pass never happens because nothing forced it to; a
third-party name appears as if endorsing the product with no
authorization on file. None of these require malice — they happen
because nothing in the process makes "not yet reviewed" a state that
visibly, mechanically blocks publication.

This skill provides that mechanism: a checklist-driven review gate whose
default state is **PENDING**, where PENDING is treated as an intentional
blocking state rather than a formality to clear on the way to shipping.
Preparing the checklist package — writing out the items, filling in
draft answers — does **not** itself certify that anything is compliant,
accessible, accurate, or authorized. Only an explicit, evidenced,
named-owner sign-off moves status off PENDING.

The skill is domain-agnostic. It grew out of a project launching a
scholarly-research product's public campaign, and that flavor survives
in a few worked examples below, but the checklist categories and the
disclosure/replacement procedure apply equally to a SaaS landing page, a
mobile app store listing, an internal tool going public, a nonprofit
campaign page, or any other public launch.

## Core design principle: PENDING is a blocking state, not a formality

Three rules make this real instead of decorative:

1. **The default status of any review-gate file this skill produces is
   `PENDING EXTERNAL REVIEW — DO NOT PUBLISH`.** State it once at the top
   of the file and once at the bottom, so it cannot be missed by a
   reader who only skims one end.
2. **The agent or session that authored the public-facing content must
   never be the one that flips PENDING to APPROVED.** Checking off a
   checklist item you filled in yourself, using only your own judgment,
   is not evidence — it is a to-do list. Each item needs either (a)
   independent verification (a named human reviewer, a separate audit,
   an external test) or (b) an explicit, recorded acceptance by a named
   accountable owner who understands they are accepting residual risk.
   If neither exists yet, the item stays unchecked and the file stays
   PENDING, however complete the content underneath it looks.
3. **A status flip is itself a governance record**, not a silent file
   edit. When a project keeps a decision log (see the companion
   `governance-records-ledger-conventions` skill, if available, or any
   equivalent record), the PENDING → APPROVED transition gets its own
   entry: who approved it, when, and what (if anything) was accepted as
   an open risk rather than fully resolved.

Never write "PENDING" and then behave as though the item is done. Never
silently change PENDING to APPROVED because the checklist looks
complete. The whole value of this pattern is that a blocking state stays
visibly blocking until a real person with the authority to accept
publication risk says otherwise.

## When to invoke this skill

Before any public-facing material ships to an audience beyond the
immediate project team: a marketing or campaign site, a product landing
page, an app store listing, promotional screenshots or demo videos,
press or outreach copy, or a public beta announcement. Invoke it earlier
rather than later — the checklist below works best as a drafting
scaffold, not just a final gate, because several items (accessibility,
synthetic-data replacement) take real lead time to close out.

## The review-gate categories

Build one checklist file with these sections, in this order. Keep every
item as a literal checkbox (`- [ ]`) so partial completion is visible at
a glance. Drop a whole section only when it is genuinely inapplicable to
the material being reviewed (e.g. "Commercial terms" for a free
informational page with no payment flow) — note the section as "N/A —
<one-line reason>" rather than silently omitting it, so a later reviewer
can see the decision was made, not missed.

### 1. Claims

- [ ] Every capability or feature claimed in public copy is demonstrated
      in the current, actually-shippable build — not a roadmap item, not
      an earlier prototype.
- [ ] Screenshots and demo media match the build being offered, and
      contain no fabricated data presented as real (see the synthetic
      content disclosure procedure below for anything that is
      intentionally illustrative).
- [ ] Any goal, limit, deadline, price, or status language in public
      copy matches the canonical source of truth for that value (a
      single manifest/config file, not copy-pasted independently into
      each surface).
- [ ] No undisclosed companion property, private beta, or unreleased
      surface is referenced in public material.
- [ ] No institution, individual, press outlet, partner, or backer is
      presented as endorsing the product, or otherwise associated with
      it, without that party's written authorization on file.
- [ ] Every metric, total, audience count, or testimonial shown in
      public material is sourced and dated, and traceable back to that
      source.

### 2. Accessibility

- [ ] An independent accessibility review against WCAG 2.2 AA (or the
      current standard your project targets) has been completed for
      every public surface — not just spot-checked.
- [ ] Keyboard operation order, visible focus indication, heading
      structure, landmark regions, link text, disclosure widgets
      (details/summary or equivalent), and form labels are all verified
      directly, not assumed from framework defaults.
- [ ] A 200% zoom / reflow pass has been completed on every public page.
- [ ] Reduced-motion behavior is verified (an OS-level reduced-motion
      preference actually suppresses non-essential animation).
- [ ] Every image, carousel, social-share image, video, and audio asset
      has approved alt text, captions, transcripts, or an
      audio-description script as appropriate to its type.
- [ ] Any 3D, canvas-rendered, or otherwise non-text-accessible
      visualization has a parity accessible fallback (e.g. a sortable
      table) verified against identical underlying data and filters —
      never shipped as the *only* way to access that information.
- [ ] Any downloadable document (PDF or equivalent) has correct reading
      order, tagging, working links, sufficient contrast, and selectable
      (not image-only) text.

### 3. Privacy and security

- [ ] The data controller, contact point, governing jurisdiction, any
      subprocessors, any third-party model/service providers, storage
      locations, retention periods, encryption posture, logging
      practices, and incident-response process are all documented and
      approved.
- [ ] If the product does anything with user data via a third-party
      AI/ML provider, the public-facing statement about whether that
      data is used for model training matches the actual provider
      contract terms and production configuration — do not let public
      copy make a stronger privacy promise than the underlying contract
      actually supports.
- [ ] Account/data deletion is verified to cover uploaded content and
      anything derived from it, with current (not stale) evidence that
      a real deletion test was run.
- [ ] Cross-user authorization boundaries are tested directly: one
      user's private data, export, and deletion actions cannot reach or
      affect another user's data.
- [ ] Any cohort-level or survey data collection has been reviewed for
      minimization — collect only what the stated purpose needs.
- [ ] A security review has identified any release-blocking findings and
      named an owner responsible for remediation of each one.

### 4. Copyright and intellectual property

- [ ] Any user-upload or user-submission terms, and any lawful-use
      guidance shown to users, have been reviewed by counsel or an
      equivalent qualified reviewer.
- [ ] Any third-party excerpt, thumbnail, frame, quotation, citation, or
      other embedded third-party material shown publicly is
      rights-cleared.
- [ ] Synthetic or placeholder imagery, personas, or records used in
      marketing or demo materials are disclosed appropriately — see the
      synthetic content disclosure procedure below.
- [ ] Font, media, narration, icon, and third-party software licenses
      used in public-facing material are recorded (what license, what
      it permits, where the obligation is satisfied — attribution file,
      footer credit, etc.).
- [ ] A trademark/logo search and visual-conflict review has been
      completed for any new mark being launched publicly.
- [ ] No full third-party work, or full-resolution protected image, is
      redistributed without explicit authorization.

### 5. Content and factual integrity

This section generalizes across domains — instantiate its items for
whatever kind of factual or evidentiary claim your product's public
material makes. (A research or scholarly product would apply these to
bibliographic and citation claims specifically; a health, financial, or
news-adjacent product would apply the same shape of item to its own
domain's claims.)

- [ ] Factual or reference claims in public material resolve to real,
      checkable, authoritative sources — not to an unverified or
      AI-generated assertion presented as settled fact.
- [ ] Any quotation shown publicly matches the inspected original source
      exactly, including edition/version where that matters.
- [ ] Where public material names or credits a real person as an expert,
      creator, or example, that person's identity and credentials are
      independently verified.
- [ ] Distinct quality dimensions — e.g. peer review status, publication
      rigor, creator expertise, source provenance, evidentiary strength,
      topical relevance, and general popularity — are kept visibly
      separate from one another, never collapsed into a single score
      that quietly lets one dimension (like popularity) stand in for
      another (like credibility).
- [ ] An anonymous or unverified social-media source never solely
      supports a factual or evaluative claim in public material.
- [ ] Where a domain has genuine competing interpretations or open
      uncertainty, public material reflects that rather than presenting
      one view as uncontested.
- [ ] If the product itself evaluates, scores, or rates content, that
      evaluation's own accuracy has been measured — including its error
      or fabrication rate, how completely it captures source provenance,
      and its performance on realistic, representative cases, not only
      favorable ones — before publishing claims about what it can do.

### 6. Commercial terms (skip with a one-line reason if not applicable)

- [ ] Current payment-processor, platform, and marketplace terms
      relevant to the launch are confirmed against the actual terms in
      force, not an earlier or assumed version.
- [ ] A tax or legal adviser has reviewed jurisdiction, income
      recognition, applicable sales tax/VAT, any required reserve, and
      the treatment of anything promised in exchange for payment.
- [ ] Underlying labor and vendor cost estimates actually support any
      stated price, goal, or funding target — not a rough guess.
- [ ] Fulfillment or delivery capacity, infrastructure cost, and support
      load have been stress-tested against a realistic (not best-case)
      demand scenario.
- [ ] Failed-payment, refund, chargeback, and multi-currency handling
      are documented, not left implicit.
- [ ] Any stretch goal, future tier, or additional commitment stays
      unpublished until it has been separately costed and scheduled —
      publishing an uncosted stretch goal is a claims-section violation
      as much as a commercial-terms one.

### 7. Final release decision

- [ ] Every critical finding from the sections above is either closed,
      or explicitly accepted as an open risk by a named accountable
      owner — "closed or accepted," never "ignored."
- [ ] All final URLs, dates, times, terms, privacy-policy links, and
      contact channels are the real production values, not placeholders
      left over from drafting.
- [ ] Every public surface that repeats a value (site, app, social
      copy, email, any downloadable material) has been checked to
      reconcile on that value — one canonical source, not independently
      retyped copies that can silently drift apart.
- [ ] A final archive snapshot of the claims/financial figures being
      published has been created, so a later audit can see exactly what
      was live at launch even if the site changes afterward.
- [ ] Publication authorization is recorded in a decision log: who
      approved it, when, and what (if anything) was accepted as residual
      risk rather than fully resolved.

The file's status line at top and bottom: `PENDING EXTERNAL REVIEW — DO
NOT PUBLISH` until every applicable item above is genuinely closed or
explicitly, namedly accepted — then, and only then, a named owner
updates the status line itself as part of the decision-log entry that
authorizes publication.

A ready-to-copy version of this checklist lives in
`references/checklist_template.md`.

## Synthetic or placeholder demonstration content: disclosure and replacement

Public-facing demos, screenshots, and marketing material frequently need
to show *something* in a UI before real user data exists — example
records, invented source titles, placeholder personas, illustrative
example text. That is legitimate, but it creates a specific risk: shown
without a label, synthetic content is publication fraud dressed as a
demo. This procedure closes that risk with a disclosure record plus a
mandatory pre-launch replacement pass.

**What the disclosure states, and what it must never state:** the
disclosure record names *what* content is synthetic and *what must
happen to it before launch*. It never describes, names, or hints at the
specific tool, workflow, model, or method used to produce that content
— that is production-process detail, is out of scope for a disclosure
whose job is protecting the audience from being misled about the
*content*, and belongs nowhere in material a public reader might see.

Maintain a disclosure file with this shape (full template in
`references/synthetic_content_disclosure_template.md`):

1. A plain statement of what categories of shown content are synthetic
   or placeholder (imagery, personas, example records, sample text,
   invented source titles, mock metrics — whatever applies), and an
   explicit statement that no real person, institution, study,
   endorsement, testimonial, or backer is represented by that content
   unless separately and explicitly labeled otherwise.
2. What that synthetic content is illustrating (an interaction model, a
   layout, a feature) and an explicit statement that it must not be
   read as verified real-world data.
3. The replacement procedure, run to completion before publication:
   - [ ] Replace every synthetic/placeholder example with rights-cleared,
         verified, real data specific to the actual production content.
   - [ ] Verify every quotation, credential claim, URL, status claim,
         and relationship/attribution claim that will actually appear
         in public material.
   - [ ] Anywhere synthetic or placeholder content deliberately remains
         at launch (e.g. a genuinely fictional example used for
         onboarding), keep a clear, visible label on it — never ship
         unlabeled fabricated content as if it were real.
   - [ ] Never let an anonymous or otherwise unverified source be the
         sole support for a factual statement in public material.
   - [ ] Never represent an engagement count, citation count, or other
         popularity signal as if it were a credibility or quality
         signal.
   - [ ] Never fabricate a real-seeming person's portrait, biography,
         affiliation, testimonial, or endorsement. A synthetic persona
         used for illustration must be unambiguously, visibly fictional
         — never presented in a way a reasonable viewer could mistake
         for a real individual.

This procedure is a hard prerequisite of Section 7 ("Final release
decision") above — an item there cannot be honestly checked off while
placeholder content that fails this checklist is still live on a public
surface.

## How to run this gate, end to end

1. **Identify the review-gate file's location** for the project (create
   one if none exists — a natural home is a `governance/` or `review/`
   directory near other project records). Use
   `references/checklist_template.md` as the starting content, deleting
   or marking N/A only the sections that are genuinely inapplicable.
2. **Identify whether a synthetic content disclosure file is needed** —
   it is, the moment any demo, screenshot, or marketing asset shows
   invented data. Create it from
   `references/synthetic_content_disclosure_template.md` alongside the
   checklist.
3. **Populate items with real, checkable evidence as work happens**, not
   in one final pass — an accessibility scan result, a named reviewer, a
   dated source for a metric. An unchecked item with no evidence stays
   unchecked; do not check an item because the underlying work merely
   feels finished.
4. **Never let the content-authoring session also be the approval
   session.** If you (the agent) drafted the public copy or built the
   demo, you can populate and evidence the checklist, but the PENDING →
   APPROVED transition itself needs a separate, named accountable owner
   — surface that requirement explicitly rather than silently
   completing it yourself.
5. **Run the synthetic-content replacement procedure to completion**
   before treating Section 7 as closeable.
6. **Record the final decision** — who approved publication, when, and
   what (if anything) was accepted as residual risk — in whatever
   decision-log convention the project uses, at the same time the status
   line changes.
7. **Create a final archive snapshot** of the claims and any financial
   figures being published, for later audit, before or at the moment of
   publication.

## Applying this in a project with no existing governance conventions

If the project has no prior review-gate file, no decision log, and no
designated "accountable owner" role, say so explicitly rather than
inventing an approval that didn't happen — populate the checklist fully,
leave the status at `PENDING EXTERNAL REVIEW — DO NOT PUBLISH`, and flag
to whoever is directing the work that a real human sign-off step is
needed before this gate can honestly close.
