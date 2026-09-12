# Archiving a closed shape

Shape files usually live in the working tree without being committed, so they die with the branch. The log, the Re-cuts and the Skill Feedback are the record of how the work actually went — archive them before the branch goes away.

Run this when the developer asks: *"archive this shape"*, *"close this out before the PR"*, or similar. Never automatically.

## Before archiving

The shape must actually be closed first — this step copies, it doesn't decide:

1. Status is `Closed`.
2. The closure summary in the log is filled in: what shipped, what was deferred and where it went, successor shape if any.
3. Decisions are pruned in the live shape (superseded entries marked or moved).

If any of these are missing, do them as part of the close, then archive.

## Destination

```text
~/.claude/shape-archive/{repo}/{YYYY-MM-DD}-{shape-slug}/
```

- `{repo}` — `basename "$(git rev-parse --show-toplevel)"`
- `{YYYY-MM-DD}` — the close date
- `{shape-slug}` — the shape's directory or file name, minus any `-shape` suffix

## Procedure

**1. Copy the shape verbatim.** `shape.md`, `log.md`, and any `slices/`. For a single-file shape, copy that one file.

Copy, don't move. Shape files aren't committed, so moving means deleting the developer's working files during a mechanical step. Leave the originals; say at the end that they can be deleted or left to die with the branch.

Do not prune, merge or summarize while copying. Pruning belongs in the live shape at close — the archive exists so future analysis can read the raw record, and curating at archive time silently decides what future sessions get to see.

**2. Find related journal reflections.** Reflections are named `YYYY-MM-DD-{slug}.md`, so the date range filters on filename alone:

```bash
ls ~/.claude/journal/reflections/ 2>/dev/null | awk -v a=2026-03-01 -v b=2026-03-14 '$0>=a && $0<=b'
```

Use the shape's first log entry date and its close date as the range. If the directory doesn't exist, skip this step silently — the journal is optional.

**3. Write the archive index** as `README.md` in the archive directory:

```markdown
# {Shape name}

**Repo:** {repo} · **Branch:** {branch} · **Ran:** {first log date} → {close date}
**Units:** {n} ({n} Build, {n} Decision, {n} Re-cut, {n} Pass)

## Intent

{one or two sentences, copied from the shape}

## Shipped

- 

## Deferred, and where it went

- 

## Successor

{link, or "none"}

## Related reflections

- `~/.claude/journal/reflections/{file}.md` — {one-line subject}

## Skill Feedback raised

- {each entry from the log's Skill Feedback section, or "none"}

## Files

- `shape.md` — state at close
- `log.md` — full history
```

The Skill Feedback list is duplicated into the index on purpose: it's the reason the skill-improvement pass opens an archive at all, and it shouldn't require reading the whole log to find.

**4. Report the archive path** and say the working-tree originals are safe to delete.

## Why the index matters

The archive is a corpus, not a backup. Its value is being read months later to answer questions like *where do plans usually bend*, *which Skill Feedback keeps recurring*, or *how big were the units that actually went smoothly* — so each folder needs to be answerable at a glance, without opening the log.

If the index would be empty or generic, the shape probably wasn't worth archiving. Say so rather than creating a folder.
