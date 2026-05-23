# DAW Sample Organizer — Claude Code Skill

You open your DAW. You need a punchy kick. You search your samples folder and find 1,400 files named things like `CO_BG_Kick_Punchy_01.wav`, `kick_final_FINAL_v3.wav`, and `loop_???_120bpm_Gm.wav` all dumped in the same folder. You waste 20 minutes digging. You lose the vibe.

**This Claude Code skill fixes that.**

---

## What It Does

`/organize-samples` scans your messy sample library and reorganizes it into a clean, DAW-ready folder structure — automatically. It:

- Separates **loops** from **one-shots** (the most important rule in sample organization)
- Sorts by **genre** (Trap, House, Lo-Fi, Latin, etc.) or by **instrument** (Kicks, Snares, Pads, etc.) — your choice
- Keeps **complete sample packs** together instead of splitting them up
- Detects and stages **Splice re-download duplicates** (`_1.wav`, `_2.wav` artifacts)
- **Never deletes anything** without your explicit confirmation
- Creates a **backup manifest** before touching a single file

### Before & After

```
BEFORE — 1 folder, 400 files, pure chaos:
samples/
├── CO_BG_Kick_01.wav
├── kick_final_FINAL_v3.wav
├── Piano_Am_90bpm_loop.wav
├── Snare_Crispy_Hit.wav
├── loop_house_128bpm.wav
├── darbuka_perc_hit.wav
└── ... (394 more)

AFTER — clean, searchable, DAW-ready:
samples/Organized-Samples/
├── Trap/
│   ├── Trap_Kicks/
│   ├── Trap_Snares/
│   └── Trap_Drum_Loops/
├── Lo-Fi/
│   ├── LoFi_Melodic_Loops/
│   └── LoFi_Kicks/
├── World Ethnic/
│   └── WorldEthnic_Percussion/
├── House/
│   └── House_Drum_Loops/
├── _PROTECTED_PACKS/   ← complete packs kept intact
├── Duplicates/         ← flagged for your review
└── Island_of_Misfit_Toys/  ← unclassifiable, review manually
```

---

## Requirements

- [Claude Code](https://claude.ai/code) installed (free to get started)

---

## Installation

1. Copy the `.claude/commands/` folder from this repo into your project:

```bash
# Option A — clone the whole repo
git clone https://github.com/milomaurer23/music_producer_sample_one_shot_loops_automated_organizer.git
cp -r music_producer_sample_one_shot_loops_automated_organizer/.claude your-project/

# Option B — just grab the command file
mkdir -p your-project/.claude/commands
curl -o your-project/.claude/commands/organize-samples.md \
  https://raw.githubusercontent.com/milomaurer23/music_producer_sample_one_shot_loops_automated_organizer/main/.claude/commands/organize-samples.md
```

2. Open Claude Code in your project folder.

---

## Usage

### Quick mode — just point it at your folder:
```
/organize-samples /Users/yourname/Desktop/Samples
```

### Setup mode — configure preferences first:
```
/organize-samples --setup
```

Setup mode asks:
- Where's your samples folder?
- Genre-first or instrument-first structure?
- Any complete packs you want kept intact?

Claude will **show you the full plan before doing anything.** You confirm, then it runs.

---

## How It Works

1. **Scans** your folder and counts files
2. **Detects complete packs** — keeps them together in `_PROTECTED_PACKS/` instead of splitting them up
3. **Classifies** every file as a loop or one-shot, then by genre/instrument
4. **Shows you the plan** — no surprises
5. **Saves a backup manifest** so nothing is ever truly lost
6. **Copies** files into the new structure (`cp`, never `mv`)
7. **Asks before deleting** originals — you stay in control
8. **Generates a report** with counts, duplicates flagged, and anything it couldn't classify

---

## Customizing the Rules

The skill is a single markdown file: `.claude/commands/organize-samples.md`. Open it and edit:

- **Add genre keywords** to map more filenames to the right folder
- **Add your own protected packs** to the instructions
- **Adjust the folder structure** to match how you think about your library
- **Add a rule after a misclassification** — the file has an "Iterative Fix Loop" section at the bottom for exactly this

Your changes stay local to your setup, and the skill gets smarter every time you run it.

---

Built for music producers who are tired of losing the vibe to a messy sample library.
