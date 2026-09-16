---
name: soundsmith
description: Builds Suno v6 prompts — Styles box, Exclude field, structure tags, model choice (v6 / v6-wild / v6-mini) and generation settings — and fills in a track file's Suno Inputs for album work. Also covers instrumental scores cut to picture (tempo-locked music for video edits). Use when creating, fixing, or iterating any Suno prompt or generation plan.
argument-hint: <track-file-path | "prompt for [concept]" | "score for [edit]">
allowed-tools:
  - Read
  - Edit
  - Write
  - Grep
  - Glob
  - Bash
  - WebFetch
---

# Suno Engineer · v6

Suno released the **v6 family on 9 September 2026**. This skill is written for it. Pre-v6 models are retired, so anything you build here targets v6, v6-wild or v6-mini.

---

## 0. Evidence discipline (read first)

Suno documents its models generously and its *fields* sparsely. Three tiers, and they must not be mixed when you tell a user what is true:

| Tier | Meaning | How to speak about it |
|---|---|---|
| **Official** | Stated in Suno's help centre, release notes or pricing | State plainly |
| **In-app observed** | Measured in the live UI/API, not published by Suno (character limits, duration range, Max Mode cost) | "Currently shows X in the app — verify on your plan" |
| **Community lore** | Practitioner convention (pipe-syntax cues, `[No Vocals]`, "ideal" slider percentages, ±BPM accuracy) | "Convention, not documented — try it, don't promise it" |

Full fact sheet with tier labels: [reference/suno/v6-capabilities.md](reference/suno/v6-capabilities.md). When a user asks for a limit or a price, check that file before answering, and never invent a number.

---

## 1. Pick the model

| Model | Character | Plans | Use it for |
|---|---|---|---|
| **v6** | Flagship. Precise, polished, follows the prompt | Pro, Premier | The default. Anything where you know what you want |
| **v6-wild** | Less predictable, genre-blending, textured | Pro, Premier | Ideation, when v6 keeps giving you the obvious answer |
| **v6-mini** | Lighter and faster | All plans, including free | Drafts, high-volume exploration, testing a style box before spending on v6 |

**All three generate up to 8 minutes in one pass.** Standard generation returns **two songs for 10 credits**; image/video references can cost more.

**Max Mode** spends more compute on consistency. Suno recommends it for songs over two minutes, close Covers, and holding a vocal or style steady across a long track. Draft with it off; turn it on for the settled take. Its exact cost is not published.

---

## 2. The four inputs

### Styles box — the main lever
Order matters. **Vocal description first**, then genre and instrumentation, then production, tempo and key.

```
Male baritone, gritty, close-mic. Alternative rock, driving bass, tight live drums,
clean electric guitar. 112 BPM, D minor, dry punchy mix, hard stop at the end.
```

Every descriptor must add distinct information: vocal identity, genre, tempo, two or three instruments, a production note. What dilutes the result is a **synonym pile** — "imperious, commanding, regal, grand, theatrical" is one idea said five times. Collapse synonyms; keep genuinely distinct detail. A focused ~10 descriptors is healthy; real bloat starts past ~12.

Put **global** instructions here: genre, instrumentation, BPM, key, mix character, overall arc. Put **local** direction (section by section) in the lyrics box instead.

### Exclude field — negatives live here, not in Styles
Official location: Advanced mode → Advanced Options → **Exclude**. Enter what you don't want: instruments, vocal types, production traits.

```
vocals, choir, trap hi-hats, saxophone
```

Never write "no piano" in the positive Styles box if you can use Exclude instead — a generative model happily attends to the noun and hands you a piano. Exclusions shift odds; they are not a filter. Keep the list short and concrete.

### Lyrics box — structure and words only
**Suno sings everything in this box.** Stage directions, production notes, parentheticals — all sung. Only section tags and actual lyrics belong here.

### Controls
The Create form carries sliders and toggles beside the text fields — Weirdness, Style Influence, Variety, Instrumental, Duration, Max Mode, plus Audio Influence when a reference is attached. Behaviour and how to reason about them: [reference/suno/creative-sliders.md](reference/suno/creative-sliders.md).

