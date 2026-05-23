# sample-library-organizer

**A Claude Code skill to help you organize disorganized sample libraries and break down your one shots and loops simply.**

---

You open your DAW. You need a punchy kick. You search your samples folder and find 1,400 files named things like `CO_BG_Kick_Punchy_01.wav`, `kick_final_FINAL_v3.wav`, and `loop_???_120bpm_Gm.wav` all dumped in the same folder. You waste 20 minutes digging. You lose the vibe.

**This fixes that.**

---

## Before & After

```
BEFORE — chaos:
samples/
├── CO_BG_Kick_Punchy_01.wav
├── kick_final_FINAL_v3.wav
├── Piano_Am_90bpm_loop.wav
├── Snare_Crispy_Hit.wav
├── loop_house_128bpm.wav
├── darbuka_perc_hit.wav
└── ... (394 more files, no structure)

AFTER — clean, searchable, DAW-ready:
samples/Organized-Samples/
├── Trap/
│   ├── Trap_Kicks/
│   ├── Trap_Snares/
│   └── Trap_Drum_Loops/
├── Lo-Fi/
│   └── LoFi_Melodic_Loops/
├── House/
│   └── House_Drum_Loops/
├── World Ethnic/
│   └── WorldEthnic_Percussion/
├── _PROTECTED_PACKS/     ← complete packs kept intact
├── Duplicates/           ← flagged for your review, never auto-deleted
└── Island_of_Misfit_Toys/  ← unclassifiable, review manually
```

---

## What It Does

- Separates **loops from one-shots** — the most important rule in sample organization
- Sorts by **genre**, **instrument**, or a **custom structure you define**
- Analyzes your library first and **recommends an organization strategy** tailored to how you produce
- Asks about **special folders** you want (breakbeats, song stems, Koala packs, etc.)
- Keeps **complete sample packs** together instead of splitting them up
- Detects **Splice re-download duplicates** (`_1.wav`, `_2.wav` artifacts) and stages them for your review
- **Never deletes anything** without your explicit confirmation
- Creates a **backup manifest** before touching a single file
- Generates a **report** when done

---

## Requirements

- [Claude Code](https://claude.ai/code) installed

---

## Installation

**Option A — Clone the repo and copy the command:**
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

Then open Claude Code in your project folder.

---

## Usage

### Quick — just point it at your folder:
```
/organize-samples /Users/yourname/Desktop/Samples
```
Scans, shows a plan, asks before doing anything.

### Setup — full customization:
```
/organize-samples --setup
```
Scans your library, shows you what's in it, asks about your workflow and genres, then recommends an organization structure tailored to you. You can accept, modify, or mix and match before anything gets moved.

---

## Customizing the Rules

The skill is a single markdown file: `.claude/commands/organize-samples.md`

Open it to:
- Add genre keywords
- Define your own folder structure
- Add protected packs by name or prefix
- Record misclassification fixes so they don't repeat

---

Built for music producers who are tired of losing the vibe to a messy sample library.
