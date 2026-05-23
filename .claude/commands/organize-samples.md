# /organize-samples

A Claude Code skill to help you organize disorganized sample libraries and break down your one shots and loops simply.

---

## MODES

- **Quick mode:** `/organize-samples /path/to/samples` — smart defaults, no setup
- **Setup mode:** `/organize-samples --setup` — full interview + analysis + custom recommendations

If `$ARGUMENTS` is a folder path, run Quick Mode.
If `$ARGUMENTS` is `--setup` or empty, run Setup Mode.

---

## SETUP MODE

Setup Mode scans the library first, then asks targeted follow-up questions based on what it finds. It has four phases.

---

### PHASE 1 — Opening Question

Ask the user exactly this:

> "What sample folder do you want to organize here today? Please paste the file path to that folder, and if you like, add anything you would like me to know about the kind of samples you are using."

Take note of the folder path and any context they share. Proceed immediately to Phase 2.

---

### PHASE 2 — Deep Library Scan & Report

Ask: "What is the full path to your samples folder?"

Then run a detailed analysis:

```bash
# Total file count
find "<folder_path>" -type f \( -iname "*.wav" -o -iname "*.mp3" -o -iname "*.aiff" -o -iname "*.aif" -o -iname "*.flac" \) | wc -l

# List all files for analysis
find "<folder_path>" -type f \( -iname "*.wav" -o -iname "*.mp3" -o -iname "*.aiff" -o -iname "*.aif" -o -iname "*.flac" \) | sort

# Existing folder structure
find "<folder_path>" -type d | sort
```

Analyze the file list and produce a **Library Report**:

```
📊 YOUR SAMPLE LIBRARY — QUICK REPORT
======================================
Total files: X

CONTENT BREAKDOWN (estimated from filenames):
  Loops:        X files (~X%)
  One-Shots:    X files (~X%)
  Unknown:      X files (~X%)

TOP INSTRUMENTS DETECTED:
  Kicks         ~X files
  Snares        ~X files
  Hi-Hats       ~X files
  808/Bass      ~X files
  Melodic Loops ~X files
  Pads/Synths   ~X files
  Vocals        ~X files
  Perc/World    ~X files
  FX/Textures   ~X files

TOP GENRES DETECTED (from filename keywords):
  [list top 3-5 genres found]

COMPLETE PACKS DETECTED:
  [list any folder or prefix group with 10+ consistently-named files]

DUPLICATE CANDIDATES:
  X files with _1 / _2 suffix patterns (likely Splice re-downloads)

EXISTING FOLDER STRUCTURE:
  [summarize what's already there, if anything]
```

After showing the report, ask 2-3 targeted follow-up questions based on what was found. Only ask what's actually relevant — don't ask about genres if the library is clearly all drums, don't ask about packs if none were detected. Examples:

- If multiple genres detected: "I see a lot of [X] and [Y] in here — do you mainly produce those, or is this a mixed library from different sources?"
- If complete packs detected: "I found what looks like [X] complete pack(s) with consistent file prefixes. Do you want those kept together, or broken up and merged into the main structure?"
- If no existing structure: "Are there any special folders you know you want — like breakbeats, song stems, vocal chops, or anything specific to how you work?"
- If DAW-relevant: "What DAW do you use? Ableton, Logic, and FL all have slightly different ways of browsing samples, and I can optimize the folder naming for yours."

Keep it conversational. Two or three questions max. Then move to Phase 3.

---

### PHASE 3 — Recommend Organization Strategies

Based on the scan report and follow-up answers, recommend **2 or 3 organization strategies** tailored to this producer. Present them clearly so the user can compare and pick one.

**How to choose which strategies to recommend:**

- Heavy drum content + beatmaker → lead with a Drums-focused structure
- Multiple genres + large library → lead with Genre-first
- Film/sync composer → lead with Mood/Texture-first or Instrument-first
- Live performer → lead with Playability-first (quick-access folders)
- Small library (<200 files) → Instrument-first is simpler and better
- Large library (500+ files) → Genre-first scales better
- User mentioned special folders → always include a custom structure option

