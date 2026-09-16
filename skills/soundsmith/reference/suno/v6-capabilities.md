# Suno v6 — capabilities, fields and limits

Fact sheet for the v6 family, released **9 September 2026**. Compiled 16 September 2026.

Every row carries an evidence tier. Keep it attached when you copy a fact out of here.

- **Official** — Suno help centre, release notes, pricing or terms
- **Observed** — measured in the live app or API, not published by Suno
- **Lore** — practitioner convention; useful, unproven

---

## Model family

| Model | Description | Plans | Tier |
|---|---|---|---|
| **v6** | "Our most advanced model… expressive, versatile, high-quality generations" with stronger precision control. Start here when you want the most control | Pro, Premier | Official |
| **v6-wild** | Experimental; "less predictable directions", genre-blending, textured | Pro, Premier | Official |
| **v6-mini** | Lighter and faster; brings v6 to the free plan; good for quick ideas and high-volume iteration | All plans | Official |

- Model picker sits at the **top right of the Create form**. *(Official)*
- **Up to 8 minutes per generation**, all three models. **Extend** continues a song beyond that. *(Official)*
- Standard generation makes **two songs for 10 credits**. Adding multiple images/videos increases cost. *(Official)*
- Pre-v6 models are retired. Old songs stay playable, but new iterations of them use current models. *(Official)*
- Custom Models built on v5.5 were **automatically upgraded to run on v6**. *(Official)*
- v6 was developed with licensed catalogues from **Warner Music Group, BMG and Believe/TuneCore**, with opt-in artist programmes. Exact dataset composition is undisclosed. *(Official announcement; details not public)*

### Max Mode

| Aspect | Fact | Tier |
|---|---|---|
| What it does | Spends more compute on consistency | Official |
| Recommended for | Songs longer than two minutes, close Covers, holding vocal/style consistency across a track | Official |
| Cost | Higher than standard; exact figure not published. The app has commonly shown 20 credits per two-song request | Observed |

---

## Create page fields

| Field | Behaviour | Limit | Tier |
|---|---|---|---|
| **Simple** mode | One natural-language description; v6 infers whether to create, remix or extend from what you give it | — | Official |
| **Advanced** mode | Lyrics, Styles, Title, voice selection, advanced options (the former "Custom" mode) | — | Official |
| **Styles / Style of Music** | Genre, era, mood, instrumentation, vocal delivery, tempo, key, production | ~1,000 characters | Observed |
| **Lyrics** | Lyrics plus section tags and cues | ~5,000 characters | Observed |
| **Exclude** | Negative descriptors: instruments, vocal types, traits. Advanced → Advanced Options → Exclude. Suno's instruction: "enter any information (instruments, etc) that you do not want in your track" | ~1,000 characters | Field Official; limit Observed |
| **Instrumental** toggle | Suppresses lyric generation, requests music only | — | Official |
| **Vocal Gender** | Male/female preference under Advanced Options | Two values | Official |
| **Duration** | Auto or Custom target length | API/UI observed 10–360 s; not a timing guarantee | Observed |
| **Title** | Song title | Not published | — |

### Controls

| Control | Behaviour | Tier |
|---|---|---|
| **Weirdness** | Safe → Chaos. Mid is the normal setting | Official (exact "best" values are Lore) |
| **Style Influence** | How strongly output follows the Styles text, loose → strong | Official |
| **Variety** | **New in v6.** May adjust or rewrite your style prompt to diversify results. **Set to 0 to preserve your exact wording** | Official |
| **Audio Influence** | Appears only with reference audio; how strongly the reference shapes output | Official |
| **My Taste / Personalize** | Personalises enhanced style descriptions from your listening and creation history; can be disabled | Official |

Exclusions display afterwards with a `-` prefix, e.g. `-piano`. *(Observed)*

---

## v6 capabilities

