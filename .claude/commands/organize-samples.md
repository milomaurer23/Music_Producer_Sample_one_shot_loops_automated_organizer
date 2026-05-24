# /organize-samples

A Claude Code skill to help you organize disorganized sample libraries and break down your one shots and loops simply.

---

## MODES

Read `$ARGUMENTS` to determine which mode to run:

| Arguments | Mode |
|-----------|------|
| `--setup` | Setup Mode — interview + deep scan + custom structure |
| `--quick /path` | Quick Mode — smart defaults, no questions |
| `--add /path` | Add Mode — drop new downloads into existing library |
| `--curate` | Curate Mode — builds a personalized sample pack from your own library |
| (empty) | Ask the user which mode they want |

Duplicate detection runs automatically in every mode and is always included in the final report.

---

## QUICK MODE (`--quick /path`)

1. Scan the folder at the given path (see SCANNING section)
2. Print a brief report: files found, loops vs one-shots, complete packs detected, duplicate candidates flagged
3. Show a proposed folder structure using smart defaults — genre-first if 3+ genres detected, instrument-first otherwise
4. Ask: "Proceed with this structure? Or run `--setup` to customize first."
5. On confirmation → EXECUTE → COMPLETION REPORT (including duplicates found)

---

## SETUP MODE

Setup Mode scans first, then asks targeted follow-up questions based on what it finds.

### Phase 1 — Opening Question

Ask exactly this:

> "What sample folder do you want to organize here today? Please paste the file path to that folder, and if you like, add anything you would like me to know about the kind of samples you are using."

Take note of the path and any context. Proceed to Phase 2.

### Phase 2 — Deep Scan & Library Report

Run the full scan (see SCANNING section). Then produce a Library Report:

```
📊 YOUR SAMPLE LIBRARY
=======================
Total files: X
Estimated size: X GB

CONTENT BREAKDOWN:
  Loops:     X files (~X%)
  One-Shots: X files (~X%)
  Unknown:   X files (~X%)

TOP INSTRUMENTS DETECTED:
  Kicks / Snares / Hi-Hats / 808s / Melodic Loops / Pads / Vocals / Perc / FX

TOP GENRES DETECTED:
  [top 3–5 genres from filename keywords]

COMPLETE PACKS DETECTED:
  [any folder or file group with consistent prefix + 10+ files]

DUPLICATE CANDIDATES:
  X files / ~X MB (Splice re-download _1/_2 suffix patterns)

EXISTING STRUCTURE:
  [summarize any folders already present]
```

### Phase 3 — Targeted Follow-Up Questions

Ask 2–3 questions based on what was found. Only ask what's relevant. Examples:

- Multiple genres detected → "I see a lot of [X] and [Y] — do you mainly produce those, or is this a mixed library?"
- Complete packs detected → "I found what looks like [X] complete pack(s). Keep them together or merge into the main structure?"
- No existing structure → "Any special folders you know you want — breakbeats, song stems, vocal chops, anything specific to how you work?"
- DAW browsing context → "What DAW do you use? I can optimize folder naming for how it browses."
- Go-to sounds → "Do you have any samples you reach for constantly? I can create a !Favorites folder that puts them one click away."

### Phase 4 — Recommend Structure Options

Present 2–3 organization strategies tailored to what you learned. Format:

```
Based on your library, here are your options:

──────────────────────────────────────
OPTION A — Genre-First (Recommended for large, mixed libraries)
  Trap/Trap_Kicks/  Trap_Drum_Loops/
  House/House_Kicks/  House_Drum_Loops/
  Drums/  (genre-agnostic hits)
  FX_and_Foley/
──────────────────────────────────────
OPTION B — Instrument-First (Faster for single-genre producers)
  One-Shots/Kicks/  One-Shots/Snares/  One-Shots/Hi-Hats/
  Loops/Drum_Loops/  Loops/Melody_Loops/
──────────────────────────────────────
OPTION C — Custom (based on what you told me)
  [Generated dynamically from follow-up answers.
   Include any special folders the user requested.]
──────────────────────────────────────
Which do you want, or should we mix and match?
```

### Phase 5 — Customize

Ask: "Anything to add, rename, or remove before I finalize? Any extra folders, special categories, or sounds you want handled differently?"

Incorporate changes. Show the final structure one more time. Get confirmation → EXECUTE.

---

## ADD MODE (`--add /path`)

For dropping a fresh batch of samples into an already-organized library without disturbing the existing structure.

1. Ask: "Where is your existing organized library?" (skip if already known)
2. Scan the new folder
3. Classify each file (see CLASSIFICATION section)
4. Map each file to its destination in the existing library
5. Show a proposed move list
6. On confirmation → copy files to destination → COMPLETION REPORT (including duplicates found)

Do NOT reorganize the existing library. Only add to it.

---

## CURATE MODE (`--curate`)