Two that matter most in v6:
- **Variety** rewrites or augments your style text for diversity. **Set it to 0 whenever the exact style wording matters** — for example when you are reproducing an approved prompt or matching an earlier track.
- **Style Influence** governs how hard the output hugs the Styles box. Raise it when the result drifts off-genre; don't assume the default is maximal.

Change one control at a time. Maxing Weirdness, Variety and Style Influence together pulls in three directions at once.

---

## 3. Structure tags and performance cues

Use conventional tags — `[Intro]`, `[Verse]`, `[Pre-Chorus]`, `[Chorus]`, `[Post-Chorus]`, `[Bridge]`, `[Break]`, `[Instrumental]`, `[Outro]`, `[End]`. Full set and notes: [reference/suno/structure-tags.md](reference/suno/structure-tags.md).

**Append a short performance cue to every section tag** — this is the default, not a flourish, and it is how an emotional arc gets carried across a track:

```
[Verse 1 - cold, restrained]
[Chorus - full band lift]
[Bridge - raw, breaking]
```

Budget: cues plus any standalone delivery tag (`[Whispered]`, `[Spoken]`) stay at **three bracketed descriptors per section maximum**. More reads as noise.

Do not invent parameter syntax. `[BPM: 128]`, `[Reverb: 30%]` and `[No Vocals]` are not documented commands — tempo and key go in Styles, negatives go in Exclude, and the instrumental toggle handles vocals.

---

## 4. Instrumentals

Instrumental tracks skip lyric writing entirely; this skill is their entry point. (If your setup has a separate lyric-writing skill, vocal tracks start there and come here second.)

1. **Instrumental toggle ON** — the officially supported method.
2. **Styles**: describe the music, and say "instrumental" early.
3. **Exclude**: `vocals, singing, spoken word, choir, vocal chops`.
4. **Lyrics box**: structure tags only, no parentheticals.

Even then, wordless humming or vocal pads can appear. There is no guarantee of perfect suppression: regenerate, or strip the vocal stem. `[Instrumental]` inside a lyric marks an instrumental *section*; it does not reliably make a whole track instrumental.

---

## 5. Scoring to picture

When the music has to fit an edit, tempo is the whole game. Suno acknowledges that generated tempo drifts — its help centre describes it as behaving "just like live music" — and points to **Studio → Transport → Project Tempo → Manual BPM** as the fix, after which you export and set the same tempo in your DAW.

**Pick a tempo whose beat is a whole number of frames**, so cuts land on beats:

| Frames per beat | 24 fps | 25 fps | 30 fps |
|---|---|---|---|
| 10 | 144 BPM | 150 BPM | 180 BPM |
| 12 | 120 BPM | 125 BPM | 150 BPM |
| 15 | 96 BPM | 100 BPM | 120 BPM |
| 16 | 90 BPM | 93.75 BPM | 112.5 BPM |
| 20 | 72 BPM | 75 BPM | 90 BPM |

Workflow:
1. Put the exact BPM and key in the Styles box, and add "no tempo changes".
2. Generate several candidates; pick one that is *stable*, not just the one closest to target.
3. Measure the real tempo, then lock it — Manual BPM in Studio, or time-stretch in the DAW. Do not bend the edit to a drifting track.
4. Trim so bar 1 starts on frame 0.
5. Build the length you need in whole bars. Generate long and cut on bar lines, or Extend if short.
6. Exclude `fade-out` when you need a hard ending on a specific frame.
7. Structure the arrangement to the picture: section tags in the lyrics box, one per act of the edit, with cues like `[Break - drums drop out, riser]`.
8. Duck the music 8–10 dB under dialogue. Deliver −14 LUFS integrated, −1 dBTP for online.

Stems (Pro/Premier) let you duck only the melodic layer and keep the pulse running.

---

## 6. Iterate by editing, not rerolling

This is the biggest workflow change in v6. Once a take has the right identity, **stop regenerating**:

| Want | Do |
|---|---|
| One section different | Plain-language section edit: "make this chorus sparser, just piano and voice" |
| One wrong word | Single-lyric edit — no full rebuild |
| More song | **Extend** from a chosen point |
| Same melody, new style | **Cover** |
| Rebuild a middle passage | **Replace Section** |
| Elements from several songs | **Mashup**: name source and role — "vocals from A, drum feel from B, the riff at 0:45 from C" |
| A riff to build on | **Sampling** — isolate a segment, then write around it |

