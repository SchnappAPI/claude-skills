---
name: live-session-cache
description: Captures an in-progress chat into a GitHub branch as it happens so context survives chat compaction, tab closes, or unexpected loss. Activates automatically when the chat is about to cause a non-chats repo write (default on claude.ai), or at session start (default on Claude Code). Use when the user says "start logging this chat", "cache this conversation", "log this chat", "start session cache", or any similar manual trigger phrase. Once active, the skill commits each substantive turn to a dedicated chat branch with full reasoning preserved, monitors context size, offers wrap or pause options before compaction risk, and supports resuming open branches in future chats.
---

# Live Session Cache

A persistence layer for chats whose context should survive compaction, tab closes, or context resets. Opt-in per project. Writes to the project's linked GitHub repository under a `chats/` folder.

## Prerequisites

Before activating, confirm both:

1. The project has a linked GitHub repository recorded in project memory (owner and name).
2. The GitHub MCP is available in the current session (claude.ai) or local git is configured for the repo (Claude Code).

If either is missing, tell the user what is missing and stop.

## Mode selection

The skill has three modes. Default is determined by surface and can be overridden in project memory.

| Mode | When it activates | Default surface |
| --- | --- | --- |
| `trigger` | First time Claude is about to write to any path other than `chats/` | claude.ai chat |
| `always` | Session start | Claude Code |
| `manual` | Only when the user invokes a trigger phrase | Neither (opt-in) |

To override the default, add a line to project memory: `live-session-cache: trigger` or `live-session-cache: always` or `live-session-cache: manual`.

Manual trigger phrases work in all modes as an override. Recognized phrases: "start logging this chat", "cache this conversation", "log this chat", "start session cache".

## Activation procedure

The procedure is the same regardless of which mode triggered it. Steps:

1. Generate a slug from the chat topic, 2 to 4 lowercase hyphenated words. Examples: `live-session-cache-skill`, `mlb-statcast-pull`, `nda-negotiation`.
2. Create branch `chat/YYYY-MM-DD-{slug}` off the default branch of the linked repo.
3. Create file `chats/in-progress/{slug}.md` on that branch.
4. Backfill the conversation up to this point as a Turn 0 reconstruction (see Backfill section).
5. Confirm to the user: branch name, file path, and that per-turn capture is now active.

After activation, every subsequent substantive turn appends a new turn block to the file (see Per-turn entry format).

For Mode `trigger`: the activation happens immediately before the actual non-chats repo write. The repo edit then proceeds on its normal branch (main, a feature branch, wherever it would have gone). The chat branch is purely context, separate from the work branch by design. The triggering turn's State delta references the work-branch commit hash.

## Backfill

The Turn 0 backfill is a full reconstruction of the conversation up to the activation point, not a summary. Every prior turn appears in full with all four fields populated where applicable. The only thing condensed is reasoning, which gets the per-turn 2 to 5 sentence treatment.

The point: capture the evolution of the idea, including framing shifts and discussions that did not directly produce code. A turn where the user said "wait, what about this edge case" matters even if no code changed that turn, because it shaped what came next.

## Per-turn entry format

```
## Turn N — YYYY-MM-DD HH:MM

### User
{verbatim user message}

### Reasoning
{2 to 5 sentence summary of the approach taken and why}

### Response
{verbatim assistant response}

### Evolution note
{when this turn caused a reframing or shift in approach: how the shift happened, even if no code changed. Omit this field when the turn was straightforward execution with no inflection.}

### State delta
{what changed this turn: decisions made, files touched on the work branch with commit hashes, errors hit, open questions. Write "No state change" rather than omitting the section.}
```

Commit message format: `chat: turn N — {short description}`

The Evolution Note is the explicit hook for capturing reasoning that influenced later turns without producing immediate output. The State Delta captures concrete artifacts. Together they capture both the journey and the destination.

## Skip rules

Do not commit turns that consist of:

- Pure acknowledgments from the user (thanks, ok, yes proceed, go ahead) paired with a one-line assistant reply
- Trivial confirmations with no new information, decisions, framing shifts, or state change

When skipping, skip silently. Do not narrate it.

