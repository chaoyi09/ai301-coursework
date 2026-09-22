# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/56

**Verdict output**

````
## Grading summary — all three from `codepath/pathreview-ai301-fa26-s1`

**Repo-level facts (apply to all three):** not archived, newest commit 6 days old (Andrew Burke, human), last push 6 days old, 2 stars, 0 releases, `docs/CONTRIBUTING.md` states no AI-use ban (silent). So `repo-alive`, `repo-not-archived`, `repo-in-use`, and `ai-work-not-banned` all **pass** for every candidate.

| Check (weight) | #56 chunker | #54 resume parser | #53 pii scrubber |
|---|---|---|---|
| repo-alive (req) | pass | pass | pass |
| repo-not-archived (req) | pass | pass | pass |
| repo-in-use (req) | pass | pass | pass |
| scope-bounded (req) | pass — one bounded regex/logic fix, concrete repro | pass — one bounded regex fix, concrete repro | pass — one bounded regex fix, concrete repro |
| not-claimed (req) | pass — no assignee, no linked PR, no comments | pass — same | pass — same |
| ai-work-not-banned (req) | pass | pass | pass |
| maintainer-answers (pref) | fail — sample of 5 other active issues shows zero maintainer replies | fail — same repo-wide sample | fail — same repo-wide sample |
| newcomer-labeled (pref) | pass — `good first issue`, `tier-1` | pass — `good first issue`, `tier-1` | pass — `good first issue`, `tier-1` |
| maintainer-in-this-thread (pref) | fail — 0 comments on the issue | fail — 0 comments | fail — 0 comments |
| no-abandoned-attempts (pref) | pass — no PRs, open 12 days | pass — no PRs, open 12 days | pass — no PRs, open 12 days |

