# Rubric: is this reproduction package ready to post?

Each check judges the proof itself against the issue, never the
write-up's length, formatting, or headings. Locations in the Evidence
column are defined in `references/evidence-guide.md`.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `env-recorded` | The repro report's environment record, read against the version / OS / install method / config the issue (and the repo-facts bug-report template) names as the target. See evidence guide: Environment. | The report states the tool's version AND the OS/platform, plus any factor the issue or thread says changes the behavior (driver, shell, build profile, config, language setting). Every place the tested environment differs from the issue's target is acknowledged in the report. Fails if there is no environment record, if a behavior-relevant factor is missing, or if the report tests a different version than the issue targets without saying so. | required |
| `steps-rerunnable` | The repro report's steps and inputs: commands, input files, config shown in the report. See evidence guide: Steps. | A stranger with only the posted text plus the public issue could re-run the attempt from a stated starting state to the trigger. Each input that matters is either quoted, taken verbatim from the issue (e.g. "ran the issue's script verbatim"), or described precisely enough to recreate without guessing (e.g. "an env.yml with a valid dependencies list plus a category: section"). Fails if a step depends on private code, unshared config, or an unspecified "set up the project", or if a behavior-relevant step (driver, flag, setting) is left out. | required |
| `trigger-matches-issue` | The report's input and command, read side by side with the issue's input and command. See evidence guide: Steps and Behavior shown. | The input and command exercise the same trigger the issue describes (same syntax, operator, flag, data shape). Any change from the issue's trigger is called out with a reason. Fails if the report silently alters the trigger (e.g. a different operator, range form, or expression) even if it still produces an error. | required |
| `behavior-matches-issue` | The report's artifacts (output excerpts, logs, exit codes, screenshots described) read against the specific behavior the issue reports (its error text, panic, exit code, wrong value). See evidence guide: Behavior shown. | Either (a) an artifact shown in the report displays the issue's distinctive signature (the same error message / panic / exit code / wrong output, not merely "an error"), or (b) the report is an honest cannot-reproduce whose artifacts show the attempt's actual result. Fails if there is no artifact at all, if the artifact shows a different failure (a syntax error, a graceful validation error, a compile error, or the tool simply running) than the issue's, or if the artifact contradicts what the text claims it shows. | required |
| `outcome-honest` | The report's conclusion / "actual" / analysis sentences, each read against the artifacts the report actually shows. See evidence guide: Honesty. | Every claim of reproduction, root cause, determinism, or scope is backed by something shown in the package; uncertain points are stated as uncertain. An evidenced cannot-reproduce that names what differed passes. Fails if the report asserts more than its artifacts show (e.g. "confirms the bug", "I verified the race", "guaranteed reproducible", "affects all platforms") without the artifact to back it. | required |
| `claim-specific-modest` | The candidate claim comment, read against the issue. See evidence guide: Comms. | The claim names something specific to this issue (the function, symptom, input, or file involved) and a concrete next step of investigation. It promises only what the author controls: no guaranteed fix, no delivery date, no claim of certainty beyond the evidence. Fails on interchangeable "please assign me" boilerplate, a bare +1 / "same here", or a promised fix or deadline. | required |
| `ai-policy-respected` | The repo-facts block's contribution policy (CONTRIBUTING / AI policy), read against both comments. See evidence guide: Comms. | If the stated policy REQUIRES disclosure of AI assistance, at least one of the comments contains an explicit disclosure statement (treat the package as AI-assisted work). If the policy only requires human-written comments, human responsibility, or understanding, or states no AI policy, this check passes without a disclosure. Fails only when a disclosure requirement exists and neither comment discloses. | required |
| `control-run` | The report's artifacts. | The report includes a control or comparison run (a nearby input that does not fail, an older/newer version, or the expected output) that isolates the trigger. | preferred |

## Verdict rule

Grade every check. **accept** if every `required` check is `pass`;
otherwise **reject**. `preferred` checks are reported but never change
the verdict. `unclear` counts as `fail` for required checks, because
proof that cannot be verified from the package is not ready to post.

Exception, live mode claim-only drafts: checks whose evidence is the
repro report (`env-recorded`, `steps-rerunnable`,
`trigger-matches-issue`, `behavior-matches-issue`, `outcome-honest`,
`control-run`) are reported as `unclear` with "not yet applicable:
claim-only draft" and are left out of the verdict; the verdict then
rests on `claim-specific-modest` and `ai-policy-respected`. For a
claim posted before reproducing, `claim-specific-modest` also fails if
the claim asserts a reproduction or root cause the author has not yet
shown.
