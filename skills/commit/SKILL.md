---
name: commit
description: 'Create a git commit using the enforced Conventional Commits contract. Use when the user asks to commit changes, create a git commit, stage and commit, or mentions "/commit". Mirrors the human editor template at ~/.config/git/commit-template and the commit-msg hook that enforces the same rules. Covers: analyzing the diff for type/scope, composing a compliant message (subject + required body for feat/fix + footers), logical staging, and recovering when the hook rejects a commit.'
license: MIT
allowed-tools: Bash
---

# Commit — Conventional Commits (template-backed, hook-enforced)

## What this is

One commit contract, shared by three things that must stay in sync:

- **Human editor template** — `~/.config/git/commit-template`. When the user runs
  `git commit` by hand, the editor opens pre-filled with this (Gerrit-style).
- **This skill (the agent path)** — you compose the message yourself and commit
  non-interactively with `git commit -F -`.
- **The enforcement hook** — `~/.config/git/hooks/commit-msg` validates *every*
  commit in scoped repos and **rejects** anything that doesn't comply. It applies
  to you and the human equally. You cannot talk your way past it; the message must
  actually conform.

Scope: wired via an `includeIf` in `~/.config/git/config` for repos under
`~/dev/remote/github.com/yeskunall`. Outside that scope the hook may not run, but
you should still follow this contract.

> If you change the rules here, change the template and the hook too — they are the
> same contract expressed three ways.

## The contract

```
<type>(<scope>)?!?: <subject>

<body>

<footer(s)>
```

### Subject (first line) — hard rules

- `<type>` from the table below. `<scope>` is optional, lowercase, free-form
  (`[a-z0-9._/-]`).
- **≤ 72 characters.** The whole line, including type and scope.
- Imperative mood ("add", not "added"/"adds"), lowercase after the colon, **no
  trailing period**.
- Must be a **complete, standalone thought** — readable in the `main` commit list
  without expanding. Never rely on hover to finish the title.
- Breaking change → `!` before the colon: `feat(api)!: drop v1 auth tokens`.

### Body

- **Required for `feat` and `fix`.** Optional for other types — include it whenever
  the change is non-trivial.
- Exactly one blank line between subject and body.
- **Hard-wrap prose at 72 columns.** Git never reflows the body and `git log`
  indents it 4 spaces, so unwrapped lines look ragged. This is *your* job, not the
  hook's — the hook does not check body width, so get it right when you compose.
- **Leave unwrappable content on its own lines even if long:** fenced code blocks,
  URLs, file paths, and footer trailers. Never break those just to hit 72.
- Explain the **why / context / trade-offs / side effects** — the stuff you want
  revealed when the commit is expanded. Not the "how" (the diff shows that).

### Footer (optional)

- `BREAKING CHANGE: <what broke + how to migrate>`
- `Closes #<issue>` (auto-closes on GitHub) or `Refs #<issue>` (links only).

## Commit types

| Type       | Purpose                        | Body required? |
| ---------- | ------------------------------ | -------------- |
| `feat`     | New feature                    | **Yes**        |
| `fix`      | Bug fix                        | **Yes**        |
| `docs`     | Documentation only             | If non-trivial |
| `style`    | Formatting/style (no logic)    | If non-trivial |
| `refactor` | Code refactor (no feature/fix) | If non-trivial |
| `perf`     | Performance improvement        | If non-trivial |
| `test`     | Add/update tests               | If non-trivial |
| `build`    | Build system/dependencies      | If non-trivial |
| `ci`       | CI/config changes              | If non-trivial |
| `chore`    | Maintenance/misc               | If non-trivial |
| `revert`   | Revert a commit                | If non-trivial |

## Procedure (follow every time)

### 1. Inspect state

```bash
git status --porcelain
git diff --staged      # what's already staged
git diff               # unstaged changes
```

### 2. Stage the right things

Prefer one logical change per commit. Stage explicitly:

```bash
git add path/to/file1 path/to/file2
git add -p             # split a file into logical hunks
```

**Never stage secrets** (`.env`, credentials, private keys). If they're already
staged, unstage and stop to warn the user.

### 3. Decide type / scope / subject

Read the actual diff. Pick the type from the intent of the change (not the file
kind), a scope from the affected area, and a subject that stands alone in ≤72
chars.

### 4. Write and wrap the body

For `feat`/`fix` a body is mandatory — write the *why*. For other types, add one
when the change isn't self-explanatory.

**Hard-wrap prose lines to ≤72 columns yourself** — the hook does not enforce this,
so it is on you. Wrapping prose paragraphs through `fmt -w 72` is a reliable way to
do it; leave fenced code blocks, URLs, file paths, and footer trailers untouched.

### 5. Commit non-interactively

Pass the full message on stdin so structure is preserved and there are no quoting
pitfalls:

```bash
git commit -F - <<'EOF'
<type>(<scope>): <subject>

<body line 1>
<body line 2>

Closes #<issue>
EOF
```

Do **not** use `git commit -m` for multi-line messages, and do **not** open the
interactive editor.

### 6. If the hook rejects it, fix and retry

See the next section. Never bypass.

### 7. Confirm

```bash
git log -1 --stat
```

Report the created subject line back to the user.

## When the hook rejects a commit

The `commit-msg` hook prints a specific reason and exits non-zero, e.g.:

```
  x "feat" commits need a body explaining the why / context.
  see: ~/.config/git/commit-template
```

Do this:

1. **Read the reason** — it names the exact rule that failed.
2. **Fix the message** to comply (add the body, shorten the subject to ≤72, drop
   the trailing period, add the blank line, correct the type, etc.).
3. **Re-run the commit** with the corrected message.

Never work around enforcement. Specifically:

- **Never** `--no-verify` / `-n`.
- **Never** edit, move, or delete the hook, the template, or git config to get a
  commit through.
- **Never** `--amend`, reset, or re-init to dodge the hook — fix the message and
  commit again.

## Git safety protocol

- **Never** skip hooks (`--no-verify`) unless the user explicitly asks.
- **Never** update git config as a side effect of committing.
- **Never** run destructive commands (`--force`, `push --force`, hard reset)
  without an explicit request; never force-push `main`/`master`.
- Commits here are **SSH-signed** (`commit.gpgsign=true`, 1Password signer) — a
  signing step on commit is expected; don't disable it.
- If a commit fails for a non-message reason (e.g. a pre-commit formatter changed
  files), fix the cause and create a **new** commit rather than amending.
