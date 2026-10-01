# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

chaoyi09

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/56#issuecomment-5923836852

Hi! I want to work on this as my first contribution to PathReview. I'm curious about how documents get chunked before retrieval, and this bug is in exactly that step: `StructuralChunker.chunk()` returning `[]` for a document with no markdown headings.

My plan: on a fresh checkout of `main` (`f89c06f`), I'll run the snippet from the issue body and the `test_document_with_no_headings` test in `tests/unit/test_structural_chunker.py`, and compare against the same text with one heading added. Then I'll read `_extract_sections()` to find where heading-less content is lost. I'll post a repro report here with my environment, the exact commands, and the output, whether or not it reproduces.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/56#issuecomment-5923916224

reproduce this: the issue's snippet prints `0` on my machine. My setup and every command I ran are below.

**Environment**
- OS: macOS 26.3.1 (arm64)
- Python: 3.11.11, fresh venv
- Repo: my fork of `codepath/pathreview-ai301-fa26-s1` at `f89c06f` (same as upstream `main`), no local changes
- Deps installed per `docs/SETUP.md` / `make setup`: `pip install -e ".[dev]"` (tiktoken 0.14.0, pytest 9.1.1). I skipped the Docker/DB steps because the chunker doesn't use them.

**Steps**
```bash
git clone https://github.com/chaoyi09/pathreview-ai301-fa26-s1.git && cd pathreview-ai301-fa26-s1
git checkout f89c06f
python3.11 -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"
```

1. The issue's snippet, unchanged:
```bash
python -c "from ingestion.chunking.structural_chunker import StructuralChunker
c = StructuralChunker()
print(len(c.chunk('This is a plain document with no headings at all. ' * 20, {})))"
```
```
0
```

2. Control: the same text with one `# Title` line in front:
```bash
python -c "from ingestion.chunking.structural_chunker import StructuralChunker
c = StructuralChunker()
print(len(c.chunk('# Title\n' + 'This is a plain document with no headings at all. ' * 20, {})))"
```
```
1
```

3. The related test. It is marked `xfail(strict=True)`, so a normal run only shows `1 xfailed`; with `--runxfail` it shows the real assertion:
```bash
python -m pytest tests/unit/test_structural_chunker.py::TestStructuralChunker::test_document_with_no_headings -q
python -m pytest tests/unit/test_structural_chunker.py::TestStructuralChunker::test_document_with_no_headings -q --runxfail
```
```
1 xfailed in 0.89s
```
```
>       assert len(result) >= 1
E       assert 0 >= 1
tests/unit/test_structural_chunker.py:36: AssertionError
1 failed in 0.12s
```

**Expected:** a document with no headings still produces at least one chunk (what the test asserts), so it reaches the RAG index.

**Actual:** `chunk()` returns `[]` (0 chunks) for the heading-less text, while the same text with one heading returns 1 chunk. So the trigger is the missing heading, as the issue says.

**What I see in the code (not confirmed yet):** in `ingestion/chunking/structural_chunker.py`, `_extract_sections()` only collects a content line when `heading_stack or current_section_lines` is true (line 120), and only saves the final section when `current_section_lines and heading_stack` (line 124). With no headings, `heading_stack` stays empty, so nothing is collected or saved. Next I want to work out what a heading-less document should turn into (for example one section with an empty `path`) and share that here before opening a PR.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Four runs, in order:

1. `--limit 3` smoke test: **agreement 3/3** (`pkg-01`, `pkg-02`, `pkg-03` all matched).
2. Full run: **agreement 18/20** (`categories: clear-accept 6/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4`). Two false rejects, `pkg-05` and `pkg-12`, both `failed: steps-rerunnable, control-run`.
3. After loosening `steps-rerunnable`: `--only pkg-05,pkg-12,pkg-06,pkg-18,pkg-20`: **agreement 5/5**. The two targets flipped to `accept`; the three canaries stayed `reject`.
4. Full run with `--save-run eval-run.txt`: **agreement 19/20** (`categories: clear-accept 7/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4`), `bar: 18/20: PASS`. This is the committed `eval-run.txt`. The one disagreement was `pkg-10`.

