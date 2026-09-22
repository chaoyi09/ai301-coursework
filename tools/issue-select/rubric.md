# Rubric: is this a good first issue?

<!-- All recency thresholds below are measured against the repo-facts
block's stated capture date in eval mode, and against today's date in
live mode. -->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `repo-alive` | Repo facts: the "last 5 default-branch commits" list, including each commit's author name | The newest commit in that list is dated no more than 120 days before the capture date. A commit whose author name ends in `[bot]` counts toward this only if it merged a human-authored pull request; otherwise the newest non-bot commit must meet the 120-day threshold. | required |
| `repo-not-archived` | Repo facts: the `archived:` value on the repo line; any "unmaintained", "deprecated", or "seeking new maintainer" notice in the repo facts or issue body | `archived:` is false AND no such notice is present. | required |
| `repo-in-use` | Repo facts: "latest release" date, "last push to any branch" date, and the star count on the repo line | At least 1 of these 3 holds: (a) latest release is dated within 730 days of the capture date; (b) last push to any branch is within 180 days of the capture date; (c) stars are 10 or more. | required |
| `scope-bounded` | Issue body and Comments section: self-described tracking/umbrella wording, breadth of the change, maintainer statements about internals, unsettled design debate, support-request phrasing, absence of a specification | Passes unless any of these appear: (a) the body describes itself as a tracking, meta, umbrella, or mega issue, or lists items each meant to be filed or claimed as separate work; (b) the change is a codebase-wide sweep (every file, all modules, the whole package); (c) a maintainer comment says the fix touches core internals; (d) the thread shows a design still being debated with no maintainer decision; (e) the issue is a usage or support question rather than a request for a change; (f) the issue is a feature wish that never states the desired behavior concretely enough to implement. A detailed proposal that names several files to change as parts of ONE deliverable passes. A checklist of sub-steps inside a single bounded piece of work passes. A terse body, a missing reproduction, or a bare checklist does NOT fail this check. | required |
| `not-claimed` | Issue right sidebar / Repo facts: `this issue: assignees:`, `linked PRs:` with state per PR. Comments section: claim comments with their dates and any maintainer reply. Path Review house rule in `scope.md`. | `assignees:` is empty AND no linked PR is open AND no live claim comment is present. A claim comment is live only if it is dated within 180 days of the capture date; an older claim with no open linked PR behind it is stale and does not count. A maintainer comment inviting new takers clears any earlier claim. Per the house rule, claim comments from course classmates do not count as claims. Where the sidebar and the thread disagree, the thread decides. | required |
| `ai-work-not-banned` | Repo facts: the "contribution policy" line, including any quoted `CONTRIBUTING.md`, `AI_POLICY.md`, or PR-template wording | Passes unless the policy states an outright ban on AI-generated or AI-assisted contributions. Conditions (disclosure, personal understanding, testing, human review) pass. Silence passes. | required |
| `maintainer-answers` | Repo facts: the "maintainer first-response sample" | At least one entry in the sample is a numeric first-response time of 90 days or less. Entries reading "no maintainer comment in thread" are not counted toward that threshold and do not individually disqualify the check. | preferred |
| `newcomer-labeled` | Issue labels in the issue header or Repo facts | The issue carries `good first issue`, `tier-1`, or an equivalent starter label. | preferred |
| `maintainer-in-this-thread` | Comments section: each comment's `author_association` | At least one comment has an `author_association` of OWNER, MEMBER, or COLLABORATOR. | preferred |
| `no-abandoned-attempts` | Repo facts: `linked PRs:` states. Issue open date vs capture date. | No linked PR is closed-unmerged, AND the issue has been open for 365 days or less. | preferred |

## Verdict rule

**`accept` if and only if every `required` check grades `pass`.** One
`required` check grading `fail` produces `reject`.

`unclear` on a `required` check counts as `fail`, with one class of
exception built into the pass conditions themselves. Three required
checks — `repo-not-archived`, `scope-bounded`, and `ai-work-not-banned` —
pass on the absence of a disqualifying signal rather than on the presence
of a qualifying one, so missing evidence is a `pass` for them, not an
`unclear`. This is deliberate: most repos state no AI policy, and most
well-scoped issues carry no explicit statement that they are
well-scoped. The remaining required checks (`repo-alive`, `repo-in-use`,
`not-claimed`) need positive evidence, and grade `unclear` — therefore
`fail` — when the repo-facts block does not carry the field they read.

Maintainer responsiveness is graded but does not gate the verdict. A
sampled first-response time is noisy: a living repo can have five quiet
threads in a row, and rejecting on that would throw away good issues in
small or low-traffic projects. Repo liveness is carried by `repo-alive`
and `repo-not-archived`, which read commit and archive state directly.

`preferred` checks never change the verdict. They are reported, and used
only to rank accepted candidates against each other: an accepted issue
with more `preferred` checks passing ranks above one with fewer. The fit
profile in `scope.md` breaks any remaining tie.
