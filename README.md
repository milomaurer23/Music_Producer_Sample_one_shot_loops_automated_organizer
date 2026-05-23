# sample-library-organizer

**A Claude skill that organizes your messy sample library — and tells you exactly how much time and storage space you got back.**

---

Producers lose an average of 20–40 minutes per session digging through unorganized samples. That's hours every week not spent making music. This skill fixes your library once, so every session after is faster.

---

## How to Get It Running

### Recommended — Claude Cowork (no terminal needed)
The easiest way. Claude Cowork is built into the Claude desktop app and can access your files directly — no command line, no setup beyond granting folder access.

1. Open the Claude desktop app and switch to **Cowork** (paid plan required)
2. Grant it access to your samples folder when prompted
3. Paste the contents of [`organize-samples.md`](.claude/commands/organize-samples.md) into the chat, or just say:
   > *"I want to organize my sample library. Here are the instructions to follow: [paste file contents]"*
4. Tell it your samples folder path — it handles the rest

### Advanced — Claude Code CLI
For producers comfortable in the terminal. Gives you full slash command control.

1. Install [Claude Code](https://claude.ai/code)
2. Copy the command file into your project:
```bash
mkdir -p .claude/commands
curl -o .claude/commands/organize-samples.md \
  https://raw.githubusercontent.com/milomaurer23/music_producer_sample_one_shot_loops_automated_organizer/main/.claude/commands/organize-samples.md
```
3. Open Claude Code in that folder and run any command below

### Also works — Claude Desktop App (guided experience)
1. Open the Claude desktop app
2. Go to **Skills → Create Skill → Upload a skill**
3. Upload the [`organize-samples.md`](.claude/commands/organize-samples.md) file from this repo
4. Click the skill and follow the prompts

---

## Works With

| Tool | Terminal needed | File access | Best for |
|------|----------------|-------------|----------|
| **Claude Cowork** ⭐ | No | Direct | Most producers |
| **Claude Code CLI** | Yes | Direct | Power users |
| **Claude Desktop App** | No | Guided only | Quick exploration |

---

## Commands

```
/organize-samples --setup              Full setup: scans your library, learns your workflow,
                                       recommends a custom folder structure, then executes.

/organize-samples /path/to/folder      Quick mode: smart defaults, shows a plan, asks before
                                       doing anything. Good for a full library you want sorted fast.

/organize-samples --new /path          New downloads mode: drops a fresh Splice batch into your
                                       existing organized library without touching anything else.

/organize-samples --favorites          Favorites mode: creates a !Favorites folder pinned to the
                                       top of your library. Tell Claude your go-to sounds —
                                       it copies them there so they're always one click away.

/organize-samples --duplicates /path   Duplicate scan: finds Splice re-downloads and exact
                                       duplicates, shows how much storage you'd free up,
                                       and stages them for deletion on your approval.
```

*Note: slash commands work in Claude Code CLI. In Cowork or the desktop app, just describe what you want in plain English — same result.*

---

## Before & After

```
BEFORE — 1,400 files, one folder, pure chaos:
samples/
├── CO_BG_Kick_Punchy_01.wav
├── kick_final_FINAL_v3.wav
├── Piano_Am_90bpm_loop.wav
├── kick_final_FINAL_v3_1.wav       ← Splice duplicate (wasted space)
├── Snare_Crispy_Hit.wav
├── loop_house_128bpm.wav
└── ... (1,394 more)

AFTER — clean, browsable, DAW-ready:
samples/Organized-Samples/
├── !Favorites/                     ← your go-to sounds, always one click away
├── Trap/
│   ├── Trap_Kicks/
│   ├── Trap_Snares/
│   └── Trap_Drum_Loops/
├── Lo-Fi/
│   └── LoFi_Melodic_Loops/
├── Drums/
│   ├── Kicks/
│   ├── Snares/
│   └── Hi-Hats/
├── _PROTECTED_PACKS/               ← complete packs kept intact
├── Duplicates/                     ← flagged for your review
└── Island_of_Misfit_Toys/          ← unclassifiable, review manually
```

---

## What You Get When It's Done

```
✅ 847 files organized
🗂️  Moved from: 1 chaotic folder → 24 clean folders
⏱️  Estimated time saved: ~22 minutes per session
💾  Storage savings available: 2.3 GB in confirmed duplicates (awaiting your approval to delete)
⚠️  14 files need your review → Island_of_Misfit_Toys/
🔒  3 complete packs preserved intact → _PROTECTED_PACKS/
```

---

## Customizing the Rules

The skill is a single markdown file: `.claude/commands/organize-samples.md`

Open it to add genre keywords, define custom folders, protect specific packs by prefix, or record misclassification fixes so they don't repeat. The file has an "Iterative Fix Loop" section at the bottom for exactly this.

---

Built for music producers who are tired of losing the vibe to a messy sample library.
