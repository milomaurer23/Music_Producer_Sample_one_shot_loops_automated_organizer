# music-sample-library-organizer

**A Claude skill that organizes your messy sample library around the way you actually produce — and tells you exactly how much time and storage you got back.**

---

Producers lose 20–40 minutes per session just digging through unorganized samples. That’s 2–4 hours a week — hundreds of hours a year — not spent making music. This skill fixes your library once, so every session after is faster.

It doesn't just sort by genre. It learns how you work — what DAW you use, what sounds you reach for most, what special folders you need — and builds a structure tailored to you.

---

## What You Can Do With It

| Command | What it does |
|---------|-------------|
| `--setup` | Full setup: scans your library, learns your workflow, recommends a structure tailored to you, then executes |
| `/path/to/folder` | Quick mode: smart defaults, shows you the plan, asks before doing anything |
| `--new /path` | New downloads: drops a fresh Splice batch into your existing organized library without touching anything else |
| `--favorites` | Creates a `!Favorites` folder pinned to the top — your go-to sounds, always one click away |
| `--duplicates /path` | Scans for Splice re-downloads and duplicates, shows how much storage you'd free up, stages for deletion on your approval |

**In Claude Code CLI**, run these as `/organize-samples --setup`, `/organize-samples --favorites`, etc.
**In Claude Cowork or the desktop app**, just describe what you want in plain English — same result, no slash needed.

---

## How to Get It Running

### 1. Claude Cowork (Recommended)
The easiest way. Built into the Claude desktop app — no terminal, no setup beyond granting folder access.

1. Open the Claude desktop app and switch to **Cowork** (paid plan required)
2. Grant it access to your samples folder when prompted
3. Paste the contents of [`organize-samples.md`](.claude/commands/organize-samples.md) into the chat, or say:
   > *"I want to organize my sample library. Here are the instructions to follow: [paste file contents]"*
4. Tell it your samples folder path — it handles the rest

### 2. Claude Code
Upload the skill directly from the Claude desktop app's skill browser.

1. Open the Claude desktop app
2. Go to **Skills → Create Skill → Upload a skill**
3. Upload the [`organize-samples.md`](.claude/commands/organize-samples.md) file from this repo
4. Click the skill and follow the prompts

### 3. Claude Code CLI
For producers comfortable in the terminal. Full slash command control.

1. Install [Claude Code](https://claude.ai/code)
2. Copy the command file into your project:
```bash
mkdir -p .claude/commands
curl -o .claude/commands/organize-samples.md \
  https://raw.githubusercontent.com/milomaurer23/music-sample-library-organizer/main/.claude/commands/organize-samples.md
```
3. Open Claude Code in that folder and run any command above

---

## Works With

| | Tool | Terminal needed | Best for |
|-|------|----------------|----------|
| 1 | **Claude Cowork** ⭐ | No | Most producers |
| 2 | **Claude Code** | No | Desktop app users |
| 3 | **Claude Code CLI** | Yes | Power users |

---

## Before & After

| ❌ Before | ✅ After |
|-----------|---------|
| 1,400 files dumped in one folder | Clean folders you can actually browse |
| Loops and one-shots mixed together | Loops and one-shots always separated |
| Splice duplicates eating your storage | Duplicates flagged — delete with one word |
| Complete packs broken up and scattered | Full packs preserved intact |
| Your go-to sounds buried somewhere | `!Favorites/` pinned to the top of your DAW |
| No idea what’s in there | Report tells you exactly what moved and what was saved |

---

## What You Walk Away With

- **A library built around you** — genre-first, instrument-first, or fully custom based on how you answered the setup questions
- **Your go-to sounds one click away** — `!Favorites` sits at the top of every DAW browser
- **Storage back** — confirmed duplicates staged and ready to delete, with an exact GB count before you decide
- **Hours back every week** — producers lose 20–40 minutes per session just digging for sounds. That’s 2–4 hours a week not spent making music. Organize once, and you get that time back every single session after
- **Nothing lost** — every file is copied before originals are touched, with a backup manifest saved before anything moves

---

## Customizing the Rules

The skill is a single markdown file: `.claude/commands/organize-samples.md`

Open it to add genre keywords, define custom folders, protect specific packs by prefix, or log misclassification fixes so they don't repeat. The file has an "Iterative Fix Loop" section at the bottom for exactly this.

---

Built for music producers who are tired of losing the vibe to a messy sample library.
