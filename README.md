# sample-library-organizer

**A Claude Code skill that organizes your messy sample library — and tells you exactly how much time and storage space you got back.**

---

Producers lose an average of 20–40 minutes per session digging through unorganized samples. That's hours every week not spent making music. This skill fixes your library once, so every session after is faster.

---

## Commands

```
/organize-samples --setup              Full setup: scans your library, learns your workflow,
                                       recommends a custom folder structure, then executes.

/organize-samples /path/to/folder      Quick mode: smart defaults, shows a plan, asks before
                                       doing anything. Good for a full library you want sorted fast.

/organize-samples --new /path          New downloads mode: drops a fresh batch of samples into
                                       your existing organized library without touching anything else.

/organize-samples --favorites          Favorites mode: creates a !Favorites folder pinned to the
                                       top of your library. You tell Claude your go-to sounds —
                                       it copies them there so they're always one click away.

/organize-samples --duplicates /path   Duplicate scan: finds Splice re-downloads and exact
                                       duplicates, shows you how much storage you'd free up,
                                       and stages them for deletion on your approval.
```

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

## Requirements

- [Claude Code](https://claude.ai/code) installed

---

## Installation

**Option A — Clone and copy:**
```bash
git clone https://github.com/milomaurer23/music_producer_sample_one_shot_loops_automated_organizer.git
cp -r music_producer_sample_one_shot_loops_automated_organizer/.claude /path/to/your/project/
```

**Option B — Just grab the command file:**
```bash
mkdir -p .claude/commands
curl -o .claude/commands/organize-samples.md \
  https://raw.githubusercontent.com/milomaurer23/music_producer_sample_one_shot_loops_automated_organizer/main/.claude/commands/organize-samples.md
```

Open Claude Code in your project folder and run any command above.

---

## Customizing the Rules

The skill is a single markdown file: `.claude/commands/organize-samples.md`

Open it to add genre keywords, define custom folders, protect specific packs by prefix, or record misclassification fixes so they don't repeat. The file has an "Iterative Fix Loop" section at the bottom for exactly this.

---

Built for music producers who are tired of losing the vibe to a messy sample library.
