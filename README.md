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
> Treat directories managed by `vendir.yml` as read-only. Syncing replaces local changes.

## Skills

Browse the [`skills/`](skills/) directory for the full collection.