**Example recommendation format:**

```
Based on your library, here are 3 ways we could organize this:

──────────────────────────────────────────
OPTION A — Genre-First (Recommended for you)
Best for: producers working across multiple genres who want to
          match the vibe first, then find the right sound.

Trap/
  Trap_Kicks/         Trap_Snares/
  Trap_Drum_Loops/    Trap_Melodic_Loops/
House/
  House_Kicks/        House_Drum_Loops/
Lo-Fi/
  LoFi_Drums/         LoFi_Melodic_Loops/
Drums/                ← genre-agnostic hits
FX_and_Foley/
_PROTECTED_PACKS/
──────────────────────────────────────────
OPTION B — Instrument-First (Simpler)
Best for: producers who search by sound type, not by genre.

One-Shots/
  Kicks/   Snares/   Hi-Hats/   Claps/
  808s/    Keys/     Synths/    FX/
Loops/
  Drum_Loops/   Melody_Loops/   Bass_Loops/
_PROTECTED_PACKS/
──────────────────────────────────────────
OPTION C — Custom (based on what you told me)
[Generate this dynamically based on Phase 1 answers.
 Include the special folders the user mentioned.
 e.g. if they said "breakbeats and song stems":
   Breakbeats/
   Song_Stems/
     {Song_Name}/
   One-Shots/
   Loops/
   _PROTECTED_PACKS/
]
──────────────────────────────────────────

Which option do you want, or should we mix and match?
```

---

### PHASE 4 — Customize Before Committing

Once the user picks a structure, ask:

**"Want to add, rename, or remove any folders before I finalize the plan? For example:**
- *Add a 'Breakbeats' folder for chopped drum loops*
- *Add a 'For Koala' folder for sampler-ready hits*
- *Rename 'Drums' to 'Drum Kit'*
- *Add subfolders inside any category*
- *Anything else?"*

Incorporate their changes, then show the **final structure** one more time for confirmation.

Once confirmed, proceed to EXECUTION (below).

---

## QUICK MODE

When a folder path is given as `$ARGUMENTS`:

1. Scan the folder (same as Phase 2 above)
2. Print a brief summary: "Found X files. X loops, X one-shots, X unknown."
3. Use Genre-first as the default structure if 3+ genres are detected, otherwise Instrument-first
4. Show the proposed plan
5. Ask: "Proceed? Or run `/organize-samples --setup` to customize first."
6. On confirmation, proceed to EXECUTION

---

## THE LOOP VS ONE-SHOT RULE ⚠️

**Loops and One-Shots must NEVER share a folder. This is non-negotiable.**

### Classify as LOOP if:
- Filename contains: `loop`, `groove`, `phrase`, `pattern`, `cycle`, `fill`, `top_loop`, `lp`
- Filename contains a BPM value: `120bpm`, `128_bpm`, `90BPM`, `_120_`
- Filename contains a musical key: `Am`, `Cmaj`, `F#`, `_Bb_`
- Shakers, maracas, hi-hat patterns with BPM → LOOP (rhythmic, not a hit)

### Classify as ONE-SHOT if:
- Filename contains: `one_shot`, `oneshot`, `hit`, `shot`, `single`, `staccato`
- Single drum element without BPM or loop context: `kick`, `snare`, `hat`, `clap`

### Edge Cases:
- Both indicators present (e.g. `Kick_Loop_120.wav`) → **LOOP wins**
- File is in an "One-Shots" folder but has BPM in the name → reclassify as LOOP
- Truly ambiguous → `Island_of_Misfit_Toys/`, flag for user review

---

## INSTRUMENT DETECTION (from filename keywords)

**Drum One-Shots:** kick/kik/bd, snare/snr/sd, hat/hh/hihat, clap/clp, perc/shaker/conga/tom, cymbal/crash/ride