Editing preserves the rest "as much as possible", not sample-accurately: audio around the selection is regenerated, so check the boundaries.

---

## 7. Multimodal prompting

A v6 request can reference Suno songs, playlists, uploaded audio, images and video together — not text alone. Be explicit about what each reference is for; a picture with no instruction is a mood board Suno interprets freely. Many visual inputs can raise credit cost.

---

## 8. Genre selection

Pattern: `[Primary genre] + [1-2 subgenre modifiers] + [1 key instrument or technique]`.

- Generic: "Rock"
- Better: "Alternative rock"
- Best: "Midwest emo, math rock influences, clean guitar"
- Too much: six genres at once — Suno cannot honour them simultaneously

Genre strategies per style: [genre-practices.md](genre-practices.md). 500+ genre names: [reference/suno/genre-list.md](reference/suno/genre-list.md).

---

## 9. Never use real artist or band names

Suno filters them, and the prompt fails or behaves strangely. Describe the sound instead — era, instrumentation, vocal texture, arrangement, production. Substitutions for 80+ artists: [reference/suno/artist-blocklist.md](reference/suno/artist-blocklist.md).

This matters more in v6, not less: the models were built with licensed catalogues from Warner Music, BMG and Believe/TuneCore, and imitation-by-name is exactly what the licensing regime polices.

---

## 10. Problems and fixes

| Symptom | Fix |
|---|---|
| Vocals buried | Move the vocal description to the front of Styles; name vocal prominence |
| Wrong genre | More specific genre terms; raise Style Influence |
| Style text came back changed | Set **Variety to 0** |
| Result too safe | Raise Weirdness, or switch to **v6-wild** |
| Unwanted instrument or choir | Move it to **Exclude**; remove any mention from Styles |
| Vocals on an "instrumental" | Instrumental toggle on, Exclude `vocals, choir, vocal chops`, lyrics box tags only; regenerate or strip the vocal stem |
| Song cuts off early | `[Outro]` then `[End]`; consider Max Mode for long takes |
| Tempo drifts against picture | Manual BPM in Studio, or time-stretch in the DAW — see §5 |
| Inconsistent voice across a long track | Max Mode; or a Voice/Persona |
| Mispronunciation | Phonetic spelling in the lyrics box — [reference/suno/pronunciation-guide.md](reference/suno/pronunciation-guide.md) |

---

## 11. Track file and album workflow

When invoked with a **track file path**:

1. **Read the track file.**
2. **Check if instrumental** — `instrumental: true` in frontmatter, or `**Instrumental** | Yes` in Track Details. Instrumental tracks need no lyric-writer prerequisite; this skill is their entry point.
3. **Read album context** — the album directory is `dirname $(dirname $TRACK_PATH)`; read its `README.md` for album-level genre, theme and production style. If it's missing, work from track context alone.
4. **Check duration target** — track Target Duration → album Target Duration → genre default. Fewer section tags means a shorter track; `[End]` is the strongest stop signal. There is no exact-duration parameter, so expect two or three generations to land a target, and trim in post.
5. **Check for a saved Voice, Persona or Custom Model** on the album. If one is in play, drop competing descriptors from Styles: with a **Voice**, drop gender and register words; with a **Custom Model**, drop generic production language — the model already carries it.
6. **Build the inputs** — model choice, Styles, Exclude, controls, lyrics/structure.
7. **Write them into the track file's Suno Inputs section** (template below). Keep every heading even when empty, so downstream tools can tell "considered" from "skipped".
8. **Log generations** as you go, with ratings, so the album keeps a record of what worked.

### Suno Inputs template

```markdown
## Suno Inputs

### Model
v6 · Max Mode: off

### Style Box
Male baritone, gritty, close-mic. Alternative rock, driving bass, tight live drums.
112 BPM, D minor, dry punchy mix.

### Exclude Styles
(none)

### Controls
Variety: 0 · Style Influence: high · Weirdness: low · Instrumental: off · Duration: auto

### Lyrics Box
[Intro - sparse]

[Verse 1 - cold, restrained]
...

[Chorus - full band lift]
...

[Outro - decaying]
[End]

### Generation Log
| Date | Model | Take | Credits | Rating | Notes |
|------|-------|------|---------|--------|-------|
| 2026-09-16 | v6 | 2 of 2 | 10 | 4/5 | Chorus lifts; verse drums too busy → Replace Section |
```

