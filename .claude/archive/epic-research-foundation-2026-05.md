---
epic_issue: 3
epic_title: "Research Foundation: Annotation-Driven Neuroscience Survey & White Papers"
integration_branch: main
epic_branch: feature/issue-3-epic-research-foundation
worktree_base: "/Users/yahya/Documents/git/annot-garden/epic-research-foundation"
phases:
  - number: 1
    title: "Methodical literature & artifact collection (parallel strands)"
    issue: 4
    branch: "feature/issue-4-phase1-collection"
    status: complete
    pr: 7
    merged_at: "2026-05-01T07:47:50Z"
  - number: 2
    title: "Synthesis & hierarchies"
    issue: 5
    branch: "feature/issue-5-phase2-synthesis"
    status: complete
    pr: 8
    merged_at: "2026-05-02T05:37:05Z"
    merge_commit: "3dd8649"
  - number: 3
    title: "White paper update & direction drafts"
    issue: 6
    branch: "feature/issue-6-phase3-drafts"
    status: complete
    pr: 9
    merged_at: "2026-05-02T06:35:15Z"
    merge_commit: "da24f46"
current_phase: 4
created_at: "2026-04-30T23:11:00-07:00"
---

## Notes

- Repo: Annotation-Garden/management (integration: main)
- Epic worktree: /Users/yahya/Documents/git/annot-garden/epic-research-foundation
- Phase worktrees go beside it: /Users/yahya/Documents/git/annot-garden/research-phase{N}-{slug}
- Existing related issues: #1 (white paper new-science framing), #2 (FAIR space survey) — Phase 3 should close/link these
- Seed material: ANNOTATE R01 lit review at /Users/yahya/Documents/git/grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/
- Phase 1 strategy: 3 parallel strand agents (Tools, Data, Science) per user direction
- Corpus location: research/ folder in management repo (tracked)
- Strategy change 2026-04-30: CLAUDE.md, planning docs, .context, .rules are TRACKED, not gitignored

## Phase 1 wrap-up (for resume)

- 99 entries committed under research/collection/ (33 tools, 36 data, 30 science)
- 54 OA PDFs archived in-tree; 5 paywalled retrieved via UCSD institutional access (gitignored, source.md committed)
- 10 science papers still md_quality: abstract-only — Tier 2/3, future backfill candidates: benyakov2018, cichy2014, deheer2017, finn2020, hasson2010, kay2008, lerner2011, naselaris2011, zacks2007, zheng2022
- agi_relevance recalibrated: 46 high / 40 medium / 13 low
- Schema at research/collection/_schema/paper-card.md formalizes the calibration anchors and pdf_license vocabulary
- Phase 1 PR squash-merged 2026-05-01T07:47:50Z; issue #4 closed

## Phase 2 wrap-up (for resume)

- 5 synthesis docs plus README delivered under research/synthesis/ on epic branch (commit 3dd8649)
- tool-ontology covers all 33 tool entries (5 layers, BIDS / HED / license / agi_relevance per node)
- dataset-hierarchy covers all 36 dataset entries (6 categories, 6 axes, flagship status)
- science-map covers all 30 science entries (7 themes, source-attributed open questions)
- gap-analysis names 8 concrete gaps (acceptance bar was 5)
- scope-diagram has explicit AGI / ANNOTATE complementarity statement
- PR review (2 agents): broken file:// link fixed, 5 missing abbreviations added, 7 factual fidelity fixes (Xiong 2025 hedging restored, DataLad in R01 row, HBN-EEG-only in scope-diagram, bang-multimodal copyright tier corrected, license recount with linking-exception claim removed, Theme 1 attribution per source card)
- Phase 2 PR #8 squash-merged 2026-05-02T05:37:05Z; issue #5 closed manually (Closes #5 trailer didn't auto-close because target was epic branch, not main)

## Phase 3 wrap-up (for resume)

- Updated agi-white-paper.md (1761 words). Leads with annotation-poverty thesis (#1), adds FAIR-services positioning (#2), broadens to cognitive-task wedge, adds ANNOTATE complementarity, replaces ad-hoc citations with paper-card relative paths.
- 3 direction papers added under direction-papers/: science (2139w, closes #1), tools (2063w, closes #2), data (1839w). Plus direction-papers/README.md.
- PR review (2 agents): style clean (em-dashes 0, abbreviations on first use, no AI trailers); 7 factual fidelity fixes (HBN sample sizes split, cognitive-task wedge taxonomy reconciled to 5 batteries plus 3 localizers, R01 modality matrix clarified, Huth attribution restored, production-vs-interpretation gating distinction, Pliers BIDS phrasing tightened).
- Phase 3 PR #9 squash-merged 2026-05-02T06:35:15Z (commit da24f46); issues #6, #1, #2 closed manually (Closes trailers don't auto-close because target was epic branch, not main).

## Phase 4 (final: epic to main)

When resuming via /project:epic-dev --finalize:
- Open PR from feature/issue-3-epic-research-foundation to main
- PR body: closes #3 (epic), summarizes the three phases (Phase 1 corpus + Phase 2 syntheses + Phase 3 drafts), notes that #4, #5, #6, #1, #2 already closed
- Run /review-pr on the full epic
- Final-merge gate: confirm with user before squash-merging the epic to main (per workflow)
- After merge: close epic #3 if not auto-closed, archive the state file, remove the epic worktree