After run 4 I re-graded `pkg-10` alone with `--only pkg-10` and it came back `accept`, agreeing with gold. I did not change the rubric after that, so the committed run still matches the uploaded files.

**Package analysis**

`pkg-10` (starship/starship directory module with a symlinked repo path). Gold label: **`accept`**, noted as "honest cannot-reproduce: exact layout and config, prompt artifact shown, names the environment differences (Linux+zsh vs macOS+fish) and the PWD-resolution hypothesis for why fish matters." My rubric decided **`reject`** in the committed run 4 (`failed: outcome-honest, control-run`), but **`accept`** in run 2 and again in the single-package re-run.

Why it reads both ways: every proof check has a clear answer here. The environment line says "The report is macOS + fish 4.7.1; shell and OS both differ", the steps are exact shell commands, and the prompt artifact `monorepo/packages/app-dir on  master` is shown. That is condition (b) of `behavior-matches-issue`, an honest cannot-reproduce. The part that splits the grader is the last sentence: "A fish shell resolving `PWD` logically looks necessary to hit the `contract_repo_path` failure". In the re-run, `outcome-honest` passed, quoting "suggests my shell reports PWD differently..." as hedged. In run 4 it failed. My `outcome-honest` condition says uncertain points must be "stated as uncertain", and "looks necessary" sits right on that line. It is a hypothesis, but it is worded more firmly than "suggests". `control-run` failed both times (no passing-vs-failing pair), but it is `preferred`, so it was never what flipped the verdict. The gold reading is that naming a hypothesis about *why it didn't reproduce* is exactly what a good cannot-reproduce does. My rubric doesn't say that explicitly, so the grader has to decide each time.

**Check rationale**

From the `rubric.md` uploaded to `tools/repro-check/`, the `steps-rerunnable` row as it reads now:

> | `steps-rerunnable` | The repro report's steps and inputs: commands, input files, config shown in the report. See evidence guide: Steps. | A stranger with only the posted text plus the public issue could re-run the attempt from a stated starting state to the trigger. Each input that matters is either quoted, taken verbatim from the issue (e.g. "ran the issue's script verbatim"), or described precisely enough to recreate without guessing (e.g. "an env.yml with a valid dependencies list plus a category: section"). Fails if a step depends on private code, unshared config, or an unspecified "set up the project", or if a behavior-relevant step (driver, flag, setting) is left out. | required |

My first version said every command and input "is shown or quoted". In run 2 that rejected two gold accepts. On `pkg-12` the grader wrote "repro.mjs's actual prettier.format calls/input strings are described in prose, never quoted verbatim". On `pkg-05` it wrote "env.yml is described ... but its actual contents are never quoted or shown". Both were wrong for the same reason. `pkg-12` ran "the issue's script verbatim", and the issue is public, so a stranger already has the input. `pkg-05` described a minimal file precisely enough to rebuild. So I changed the test from "is the input pasted?" to "could a stranger get to the trigger without guessing?". I added the "plus the public issue" wording and the two examples, which come straight from those packages. I kept the fail cases concrete (private code, unshared config, "set up the project", a missing behavior-relevant step) so the loosened check still holds `pkg-18`'s private monorepo and `pkg-06`'s missing driver.

**Trade-offs**

Loosening `steps-rerunnable` could flip packages that agreed before, so run 3 added canaries next to the two targets: `pkg-06` and `pkg-18` (unfollowable-comms, both rejected partly on steps) and `pkg-20` (the single-package disclosure category). All three stayed `reject` at 5/5, and the confirming full run kept `unfollowable-comms 3/3` and `disclosure 1/1`. That is how I know the change didn't cost anything elsewhere.

What I accept it will miss: "described precisely enough to recreate without guessing" is a judgment call. A report that describes its input in confident but incomplete prose can now pass this check. I'm counting on `trigger-matches-issue` and `behavior-matches-issue` to catch that case, since a vague input usually shows up as an artifact that doesn't match the issue. I chose the false accepts the other checks can catch over false rejects on terse, honest reports like `pkg-12`, which the gold set treats as ready.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