If unsure whether a turn is trivial, commit it. An extra commit is cheap. A missing turn at resumption time is expensive.

## Context size monitoring

Monitor cumulative conversation size each turn using:

- Turn count
- Cumulative message length, including artifacts, file contents, and tool outputs in context
- Large reads (file fetches, long search results)

This is approximate, not a precise token count.

### Soft threshold (around 60 to 70 percent of capacity)

Flag once with a brief note at the end of a response. Do not repeat the warning.

> Heads up: this conversation is getting long. Want to start thinking about wrap-up? I can offer the options whenever you are ready.

### Hard threshold (around 85 percent of capacity)

Stop and present the wrap-up options before continuing substantive work. Wait for the user's choice.

> We are close to the point where context could start getting compacted. Three options:
>
> 1. **Wrap and merge.** Final summary, open a PR, you approve, merge to main.
> 2. **Pause and continue later.** Session-pause block with current state. Branch stays open. Next chat resumes here.
> 3. **Keep going.** Dismiss this and accept the risk.

## Wrap-up flows

### Option 1: Wrap and merge

1. Write a final summary block at the top of the file (above Turn 0) with: TL;DR (2 to 3 sentences), key decisions, open threads, suggested next chat starting point.
2. Move the file from `chats/in-progress/{slug}.md` to `chats/archive/{YYYY}/{MM}/{slug}.md` in a final commit.
3. Open a PR from the chat branch to the default branch. Title: `chat: {slug}`. Body: the final summary.
4. Recommend squash-merge in the PR body so main gets one clean commit instead of N turn-level commits.
5. Wait for the user to approve and merge. Do not auto-merge.

### Option 2: Pause and continue

1. Append a `## Session paused — {timestamp}` block to the file with: current goal, last action taken, open questions, exact resumption point.
2. Commit. Do not open a PR. Leave the branch in `chats/in-progress/`.
3. Tell the user the branch name. The resumption flow will detect it automatically in the next chat.

### Option 3: Keep going

Dismiss the warning. Do not raise it again unless context grows substantially further.

## Resumption on chat start

At the start of any chat where this skill is auto-active or gets manually activated, check for open `chat/*` branches in the linked repo. If any exist:

1. List them with slug and last-updated timestamp.
2. Ask the user: resume one of these, or start a new branch?
3. If resuming, continue appending to that branch's existing file. Add a `## Session resumed — {timestamp}` marker before the next turn.

Multiple open branches across different topics are supported.

## Surface-specific notes

### claude.ai chat

- Per-turn writes go via GitHub MCP `create_or_update_file`, which uploads the full file each commit. The chat file grows each turn, so latency grows too.
- Activation only on first non-chats write keeps this overhead off short throwaway chats.
- Mode `trigger` is the recommended default.

### Claude Code

- Per-turn writes are local git operations, then a single push at session end pushes all turn commits at once.
- Latency is negligible.
- Mode `always` is the recommended default.
- The chat branch lives alongside the work branch in the local repo. Switching between them is a normal git checkout.

## Failure handling

If a write fails mid-chat:

1. Tell the user immediately. Do not silently swallow the error.
2. Show the turn content that would have been written so it is at least visible in the chat.
3. On the next turn, retry the failed write before doing the new turn's write.
4. If failures persist, ask the user whether to keep trying or pause logging for this chat.

Do not pretend a write succeeded when it did not.

## Project-specific integration

When the linked repo contains a file at `docs/skills/live-session-cache.md`, read it at activation. That file holds project-specific integration rules: how the chat log relates to the project's CHANGELOG and ADR conventions, any project-specific branch or file conventions, and any integration with existing session-end protocols.

The repo doc takes precedence over this skill's defaults when they conflict.

## What this skill does not do

- Does not capture raw thinking blocks. The Reasoning field is a written summary, not a transcript of internal scratch space.
- Does not replace project-level session-end protocols (CHANGELOG, ADR, INVARIANTS edits). The chat log is supplementary, not a substitute.
- Does not modify files outside `chats/` on the chat branch.
- Does not deduplicate across branches. Two chats on overlapping topics keep separate logs.
