# pi-review

`pi-review` adds a practical code review workflow to Pi via `/review` and `/end-review`
that is used by us at Earendil.

## Install

```bash
pi install git:github.com/earendil-works/pi-review
```

## What It Does

- Review **uncommitted changes**
- Review changes against a **base branch**
- Review a specific **commit**
- Review a GitHub **pull request** (checks it out locally via `gh`)
- Review one or more **folders/files** as a snapshot (not a diff)
- Produce prioritized findings with a clear verdict and actionable follow-ups
- Switch to a configured review model on review branches, then restore the main model
- It separates feedback to the agent from human callouts

It also supports custom shared instructions that are loaded from `REVIEW_GUIDELINES.md`.

## Quick usage

```bash
/review
/review uncommitted
/review branch main
/review commit abc123
/review pr 123
/review pr https://github.com/owner/repo/pull/123
/review folder src docs
/review branch main --extra "focus on performance and error handling"
/review model anthropic/claude-sonnet-5
/review model clear
```

`/review model` opens a selector for the model used on review branches. pi-review
stores that choice in the global Pi config directory, so it survives new sessions
and restarts. It saves the current model before starting the review, switches to
the configured review model on the review branch, then restores the saved model
before returning or queuing fix work.

When a review session is active, finish it with:

```bash
/end-review
```

You can then return only, return with a compact summary, queue fixing work from that summary, or queue fixing work from a minimal fix-request handoff.