For **album consistency**, reuse the album's genre spine and production language across tracks and let each track vary vocal delivery, tempo and arrangement. A Custom Model trained on the album's own finished tracks is the strongest consistency tool (Pro/Premier, minimum six songs, up to three models).

---

## 12. User overrides

Check for `suno-preferences.md` in the overrides directory before building a prompt. If a `load_override` helper exists in the session, use it; otherwise **Read the file directly** — its absence is normal and never an error.

```markdown
# Suno Preferences
## Genre Mappings
| My Genre | Suno Genres |
|----------|-------------|
| dark-electronic | dark techno, industrial, ebm |
## Default Settings
- Model: v6
- Instrumental: false
## Avoid
- Never use: happy, upbeat, cheerful
```

User mappings and avoidance rules outrank everything in this skill.

---

## 13. Reference files

| File | Contents | Currency |
|---|---|---|
| [reference/suno/v6-capabilities.md](reference/suno/v6-capabilities.md) | Model family, fields, limits, editing, rights — with evidence tiers | **v6, authoritative** |
| [reference/suno/creative-sliders.md](reference/suno/creative-sliders.md) | Weirdness, Style Influence, Variety, Audio Influence | v6 section at top |
| [reference/suno/structure-tags.md](reference/suno/structure-tags.md) | Section tags, performance cues, delivery tags | Still valid |
| [reference/suno/voice-tags.md](reference/suno/voice-tags.md) | Vocal texture, style and FX descriptors | Still valid |
| [reference/suno/instrumental-tags.md](reference/suno/instrumental-tags.md) | Instruments, instrumental sections | Still valid |
| [reference/suno/genre-list.md](reference/suno/genre-list.md) | 500+ genres | Still valid |
| [reference/suno/pronunciation-guide.md](reference/suno/pronunciation-guide.md) | Homographs, tech terms, phonetic fixes | Still valid |
| [reference/suno/artist-blocklist.md](reference/suno/artist-blocklist.md) | Names to avoid, with substitutions | Still valid |
| [reference/suno/tips-and-tricks.md](reference/suno/tips-and-tricks.md) | Troubleshooting, operational technique | V5-era, mostly valid |
| [reference/suno/v5-best-practices.md](reference/suno/v5-best-practices.md) | Deep V5 prompting guide | **Superseded for model/UI facts**; prompt craft still sound |
| [genre-practices.md](genre-practices.md) | Per-genre prompting strategies | Still valid |
| [reference/suno/CHANGELOG.md](reference/suno/CHANGELOG.md) | Log of Suno changes and doc updates | Update it |
| [reference/suno/version-history/](reference/suno/version-history/) | Migration notes and the archived V5-era skill | Archive |

Lazy-load. Don't read everything up front.

---

## 14. Quality gate

Before generating:
- [ ] Model chosen deliberately (v6 default; v6-wild only when surprise is the goal; v6-mini for drafts)
- [ ] Vocal description first in Styles — or "instrumental" first, with the toggle on
- [ ] Every descriptor adds distinct information; no synonym piles
- [ ] Negatives in **Exclude**, not phrased as "no X" in Styles
- [ ] `### Exclude Styles` present in the track file even if `(none)`
- [ ] Every section tag carries a performance cue; ≤3 bracketed descriptors per section
- [ ] No artist or band names
- [ ] BPM and key in Styles, not in bracket tags
- [ ] Variety set to 0 if the exact style wording matters

After generating:
- [ ] Style, mood and structure match intent
- [ ] Vocals clear and correctly pronounced; not buried
- [ ] No unwanted instruments — exclusions actually worked
- [ ] No awkward cut at the end
- [ ] For picture: tempo measured and locked, first downbeat on frame 0
- [ ] Logged in the Generation Log with a rating

---

## 15. Keeping this skill current

Suno ships often. When you learn something new:

| Discovery | Write it to |
|---|---|
| Model, field, limit, price or rights change | `reference/suno/v6-capabilities.md` (with its evidence tier) |
| New prompting technique | `genre-practices.md` or the relevant tag reference |
| Any Suno update | `reference/suno/CHANGELOG.md`, dated |

Keep the evidence tier attached to every fact you add. A number without a source becomes lore within a week.
