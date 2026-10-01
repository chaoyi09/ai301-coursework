# Voice guide: how I talk upstream

## Who I am in threads

I'm a student making my first open-source contribution, here to learn
how documents get parsed and chunked before retrieval. English is my
second language, so I keep sentences short and plain. Readers can
expect me to say what I will check next, show what I ran, and report
what happened, including when it did not work.

## Rules I write by

### Rule: Name this issue's specifics

Every comment mentions something only this issue has: the function,
the input, the file, or the exact symptom. If the sentence could be
pasted on any other issue, rewrite it.

- Wrong: "Hi, I'd love to help with this bug, please assign it to me!"
- Right: "I want to work on this: `StructuralChunker.chunk()` returns `[]` for a document with no markdown headings."

### Rule: Promise the next step, not the result

Before I have reproduced, I say what I will run and what I will report.
I never say I reproduced it, know the cause, or will fix it by a date.

- Wrong: "I already know the cause and will have a fix ready in two days."
- Right: "Then I'll read `_extract_sections()` to find where heading-less content is lost, and post a repro report here."

### Rule: Show it, don't just say it

Anything I claim to have seen comes with the command and the output
that shows it. A guess about the cause is written as a guess.

- Wrong: "I confirmed the bug, it's definitely the heading check."
- Right: "Running the issue's snippet on `f89c06f` prints `0`; my guess is the heading check in `_extract_sections()`, which I haven't confirmed yet."

### Rule: Report the outcome honestly, either way

If it does not reproduce, I say so and say what was different. I
don't bend a different error into "the same bug".

- Wrong: "I got an error too, so I can confirm the issue."
- Right: "On my setup it did not reproduce: the snippet printed `1`. My environment differs in Python version (3.11 vs. the issue's), and I'm checking that next."

### Rule: Plain words, no filler

Short sentences, no AI-sounding openers or stacked politeness. One
"Hi!" or "Thanks" is enough.

- Wrong: "I hope this message finds you well! I would be absolutely thrilled and truly honored to contribute to this amazing project."
- Right: "Hi! I want to work on this as my first contribution to PathReview."

## Things I never post

- A promised fix, PR, or delivery date ("I'll fix it by Friday").
- "I reproduced it" / "confirmed" before I have output to show.
- Piggyback repros: "same as above", "+1, can confirm".
- Text copied from a classmate's claim or repro on the same issue.
- An AI-written comment I haven't read line by line and rewritten in my own words.
- Typos in code names: I copy function, file, and commit names from the source instead of typing them.
