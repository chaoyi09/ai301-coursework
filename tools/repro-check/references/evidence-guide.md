# Evidence guide: where proof lives in a reproduction package

Eval mode: a package is one markdown bundle with these sections, in
order: `Repo facts`, `Issue` (title, body excerpt), `Thread
highlights`, `Candidate claim comment`, `Candidate repro report`. The
bundle is the whole world.

Live mode: the issue body and its comment thread on GitHub (`gh issue
view <n> -R <repo> --comments`), the repo's `README`, `CONTRIBUTING.md`
/ `docs/CONTRIBUTING.md`, any AI policy file, and the issue template;
the candidate side is the student's draft file(s) only.

## Environment

- Where it lives: the target is in the `Issue` body (version, OS,
  install method the reporter used), in `Thread highlights` (a
  maintainer saying "only on Windows", "only release builds", "can't
  reproduce on X"), and in `Repo facts` (`latest release`, the bug
  template's asks). The candidate side is the environment line or
  section of the `Candidate repro report`. Live: the issue body and
  thread, plus the repo's issue template; the draft's environment
  section. For a source repo, the code state (commit hash or branch)
  is part of the environment.
- What good looks like: the report names the version tested and the
  OS/platform, plus every factor the issue or thread marks as
  behavior-relevant. Where any of these differ from the issue's
  target (newer release, different OS, different shell), the report
  says so in words ("filed against 4.53.2; I tested 4.53.3"). A
  version mismatch that is never mentioned is a silent deviation, not
  a recorded environment.

## Steps

- Where it lives: the `Candidate repro report`'s steps, commands, and
  any input file contents it shows (`cat input.x`, inline code). Read
  them next to the `Issue` body's own input and command.
- What good looks like: from a stated starting state (clean install,
  fresh checkout at a commit, a shown config), a stranger could reach
  the trigger. An input counts as given if it is quoted, if the report
  says it is the issue's own input used verbatim (the issue is public),
  or if it is described precisely enough to recreate without guessing.
  Count as unfollowable: "set up the project",
  private repos or unshared config, a step on an issue-relevant
  factor (driver, flag, setting) that is not shown. Count as a changed
  trigger: any character-level difference from the issue's input that
  touches the reported syntax (`=` vs `:`, `-N:` vs `N:`, a variable
  left unbound), unless the report calls it out.

## Behavior shown

- Where it lives: fenced output blocks, log excerpts, exit codes, test
  results, or described screenshots inside the `Candidate repro
  report`. The thing to match is the specific symptom in the `Issue`
  body: its exact error text, panic message, exit code, wrong value, or
  missing output.
- What good looks like: the shown artifact carries the issue's
  distinctive signature. Same family is not enough: a graceful syntax
  or argument-validation error is not the reported panic/crash; a
  compile error is not the reported runtime error; a banner, help text,
  or session list only shows the tool runs. Read the artifact before
  the narration: if the artifact shows X and the text says it shows Y,
  trust the artifact. A control run (a near-identical input that does
  not fail) strengthens the match.

## Honesty

- Where it lives: the report's `Analysis`, `Actual`, `Root cause`, and
  summary sentences, plus any certainty claims in the claim comment
  ("confirmed", "verified", "deterministic", "affects all platforms").
- What good looks like: each claim points to something shown. "I ran
  it ten times" with one output shown is a claim; root-cause
  statements are either backed by quoted code/trace or worded as a
  hypothesis. An honest cannot-reproduce passes when it shows the real
  attempt's output and names what differed from the reporter's setup
  (and, ideally, what a triggering setup likely needs). A confident
  "reproduced" over an artifact that does not show the issue's
  behavior is the failure this section exists to catch.

## Comms

- Where it lives: the `Candidate claim comment` read against the
  `Issue`; both comments read against `Repo facts`' contribution policy
  and bug-report template. Live: the draft against the issue thread and
  the repo's `CONTRIBUTING.md` / AI policy file; plus `scope.md` house
  rules (classmate claims do not block; no piggyback repros).
- What good looks like: the claim mentions something only this issue
  has (function, input, symptom, file) and a concrete next step of
  investigation, and promises only investigation and a report, never a
  fix, a date, or certainty. Boilerplate that could be pasted on any
  issue ("I'd love to work on this, please assign me, I'll have a PR in
  2 days") fails. AI policy: read the policy text literally. If it says
  AI use must be disclosed, a pass needs an explicit disclosure sentence
  in a comment (course packages count as AI-assisted). If it says only
  that comments must be human-written, that contributors must
  understand their work, or nothing about AI, no disclosure is needed.