| Capability | Detail | Tier |
|---|---|---|
| **Plain-language section editing** | Change one section by describing it, preserving the rest "as much as possible" — not sample-accurate; audio around the selection is regenerated | Official |
| **Single lyric edit** | Change a word or line and regenerate only that part | Official |
| **Mashups** | Combine multiple sources in one request, describing how they should work together | Official |
| **Sampling** | Isolate a segment and build a new composition around it | Official |
| **Multimodal prompting** | Create from text, audio, images and video | Official |
| **Remix & Edit** | Extend, Cover, Replace Section | Official |
| **Suno Sounds** | Generates samples and sound effects, with dedicated **BPM and Key** controls and One Shot/Loop | Official |
| **Custom Models** | Fine-tune v6 on your own tracks. Minimum six songs, up to three models, private | Official |
| **Voices** | Your verified recorded voice, usable on songs; available on mobile since August 2026 | Official |
| **Style Persona** | Reuses the vocal/style character of a source song; selecting one populates the Style of Music field, which you can then edit | Official |
| **Stems** | Auto Split up to 12 stems (50 credits); Split from Mix (10 credits per stem); Advanced Split from ~100 instruments, Premier only | Official per help centre — verify current pricing |
| **Suno Studio** | Browser DAW: clips, stems, MIDI, effects, automation, tempo locking, chat-based edits. Studio 2.0 launched August 2026 | Official, Premier |

Editing features (Replace Section, Add Vocals, Add Instrumental, section rearrangement) are generally **Pro/Premier**; Suno's own articles are inconsistent about a few of them, so treat paid access as the reliable assumption.

---

## Tempo and key

| Point | Fact | Tier |
|---|---|---|
| BPM and key in Styles | v6 understands numeric BPM and key names as **soft targets** | Official capability, soft behaviour |
| Tempo drift | Suno acknowledges it: tempo "is not consistent over time, just like live music" | Official |
| Official fix | **Studio → Transport → Project Tempo → Manual BPM**, then export stems/multitrack and set the same tempo in your DAW | Official |
| Accuracy | Practitioners report outputs within roughly ±2–5 BPM of a numeric request | Lore |
| `[BPM: 128]` in lyrics | Not a documented parameter syntax — put tempo in Styles | Lore (avoid) |

For frame-accurate work, see §5 of SKILL.md: choose a tempo whose beat is a whole number of frames, then lock it.

---

## Structure tags in v6

Suno publishes no exhaustive metatag grammar. Its glossary recognises the musical concepts Intro, Verse, Chorus, Bridge, Refrain, Break, Drop and Outro, and recommends describing song form in words. Bracket tags are a **conditioning convention that works well**, not deterministic markup. *(Official + Lore)*

- Reliable in practice: `[Intro]`, `[Verse]`, `[Pre-Chorus]`, `[Chorus]`, `[Post-Chorus]`, `[Bridge]`, `[Break]`, `[Interlude]`, `[Instrumental]`, `[Outro]`, `[End]`
- Performance cues inside the tag work well in v6, which follows section-level direction more readily than v5. Pipe syntax (`[Verse | intimate close-mic alto]`) is community-discovered, not official
- Not documented as commands: `[No Vocals]`, `[BPM: x]`, `[Reverb: 30%]`

---

## Rights and commercial use

| Plan | Position | Downloads |
|---|---|---|
| **Free** | Suno retains ownership; personal, non-commercial use. Your own written lyrics remain yours. Upgrading later is **not retroactive** | Limited trial downloads, non-commercial |
| **Pro** | Suno assigns its rights in compliant outputs you generate; commercial use applies to outputs downloaded on a paid plan; rights survive cancellation | 20 per month |
| **Premier** | As Pro, plus Studio workflows outside the ordinary cap | 60 per month |

Commercial-use rights are **not** a guarantee of copyright protection — that depends on jurisdiction and human authorship. *(Official)*

**For client work:** confirm the plan covers commercial use before delivering, and confirm the client accepts AI-generated music. Terms change; re-check rather than quoting this table as current.

---

## Sources

Official: [Introducing v6](https://suno.com/release-notes/introducing-v6) · [Release notes](https://suno.com/release-notes) · [What's new in v6](https://help.suno.com/en/articles/13924801) · [v6 FAQ](https://help.suno.com/en/articles/13924481) · [Models overview](https://help.suno.com/en/articles/13924737) · [How long will my song be?](https://help.suno.com/en/articles/13924929) · [Exclude styles](https://help.suno.com/en/articles/3161921) · [Fixing tempo drift](https://help.suno.com/en/articles/8363457) · [Pricing](https://suno.com/pricing)

Observed and lore items come from live-app measurements and practitioner reporting gathered 16 September 2026; re-verify before quoting them as fact.