Builds a personalized sample pack curated from sounds already in the user's library — based on their taste, not just folder structure. This is discovery, not organization. Like a "Made For You" playlist, but from sounds they already own.

### Phase 1 — Learn Their Taste

Ask these questions conversationally, one at a time:

1. "What genres do you produce most? List as many as you want."
2. "What type of sounds do you love working with most? For example: drum machines, organic textures, melodic loops, 808s, vintage samples, vocal chops — or describe your own."
3. "Name a few samples you always reach for — describe them in your own words or paste the filenames if you know them. Don't worry if you can't remember exactly."

Take detailed notes. These answers are the taste profile you'll match against.

### Phase 2 — Scan & Match

Scan the library (see SCANNING section). Then find sounds that match the taste profile:

- Match genre keywords from their answers against filenames
- Match instrument/sound type keywords against filenames
- For named or described samples, locate those files and find similar ones (same prefix, same instrument type, same genre folder)
- Prioritize sounds that would work together in a session — cohesion matters more than quantity
- Aim for 30–60 sounds total. Better to curate tightly than dump everything that partially matches.

### Phase 3 — Name the Pack

Based on what you found and what they told you, give the pack a name that reflects their taste. Examples:
- `!My Pack — Dark Trap Drums/`
- `!My Pack — Vintage Drum Machines/`
- `!My Pack — Lo-Fi Textures/`
- `!My Pack — 808s & Bass/`

Ask the user: "I'm going to build you a [name] pack with [X] sounds. Does that name feel right, or want to call it something else?"

### Phase 4 — Build & Report

1. Copy (never move) matched files into the named pack folder at the root of the library
2. The `!` prefix ensures it sorts to the top of every DAW browser and file explorer automatically
3. Organize inside the pack folder by type if there are multiple categories (e.g. `Kicks/`, `Loops/`, `Textures/`)
4. Report:

```
🎛️ YOUR CURATED PACK IS READY
================================
Pack name: !My Pack — Dark Trap Drums
Location: /path/to/library/!My Pack — Dark Trap Drums/
Sounds included: 47 files

  Kicks/          12 sounds
  Snares/          9 sounds
  Hi-Hats/         8 sounds
  808s & Bass/    11 sounds
  Perc/            7 sounds

All originals are untouched in their original locations.
This is your personal starting point — open it in your DAW and explore.
```

On future runs, ask: "You already have a curated pack ([name], X sounds). Want to rebuild it, add to it, or create a new one with a different vibe?"

---

## SCANNING

Run these commands for any scan:

```bash
# All audio files
find "<folder_path>" -type f \( -iname "*.wav" -o -iname "*.mp3" -o -iname "*.aiff" -o -iname "*.aif" -o -iname "*.flac" -o -iname "*.ogg" \) | sort

# Folder structure
find "<folder_path>" -type d | sort

# Total size
du -sh "<folder_path>"
```

---

## CLASSIFICATION

### Loop vs One-Shot — The Most Important Rule
**Loops and One-Shots must NEVER share a folder.**

**Classify as LOOP if:**
- Filename contains: `loop`, `groove`, `phrase`, `pattern`, `cycle`, `fill`, `top_loop`, `lp`
- Filename contains a BPM value: `120bpm`, `128_bpm`, `_120_`
- Filename contains a musical key: `Am`, `Cmaj`, `F#`, `_Bb_`
- Shakers, hi-hat patterns, or maracas with BPM → always LOOP

**Classify as ONE-SHOT if:**
- Filename contains: `one_shot`, `oneshot`, `hit`, `shot`, `single`, `staccato`
- Single drum element without BPM or loop context: `kick`, `snare`, `hat`, `clap`

**Edge cases:**
- Both indicators present (e.g. `Kick_Loop_120.wav`) → **LOOP wins**
- File in a "One-Shots" folder with BPM in the name → reclassify as LOOP
- Truly ambiguous → `Island_of_Misfit_Toys/`, list for user review

### Instrument Detection

| Category | Keywords |
|----------|----------|
| Kick | kick, kik, bd, bassdrum |
| Snare | snare, snr, sd, rimshot |
| Hi-Hat | hat, hh, hihat, ohh, chh |
| Clap | clap, clp, handclap |
| Perc | perc, shaker, tamb, conga, bongo, tom |
| Cymbal | cymbal, crash, ride, splash |
| Bass | bass, sub, 808, low |
| Keys | keys, piano, rhodes, organ, ep, wurli |
| Synth | synth, lead, pad, pluck, arp, chord, stab |
| FX | fx, riser, sweep, impact, whoosh, texture, atmo, foley |
| Vocal | vox, vocal, voice, chant, choir, adlib, hook |
| Breakbeat | break, breakbeat, amen, break_loop |

### Genre Detection

