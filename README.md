# Soundsmith

A Claude Code plugin for writing **Suno v6** prompts that survive contact with a real project — and for scoring instrumental music to a video edit, where the tempo has to land on whole frames.

Suno documents its models generously and its input fields barely at all. Most prompt guides blur that line. This one doesn't: every fact carries an evidence tier.

| Tier | Meaning |
|---|---|
| **Official** | Stated in Suno's help centre, release notes or pricing |
| **Observed** | Measured in the live app, not published by Suno |
| **Lore** | Practitioner convention — useful, unproven |

So the skill will tell you that v6 generates up to 8 minutes per pass and costs 10 credits for two songs (documented), that the Styles box currently shows ~1,000 characters (observed), and that "±2–5 BPM accuracy" is folklore you should verify rather than trust.

## Install

```
/plugin marketplace add JahooClou/soundsmith
/plugin install soundsmith@soundsmith
```

Then invoke it:

```
/soundsmith:suno-engineer prompt for a dark synthwave title sequence
/soundsmith:suno-engineer score for my 90-second product film at 24 fps
/soundsmith:suno-engineer path/to/track-file.md
```

## What it covers

- **Model choice** — v6, v6-wild, v6-mini, and when Max Mode earns its cost.
- **The four inputs** — Styles box order and descriptor discipline, the Exclude field (negatives belong there, not phrased as "no X" in the positive box), the lyrics box, and the controls. Including **Variety**, new in v6, which rewrites your style text unless you set it to 0.
- **Structure tags with performance cues** on every section, and the parameter-looking tags that are not real commands.
- **Instrumentals** that stay instrumental.
- **Scoring to picture** — a frames-per-beat table for 24/25/30 fps, Suno's documented tempo-drift fix, building length in whole bars, and why you lock the music rather than bending the edit.
- **Iterating by editing, not rerolling** — v6's section edits, single-lyric edits, Extend, Cover, mashups and sampling.
- **Track file and album workflow** — optional, for people who keep tracks as files: a Suno Inputs template and a generation log.

## Field notes worth having

- Suno filters real artist and band names. Describe the sound instead; the plugin ships a substitution list.
- Key names are a weak lever on some generators. Describe the *character* of the harmony ("bright major-key harmony that resolves to the tonic, no minor colour") and check the result by ear.
- At 25 fps, 125 BPM is exactly 12 frames per beat. That is why a corporate recap gets scored at 125 and not 128.

## Contents

```
skills/suno-engineer/
  SKILL.md                      the skill itself
  genre-practices.md            per-genre prompting strategies
  reference/suno/
    v6-capabilities.md          models, fields, limits, rights - with evidence tiers
    creative-sliders.md         Weirdness, Style Influence, Variety, Audio Influence
    structure-tags.md           section tags, performance cues
    voice-tags.md               vocal texture and FX descriptors
    instrumental-tags.md        instruments and instrumental sections
    genre-list.md               500+ genres
    pronunciation-guide.md      homographs, tech terms, phonetic fixes
    artist-blocklist.md         names to avoid, with substitutions
    tips-and-tricks.md          troubleshooting
    v5-best-practices.md        the V5 guide - prompt craft still sound
    CHANGELOG.md                log of Suno changes and doc updates
```

## Keeping it honest

Suno ships often. When something changes, record it in `reference/suno/v6-capabilities.md` with its evidence tier and date the entry in the changelog. A number without a source becomes lore within a week.

## Licence

MIT. Reference material is compiled from Suno's public help centre and release notes; it is documentation about the product, not Suno's own content.
