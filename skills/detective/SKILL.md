---
name: detective
description: Break down how a reel or short video is made, shot by shot: cuts, captions, what each scene acts out, motion, pacing and the hook. Use when the person asks how a video was made, why it works, or to break it down, or as step 2 of a remix.
---

# The Detective: break down

Watches every frame and writes down the **grammar** of the reel: not what is on screen, but the rules that make it work, so the Director can rebuild them with new material. You are the eyes: the tools cut and measure, you read every picture.

## Steps

Work in `remix/<slug>/` (layout: `../../reference/project-layout.md`). For each reference:

1. **Download.** `yt-dlp -o "refs/%(id)s.%(ext)s" --write-info-json <link>`. On a login or rate-limit error, retry once with `--cookies-from-browser chrome` and tell the person.
2. **Measure.** With `V=refs/<id>.mp4` and `B=breakdown/<id>`:

   ```bash
   npx hyperframes measure probe "$V" > "$B/probe.json"
   npx hyperframes measure cuts "$V" > "$B/cuts.json"
   npx hyperframes measure events "$V" --map --out "$B/events" > "$B/events.json"
   npx hyperframes measure frames "$V" --every 0.5 --out "$B/sheets" > "$B/sheets.json"
   npx hyperframes measure frames "$V" --events --out "$B/strips" > "$B/strips.json"
   npx hyperframes transcribe "$V" --dir "$B" --model small.en --json
   ```

   Make `$B` first. For speech that is not English, use `--model small --language <code>`. `cuts.json` gives every hard cut, `events.json` adds appears, holds and sound onsets, `sheets/` is one frame every 0.5 s with the time printed on each, `strips/` is consecutive frames around each burst of motion, and `transcript.json` is every spoken word with its time.
3. **Look.** Open every sheet in `sheets/`, then every strip in `strips/`. Read them all: the grammar lives in the details (what pops in first, which way a character faces, what the caption says at that exact moment).
4. **Write `breakdown/<id>.md`** with the sections below.

Done when every shot in `cuts.json` has a row in the shot table, every sheet and strip has been opened, and each grammar question has an answer backed by a timestamp.

## The breakdown

**Numbers.** Length, shot count, average shot length, cuts per minute, aspect, and the comment, like and post-date figures from `RANK.md` if it exists.

**Shot table.** One row per shot: start to end, the layout (split screen, full graphic, talking head, screen recording, UI card), what is on screen, the caption or chip text, the words spoken (from the transcript), and what the picture **does** with those words.

**Grammar.** Answer each with timestamps:

- **Hook:** what is on frame 0, and what changes or is promised in the first 1.5 s.
- **Words to pictures:** does each caption or line get a literal visual (a character acting it out, an icon, a UI moment)? Quote three examples of line and picture.
- **Prop arc:** is there an object that carries the story across scenes and pays off at the end?
- **Running example:** is one concrete case (a product, a fake company, a person) used throughout?
- **World and proof:** does it alternate illustrated or playful scenes with real UI, numbers or results?
- **Host:** when is the person on screen, when do they drop out, and why at those moments?
- **Motion:** the recurring moves, from the strips: entrances, punch-ins, swaps, multiplications, typing. Give frame counts.
- **Packaging:** caption style (position, case, font feel, chip or plain), how captions enter, how many words per chip.
- **Sound:** VO, music, effects. You cannot hear: work from the transcript and the onsets in `events.json` (a cluster of onsets on caption entrances suggests pops), and label every sound claim as inferred.
- **Call to action:** the exact mechanic (comment a keyword, follow, link) and when it starts.
- **Engine:** two sentences on why this reel earns comments, the thing worth taking.

**Leave behind.** List what belongs to the creator and must not travel: their face, voice, exact lines, footage, music, characters and logos (rules: `../../reference/not-a-copy.md`).

## Deeper analysis (optional)

For a per-shot verdict on how each picture was made (live action, AI video, 3D, motion graphics, screen recording), the open-source `rea-video` CLI adds that layer: `pipx install "rea-video @ git+https://github.com/JuneYaooo/rea-video"`, then `rea-video decompose "$V" -o "$B/rea" --lang en`. Use its labels as a second opinion beside your own reading of the sheets, not instead of it.
