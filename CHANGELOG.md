# Changelog

## 1.1.0 — 2026-10-03

Scoring to picture, aligned with reelsmith 2.0.

- Frames-per-beat table extended to faster tempos (8, 9, 11, 13 frames) with a pace column.
- New: turning an edit's brief (tempo, length, section plan, character, ending) into Styles, lyrics-box section tags and Exclude.
- New: measure after generation — drift is real even when a steady tempo is asked for (measured 127.8 → 131.2 BPM on one v6 track); lock it or hand tracked beats to the edit; shorten by whole sections on downbeats.
- Loudness: −14 LUFS described as common practice, not a published platform target.

## 1.0.0 — 2026-09-16

First release, targeting the Suno **v6** family (released 9 September 2026).

- Model guidance for v6, v6-wild and v6-mini, plus Max Mode.
- v6 capabilities: plain-language section editing, single-lyric edits, mashups, sampling, multimodal prompting.
- **Variety** slider documented — it rewrites your style prompt unless set to 0.
- Evidence tiers (Official / Observed / Lore) applied throughout, with a fact sheet in `reference/suno/v6-capabilities.md`.
- New: scoring to picture — frames-per-beat table for 24/25/30 fps, tempo locking, building length in whole bars.
- Track file and album workflow with an updated Suno Inputs template.
- Reference set carried over from the V5-era docs where still valid; `v5-best-practices.md` kept for prompt craft and marked superseded for model and UI facts.