| Keywords in filename | Genre Folder |
|---------------------|-------------|
| trap, drill | Trap |
| house, deep house, tech house | House |
| rnb, r&b, soul | RnB |
| hiphop, hip_hop, boom, bap | Hip-Hop |
| disco, funk | Disco |
| latin, salsa, bossa, samba, conga, bongo | Latin |
| reggae, dancehall, afro | Afro & Reggae |
| pop | Pop |
| edm, electro, club | EDM |
| ambient, cinematic, film | Cinematic |
| jazz | Jazz |
| lofi, lo-fi, chill | Lo-Fi |
| country, nashville | Country |
| world, ethnic, darbuka, riq, shamisen, nyabinghi | World Ethnic |
| vintage, retro, vinyl | Vintage & Retro |
| dnb, jungle, drum and bass | Jungle & DnB |

Note: Darbuka, riq → World Ethnic. NOT Latin.

---

## FOLDER STRUCTURE PRINCIPLES

### Avoid Redundancy — No Folder Bloat
The goal is a structure where every folder level adds meaningful navigation value. A folder that exists just to hold one other folder is waste.

- ✅ `Drums/Kicks/` — two levels, both useful
- ❌ `Drums/Drum_Elements/Drum_Hits/Kicks/` — three levels of bloat to get to the same place
- Sub-folders must NOT repeat the parent name as a prefix
  - ✅ `Drums/Kicks`
  - ❌ `Drums/Drum_Kicks`
- Exception: genre subfolders use the genre as prefix → `Trap/Trap_Kicks/` ✅

### Folder Sorting with Prefixes
Use prefix characters to pin important folders to the top in DAW browsers:
- `!My Pack — [Name]/` — curated packs sort first (! beats all letters)
- `_PROTECTED_PACKS/` — underscore pushes to top or bottom depending on DAW
- `Island_of_Misfit_Toys/` — naturally sorts late alphabetically

### Complete Pack Detection
A file group is a complete pack if it has a consistent filename prefix across 10+ files (e.g. all start with `KSHMR_`, `OLIVER_`, `ATP_`), or the user named it. Move the whole folder to `_PROTECTED_PACKS/` — do not split it up.

---

## EXECUTION

1. **Backup manifest first:**
```bash
find "<folder_path>" -type f \( -iname "*.wav" -o -iname "*.aiff" -o -iname "*.mp3" \) \
  -exec stat --format='{"file":"%n","size":%s}' {} \; \
  > "<folder_path>/_ORGANIZATION_REPORTS/backup_manifest_$(date +%Y%m%d_%H%M%S).json"
```

2. Use `cp` — **never `mv`** — to place files in new locations
3. Show progress every 25 files
4. After copies complete, verify counts match
5. Ask: "All X files copied. Want me to remove the originals? (yes / no)"
6. Only run `rm` after explicit confirmation
7. Clean up empty folders: `find "<folder_path>" -type d -empty -delete`

---

## COMPLETION REPORT

After every run (all modes), automatically scan for duplicates and print a full report. Save to `_ORGANIZATION_REPORTS/report_{timestamp}.md`:

```
✅ X files organized
🗂️  Moved from X folders → Y clean folders
⏱️  Estimated time saved: ~Z minutes per session*

💾  DUPLICATES FOUND: X files = X.X GB wasted
    Confirmed (safe to delete):   X files = X.X GB
    Unconfirmed (needs review):   X files
    → Say "delete confirmed duplicates" to free up the space
    → Say "show me each one" to review individually

⚠️  X files in Island_of_Misfit_Toys — needs your review
🔒  X complete packs preserved in _PROTECTED_PACKS/
📁  Full report saved to: _ORGANIZATION_REPORTS/report_{timestamp}.md

*Based on average of 20–30 minutes lost per session digging through unorganized samples,
 scaled by the number of files organized and folders simplified.
```

**How to estimate time saved:**
- Baseline: producers lose ~25 minutes/session average searching disorganized libraries
- For every 100 files organized into clean folders: ~3 minutes/session recovered
- For every redundant folder level removed: ~1 minute/session recovered
- For duplicates removed: factor in reduced cognitive load and faster auditioning
- Round to nearest 5 minutes. Show as a range if uncertain (e.g. "~15–25 minutes per session")

**Duplicate detection logic (runs in every mode):**
- Flag files ending in `_1.wav`, `_1_1.wav`, `_2.wav` (Splice re-download artifacts)
- Flag files with identical names in different folders
- For each candidate: check if the base filename (without suffix) exists elsewhere
  - If yes → confirmed duplicate
  - If no → unconfirmed, flag for review only
- Never delete without explicit user confirmation

---

## ITERATIVE FIX LOOP

If a file gets misclassified: fix it, then add a new rule here so it doesn't repeat.

Example entries:
- "Nyabinghi → World Ethnic (not Reggae)"
- "Files with prefix `XYZ_` = protected pack XYZ, move to _PROTECTED_PACKS/"
- "My 'Breaks' folder = breakbeats, not general loops"