**Verdict:** all three `accept` (every required check passes). Preferred checks tie exactly (2 pass / 2 fail) across all three, so the fit profile breaks the tie: it names `ingestion/` and `rag/` as preferred modules and calls out wanting practice with "document parsing, chunking, and how text gets prepared for retrieval," and asks to avoid frontend/DevOps. `#56` (chunking, `ingestion/`) and `#54` (resume parsing, `ingestion/`) both land squarely in that stated interest; `#53` sits in `safety/`, outside the named modules. Between the two ingestion issues, `#56` (structural chunker) is ranked first since chunking is the retrieval-prep step the profile calls out most directly; `#54` is a close second.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/56",
    "checks": [
      {"name": "repo-alive", "grade": "pass", "evidence": "newest default-branch commit 2026-09-16T21:42:18Z by Andrew Burke, 6 days before today (2026-09-22)"},
      {"name": "repo-not-archived", "grade": "pass", "evidence": "archived: false; no unmaintained/deprecated notice found"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "last push to any branch 2026-09-16, 6 days before capture date"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "single bounded bug: StructuralChunker.chunk() returns [] for headingless docs, with concrete repro and expected fix"},
      {"name": "not-claimed", "grade": "pass", "evidence": "assignees: [], no linked PRs (GraphQL timeline empty), 0 comments"},
      {"name": "ai-work-not-banned", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI-generated-code ban or mention"},
      {"name": "maintainer-answers", "grade": "fail", "evidence": "sampled 5 other recently-updated issues (#63,#62,#70,#68,#69): all comments are author_association NONE, no maintainer reply found"},
      {"name": "newcomer-labeled", "grade": "pass", "evidence": "labels: bug, good first issue, ingestion, tier-1"},
      {"name": "maintainer-in-this-thread", "grade": "fail", "evidence": "issue has 0 comments; only the COLLABORATOR-authored opening post exists"},
      {"name": "no-abandoned-attempts", "grade": "pass", "evidence": "no linked PRs; issue opened 2026-09-10, 12 days before today"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54",
    "checks": [
      {"name": "repo-alive", "grade": "pass", "evidence": "newest default-branch commit 2026-09-16T21:42:18Z by Andrew Burke, 6 days before today"},
      {"name": "repo-not-archived", "grade": "pass", "evidence": "archived: false; no unmaintained/deprecated notice found"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "last push to any branch 2026-09-16, 6 days before capture date"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "single bounded bug: _detect_sections() anchors on line-start so leading whitespace breaks section detection, with concrete repro"},
      {"name": "not-claimed", "grade": "pass", "evidence": "assignees: [], no linked PRs, 0 comments"},
      {"name": "ai-work-not-banned", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI-generated-code ban or mention"},
      {"name": "maintainer-answers", "grade": "fail", "evidence": "same repo-wide sample of 5 issues shows no maintainer replies"},
      {"name": "newcomer-labeled", "grade": "pass", "evidence": "labels: bug, good first issue, ingestion, tier-1"},
      {"name": "maintainer-in-this-thread", "grade": "fail", "evidence": "issue has 0 comments"},
      {"name": "no-abandoned-attempts", "grade": "pass", "evidence": "no linked PRs; issue opened 2026-09-10, 12 days before today"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53",
    "checks": [
      {"name": "repo-alive", "grade": "pass", "evidence": "newest default-branch commit 2026-09-16T21:42:18Z by Andrew Burke, 6 days before today"},
      {"name": "repo-not-archived", "grade": "pass", "evidence": "archived: false; no unmaintained/deprecated notice found"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "last push to any branch 2026-09-16, 6 days before capture date"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "single bounded bug: phone regex misses parenthesized US format, with concrete repro and expected fix"},
      {"name": "not-claimed", "grade": "pass", "evidence": "assignees: [], no linked PRs, 0 comments"},
      {"name": "ai-work-not-banned", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI-generated-code ban or mention"},
      {"name": "maintainer-answers", "grade": "fail", "evidence": "same repo-wide sample of 5 issues shows no maintainer replies"},
      {"name": "newcomer-labeled", "grade": "pass", "evidence": "labels: bug, good first issue, safety, tier-1"},
      {"name": "maintainer-in-this-thread", "grade": "fail", "evidence": "issue has 0 comments"},
      {"name": "no-abandoned-attempts", "grade": "pass", "evidence": "no linked PRs; issue opened 2026-09-10, 12 days before today"}
    ],
    "verdict": "accept"
  }
]
```
````

---

## Eval iterations

**Run history**

Four runs, in order:

1. `--limit 3` smoke test: **agreement 2/3**. `issue-02` and `issue-03` matched;
   `issue-01` came back `reject` against a gold `accept`.
2. `--only issue-01,issue-05,issue-09,issue-14` after revising the rubric:
   **agreement 4/4**.
3. Full run, no `--save-run`: **agreement 18/20**
   (`categories: claimed 4/4  clear-accept 8/8  dead-repo 3/3  policy 1/1  scope 2/4`).
4. Full run with `--save-run eval-run.txt`: **agreement 18/20**, same two
   disagreements (`issue-15`, `issue-20`) and the same per-category tallies. This is
   the run committed as `eval-run.txt`, whose agreement line reads
   `agreement: 18/20 scored items  (bar: 18/20: PASS)`.

Run 2 was a deliberate four-item canary rather than a re-run of everything: the
revision after run 1 loosened two checks, and loosening is only safe if what they
were catching is still caught. `issue-01` and `issue-14` had to flip to `accept`,
while `issue-05` still had to `reject` and `issue-09` tested a newly added clause.
Run 3 confirmed the whole set before I spent a save-run on it; run 4 confirmed that
18/20 reproduced rather than being a single lucky sample.

**Issue analysis**

`issue-15` (zulip/zulip#19589). My rubric graded it **`accept`**; the gold label is
**`reject`**, noted as "years of design debate and two abandoned PRs behind a
friendly label."

The check that let it through was not the one I expected. `maintainer-answers`
passed, because the sample carries `#39859 (opened 2026-07-31): 2.6 days` alongside
the slow `#38839 (opened 2026-04-06 by a maintainer): 91.7 days`, and my condition
needs only one entry under ninety days. `scope-bounded` passed as well, and I think
correctly: its clause (d) looks for a design still being debated with no maintainer
decision, and the thread does not show that. timabbott asked "can you provide an
example Slack payload or a pointer to the right part of their documentation?",
esamson supplied a captured POST body, and eeshangarg replied "Awesome, thank you so
much!" The spec settled within two months of filing.

What the thread actually shows is claim churn. Nine contributors picked the issue up
and none finished, each one followed by the same bot notice: "you have been
unassigned from this issue because you have not updated this issue or any referenced
pull requests for over 14 days." The repo facts confirm it —
`linked PRs: zulip/zulip#20840 (closed); zulip/zulip#23123 (closed)` — two attempts,
both closed unmerged, on an issue open since 2021-08-18.

My rubric saw every one of those facts and was structurally unable to act on them.
`not-claimed` passed because `assignees: none` is literally true (a bot cleared it),
neither linked PR is open (they were abandoned, not withdrawn), and the most recent
claim comment predates the 2026-08-05 capture by well over my 180-day staleness
window (the churn simply stopped). The check that graded it correctly,
`no-abandoned-attempts`, is weighted `preferred`, and my verdict rule says preferred
checks never change the verdict — so the single piece of evidence pointing the right
way was forbidden from mattering.

**Check rationale**

From the `rubric.md` uploaded to `tools/issue-select/`, the `not-claimed` row as it
is currently written:

> | `not-claimed` | Issue right sidebar / Repo facts: `this issue: assignees:`, `linked PRs:` with state per PR. Comments section: claim comments with their dates and any maintainer reply. Path Review house rule in `scope.md`. | `assignees:` is empty AND no linked PR is open AND no live claim comment is present. A claim comment is live only if it is dated within 180 days of the capture date; an older claim with no open linked PR behind it is stale and does not count. A maintainer comment inviting new takers clears any earlier claim. Per the house rule, claim comments from course classmates do not count as claims. Where the sidebar and the thread disagree, the thread decides. | required |

Four decisions are packed into that pass condition.

**Three separate sources, joined by AND.** The evidence guide is explicit that "not
every PR gets formally linked; people often just mention their PR in the comments,"
so an empty `Assignees` box on its own proves nothing. Requiring all three to be
clear means a claim announced in any of the three places still blocks the issue.

**The 180-day staleness window.** Treating every claim comment as permanent makes an
issue radioactive forever because somebody wrote "I'll take this" years ago and
vanished. `issue-09` is that case exactly: gold `accept`, noted as "the 2022 claim is
stale and the maintainer invited takers." Without an expiry my rubric rejects a
takeable issue on a four-year-old sentence.

**The maintainer-invitation override.** Dating alone would not have rescued
`issue-09` if the maintainer's invitation had come later than the claim, so an
explicit invitation clears any earlier claim regardless of dates. A maintainer saying
the issue is open is better evidence than a stranger saying it is theirs.

**Thread beats sidebar.** Taken verbatim from the evidence guide: "when the sidebar
and the thread disagree, believe the thread." The sidebar is structured data that
only updates when somebody uses the formal mechanism; the thread is where people
actually announce themselves.

**Trade-offs**

The staleness window is what this check gives up, and I can name the exact issue
whose result it changes in each direction.

It wins `issue-09` (conda/conda#7617, gold `accept`): the 2022 claim is dated out,
the maintainer's invitation overrides it, and the issue is correctly accepted. I
verified that specifically — `issue-09` was one of the four items in my `--only
issue-01,issue-05,issue-09,issue-14` canary run, and it came back `accept`, 4/4.

It loses `issue-15` (zulip/zulip#19589, gold `reject`): nine dead claims spread
across 2021 to 2024 all fall outside the window, so a thread that should read as a
warning reads as clear. The clause measures *when the last claim happened*, when the
fact worth measuring is *how many people have tried and stopped*. One dead claim and
nine dead claims are different facts, and my check cannot tell them apart.

I kept the clause anyway, and the reason is an asymmetry in what the two errors cost
me. A stale claim I wrongly honour deletes a good issue from my candidate list
silently — I never see it, so I never learn it was available. A stale claim I
wrongly ignore costs one comment asking whether anyone is still on it. The second
error is recoverable in a way the first is not.

The narrow fix — promoting `no-abandoned-attempts` from `preferred` to `required` —
would likely have caught `issue-15`, and I chose not to make it. Its two conditions
are noisy as gates: a single closed-unmerged PR is routine on healthy issues, and its
365-day age limit would reject `issue-09`, a gold `accept`, purely for being old.
That trade pays for two arguable `scope` items with damage to the `clear-accept`
category, which is currently 8/8. What I would build given more room is a check that
counts distinct claimants rather than dating the most recent one.

---

## Selection rationale

**Selection rationale**

**1. Fit to my interests and the time available.
** I want to practice RAG and ingestion code — specifically how documents get parsed and chunked before retrieval — which is what I put in my fit profile. #56 is a chunker bug in ingestion/, so it matches directly. It is also small: one function returning an empty list when it shouldn't, with the expected behaviour already stated in the issue. That fits the time I have before Unit 2.

**2. What the verdict identified correctly, and what I weighed that it could not.
**The verdict got the mechanical facts right: active repo, no assignee, no linked PR, no comments, one bounded fix, no AI ban in CONTRIBUTING.md. But all three candidates tied on every check, so the rubric couldn't pick between them — that part was mine. I chose the chunker over the resume parser because I want to understand chunking specifically. I also discounted the failing maintainer-answers check: this is a classroom repo, so quiet issue threads don't mean what they would in a real project.

**3. Anticipated difficulty in claiming it.
** Low. Twelve days old, no assignee, no PR, no comments, and the house rule says classmate claims don't block anything. The harder part will be reproducing it — I need the project running locally with a headingless test document before I can confirm the bug.


---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