**Melodic One-Shots:** bass/sub/808, keys/piano/rhodes/organ, synth/lead/pad/pluck/arp/chord, fx/riser/impact/whoosh/texture

**Vocals:** vox/vocal/voice/chant/choir/adlib/hook

**Loops:** drum_loop, melody_loop, bass_loop, perc_loop, top_loop, groove

**Special:** breakbeat/break/amen → `Breakbeats/` (if user wants this folder)

---

## GENRE DETECTION (from filename keywords)

| Keywords | Genre Folder |
|----------|-------------|
| trap, drill | Trap |
| house, deep house, tech house | House |
| rnb, r&b, soul | RnB |
| hiphop, hip_hop, boom, bap | Hip-Hop |
| disco, funk | Disco |
| latin, salsa, bossa, samba, conga | Latin |
| reggae, dancehall, afro | Afro & Reggae |
| pop | Pop |
| edm, electro, club | EDM |
| ambient, cinematic, film | Cinematic |
| jazz | Jazz |
| lofi, lo-fi, chill | Lo-Fi |
| country, nashville | Country |
| world, ethnic, darbuka, riq, shamisen | World Ethnic |
| vintage, retro, vinyl | Vintage & Retro |
| dnb, jungle, drum and bass | Jungle & DnB |

Note: Darbuka and riq → World Ethnic, NOT Latin.

---

## COMPLETE PACK DETECTION

A file group qualifies as a complete pack if:
- It has its own subfolder with a consistent naming prefix (e.g. all files start with `KSHMR_`, `OLIVER_`, `ATP_`)
- It was named by the user in Phase 1
- It contains 10+ files sharing the same prefix

**Action:** Move the entire pack folder intact to `_PROTECTED_PACKS/`. Do not split it up.

---

## DUPLICATE DETECTION

Files ending in `_1.wav`, `_1_1.wav`, or `_2.wav` are likely Splice re-download duplicates.
Check: does the base filename (without suffix) exist elsewhere?
- If yes → confirmed duplicate → stage in `Duplicates/`
- Never delete without explicit user confirmation

---

## FOLDER NAMING RULES

- Sub-folders must NOT repeat the parent name as a prefix
  - ✅ `Drums/Kicks` — correct
  - ❌ `Drums/Drum_Kicks` — wrong
- Exception: genre subfolders DO use the genre as a prefix
  - ✅ `Latin/Latin_Kicks/`, `Trap/Trap_Drum_Loops/`
- Preserve original filenames — they contain BPM, key, and pack info

---

## EXECUTION

1. Create backup manifest first:
```bash
find "<folder_path>" -type f \( -iname "*.wav" -o -iname "*.aiff" -o -iname "*.mp3" \) \
  -exec stat --format='{"file":"%n","size":%s}' {} \; \
  > "<folder_path>/_ORGANIZATION_REPORTS/backup_manifest_$(date +%Y%m%d_%H%M%S).json"
```

2. Use `cp` (copy) — **never `mv`** — to place files in new locations
3. Show progress every 25 files
4. After copies complete, verify counts
5. Ask: "All X files copied. Want me to remove the originals? (yes / no)"
6. Only run `rm` after explicit confirmation
7. Clean up empty folders: `find "<folder_path>" -type d -empty -delete`

---

## REPORT

Save to `_ORGANIZATION_REPORTS/report_{timestamp}.md` and print:

```
✅ X files organized
📁 Structure used: [Genre-first / Instrument-first / Custom]
🔒 X complete packs preserved in _PROTECTED_PACKS/
⚠️  X files in Island_of_Misfit_Toys — needs your review
🗑️  X duplicates in Duplicates/ — say "delete confirmed duplicates" to remove them
```

---

## ITERATIVE FIX LOOP

If a file gets misclassified: fix it, then add a new rule to this file so it doesn't happen again.

Example additions:
- "Nyabinghi → World Ethnic (not Reggae)"
- "Files with prefix `XYZ_` belong to protected pack XYZ"
- "My 'Breaks' folder = breakbeats, not general loops"
