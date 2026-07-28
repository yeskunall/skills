# skills

> A collection of [Agent Skills](https://agentskills.io/home) I’m currently testing out, managed with [Vendir](https://carvel.dev/vendir/).

## Syncing

```sh
vendir sync --locked
```

> [!NOTE]
> The `--locked` flag reproduces the exact revisions recorded in `vendir.lock.yml`.

Pull the latest revisions allowed by `vendir.yml` and update the lockfile:

```sh
vendir sync
```

> [!WARNING]
> Do not edit vendored skill directories directly. A future sync will overwrite those changes. Update the upstream source or `vendir.yml` instead.

## Inventory

| Skill | Source |
| --- | --- |
| `brainstorming` | [`obra/superpowers`](https://github.com/obra/superpowers/tree/3dcbd5c4b48e02263fbf4a3c01e3fe4f81d584d9/skills/brainstorming) |
| `dispatching-parallel-agents` | [`obra/superpowers`](https://github.com/obra/superpowers/tree/3dcbd5c4b48e02263fbf4a3c01e3fe4f81d584d9/skills/dispatching-parallel-agents) |
| `domain-modeling` | [`mattpocock/skills`](https://github.com/mattpocock/skills/tree/ed37663cc5fbef691ddfecd080dff42f7e7e350d/skills/engineering/domain-modeling) |
| `emil-design-eng` | [`emilkowalski/skill`](https://github.com/emilkowalski/skill/tree/6bf24434f7730ad169077756cf9c7cd7bd675fc6/skills/emil-design-eng) |
| `executing-plans` | [`obra/superpowers`](https://github.com/obra/superpowers/tree/3dcbd5c4b48e02263fbf4a3c01e3fe4f81d584d9/skills/executing-plans) |
| `finishing-a-development-branch` | [`obra/superpowers`](https://github.com/obra/superpowers/tree/3dcbd5c4b48e02263fbf4a3c01e3fe4f81d584d9/skills/finishing-a-development-branch) |
| `git-commit` | [`github/awesome-copilot`](https://github.com/github/awesome-copilot/tree/b94ae92ab0a6fa695803f1b79b2e41a904a237db/skills/git-commit) |
| `grill-with-docs` | [`mattpocock/skills`](https://github.com/mattpocock/skills/tree/ed37663cc5fbef691ddfecd080dff42f7e7e350d/skills/engineering/grill-with-docs) |
| `grilling` | [`mattpocock/skills`](https://github.com/mattpocock/skills/tree/ed37663cc5fbef691ddfecd080dff42f7e7e350d/skills/productivity/grilling) |
| `impeccable` | [`pbakaus/impeccable`](https://github.com/pbakaus/impeccable/tree/8259c28209b92792005cec14dad573df39f68eaf/.agents/skills/impeccable) |
| `improve-claude-md` | [`humanlayer/skills`](https://github.com/humanlayer/skills/tree/39fb32786ae7a7cd864cf2c237148c38b1e4db07/plugins/improve-claude-md/skills/improve-claude-md) |
| `modern-web-guidance` | [`GoogleChrome/modern-web-guidance`](https://github.com/GoogleChrome/modern-web-guidance/tree/c54db496e0d2137a90d197c9c01ee9a290c1b2cf/skills/modern-web-guidance) |
| `react-best-practices` | [`vercel-labs/agent-skills`](https://github.com/vercel-labs/agent-skills/tree/f8a72b9603728bb92a217a879b7e62e43ad76c81/skills/react-best-practices) |
| `receiving-code-review` | [`obra/superpowers`](https://github.com/obra/superpowers/tree/3dcbd5c4b48e02263fbf4a3c01e3fe4f81d584d9/skills/receiving-code-review) |
| `requesting-code-review` | [`obra/superpowers`](https://github.com/obra/superpowers/tree/3dcbd5c4b48e02263fbf4a3c01e3fe4f81d584d9/skills/requesting-code-review) |
| `subagent-driven-development` | [`obra/superpowers`](https://github.com/obra/superpowers/tree/3dcbd5c4b48e02263fbf4a3c01e3fe4f81d584d9/skills/subagent-driven-development) |
| `systematic-debugging` | [`obra/superpowers`](https://github.com/obra/superpowers/tree/3dcbd5c4b48e02263fbf4a3c01e3fe4f81d584d9/skills/systematic-debugging) |
| `test-driven-development` | [`obra/superpowers`](https://github.com/obra/superpowers/tree/3dcbd5c4b48e02263fbf4a3c01e3fe4f81d584d9/skills/test-driven-development) |
| `use-semble` | Local skill |
| `using-git-worktrees` | [`obra/superpowers`](https://github.com/obra/superpowers/tree/3dcbd5c4b48e02263fbf4a3c01e3fe4f81d584d9/skills/using-git-worktrees) |
| `using-superpowers` | [`obra/superpowers`](https://github.com/obra/superpowers/tree/3dcbd5c4b48e02263fbf4a3c01e3fe4f81d584d9/skills/using-superpowers) |
| `verification-before-completion` | [`obra/superpowers`](https://github.com/obra/superpowers/tree/3dcbd5c4b48e02263fbf4a3c01e3fe4f81d584d9/skills/verification-before-completion) |
| `vocabulary` | [`index-how/vocabulary`](https://github.com/index-how/vocabulary/tree/b2d53205a03a6538c394b22f28ea175fdbfb97e3/skills/vocabulary) |
| `web-design-guidelines` | [`vercel-labs/agent-skills`](https://github.com/vercel-labs/agent-skills/tree/f8a72b9603728bb92a217a879b7e62e43ad76c81/skills/web-design-guidelines) |
| `writing-plans` | [`obra/superpowers`](https://github.com/obra/superpowers/tree/3dcbd5c4b48e02263fbf4a3c01e3fe4f81d584d9/skills/writing-plans) |
| `writing-skills` | [`obra/superpowers`](https://github.com/obra/superpowers/tree/3dcbd5c4b48e02263fbf4a3c01e3fe4f81d584d9/skills/writing-skills) |
