# Fieldnotes

A Claude Code skill that keeps a project's hard-won knowledge in the repository instead
of in one person's local AI memory.

Named for what it is: the notes you take **while the work is happening**, by the person
doing it — dated, specific, and written for whoever reads them next.

## The problem

Most of what a project costs to learn never reaches a file. It ends up in local AI
memory that only one machine can see, in the seventh paragraph of a commit message, or
nowhere. A second contributor pays for all of it again — and so does the same person
three months later.

The knowledge that matters most is exactly the knowledge that is hardest to write down:

- the platform behaviour that took hours to find and that no documentation mentions
- why an obvious approach was rejected
- what a fault *looked like*, which is never what it turned out to be

## What it does

Maintains a `.ai/` directory:

```
.ai/
├── README.md          routing rules: where a new piece of information goes
├── architecture.md    end-to-end data flow
├── debug/             incidents, indexed by symptom
├── memory/            shared AI memory, one fact per file
└── handoff.md         current state; expires by design
```

Four behaviours: **scaffold** what has content today, **route** a new finding to the
right place, **promote** local memory that belongs to the project, and **report** rot —
stale indexes, an out-of-date handoff, leftover instruction files from a template that
now describe something else.

## The two ideas worth stealing even if you don't use the skill

**Organize by lifetime, not by topic.** A thousand-line technical document is usually
four documents stapled together: permanent constraints, reversible decisions, one-off
incidents, and a plan that expires. Updating any one means reading past the other three.

**Index debug records by symptom, not by cause.** When you start looking you know "the
face is frozen". You do not know "the device is returning a stale buffer with the valid
flag still set". A file named after the cause cannot be found at the moment it is needed.

## Install

Drop it where Claude Code looks for skills:

```bash
git clone https://github.com/ZQC8848/Fieldnotes ~/.claude/skills/fieldnotes
```

Per-project instead of global:

```bash
git clone https://github.com/ZQC8848/Fieldnotes .claude/skills/fieldnotes
```

Then ask for it by name, or just describe the situation — "write this debugging finding
down somewhere useful", "a new person is joining this repo".

## Provenance

The structure was not designed up front. It came out of a Unity/OpenXR research project
where the same three lessons kept being re-learned: a headset that reported healthy data
while returning a frozen buffer, a build that silently never compiled, and an RPC channel
that looked like a decoding bug. Those incidents are what the routing rules are shaped
around.

## License

MIT.
